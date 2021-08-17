---
title: Marketo Engage目标
description: Marketo Engage是用于营销、广告、分析和商务的唯一端到端客户体验管理(CXM)解决方案。 它让您能够自动执行和管理活动，从CRM潜在客户管理和客户参与到基于帐户的营销和收入归因中。
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---


# （测试版）Marketo Engage目标 {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform中的Marketo Engage目标当前为测试版。 文档和功能可能会发生更改。

## 概述 {#overview}

Marketo Engage是用于营销、广告、分析和商务的唯一端到端客户体验管理(CXM)解决方案。 它让您能够自动执行和管理活动，从CRM潜在客户管理和客户参与到基于帐户的营销和收入归因中。

区段连接器允许营销人员将在Adobe Experience Platform中创建的区段推送到Marketo，在那里，这些区段将显示为静态列表。

## 支持的身份 {#supported-identities}

| Target标识 | 描述 |
|---|---|
| ECID | 表示ECID的命名空间。 此命名空间也可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 有关更多信息，请参阅以下关于[ECID](/help/identity-service/ecid.md)的文档。 |
| 电子邮件 | 表示电子邮件地址的命名空间。 此类命名空间通常与单个人员关联，因此可用于跨不同渠道识别该人员。 |

## 导出类型 {#export-type}

区段导出 — 您要导出区段（受众）的所有成员，以及Marketo Engage目标中使用的标识符（名称、电话号码或其他）。

## 设置 {#set-up}

有关如何设置目标[的说明，请参阅此处](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en)。

## 连接到目标 {#connect}

要连接到此目标，请按照[目标配置教程](../../ui/connect-destination.md)中描述的步骤操作。

## 数据使用和管理 {#data-usage-governance}

处理数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据管理的详细信息，请参阅[数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

## 将区段激活到此目标 {#activate}

有关将受众区段激活到此目标的说明，请参阅[将受众数据激活到流区段导出目标](../../ui/activate-segment-streaming-destinations.md)。
