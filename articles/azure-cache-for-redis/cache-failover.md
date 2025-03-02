---
title: Failover and patching - Azure Cache for Redis
description: Learn about failover, patching, and the update process for Azure Cache for Redis.
author: curib
ms.author: cauribeg
ms.service: cache
ms.topic: conceptual
ms.date: 11/3/2021
---

# Failover and patching for Azure Cache for Redis

To build resilient and successful client applications, it's critical to understand failover in the Azure Cache for Redis service. A failover can be a part of planned management operations, or it might be caused by unplanned hardware or network failures. A common use of cache failover comes when the management service patches the Azure Cache for Redis binaries.

In this article, you find this information:  

- What is a failover?
- How failover occurs during patching.
- How to build a resilient client application.

## What is a failover?

Let's start with an overview of failover for Azure Cache for Redis.

### A quick summary of cache architecture

A cache is constructed of multiple virtual machines with separate and private IP addresses. Each virtual machine, also known as a node, is connected to a shared load balancer with a single virtual IP address. Each node runs the Redis server process and is accessible with using the host name and the Redis ports. Each node is considered either a primary or a replica node. When a client application connects to a cache, its traffic goes through this load balancer and is automatically routed to the primary node.

In a Basic cache, the single node is always a primary. In a Standard or Premium cache, there are two nodes: one is chosen as the primary and the other is the replica. Because Standard and Premium caches have multiple nodes, one node might be unavailable while the other continues to process requests. Clustered caches are made of many shards, each with distinct primary and replica nodes. One shard might be down while the others remain available.

> [!NOTE]
> A Basic cache doesn't have multiple nodes and doesn't offer a service-level agreement (SLA) for its availability. Basic caches are recommended only for development and testing purposes. Use a Standard or Premium cache for a multi-node deployment, to increase availability.

### Explanation of a failover

A failover occurs when a replica node promotes itself to become a primary node, and the old primary node closes existing connections. After the primary node comes back up, it notices the change in roles and demotes itself to become a replica. It then connects to the new primary and synchronizes data. A failover might be planned or unplanned.

A *planned failover* takes place during two different times:

- System updates, such as Redis patching or OS upgrades.  
- Management operations, such as scaling and rebooting.

Because the nodes receive advance notice of the update, they can cooperatively swap roles and quickly update the load balancer of the change. A planned failover typically finishes in less than 1 second.

An *unplanned failover* might happen because of hardware failure, network failure, or other unexpected outages to the primary node. The replica node  promotes itself to primary, but the process takes longer. A replica node must first detect its primary node isn't available before it can start the failover process. The replica node must also verify this unplanned failure isn't transient or local, to avoid an unnecessary failover. This delay in detection means an unplanned failover typically finishes within 10 to 15 seconds.

## How does patching occur?

The Azure Cache for Redis service regularly updates your cache with the latest platform features and fixes. To patch a cache, the service follows these steps:

1. The management service selects one node to be patched.
1. If the selected node is a primary node, the corresponding replica node cooperatively promotes itself. This promotion is considered a planned failover.
1. The selected node reboots to take the new changes and comes back up as a replica node.
1. The replica node connects to the primary node and synchronizes data.
1. When the data sync is complete, the patching process repeats for the remaining nodes.

Because patching is a planned failover, the replica node quickly promotes itself to become a primary. Then, the node begins servicing requests and new connections. Basic caches don't have a replica node and are unavailable until the update is complete. Each shard of a clustered cache is patched separately and won't close connections to another shard.

> [!IMPORTANT]
> Nodes are patched one at a time to prevent data loss. Basic caches will have data loss. Clustered caches are patched one shard at a time.

Multiple caches in the same resource group and region are also patched one at a time.  Caches that are in different resource groups or different regions might be patched simultaneously.

