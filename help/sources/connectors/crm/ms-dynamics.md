---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics;Microsoft Dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source Connector概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Microsoft Dynamics连接到Adobe Experience Platform。
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# Microsoft Dynamics 连接器

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用[!DNL Platform]服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[!DNL Experience Platform] 支持从第三方CRM系统摄取数据。对CRM提供程序的支持包括[!DNL Microsoft Dynamics]。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表。 无法将特定于区域的IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关更多信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页面。

>[!IMPORTANT]
>
>[!DNL Microsoft Dynamics]源连接器当前不支持与平台的同一区域连接。 这意味着如果您的Azure实例使用与Platform相同的网络区域，则无法建立与Platform源的连接。 目前，仅支持跨区域连接。 有关更多信息，请联系您的Adobe客户经理。

以下文档提供了有关如何使用API或用户界面将[!DNL Microsoft Dynamics]连接到[!DNL Platform]的信息：

## 使用API将[!DNL Microsoft Dynamics]连接到[!DNL Platform]

- [使用流服务API创建Microsoft Dynamics基本连接](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用流服务API探索CRM源的数据结构和内容](../../tutorials/api/explore/crm.md)
- [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)

## 使用UI将[!DNL Microsoft Dynamics]连接到[!DNL Platform]

- [在UI中创建Microsoft Dynamics源连接](../../tutorials/ui/create/crm/dynamics.md)
- [在UI中为CRM连接创建数据流](../../tutorials/ui/dataflow/crm.md)
