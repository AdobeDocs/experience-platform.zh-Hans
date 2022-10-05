---
title: Marketo Engage目标
description: Marketo Engage是用于营销、广告、分析和商务的唯一端到端客户体验管理(CXM)解决方案。 它让您能够自动执行和管理活动，从CRM潜在客户管理和客户参与到基于帐户的营销和收入归因中。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 9f305ee7824bd8790dec57ccbd2d9462ccfa8b49
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 2%

---

# Marketo Engage目标 {#beta-marketo-engage-destination}

## 目标更改日志 {#changelog}

>[!IMPORTANT]
>
>随着 [增强的Marketo V2目标连接器](/help/release-notes/2022/july-2022.md#destinations)，则您现在会在目标目录中看到两张Marketo卡。
>* 如果您已经在 **[!UICONTROL Marketo V1]** 目标：请为 **[!UICONTROL Marketo V2]** 目标和删除现有数据流 **[!UICONTROL Marketo V1]** 到2023年2月。 截至该日期， **[!UICONTROL Marketo V1]** 目标卡将被删除。
>* 如果您尚未为 **[!UICONTROL Marketo V1]** 目标，请使用新 **[!UICONTROL Marketo V2]** 用于连接并将数据导出到Marketo的卡。


![并排视图中两个Marketo目标卡的图像。](/help/destinations/assets/catalog/adobe/marketo-side-by-side-view.png)

Marketo V2目标的改进包括：

* 在 **[!UICONTROL 计划区段]** 激活工作流的步骤(在Marketo V1中)，您需要手动添加 **映射ID** 成功将数据导出到Marketo。 Marketo V2不再需要此手动步骤。
* 在 **[!UICONTROL 映射]** 在Marketo V1中，您能够将XDM字段仅映射到Marketo中的三个目标字段： `firstName`, `lastName`和 `companyName`. 在Marketo V2版本中，您现在可以将XDM字段映射到Marketo中的更多字段。 有关更多信息，请阅读 [受支持属性](#supported-attributes) 部分。

## 概述 {#overview}

[!DNL Marketo Engage] 是用于营销、广告、分析和商务的唯一端到端客户体验管理(CXM)解决方案。 它让您能够自动执行和管理活动，从CRM潜在客户管理和客户参与到基于帐户的营销和收入归因中。

通过目标，营销人员可以将在Adobe Experience Platform中创建的区段推送到Marketo，以便这些区段显示为静态列表。

## 支持的身份和属性 {#supported-identities-attributes}

>[!NOTE]
>
>在 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 激活目标工作流的 *强制* 映射身份和 *可选* 来映射属性。 要确保人员在Marketo中进行匹配，最重要的任务是从“身份命名空间”选项卡中映射电子邮件和/或ECID。 映射电子邮件可确保最高匹配率。

### 支持的身份 {#supported-identities}

| Target标识 | 描述 |
|---|---|
| ECID | 表示ECID的命名空间。 此命名空间也可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档(位于 [ECID](/help/identity-service/ecid.md) 以了解更多信息。 |
| 电子邮件 | 表示电子邮件地址的命名空间。 此类命名空间通常与单个人员关联，因此可用于跨不同渠道识别该人员。 |

{style=&quot;table-layout:auto&quot;}

### 支持的属性 {#supported-attributes}

您可以将属性从Experience Platform映射到贵组织在Marketo中有权访问的任何属性。 在Marketo中，您可以使用 [描述API请求](https://developers.marketo.com/rest-api/lead-database/leads/#describe) 用于检索贵组织有权访问的属性字段。

## 导出类型和频度 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 区段导出]** | 您要导出区段（受众）的所有成员，以及 [!DNL Marketo Engage] 目标。 |
| 导出频度 | **[!UICONTROL 流]** | 流目标“始终运行”基于API的连接。 在基于区段评估的Experience Platform中更新用户档案后，连接器会立即将更新发送到目标平台下游。 有关更多信息 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 设置目标并激活区段 {#set-up}

>[!IMPORTANT]
> 
>* 要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions).
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。


有关如何设置目标和激活区段的详细说明，请阅读 [将Adobe Experience Platform区段推送到Marketo静态列表](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) (在Marketo文档中)。

以下视频还演示了配置Marketo目标和激活区段的步骤。

>[!IMPORTANT]
>
>该视频并不完全反映当前的功能。 有关最新信息，请参阅上面链接的指南。 视频的以下部分已过时：
> 
>* 您应在Experience PlatformUI中使用的目标卡是 **[!UICONTROL Marketo V2]**.
>* 该视频不显示新 **[!UICONTROL 人员创建]** “连接到目标”工作流中的选择器字段。
>* 视频中调用的两个限制不再适用。 除了在视频录制时支持的区段成员资格信息之外，您现在还可以映射许多其他配置文件属性字段。 您还可以将区段成员导出到Marketo，这些区段成员在Marketo静态列表中尚不存在，并且这些成员将会添加到列表中。
>* 在 **[!UICONTROL 计划区段步骤]** 在Marketo V1中，您需要手动添加 **[!UICONTROL 映射ID]** 成功将数据导出到Marketo。 Marketo V2不再需要此手动步骤。


>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 数据使用和管理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理数据时与数据使用策略相兼容。 有关如何 [!DNL Adobe Experience Platform] 实施数据管理，请查看 [数据管理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
