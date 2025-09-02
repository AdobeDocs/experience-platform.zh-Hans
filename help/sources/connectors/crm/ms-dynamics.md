---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics；microsoft dynamics；dynamics；Dynamics
solution: Experience Platform
title: Microsoft Dynamics Source Connector概述
description: 了解如何使用API或用户界面将Microsoft Dynamics连接到Adobe Experience Platform。
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 16fe5340582dcea0ff40000fb516c1b72d5f150e
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# [!DNL Microsoft Dynamics]源

[!DNL Microsoft Dynamics]是一套业务应用程序，您可以使用它来更有效地管理您的操作。 无论您是管理客户关系、财务还是供应链，[!DNL Microsoft Dynamics]都可以为您提供工具，以简化您的工作流程并做出更明智的决策。 该平台旨在支持企业资源规划和客户关系管理(CRM)，允许您在一个集成系统中统一业务流程。

您可以使用[!DNL Microsoft Dynamics]源将数据从[!DNL Microsoft Dynamics]帐户摄取到Adobe Experience Platform。

## IP地址允许列表

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[列入允许列表IP地址以连接到Experience Platform](../../ip-address-allow-list.md)的指南。

## 从[!DNL Microsoft Dynamics]到XDM的字段映射

要建立[!DNL Microsoft Dynamics]与Experience Platform之间的源连接，在将[!DNL Microsoft Dynamics]源数据字段摄取到Experience Platform中之前，必须将其映射到相应的目标XDM字段。

有关[!DNL Microsoft Dynamics]数据集与Experience Platform之间的字段映射规则的详细信息，请参阅以下内容：

- [联系人](../adobe-applications/mapping/dynamics.md#contacts)
- [潜在客户](../adobe-applications/mapping/dynamics.md#leads)
- [帐户](../adobe-applications/mapping/dynamics.md#accounts)
- [机会](../adobe-applications/mapping/dynamics.md#opportunities)
- [机会联系人角色](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [营销活动](../adobe-applications/mapping/dynamics.md#campaigns)
- [营销列表](../adobe-applications/mapping/dynamics.md#marketing-list)
- [营销列表成员](../adobe-applications/mapping/dynamics.md#marketing-list-members)

以下文档提供了有关如何使用API或用户界面将[!DNL Microsoft Dynamics]连接到[!DNL Experience Platform]的信息：

## 使用API将[!DNL Microsoft Dynamics]连接到[!DNL Experience Platform]

- [使用流服务API创建Microsoft Dynamics基本连接](../../tutorials/api/create/crm/ms-dynamics.md)
- [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
- [使用流服务API为CRM源创建数据流](../../tutorials/api/collect/crm.md)

## 使用UI将[!DNL Microsoft Dynamics]连接到[!DNL Experience Platform]

- [在UI中创建Microsoft Dynamics源连接](../../tutorials/ui/create/crm/dynamics.md)
- [在用户界面中为CRM连接创建数据流](../../tutorials/ui/dataflow/crm.md)
