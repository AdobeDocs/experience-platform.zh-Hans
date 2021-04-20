---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics;microsoft Dynamics;dynamics;Dynamics
solution: Experience Platform
title: Microsoft Dynamics源连接器概述
topic: overview
description: 了解如何使用API或用户界面将Microsoft Dynamics连接到Adobe Experience Platform。
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# Microsoft Dynamics 连接器

Adobe Experience Platform允许从外部源摄取数据，同时为您提供使用[!DNL Platform]服务构建、标记和增强传入数据的能力。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、数据库和许多其他来源。

[!DNL Experience Platform] 支持从第三方CRM系统中摄取数据。对CRM提供程序的支持包括[!DNL Microsoft Dynamics]。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法将您的区域特定IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

>[!IMPORTANT]
>
>[!DNL Microsoft Dynamics]源连接器当前不支持与平台的同一区域连接。 这意味着，如果您的Azure实例使用与平台相同的网络区域，则无法建立到平台源的连接。 目前，仅支持跨区域连接。 有关详细信息，请与您的Adobe客户经理联系。

以下文档提供了如何使用API或用户界面将[!DNL Microsoft Dynamics]连接到[!DNL Platform]的信息：

## 使用API将[!DNL Microsoft Dynamics]连接到[!DNL Platform]

- [使用Flow Service API创建Microsoft Dynamics源连接](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用Flow Service API探索CRM系统](../../tutorials/api/explore/crm.md)
- [使用Flow Service API收集CRM数据](../../tutorials/api/collect/crm.md)

## 使用UI将[!DNL Microsoft Dynamics]连接到[!DNL Platform]

- [在UI中创建Microsoft Dynamics源连接](../../tutorials/ui/create/crm/dynamics.md)
- [在UI中为CRM连接配置数据流](../../tutorials/ui/dataflow/crm.md)