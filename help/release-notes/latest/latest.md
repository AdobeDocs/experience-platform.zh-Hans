---
title: Adobe Experience Platform 发行说明（2025 年 2 月）
description: Adobe Experience Platform 的 2025 年 2 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 300be2f922f81f0666a794815cb27777802efb60
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 94%

---

# Adobe Experience Platform 发行说明

>[!TIP]
>
>此版本包括对联合受众构成附加组件的改进。如需了解更多信息，请阅读[联合受众构成发行说明](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/release-notes)。

**发行日期：2025 年 2 月 18 日**

Adobe Experience Platform 中现有功能和文档的更新：

- [AI 助手](#ai-assistant)
- [目录服务](#catalog-service)
- [数据准备](#data-prep)
- [目标](#destinations)
- [源](#sources)
- [文档更新](#documentation-updates)
   - [Edge Network 与 Hub Network 比较](#edge)
   - [扩展的源 Flow Service API](#flow-service)
   - [使用沙盒工具备份对象配置](#back-up-object-configurations)
   - [使用沙盒工具启用卓越中心](#center-of-excellence)
   - [数据湖中的体验事件数据集保留](#experience-event-dataset-retention)

## AI 助手 {#ai-assistant}

Adobe Experience Platform 中的 AI 助手是一种对话体验，您可以使用它来加速 Adobe 应用程序中的工作流程。您可以使用 AI 助手更好地了解产品知识、解决问题或搜索信息并找到运营洞察。AI 助手支持 Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer 和 Customer Journey Analytics。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 运营洞察正式发布 | AI 助手中的运营洞察现已正式发布。运营洞察是指 AI 助手针对您的元数据对象（属性、受众、数据流、数据集、目标、历程、模式和来源）生成的回答，包括计数、查找和谱系影响。运营洞察不查看沙盒内的任何数据。有关更多信息，请阅读 [AI 助手 UI 指南](../../ai-assistant/ui-guide.md)。 |
| 支持问题自动完成 | 向 AI 助手输入问题时，您现在可以从 AI 助手提供的推荐问题列表中进行选择。使用此功能可以进一步加速您的 AI 助手工作流程。有关更多信息，请阅读[使用 AI 助手问题自动完成](../../ai-assistant/ui-guide.md#use-question-autocomplete)指南。 |
| 支持数据集可观察性 | 您现在可以使用 AI 助手回答有关存储大小和行数等特定数据集量度的问题。数据可观察性问题支持限定符，您可以使用限定符按特定时段筛选查询。有关更多信息，请阅读 [AI 助手问题指南](../../ai-assistant/questions.md)。 |

{style="table-layout:auto"}

有关更多信息，请阅读 [AI 助手概述](../../ai-assistant/home.md)。

## 目录服务 {#catalog-service}

目录服务是 Adobe Experience Platform 中记录数据位置和沿袭的系统。虽然所有摄取到 Experience Platform 中的数据均作为文件和目录存储在数据湖中，但目录保存这些文件和目录的元数据和描述以供查找和监控目的。

| 功能 | 描述 |
| --- | --- |
| 新的 API 端点 | 使用新的[目录服务 API /v2/数据集/{DATASET_ID} 端点](../../catalog/api/update-object.md#patch-v2-notation)更有效地管理 Adobe Experience Platform 数据集元数据。轻松更新复杂的深层嵌套数据集属性，因为系统会自动创建缺失的路径级别，从而节省您的时间、减少手动步骤并将错误降至最低。 |

{style="table-layout:auto"}

有关目录服务的更多信息，请阅读[目录服务概述](../../catalog/home.md)。

## 数据准备 {#data-prep}

使用数据准备从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 增强对导入和导出映射的支持 | 您现在可以将映射导出到 CSV 文件，并在电子表格上进行本地配置。然后，您可以使用 UI 中的映射界面将更新后的映射导入 Experience Platform。您可以使用此功能配置大量映射，而无需在 UI 中手动生成映射。此外，在创建新数据流时，您可以将映射的副本直接上传到 Experience Platform，以加快工作流程。有关更多信息，请阅读[导入和导出映射](../../data-prep/ui/mapping.md#import-mapping)指南。 |

{style="table-layout:auto"}

有关更多信息，请阅读[数据准备概述](../../data-prep/home.md)。

## 目标（更新日期：2月20日） {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 描述 |
| --- | --- |
| [（Beta）Marketo Engage 人员同步](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | 使用[!DNL Marketo Engage Person Sync] 连接器将人员受众的更新传输到您实例中的相应记录[!DNL Marketo Engage]。此目标连接器处于测试阶段，仅提供给特定客户。要请求访问权限，请与 Adobe 代表联系。 |
| [Trade Desk CRM 连接](/help/destinations/catalog/advertising/tradedesk-emails.md)正式发布 | [!DNL The Trade Desk CRM] 连接现已正式发布。使用 [!DNL The Trade Desk] CRM 目标为您的帐户激活轮廓[!DNL Trade Desk]，以根据 CRM 数据进行受众目标市场选择和禁止。 |
| [RainFocus 与会者轮廓连接](/help/destinations/catalog/marketing-automation/rainfocus.md) | 使用[!DNL RainFocus Attendee Profiles]目标将客户轮廓从 Adobe Experience Platform 传输到[!DNL RainFocus]平台，以创建和更新与会者轮廓。 |
| [Criteo 连接](/help/destinations/catalog/advertising/criteo.md)正式发布 | [!DNL Criteo] 连接现已正式发布。Criteo 支持值得信赖且具有影响力的广告，在开放的互联网上为每位消费者带来更丰富的体验。Criteo 拥有全球最大的商业数据集和同类最佳 AI，可确保购物历程中的每个接触点都是个性化的，以便在合适的时间向客户推送合适的广告。 |
| [[!DNL Amazon Ads] 连接](../../destinations/catalog/advertising/amazon-ads.md) | [!DNL Amazon Ads] 连接器之前处于测试阶段，现已正式发布。该连接器也已更新，可向所有同意将其个人数据用于广告的用户发送同意信号。参阅更多关于新的 [Amazon 广告同意信号](../../destinations/catalog/advertising/amazon-ads.md#destination-details)控件。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| 使用访问标签管理用户对目标数据流的访问权限 | 作为 Real-Time CDP 中[[!UICONTROL 基于属性的访问控制]](/help/access-control/abac/overview.md)功能的一部分，您现在可以将访问标签应用于[目标数据流](/help/dataflows/ui/monitor-destinations.md)。这样，您就可以确保组织中只有一部分用户可以访问特定的目标数据流。<br> **重要提示**：使用 Experience Platform 用户界面顶部的搜索框搜索目标数据流时，结果可能包括用户访问标签限制您查看的目标数据流。这种行为将在未来的更新中得到纠正。 |
| 针对 [Marketo Engage 连接](/help/destinations/catalog/adobe/marketo-engage.md)的[受众级报告](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) | 您现在可以[查看](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations)有关此目标数据流中每个受众的激活、排除或失败身份信息（按受众级细分）。 |
| 为 [TikTok](/help/destinations/catalog/social/tiktok.md) 和 [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) 连接提供外部受众支持 | 您可以通过[自定义上传](../../segmentation/ui/audience-portal.md#import-audience)和[联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/start/audiences)将外部受众激活到这些目标。 |
| 将阵列、映射和对象导出到云存储目标 | 在连接到云存储目标时，通过使用新的&#x200B;**[!UICONTROL 导出阵列、映射、对象]**&#x200B;切换，您可以将复杂对象新导出到选定的目标。 [参阅更多](/help/destinations/ui/export-arrays-calculated-fields.md)关于该功能的信息。 |

{style="table-layout:auto"}

**修复和增强** {#destinations-fixes-and-enhancements}

- Destination SDK 测试工具中的一个问题已修复。当用于生成轮廓的模式包含带有 `No format` 选择器的数据类型时，由于格式不受支持，一些客户或合作伙伴在使用[样本轮廓生成工具](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md)时遇到了问题。
- 修复了使用 Flow Service API 更新目标 `targetConnection` 规范时出现的问题。在某些情况下，PATCH 运行的行为与 POST 运行类似，会破坏现有的数据流。此问题现已修复，所有客户都可以使用 Flow Service API 来更新他们的 `targetConnection` 规范。[了解更多信息](/help/destinations/api/edit-destination.md#patch-target-connection)。
- 将用户档案导出到基于文件的目标时，重复数据删除可确保在多个用户档案共享相同的重复数据删除键和相同的引用时间戳时，仅导出一个用户档案。 此版本包括了对重复数据删除流程的更新，确保使用相同的坐标连续运行将始终产生相同的结果，从而提高一致性。 [了解更多信息](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp)。

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持 [!DNL Microsoft Dynamics] 中的视图 | 您现在可以在`"entityType": "view"`使用源时[!DNL Microsoft Dynamics]进行摄取。有关更多信息，请阅读将源[连接 [!DNL Microsoft Dynamics] 到 Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md) 指南。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。

## 文档更新 {#documentation-updates}

### Edge Network 与 Hub Network 比较 {#edge}

[Edge Network 与 Hub Network 比较](../../landing/edge-and-hub-comparison.md)概述了 Adobe Experience Platform 两种服务器类型（Hub Network 和 Edge Network）之间的详细区别，包括每种服务器类型可提供哪些服务、服务器的位置以及使用每种服务器类型的推荐场景。

### 扩展的源 Flow Service API 参考 {#flow-service}

更新了源的 [[!DNL Flow Service] API 参考](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections)，包含新的 API 请求和响应示例。在将您自己的源集成到 Experience Platform 时，使用扩展的 API 参考来创建和更新连接规范。您还可以使用扩展的 API 参考对源实体执行状态过渡、更新现有的源和目标连接，并根据特定的过滤条件检索流和流规范。

### 使用沙盒工具备份对象配置 {#back-up-object-configurations}

阅读[对象配置备份指南](../../sandboxes/use-cases/backup-object-configuration.md)，获取使用沙盒工具创建备份包的分步说明，以确保存储和保护您的对象配置。

### 使用沙盒工具启用卓越中心 {#center-of-excellence}

阅读[卓越中心指南](../../sandboxes/use-cases/center-of-excellence.md)，获取创建“黄金沙盒”包的分步说明，该包用作高效共享关键配置的卓越中心。

### 数据湖中的体验事件数据集保留 {#experience-event-dataset-retention}

使用生存时间（TTL）控制 Adobe Experience Platform 中的体验事件数据集保留。[本指南](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md)将引导您评估、配置和管理 TTL 设置，以自动移除过时的记录、优化存储并保持数据的相关性。探索最佳实践、实际用例和关键考虑因素，以增强您的数据生命周期管理。
