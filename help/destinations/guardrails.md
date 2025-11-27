---
keywords: Experience Platform；激活；故障排除；护栏；指南；限制
title: 数据激活的默认护栏
solution: Experience Platform
product: experience platform
type: Documentation
description: 了解有关数据激活默认使用量和速率限制的更多信息。
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 216621652697c378164125a6d0e125a33ee008be
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 2%

---

# 数据激活的护栏

>[!IMPORTANT]
>
>除了此护栏页面外，还检查销售订单中的许可证授权和相应的[产品描述](https://helpx.adobe.com/cn/legal/product-descriptions.html)中的实际使用限制。

本页提供有关激活行为的默认使用量和速率限制。 查看以下护栏时，假定您已正确[连接到目标](/help/destinations/ui/connect-destination.md)。

>[!NOTE]
>
>* 大多数客户不会超过这些默认限制。 如果您想了解自定义限制，请联系您的客户关怀代表。
>* 本文档中概述的限制不断得到改进。 请定期查看以获取最新信息。
>* 根据各个下游限制，某些目标的护栏可能会比此页面上记录的护栏更严格。 请确保同时查看要连接并激活数据的目标的[目录](/help/destinations/catalog/overview.md)页面。

## 护栏类型 {#limit-types}

此文档有两种类型的默认限制：

| 护栏类型 | 描述 |
|----------|---------|
| **性能护栏（软限制）** | 性能护栏是与用例范围相关的使用限制。 当超出性能护栏时，您可能会遇到性能下降和延迟问题。 Adobe不对此类性能下降负责。 始终超过性能护栏的客户可以选择许可额外的容量，以避免性能下降。 |
| **系统强制的护栏（硬限制）** | Real-Time CDP UI或API强制实施系统强制的护栏。 这些限制不得超过，因为UI和API将阻止您这样做或您会返回错误。 |

{style="table-layout:auto"}


## 激活限制 {#activation-limits}

在将实时客户档案数据激活到目标时，以下护栏提供了建议的限制。

### 常规激活护栏 {#general-activation-guardrails}

以下护栏通常适用于通过[所有目标类型](/help/destinations/destination-types.md#destination-types)进行的激活。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 单个目标的最大受众数量 | 250 | 性能护栏 | 建议将最多250个受众映射到数据流中的单个目标。 <br><br>如果您需要向某个目标激活超过250个受众，您可以： <ul><li> 取消映射您不想再激活的受众，或</li><li>创建到所需目标的新数据流，并将受众映射到此新数据流。</li></ul> <br>请注意，对于某些目标，映射到目标的受众可能限制为250个以下。 这些目标将在页面中各自部分的下面进一步说明。 |
| 映射到目标的最大属性数 | 50 | 性能护栏 | 如果存在多个目标和目标类型，则可以选择要映射以导出的配置文件属性和身份。 为获得最佳性能，数据流中应将最多50个属性映射到目标。 |
| 最大目标数 | 100 | 系统强制的护栏 | 您最多可以创建100个可以连接和激活数据的目标，每个沙盒&#x200B;*为*。 [Edge个性化目标（自定义个性化）](#edge-destinations-activation)最多可以构成100个推荐目标中的10个。 |
| 激活到目标的数据类型 | 配置文件数据，包括身份和身份映射 | 系统强制的护栏 | 目前，只能将&#x200B;*配置文件记录属性*&#x200B;导出到目标。 目前不支持导出描述事件数据的XDM属性。 |
| 激活到目标的数据类型 — 阵列和映射属性支持 | 部分可用 | 系统强制的护栏 | 您可以将数组属性导出到[基于文件的目标](/help/destinations/destination-types.md#file-based)。 [参阅更多](/help/destinations/ui/export-arrays-maps-objects.md)关于该功能的信息。 |

{style="table-layout:auto"}

### 流激活 {#streaming-activation}

以下护栏适用于通过[流式目标](/help/destinations/ui/activate-segment-streaming-destinations.md)进行的激活。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每秒激活次数（包含配置文件导出的HTTP消息） | 不适用 | - | 当前每秒从Experience Platform发送到合作伙伴目标的API端点的消息数没有限制。 <br>任何限制或延迟都由Experience Platform发送数据的端点决定。 请确保同时查看要连接并激活数据的目标的[目录](/help/destinations/catalog/overview.md)页面。 |

{style="table-layout:auto"}

### 批处理（基于文件）激活 {#batch-file-based-activation}

以下护栏适用于通过[批处理（基于文件）目标](/help/destinations/ui/activate-batch-profile-destinations.md)进行的激活。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 激活频率 | 每日一次完全导出或更频繁的增量导出，每3、6、8或12小时一次。 | 系统强制的护栏 | 有关批处理导出的频率递增的详细信息，请阅读[导出完整文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[导出增量文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)文档部分。 |
| 在给定小时可导出的最大受众数 | 100 | 性能护栏 | 建议向批处理目标数据流添加最多100个受众。 |
| 每个文件要激活的最大行数（记录） | 500万 | 系统强制的护栏 | Adobe Experience Platform会自动按每个文件500万条记录（行）拆分导出的文件。 每一行表示一个配置文件。 拆分文件名后附加一个数字，指示文件是较大导出的一部分，例如： `filename.csv`、`filename_2.csv`、`filename_3.csv`。 有关详细信息，请参阅激活批处理目标教程的[计划部分](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)。 |
| 数据流中激活的自定义上传受众的最大数量 | 10 | 系统强制的护栏 | 将[自定义上传受众](/help/segmentation/ui/audience-portal.md#import-audience)激活到基于文件的批处理目标时，您可以在数据流中激活10个此类受众的限制。 了解有关[将自定义上传受众激活到基于批处理文件的目标](/help/destinations/ui/activate-batch-profile-destinations.md#select-audiences)的工作流的详细信息。 |

{style="table-layout:auto"}

### Ad-hoc activation {#ad-hoc-activation}

以下护栏适用于[临时激活](/help/destinations/api/ad-hoc-activation-api.md)方法。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 根据临时激活作业激活的受众 | 80 | 系统强制的护栏 | 目前，每个临时激活作业最多可以激活80个受众。 尝试激活每个作业超过80个受众将导致作业失败。 此行为可能会在未来版本中发生更改。 |
| 每个受众的并发临时激活作业 | 1 | 系统强制的护栏 | 不要为每个受众运行多个并发临时激活作业。 |

{style="table-layout:auto"}

### Edge个性化目标激活 {#edge-destinations-activation}

以下护栏适用于通过[边缘个性化目标](/help/destinations/destination-types.md#advanced-enterprise-destinations)进行的激活。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| [自定义个性化](/help/destinations/catalog/personalization/custom-personalization.md)目标的最大数量 | 10 | 性能护栏 | 您可以将数据流设置为每个沙盒10个自定义个性化目标。 |
| 每个沙盒映射到个性化目标的最大属性数 | 30 | 性能护栏 | 数据流中最多可以将30个属性映射到每个沙盒的个性化目标。 |
| 映射到单个[Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)目标的受众的最大数量 | 50 | 性能护栏 | 在一个针对单个Adobe Target目标的激活流中，您最多可以激活50个受众。 |

{style="table-layout:auto"}

### 数据集导出 {#dataset-exports}

当前在&#x200B;**[!UICONTROL First Full and then Incremental]** [模式](/help/destinations/ui/export-datasets.md#scheduling)中支持数据集导出。 此部分&#x200B;*中描述的护栏适用于数据集导出工作流设置后出现的第一个完全导出*。

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### 数据集类型 {#dataset-types}

数据集导出护栏适用于从Experience Platform导出的两种类型的数据集，如下所述：

**基于XDM体验事件架构的数据集和基于任何其他架构的数据集**

对于基于XDM体验事件架构的数据集，数据集架构包括顶级时间戳列。 数据以仅追加方式摄取。 在基于任何其他架构的数据集的情况下，数据集架构可能包括时间戳列，并且数据以更新插入方式摄取。

以下软护栏适用于从Experience Platform导出的所有数据集。 此外，还请查看下面针对不同数据集和压缩类型的硬护栏。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 导出数据集的大小 | 50亿条记录 | 性能护栏 | 此处描述的数据集导出限制为&#x200B;*软护栏*。 例如，用户界面不会阻止您导出超过50亿条记录的数据集，但行为不可预测，导出可能会失败或导出延迟很长。 |

{style="table-layout:auto"}

#### 计划数据集导出的护栏

对于计划或定期数据集导出，以下护栏对于导出文件的两种格式（JSON或parquet）是相同的，并且按数据集类型分组。

>[!WARNING]
>
>仅在压缩模式下支持导出到JSON文件。

| 数据集类型 | 护栏 | 护栏类型 | 描述 |
|---------|----------|---------|-------|
| 基于&#x200B;**XDM体验事件架构**&#x200B;的数据集 | 最近365天的数据 | 系统强制的护栏 | 将导出上一个日历年的数据。 |
| 基于&#x200B;**除XDM体验事件架构**&#x200B;之外的任何架构的数据集 | 数据流中所有导出文件的十亿条记录 | 系统强制的护栏 | 对于压缩的JSON或parquet文件，数据集的记录数必须少于100亿，对于未压缩的parquet文件，数据集的记录数必须少于100万，否则导出失败。 如果尝试导出的数据集大于允许的阈值，请减小该数据集的大小。 |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a dataflow | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

阅读[导出数据集](/help/destinations/ui/export-datasets.md)以了解更多信息。


### Destination SDK护栏 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md)是一套配置API，允许您为Experience Platform配置目标集成模式，以根据您选择的数据和身份验证格式将受众和配置文件数据交付到您的端点。 以下护栏适用于您使用Destination SDK配置的目标。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| [私有自定义目标的最大数目](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 性能护栏 | 使用Destination SDK，您最多可以创建5个私有自定义流或批处理目标。 如果您需要创建5个以上的此类目标，请联系自定义关怀代表。 |
| Destination SDK的配置文件导出策略 | <ul><li>`maxBatchAgeInSecs`（最小1,800个，最大3,600个）</li><li>`maxNumEventsInBatch`（最小1,000个，最大10,000个）</li></ul> | 系统强制的护栏 | 对您的目标使用[可配置的聚合](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation)选项时，请注意用于确定HTTP消息发送到基于API的目标的频率以及消息应包含的用户档案数的最小值和最大值。 |
| Destination SDK的OAuth 2令牌生命周期 | 建议至少24小时 | 性能护栏 | 对于使用[OAuth 2授权](/help/destinations/destination-sdk/functionality/destination-configuration/oauth2-authorization.md)的目标，Adobe建议将访问令牌生命周期值设置为至少24小时。 如果连接中的令牌的生命周期不到1小时，则可能会导致配置文件在激活期间被丢弃。 |

{style="table-layout:auto"}

### 目标限制和重试策略 {#destination-throttling-and-retry-policy}

有关给定目标的限制阈值或限制的详细信息。 此部分还提供了有关目标的重试策略的信息。

| 目标类型 | 描述 |
| --- | --- |
| 企业目标(HTTP API、Amazon Kinesis、Azure EventHubs) | 在95%的时间中，Experience Platform会尝试为成功发送的消息提供少于10分钟的吞吐量延迟，每个数据流向企业目标的请求速率低于每秒10,000次。 <br>如果对您的企业目标的请求失败，Experience Platform将存储失败的请求，并重试两次以将请求发送到您的端点。 |

{style="table-layout:auto"}

## 后续步骤

请参阅Real-Time CDP产品描述文档中的以下文档，了解有关其他Experience Platform服务护栏、端到端延迟信息和许可信息的更多信息：

* [Real-Time CDP护栏](/help/rtcdp/guardrails/overview.md)
* [各种Experience Platform服务的端到端延迟图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=zh-Hans#end-to-end-latency-diagrams)。
* [Real-Time Customer Data Platform (B2C Edition - Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
