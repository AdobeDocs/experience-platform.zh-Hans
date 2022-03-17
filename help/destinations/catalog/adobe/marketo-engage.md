---
title: Marketo Engage目标
description: Marketo Engage是用于营销、广告、分析和商务的唯一端到端客户体验管理(CXM)解决方案。 它让您能够自动执行和管理活动，从CRM潜在客户管理和客户参与到基于帐户的营销和收入归因中。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# Marketo Engage目标 {#beta-marketo-engage-destination}

## 概述 {#overview}

Marketo Engage是用于营销、广告、分析和商务的唯一端到端客户体验管理(CXM)解决方案。 它让您能够自动执行和管理活动，从CRM潜在客户管理和客户参与到基于帐户的营销和收入归因中。

通过目标，营销人员可以将在Adobe Experience Platform中创建的区段推送到Marketo，以便这些区段显示为静态列表。

## 支持的身份 {#supported-identities}

| Target标识 | 描述 |
|---|---|
| ECID | 表示ECID的命名空间。 此命名空间也可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档(位于 [ECID](/help/identity-service/ecid.md) 以了解更多信息。 |
| 电子邮件 | 表示电子邮件地址的命名空间。 此类命名空间通常与单个人员关联，因此可用于跨不同渠道识别该人员。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>在 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 激活目标工作流的 *强制* 映射身份和 *可选* 来映射属性。 要确保人员在Marketo中进行匹配，最重要的任务是从“身份命名空间”选项卡中映射电子邮件和/或ECID。 映射电子邮件可确保最高匹配率。

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及在Marketo Engage目标中使用的标识符（电子邮件、ECID）。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 设置目标并激活区段 {#set-up}

有关如何设置目标和激活区段的详细说明，请阅读 [将Adobe Experience Platform区段推送到Marketo静态列表](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) (在Marketo文档中)。

以下视频还演示了配置Marketo目标和激活区段的步骤。

>[!NOTE]
>
>Experience Platform用户界面经常更新，自此视频录制以来可能已发生更改。 有关最新信息，请参阅上面链接的指南。

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
