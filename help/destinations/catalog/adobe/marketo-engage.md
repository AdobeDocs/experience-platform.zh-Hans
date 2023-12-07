---
title: Marketo Engage目标
description: Marketo Engage是唯一用于营销、广告、分析和商业的端到端客户体验管理(CXM)解决方案。 您可以从自动化和管理活动，从CRM商机管理和客户参与到基于帐户的营销和收入归因。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 1%

---

# Marketo Engage目标 {#beta-marketo-engage-destination}

## 目标更改日志 {#changelog}

>[!IMPORTANT]
>
>随着 [增强的Marketo V2目标连接器](/help/release-notes/2022/july-2022.md#destinations)中，您现在会在目标目录中看到两个Marketo信息卡。
>* 如果您已经激活数据到 **[!UICONTROL Marketo V1]** 目标：请为以下对象创建新数据流： **[!UICONTROL Marketo V2]** 目标并删除到的数据流 **[!UICONTROL Marketo V1]** 到2023年2月到达目的地。 截至该日， **[!UICONTROL Marketo V1]** 将删除目标卡。
>* 如果您尚未创建任何流到 **[!UICONTROL Marketo V1]** 目标，请使用新的 **[!UICONTROL Marketo V2]** 信息卡，用于连接数据并将其导出到Marketo。

![并排视图中两个Marketo目标卡的图像。](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Marketo V2目标中的改进包括：

* 在 **[!UICONTROL 计划区段]** 在Marketo V1中，激活工作流的步骤需要手动添加 **映射Id** 以成功将数据导出到Marketo。 Marketo V2中不再需要此手动步骤。
* 在 **[!UICONTROL 映射]** 在激活工作流的步骤中，在Marketo V1中，您只能将XDM字段映射到Marketo中的三个目标字段： `firstName`， `lastName`、和 `companyName`. 在Marketo V2版本中，您现在可以将XDM字段映射到Marketo中的更多字段。 欲知更多信息，请参阅 [支持的属性](#supported-attributes) 部分。

## 概述 {#overview}

[!DNL Marketo Engage] 是唯一用于营销、广告、分析和商务的端到端客户体验管理(CXM)解决方案。 您可以从自动化和管理活动，从CRM商机管理和客户参与到基于帐户的营销和收入归因。

目标允许营销人员将在Adobe Experience Platform中创建的受众推送到Marketo，并在其中显示为静态列表。

## 支持的身份和属性 {#supported-identities-attributes}

>[!NOTE]
>
>在 [映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) ，它是 *必需* 以映射身份和 *可选* 以映射属性。 从“身份命名空间”选项卡映射电子邮件和/或ECID是最重要的事情，可确保人员在Marketo中匹配。 映射电子邮件可确保最高的匹配率。

### 支持的身份 {#supported-identities}

| 目标身份 | 描述 |
|---|---|
| ECID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“Adobe Experience Cloud ID”、“Adobe Experience Platform ID”。 请参阅以下文档： [ECID](/help/identity-service/ecid.md) 以了解更多信息。 |
| 电子邮件 | 表示电子邮件地址的命名空间。 此类命名空间通常与单个人员关联，因此可用于跨不同渠道识别该人员。 |

{style="table-layout:auto"}

### 支持的属性 {#supported-attributes}

您可以将属性从Experience Platform映射到贵组织在Marketo中有权访问的任何属性。 在Marketo中，您可以使用 [描述API请求](https://developers.marketo.com/rest-api/lead-database/leads/#describe) 以检索您的组织有权访问的属性字段。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ {\f13 } | 通过Experience Platform生成的受众 [分段服务](../../../segmentation/home.md). |
| 自定义上传 | ✓ | 受众 [已导入](../../../segmentation/ui/overview.md#import-audience) 从CSV文件Experience Platform到。 |

{style="table-layout:auto"}

## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 导出类型 | **[!UICONTROL 受众导出]** | 您正在导出受众的所有成员，其中包含 [!DNL Marketo Engage] 目标。 |
| 导出频率 | **[!UICONTROL 流]** | 流目标为基于API的“始终运行”连接。 一旦根据受众评估在Experience Platform中更新了用户档案，连接器就会将更新发送到下游目标平台。 详细了解 [流目标](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 设置目标和激活受众 {#set-up}

>[!IMPORTANT]
> 
>* 要连接到目标，您需要 **[!UICONTROL 管理目标]** [访问控制权限](/help/access-control/home.md#permissions).
>* 要激活数据，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

有关如何设置目标和激活受众的详细说明，请阅读 [将Adobe Experience Platform受众推送到Marketo静态列表](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) 请参阅Marketo文档。

以下视频还演示了配置Marketo目标和激活受众的步骤。

>[!IMPORTANT]
>
>该视频未完全反映当前功能。 有关最新信息，请参阅上面链接的指南。 视频的以下部分已过时：
> 
>* 您应在Experience PlatformUI中使用的目标卡是 **[!UICONTROL Marketo V2]**.
>* 视频未显示新内容 **[!UICONTROL 人员创建]** “连接到目标工作流”中的“选择器”字段。
>* 视频中调出的两个限制不再适用。 除了在录制视频时支持的受众成员资格信息之外，您现在可以映射许多其他配置文件属性字段。 您还可以将受众成员导出到Marketo，这些成员尚不存在于Marketo静态列表中，并且会添加到列表中。
>* 在 **[!UICONTROL 计划受众步骤]** 在Marketo V1中，您需要手动添加 **[!UICONTROL 映射Id]** 以成功将数据导出到Marketo。 Marketo V2中不再需要此手动步骤。

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 数据使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目标在处理您的数据时符合数据使用策略。 有关如何执行操作的详细信息 [!DNL Adobe Experience Platform] 强制执行数据管理，请参见 [数据治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

<!--

## Activate audiences to this destination {#activate}

See [Activate audience data to streaming audience export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audiences to this destination.

-->
