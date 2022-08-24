---
title: Adobe Experience Platform发行说明2022年8月
description: 2022年8月版Adobe Experience Platform发行说明。
source-git-commit: 5967dee9c8b1c05ebd103998021e02a47ac3982c
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 7%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 8 月 24 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据准备](#data-prep)
- [体验数据模型(XDM)](#xdm)
- [实时客户资料](#profile)
- [分段服务](#segmentation)
- [源](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 支持摄取带有警告的记录 | 数据准备现在会将警告（非严重错误）本地化到字段，并允许摄取行的其余部分。 现在，所有映射器转换错误都会报告为警告，部分摄取的行被视为成功，并带有警告。  还支持对包含警告和诊断详细信息的记录进行监控。 部分摄取带有警告的记录当前仅可用于流数据。 查看 [摄取带警告的记录](../../sources/tutorials/ui/monitor-streaming.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

详细了解 [!DNL Data Prep]，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 全局模式 | [[!UICONTROL AJO实体架构]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | 描述Adobe Journey Optimizer的非规范化实体。 |
| 类 | [[!UICONTROL AJO执行实体]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-execution-entity.schema.json) | 描述用于分段的Adobe Journey Optimizer执行实体。 |
| 字段组 | [[!UICONTROL Workfront工作对象]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | 引用Adobe Workfront所有较低级别特定对象字段组的包装器字段组。 |

{style=&quot;table-layout:auto&quot;}

**更新了XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL Journey Orchestration步骤事件常用字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 添加了两个新属性： `origTimeStamp` 和 `experienceID`. |
| 字段组 | [[!UICONTROL 区段成员资格详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | 除 [!UICONTROL XDM个人配置文件]，此字段组现在也可以在基于XDM业务帐户类的架构中使用。 |
| 字段组 | （多个） | 与Marketo B2B活动相关的多个字段组已更新为稳定状态。 请参阅以下内容 [拉取请求](https://github.com/adobe/xdm/pull/1593/files) 以了解详细信息。 |
| 字段组 | （多个） | 多个与天气相关的字段组已更新，以修复 `uvIndex` 和 `sunsetTime`. 请参阅以下内容 [拉取请求](https://github.com/adobe/xdm/pull/1602/files) 以了解详细信息。 |
| 数据类型 | [[!UICONTROL 产品列表项]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 新资产 `productImageUrl` 已添加。 |
| 数据类型 | [[!UICONTROL Qoe数据详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 新资产 `framesPerSecond` 已添加。 |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` 已更名为 `appVersion`。`meta:enum` 和 `description` 字段也已更新。 |
| 数据类型和字段组 | （多个） | 一些媒体数据类型和字段组具有新字段和更新的描述。 请参阅以下内容 [拉取请求](https://github.com/adobe/xdm/pull/1582/files) 以了解详细信息。 |
| (全部) | （多个） | 包含 `enum` 字段现在还包含对应的 `meta:enum` 字段来表示每个约束的显示值。 请参阅以下内容 [拉取请求](https://github.com/adobe/xdm/pull/1601/files) 以了解详细信息。 |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## 实时客户个人资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 利用用户档案，可将客户数据整合到统一视图中，为每次客户互动提供一个加盖时间戳的可操作帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 孤立的配置文件边缘属性清理 | 对于所有组织，用户档案服务现在每天都会删除用户活动区域的剩余边缘属性，以便在系统中更准确地显示用户档案。 此清理在删除给定配置文件的所有配置文件片段之后进行，并且应会影响从其中合并的数据集中合并的配置文件 `com_adobe_aep_profile_region_dataset` 标记为 `true`. 这可能会在许可证使用情况功能板的“可寻址受众”量度中显示一个下降，并且可能在“配置文件”功能板的“配置文件计数”量度中显示一个下降，因为这些量度包含此版本之前剩余的边缘属性片段。 |

{style=&quot;table-layout:auto&quot;}

要了解有关实时客户资料的更多信息，包括有关使用资料数据的教程和最佳实践，请首先阅读 [实时客户资料概述](../../profile/home.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持4000个区段 | 现在，所有具有Platform的组织最多可支持4000个区段定义。 有关此更改如何影响区段作业API的更多信息，请阅读 [segment job endpoint指南](../../segmentation/api/segment-jobs.md) |

有关 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 自助源（批处理SDK）的正式可用性 | 开发、测试和集成基于REST API的数据源，以便使用易于配置的源规范将批量数据引入Experience Platform。 通过源SDK，您可以： <ul><li>为Experience Platform目录配置新源。</li><li>为源定义规范，包括与支持的身份验证类型、计划以及如何获取资源数据有关的信息。</li><li>为新源创建面向用户的文档。</li></ul> 有关更多信息，请阅读 [自助源（批量SDK）](../../sources/sources-sdk/overview.md). |
| 全面提供 [!DNL Google BigQuery] 来源 | 使用 [!DNL Google BigQuery] 从 [!DNL Google BigQuery] data warehouse到Experience Platform。 有关更多信息，请阅读 [[!DNL Google BigQuery] 来源](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] 来源（测试版） | 使用 [!DNL Teradata Vantage] 来源将数据从混合多云环境中摄取到Experience Platform。 有关更多信息，请阅读 [[!DNL Teradata Vantage] 来源](../../sources/connectors/databases/teradata-vantage.md). |
| 跨区域支持Adobe Analytics源 | 您现在可以接收来自任何地区（美国、英国或新加坡）的报告包。 必须将报表包映射到与在其中创建源连接的Experience Platform沙盒实例相同的组织。 有关更多信息，请阅读 [在UI中创建Adobe Analytics源连接](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |
| 对按需摄取的API支持 | 使用按需摄取，通过 [!DNL Flow Service] API。 创建的流量运行必须设置为一次性摄取。 有关更多信息，请阅读 [使用API为按需摄取创建流程运行](../../sources/tutorials/api/on-demand-ingestion.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

要进一步了解源，请参阅 [源概述](../../sources/home.md).
