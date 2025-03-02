---
title: Quickstart - Send an SMS message
titleSuffix: An Azure Communication Services quickstart
description: Learn how to send an SMS message using Azure Communication Services.
author: probableprime
manager: chpalm
services: azure-communication-services
ms.author: rifox
ms.date: 06/30/2021
ms.topic: quickstart
ms.service: azure-communication-services
ms.subservice: sms
ms.custom: tracking-python, devx-track-js, mode-other
zone_pivot_groups: acs-js-csharp-java-python
---
# Quickstart: Send an SMS message

[!INCLUDE [Regional Availability Notice](../../includes/regional-availability-include.md)]

> [!IMPORTANT]
> SMS messages can be sent to and received from United States phone numbers. Phone numbers located in other geographies are not yet supported by Communication Services SMS.
> For more information, see **[Phone number types](../../concepts/telephony-sms/plan-solution.md)**.

::: zone pivot="programming-language-csharp"
[!INCLUDE [Send SMS with .NET SDK](./includes/send-sms-net.md)]
::: zone-end

::: zone pivot="programming-language-javascript"
[!INCLUDE [Send SMS with JavaScript SDK](./includes/send-sms-js.md)]
::: zone-end

::: zone pivot="programming-language-python"
[!INCLUDE [Send SMS with Python SDK](./includes/send-sms-python.md)]
::: zone-end

::: zone pivot="programming-language-java"
[!INCLUDE [Send SMS with Java SDK](./includes/send-sms-java.md)]
::: zone-end

## Troubleshooting

To troubleshoot issues related to SMS delivery, you can [enable delivery reporting with Event Grid](./handle-sms-events.md) to capture delivery details.

## Clean up resources

If you want to clean up and remove a Communication Services subscription, you can delete the resource or resource group. Deleting the resource group also deletes any other resources associated with it. Learn more about [cleaning up resources](../create-communication-resource.md#clean-up-resources).

## Next steps

In this quickstart, you learned how to send SMS messages using Azure Communication Services.

> [!div class="nextstepaction"]
> [Receive SMS and Delivery Report Events](./handle-sms-events.md)

> [!div class="nextstepaction"]
> [Phone number types](../../concepts/telephony-sms/plan-solution.md)

> [!div class="nextstepaction"]
> [Learn more about SMS](../../concepts/telephony-sms/concepts.md)
