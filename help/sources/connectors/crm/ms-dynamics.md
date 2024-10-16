---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics；Microsoft Dynamics；Dynamics；Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source连接器概述
description: 了解如何使用API或用户界面将Microsoft Dynamics连接到Adobe Experience Platform。
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 3%

---

# Microsoft Dynamics 连接器

Adobe Experience Platform允许从外部源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

[!DNL Experience Platform]支持从第三方CRM系统中引入数据。 CRM提供商的支持包括[!DNL Microsoft Dynamics]。

## IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

## 从[!DNL Microsoft Dynamics]到XDM的字段映射

要建立[!DNL Microsoft Dynamics]与Platform之间的源连接，[!DNL Microsoft Dynamics]源数据字段必须在被引入Platform之前映射到其相应的目标XDM字段。

有关[!DNL Microsoft Dynamics]数据集与Platform之间的字段映射规则的详细信息，请参阅以下内容：

- [联系人](../adobe-applications/mapping/dynamics.md#contacts)
- [潜在客户](../adobe-applications/mapping/dynamics.md#leads)
- [帐户](../adobe-applications/mapping/dynamics.md#accounts)
- [机会](../adobe-applications/mapping/dynamics.md#opportunities)
- [机会联系人角色](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [营销活动](../adobe-applications/mapping/dynamics.md#campaigns)
- [营销列表](../adobe-applications/mapping/dynamics.md#marketing-list)
- [营销列表成员](../adobe-applications/mapping/dynamics.md#marketing-list-members)

以下文档提供了有关如何使用API或用户界面将[!DNL Microsoft Dynamics]连接到[!DNL Platform]的信息：

## 使用API将[!DNL Microsoft Dynamics]连接到[!DNL Platform]

- [使用流服务API创建Microsoft Dynamics基本连接](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)

## 使用UI将[!DNL Microsoft Dynamics]连接到[!DNL Platform]

- [在UI中创建Microsoft Dynamics源连接](../../tutorials/ui/create/crm/dynamics.md)
- [在用户界面中为CRM连接创建数据流](../../tutorials/ui/dataflow/crm.md)
