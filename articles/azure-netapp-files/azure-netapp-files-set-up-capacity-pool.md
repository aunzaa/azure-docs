---
title: Create a capacity pool for Azure NetApp Files | Microsoft Docs
description: Describes how to create a capacity pool so that you can create volumes within it.  
services: azure-netapp-files
documentationcenter: ''
author: b-juche
manager: ''
editor: ''

ms.assetid:
ms.service: azure-netapp-files
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to
ms.date: 11/4/2021
ms.author: b-juche
---
# Create a capacity pool for Azure NetApp Files

Creating a capacity pool enables you to create volumes within it.  

## Before you begin 

You must have already created a NetApp account.   

[Create a NetApp account](azure-netapp-files-create-netapp-account.md)

## Steps 

1. Go to the management blade for your NetApp account, and then, from the navigation pane, click **Capacity pools**.  
    
    ![Navigate to capacity pool](../media/azure-netapp-files/azure-netapp-files-navigate-to-capacity-pool.png)

2. Click **+ Add pools** to create a new capacity pool.   
    The New Capacity Pool window appears.

3. Provide the following information for the new capacity pool:  
   * **Name**  
     Specify the name for the capacity pool.  
     The capacity pool name must be unique for each NetApp account.

   * **Service level**   
     This field shows the target performance for the capacity pool.  
     Specify the service level for the capacity pool: [**Ultra**](azure-netapp-files-service-levels.md#Ultra), [**Premium**](azure-netapp-files-service-levels.md#Premium), or [**Standard**](azure-netapp-files-service-levels.md#Standard).

    * **Size**     
     Specify the size of the capacity pool that you are purchasing.        
     The minimum capacity pool size is 4 TiB. You can change the size of a capacity pool in 1-TiB increments.

   * **QoS**   
     Specify whether the capacity pool should use the **Manual** or **Auto** QoS type.  

     See [Storage Hierarchy](azure-netapp-files-understand-storage-hierarchy.md) and [Performance Considerations](azure-netapp-files-performance-considerations.md) to understand the QoS types.  

     > [!IMPORTANT] 
     > Setting **QoS type** to **Manual** is permanent. You cannot convert a manual QoS capacity pool to use auto QoS. However, you can convert an auto QoS capacity pool to use manual QoS. See [Change a capacity pool to use manual QoS](manage-manual-qos-capacity-pool.md#change-to-qos).   

    ![New capacity pool](../media/azure-netapp-files/azure-netapp-files-new-capacity-pool.png)

4. Click **Create**.

## Next steps 

- [Storage Hierarchy](azure-netapp-files-understand-storage-hierarchy.md) 
- [Service levels for Azure NetApp Files](azure-netapp-files-service-levels.md)
- [Azure NetApp Files pricing page](https://azure.microsoft.com/pricing/details/storage/netapp/)
- [Manage a manual QoS capacity pool](manage-manual-qos-capacity-pool.md)
- [Delegate a subnet to Azure NetApp Files](azure-netapp-files-delegate-subnet.md)