Because full data synchronization happens before the process repeats, data loss is unlikely to occur when you use a Standard or Premium cache. You can further guard against data loss by [exporting](cache-how-to-import-export-data.md#export) data and enabling [persistence](cache-how-to-premium-persistence.md).

## Additional cache load

Whenever a failover occurs, the Standard and Premium caches need to replicate data from one node to the other. This replication causes some load increase in both server memory and CPU. If the cache instance is already heavily loaded, client applications might experience increased latency. In extreme cases, client applications might receive time-out exceptions. To help mitigate the effect of more load, [configure](cache-configure.md#memory-policies) the cache's `maxmemory-reserved` setting.

## How does a failover affect my client application?

Client applications could receive some errors from their Azure Cache For Redis. The number of errors seen by a client application depends on how many operations were pending on that connection at the time of failover. Any connection that's routed through the node that closed its connections sees errors.

Many client libraries can throw different types of errors when connections break, including:

- Time-out exceptions
- Connection exceptions
- Socket exceptions

The number and type of exceptions depends on where the request is in the code path when the cache closes its connections. For instance, an operation that sends a request but hasn't received a response when the failover occurs might get a time-out exception. New requests on the closed connection object receive connection exceptions until the reconnection happens successfully.

Most client libraries attempt to reconnect to the cache if they're configured to do so. However, unforeseen bugs can occasionally place the library objects into an unrecoverable state. If errors persist for longer than a pre-configured amount of time, the connection object should be recreated. In Microsoft.NET and other object-oriented languages, recreating the connection without restarting the application can be accomplished by using a [ForceReconnect pattern](cache-best-practices-connection.md#using-forcereconnect-with-stackexchangeredis).

### Can I be notified in advance of planned maintenance?

Azure Cache for Redis publishes notifications on a publish/subscribe (pub/sub) channel called [AzureRedisEvents](https://github.com/Azure/AzureCacheForRedis/blob/main/AzureRedisEvents.md) around 30 seconds before planned updates. The notifications are runtime notifications.

The notifications are for applications that use circuit breakers to bypass the cache or applications that buffer commands. For example, the cache could be bypassed during any planned updates.

The `AzureRedisEvents` channel isn't a mechanism that can notify you days or hours in advance. The channel can notify clients of any upcoming planned server maintenance events that might affect server availability.

Many popular Redis client libraries support subscribing to pub/sub channels. Receiving notifications from the `AzureRedisEvents` channel is usually a simple addition to your client application.

Once your application is subscribed to `AzureRedisEvents`, it receives a notification 30 seconds before any node is affected by a maintenance event. The notification includes details about the upcoming event and indicates whether it affects a primary or replica node.

Another notification is sent minutes later when the maintenance operation is complete.

Your application uses the content in the notification to take action to avoid using the cache while the maintenance is done. A cache might implement a circuit breaker pattern where traffic is routed away from the cache during the maintenance operation. Instead, traffic is sent directly to a persistent store. The notification isn't intended to allow time for a person to be alerted and take manual action.

In most cases, your application doesn't need to subscribe to `AzureRedisEvents` or respond to notifications. Instead, we recommend implementing [building in resilience](#build-in-resiliency).

With sufficient resilience, applications gracefully handle any brief connection loss or cache unavailability like that experienced during node maintenance. It’s also possible that your application might unexpectedly lose its connection to the cache without warning from `AzureRedisEvents` because of network errors or other events.

We only recommend subscribing to `AzureRedisEvents` in a few noteworthy cases:

- Applications with extreme performance requirements, where even minor delays must be avoided. In such scenarios, traffic could be seamlessly rerouted to a backup cache before maintenance begins on the current cache.
- Applications that explicitly read data from replica rather than primary nodes. During maintenance on a replica node, the application could temporarily switch to read data from primary nodes.
- Applications that can't risk write operations failing silently or succeeding without confirmation, which can happen as connections are being closed for maintenance. If those cases would result in dangerous data loss, the application can proactively pause or redirect write commands before the maintenance is scheduled to begin.

### Client network-configuration changes

Certain client-side network-configuration changes can trigger "No connection available" errors. Such changes might include:

- Swapping a client application's virtual IP address between staging and production slots.
- Scaling the size or number of instances of your application.

Such changes can cause a connectivity issue that lasts less than one minute. Your client application will probably lose its connection to other external network resources, but also to the Azure Cache for Redis service.

## Build in resiliency

You can't avoid failovers completely. Instead, write your client applications to be resilient to connection breaks and failed requests. Most client libraries automatically reconnect to the cache endpoint, but few of them attempt to retry failed requests. Depending on the application scenario, it might make sense to use retry logic with backoff.

### How do I make my application resilient?

Refer to these design patterns to build resilient clients, especially the circuit breaker and retry patterns:

- [Reliability patterns - Cloud Design Patterns](/azure/architecture/framework/resiliency/reliability-patterns#resiliency)
- [Retry guidance for Azure services - Best practices for cloud applications](/azure/architecture/best-practices/retry-service-specific)
- [Implement retries with exponential backoff](/dotnet/architecture/microservices/implement-resilient-applications/implement-retries-exponential-backoff)

To test a client application's resiliency, use a [reboot](cache-administration.md#reboot) as a manual trigger for connection breaks.

Additionally, we recommend that you [schedule updates](cache-administration.md#schedule-updates) on a cache to apply Redis runtime patches during specific weekly windows. These windows are typically periods when client application traffic is low, to avoid potential incidents.

For more information, see [Connection resilience](cache-best-practices-connection.md).

## Next steps

- [Schedule updates](cache-administration.md#schedule-updates) for your cache.
- Test application resiliency by using a [reboot](cache-administration.md#reboot).
- [Configure](cache-configure.md#memory-policies) memory reservations and policies.
