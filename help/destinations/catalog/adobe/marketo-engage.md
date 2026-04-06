---
title: Marketo Engage目标
description: Marketo Engage是唯一一款用于营销、广告、分析和商务的端到端客户体验管理(CXM)解决方案。 使用它可自动化和管理从CRM商机管理和客户参与到基于帐户的营销和收入归因的活动。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 2%

---

# （旧版） (V2) Marketo Engage目标 {#beta-marketo-engage-destination}

## 目标更改日志 {#changelog}

<!--
>[!IMPORTANT]
>
>The **[!UICONTROL (Legacy) (V2) Marketo Engage]** will be deprecated in **March 2026**.
>
>To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)** destination, review the following key points and required actions:
>
>* All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.
>* **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.

-->

![并排视图中两个Marketo目标卡的图像。](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Marketo V2目标中的改进包括：

* 在激活工作流的&#x200B;**[!UICONTROL Schedule segment]**&#x200B;步骤中，在Marketo V1中，您需要手动添加&#x200B;**映射ID**&#x200B;以成功将数据导出到Marketo。 Marketo V2中不再需要此手动步骤。
* 在激活工作流的&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤中，在Marketo V1中，您只能将XDM字段映射到Marketo中的三个目标字段：`firstName`、`lastName`和`companyName`。 在Marketo V2版本中，您现在可以将XDM字段映射到Marketo中的更多字段。 有关详细信息，请阅读下面的[支持的属性](#supported-attributes)部分。

## 概述 {#overview}

[!DNL Marketo Engage]是唯一用于营销、广告、分析和商业的端到端客户体验管理(CXM)解决方案。 使用它可自动化和管理从CRM商机管理和客户参与到基于帐户的营销和收入归因的活动。

目标允许营销人员将在[!DNL Adobe Experience Platform]中创建的受众推送到Marketo，并在其中显示为静态列表。

## 支持的身份和属性 {#supported-identities-attributes}

>[!NOTE]
>
>在激活目标工作流的[映射步骤](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中，映射身份是&#x200B;*必需的*，映射属性是&#x200B;*可选的*。 从“身份命名空间”选项卡映射电子邮件和/或ECID是最重要的事情，可确保人员在Marketo中匹配。 映射电子邮件可确保最高的匹配率。

### 支持的身份 {#supported-identities}

| 目标身份 | 描述 |
|---|---|
| ECID | 表示ECID的命名空间。 此命名空间还可以由以下别名引用：“Adobe Marketing Cloud ID”、“[!DNL Adobe Experience Cloud] ID”、“[!DNL Adobe Experience Platform] ID”。 有关详细信息，请参阅[ECID](/help/identity-service/features/ecid.md)上的以下文档。 |
| 电子邮件 | 表示电子邮件地址的命名空间。 此类命名空间通常与单个人员关联，因此可以跨不同渠道识别该人员。 |

{style="table-layout:auto"}

### 支持的属性 {#supported-attributes}

您可以将属性从Experience Platform映射到您的组织在Marketo中有权访问的任何属性。 在Marketo中，您可以使用[Describe API请求](https://developers.marketo.com/rest-api/lead-database/leads/#describe)来检索您的组织有权访问的属性字段。

## 支持的受众 {#supported-audiences}

此部分介绍哪些类型的受众可以导出到此目标。

| 受众来源 | 受支持 | 描述 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 是 | 通过Experience Platform [分段服务](../../../segmentation/home.md)生成的受众。 |
| 所有其他受众来源 | 否 | 此类别包括通过[!DNL Segmentation Service]生成的受众之外的所有受众来源。 了解[各种受众源](/help/segmentation/ui/audience-portal.md#customize)。 一些示例包括： <ul><li> 自定义上传受众[从CSV文件导入](../../../segmentation/ui/audience-portal.md#import-audience)到Experience Platform，</li><li> 相似的受众， </li><li> 联合受众， </li><li> 其他Experience Platform应用程序（如[!DNL Adobe Journey Optimizer]）中生成的受众， </li><li> 等等。 </li></ul> |

{style="table-layout:auto"}



按受众数据类型划分的受众支持：

| 受众数据类型 | 受支持 | 描述 | 用例 |
|--------------------|-----------|-------------|-----------|
| [人员受众](/help/segmentation/types/people-audiences.md) | 是 | 根据客户个人资料，允许您针对特定的营销活动人群组进行定位。 | 频繁购买者，购物车放弃者 |
| [帐户受众](/help/segmentation/types/account-audiences.md) | 否 | 针对特定组织内的个人，制定基于帐户的营销策略。 | B2B营销 |
| [潜在客户受众](/help/segmentation/types/prospect-audiences.md) | 否 | 定位尚未成为客户但与目标受众具有共同特征的个人。 | 利用第三方数据发现潜在客户 |
| [数据集导出](/help/catalog/datasets/overview.md) | 否 | 存储在[!DNL Adobe Experience Platform]数据湖中的结构化数据的集合。 | 报告、数据科学工作流 |

{style="table-layout:auto"}


## 导出类型和频率 {#export-type-frequency}

有关目标导出类型和频率的信息，请参阅下表。

| 项目 | 类型 | 注释 |
|---------|----------|---------|
| 导出类型 | **[!UICONTROL Audience export]** | 您正在导出具有[!DNL Marketo Engage]目标中所用标识符（电子邮件、ECID）的受众的所有成员。 |
| 导出频率 | **[!UICONTROL Streaming]** | 流目标为基于API的“始终运行”连接。 根据受众评估在Experience Platform中更新用户档案后，连接器会立即将更新发送到下游目标平台。 阅读有关[流式目标](/help/destinations/destination-types.md#streaming-destinations)的更多信息。 |

{style="table-layout:auto"}

## 设置目标和激活受众 {#set-up}

>[!IMPORTANT]
>
>* 若要连接到目标，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [访问控制权限](/help/access-control/home.md#permissions)。
>* 若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

有关如何设置目标和激活受众的详细说明，请参阅Marketo文档中的[将Adobe Experience Platform受众推送到Marketo静态列表](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=zh-Hans)。

以下视频还演示了配置Marketo目标和激活受众的步骤。

>[!IMPORTANT]
>
>该视频未完全反映当前功能。 有关最新信息，请参阅上面链接的指南。 视频的以下部分已过时：
> 
>* 您应在Experience Platform UI中使用的目标卡是&#x200B;**[!UICONTROL Marketo V2]**。
>* 该视频未在“连接到目标工作流”中显示新的&#x200B;**[!UICONTROL Person creation]**&#x200B;选择器字段。 要使用该字段，必须在属性映射步骤中同时映射名字和姓氏。
>* 视频中调出的两个限制不再适用。 除了在录制视频时支持的受众成员资格信息之外，您现在可以映射许多其他配置文件属性字段。 您还可以将受众成员导出到Marketo，这些成员尚不存在于Marketo静态列表中，并且会添加到列表中。
>* 在激活工作流的&#x200B;**[!UICONTROL Schedule audience step]**&#x200B;中，在Marketo V1中，您需要手动添加&#x200B;**[!UICONTROL Mapping ID]**&#x200B;以成功将数据导出到Marketo。 Marketo V2中不再需要此手动步骤。

>[!VIDEO](https://video.tv.adobe.com/v/3440168?captions=chi_hans&quality=12)

## 监视目标 {#monitor-destination}

连接到目标并建立目标数据流后，您可以使用[中的](/help/dataflows/ui/monitor-destinations.md)监视功能[!DNL Real-Time CDP]获取有关每次数据流运行中激活到目标的配置文件记录的更多信息。

[!DNL Marketo Engage]连接的监视信息包括与每个数据流和数据流运行中激活、排除和失败的身份相关的受众级别信息。 [参阅更多](/help/dataflows/ui/monitor-destinations.md#segment-level-view)关于该功能的信息。

## 数据使用和治理 {#data-usage-governance}

在处理您的数据时，所有[!DNL Adobe Experience Platform]目标都符合数据使用策略。 有关[!DNL Adobe Experience Platform]如何实施数据治理的详细信息，请参阅[数据治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans)。
