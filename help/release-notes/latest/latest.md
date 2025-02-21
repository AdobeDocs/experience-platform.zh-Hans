---
title: Adobe Experience Platform 发行说明（2025 年 2 月）
description: Adobe Experience Platform 的 2025 年 2 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b29c63942b00fdf597ebfd3ab105519a6b05a476
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 22%

---

# Adobe Experience Platform 发行说明

>[!TIP]
>
>此版本包括对联合受众组合加载项的改进。 有关详细信息，请阅读[联合受众组合发行说明](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes)。

**发行日期： 2025年2月18日**

Adobe Experience Platform 中现有功能和文档的更新：

- [AI 助手](#ai-assistant)
- [目录服务](#catalog-service)
- [数据准备](#data-prep)
- [目标](#destinations)
- [源](#sources)
- [文档更新](#documentation-updates)
   - [Edge网络与集线器比较](#edge)
   - [扩展的源流服务API](#flow-service)
   - [使用沙盒工具备份对象配置](#back-up-object-configurations)
   - [使用沙盒工具实现卓越中心](#center-of-excellence)
   - [数据湖中的体验事件数据集保留](#experience-event-dataset-retention)

## AI 助手 {#ai-assistant}

Adobe Experience Platform 中的 AI 助手是一种对话体验，您可以使用它来加速 Adobe 应用程序中的工作流程。您可以使用 AI 助手更好地了解产品知识、解决问题或搜索信息并找到运营洞察。AI Assistant支持Experience Platform、Real-Time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 支持问题自动完成 | 向AI Assistant输入问题时，您现在可以从AI Assistant提供的推荐问题列表中进行选择。 使用此功能可进一步加快使用AI Assistant的工作流。 有关详细信息，请阅读有关[使用AI助手自动完成问题](../../ai-assistant/ui-guide.md#use-question-autocomplete)的指南。 |
| 支持数据集可观察性 | 现在，您可以使用AI Assistant回答有关特定数据集量度（如存储大小和行计数）的问题。 数据可观察性问题支持可用于按特定时间段筛选查询的限定符。 有关详细信息，请阅读[AI助手问题指南](../../ai-assistant/questions.md)。 |

{style="table-layout:auto"}

有关详细信息，请阅读[AI助手概述](../../ai-assistant/home.md)。

<!-- | General availability of operational insights | Operational insights in AI Assistant are now in GA. Operational insights refer to answers AI Assistant generates about your metadata objects (attributes, audiences, dataflows, datasets, destinations, journeys, schemas, and sources), including counts, lookups, and lineage impact. Operational insights does not look at any data within the sandbox. For more information, read the [AI Assistant UI guide](../../ai-assistant/ui-guide.md). | -->

## 目录服务 {#catalog-service}

目录服务是 Adobe Experience Platform 中记录数据位置和沿袭的系统。虽然所有摄取到 Experience Platform 中的数据均作为文件和目录存储在数据湖中，但目录保存这些文件和目录的元数据和描述以供查找和监控目的。

| 功能 | 描述 |
| --- | --- |
| 新API端点 | 使用新的[目录服务API /v2/dataSets/{DATASET_ID}端点](../../catalog/api/update-object.md#patch-v2-notation)更有效地管理Adobe Experience Platform数据集元数据。 由于系统会自动创建缺失的路径级别，因此可以轻松更新复杂、嵌套深度的数据集属性，从而节省您的时间、减少手动步骤并将错误降至最低。 |

{style="table-layout:auto"}

有关目录服务的详细信息，请阅读[目录服务概述](../../catalog/home.md)。

## 数据准备 {#data-prep}

使用数据准备从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 增强了对导入和导出映射的支持 | 您现在可以将映射导出到CSV文件，并在电子表格中本地配置它们。 然后，您可以使用UI中的映射界面将更新的映射导入Experience Platform。 您可以使用此功能配置大量映射，而无需在UI中手动构建它们。 此外，在创建新数据流时，您可以直接将映射副本上传到Experience Platform以加快工作流程。 有关详细信息，请参阅[导入和导出映射](../../data-prep/ui/mapping.md#import-mapping)指南。 |

{style="table-layout:auto"}

有关详细信息，请阅读[数据准备概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 描述 |
| --- | --- |
| [(Beta) Marketo Engage人员同步](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | 使用[!DNL Marketo Engage Person Sync]连接器将人员受众中的更新流式传输到[!DNL Marketo Engage]实例中的相应记录。 此目标连接器为测试版，仅向部分客户提供。 要请求获取访问权限，请联系您的Adobe代表。 |
| [交易台CRM连接](/help/destinations/catalog/advertising/tradedesk-emails.md)正式可用 | [!DNL The Trade Desk CRM]连接现已正式可用。 使用[!DNL The Trade Desk] CRM目标向您的[!DNL Trade Desk]帐户激活配置文件，以便根据CRM数据进行受众定位和隐藏。 |
| [RainFocus与会者个人资料连接](/help/destinations/catalog/marketing-automation/rainfocus.md) | 使用[!DNL RainFocus Attendee Profiles]目标将客户配置文件从Adobe Experience Platform流式传输到[!DNL RainFocus]平台，以便创建和更新与会者配置文件。 |
| [Criteo连接](/help/destinations/catalog/advertising/criteo.md)常规可用性 | [!DNL Criteo]连接现已正式可用。 Criteo支持可信且有影响力的广告，为开放互联网上的每位消费者带来更丰富的体验。 凭借世界上最大的商业数据集和同类最佳的人工智能，Criteo可确保购物历程中的每个接触点都经过个性化，以在适当的时间通过适当的广告吸引客户。 |
| [[!DNL Amazon Ads] 连接](../../destinations/catalog/advertising/amazon-ads.md) | 以前的Beta版[!DNL Amazon Ads]连接器现已正式提供。 连接器也已更新，可以为所有同意将其个人数据用于广告的用户档案发送同意授予信号。 详细了解新的[Amazon广告同意信号](../../destinations/catalog/advertising/amazon-ads.md#destination-details)控件。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| 使用访问标签管理用户对目标数据流的访问 | 作为Real-Time CDP中基于[[!UICONTROL 属性的访问控制]](/help/access-control/abac/overview.md)功能的一部分，您现在可以对[目标数据流](/help/dataflows/ui/monitor-destinations.md)应用访问标签。 这样，您就可以确保组织中只有一部分用户有权访问特定的目标数据流。<br> **重要信息**：使用Experience Platform用户界面顶部的搜索框搜索目标数据流时，结果可能包括您的用户访问标签限制您查看的目标数据流。 此行为将在以后的更新中纠正。 |
| [Marketo Engage连接](/help/destinations/catalog/adobe/marketo-engage.md)的[受众级别报表](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) | 您现在可以[查看有关在受众级别划分的激活、排除或失败身份的信息](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations)，这些信息针对属于此目标数据流一部分的每个受众。 |
| 对[TikTok](/help/destinations/catalog/social/tiktok.md)和[Snap Inc](/help/destinations/catalog/advertising/snap-inc.md)连接的外部受众支持 | 您可以从[自定义上载](../../segmentation/ui/audience-portal.md#import-audience)和[联合受众合成](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/audiences)将外部受众激活到这些目标。 |

{style="table-layout:auto"}

**修复和增强** {#destinations-fixes-and-enhancements}

- Destination SDK测试工具中的问题已修复。 某些客户或合作伙伴遇到了[示例配置文件生成工具](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md)的问题，原因是在用于生成配置文件的架构包含具有`No format`选择器的数据类型时，该工具格式不受支持。
- 修复了在使用流服务API更新`targetConnection`目标规范时出现的问题。 在某些情况下，PATCH操作的行为与POST操作类似，会损坏现有数据流。 此问题现已修复，所有客户都可以使用流服务API更新其`targetConnection`规范。 [了解更多信息](/help/destinations/api/edit-destination.md#patch-target-connection)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持[!DNL Microsoft Dynamics]中的视图 | 使用[!DNL Microsoft Dynamics]源时，您现在可以摄取`"entityType": "view"`。 有关详细信息，请阅读有关[将 [!DNL Microsoft Dynamics] 源连接到Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md)的指南。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。

## 文档更新 {#documentation-updates}

### Edge Network与中心比较 {#edge}

[Edge Network与中心服务器比较](../../landing/edge-and-hub-comparison.md)提供了一个概述，其中详细介绍了Adobe Experience Platform的两种服务器类型(中心服务器和Edge Network)之间的差异，包括每种服务器类型上可用的服务、服务器的位置以及使用每种服务器类型的建议方案。

### 扩展的源流服务API参考 {#flow-service}

源的[[!DNL Flow Service] API引用](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections)已更新为新的API请求和响应示例。 将您自己的源集成到Experience Platform时，使用扩展的API引用创建和更新连接规范。 您还可以使用扩展的API引用对源实体执行状态转换，更新现有源连接和目标连接，以及根据特定筛选条件检索流和流规范。

### 使用沙盒工具备份对象配置 {#back-up-object-configurations}

请阅读[备份对象配置指南](../../sandboxes/use-cases/backup-object-configuration.md)以了解使用沙盒工具创建备份包的分步说明，以确保您的对象配置已存储并受保护。

### 使用沙盒工具实现卓越中心 {#center-of-excellence}

阅读[卓越中心指南](../../sandboxes/use-cases/center-of-excellence.md)以了解关于创建作为卓越中心的“黄金沙盒”包以高效共享关键配置的逐步说明。

### 数据湖中的体验事件数据集保留 {#experience-event-dataset-retention}

使用生存时间(TTL)控制Adobe Experience Platform中的Experience Event数据集保留。 [本指南](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md)将指导您评估、配置和管理TTL设置，以自动删除过期的记录、优化存储并保持数据的相关性。 探索增强数据生命周期管理的最佳实践、真实用例和关键注意事项。
