---
keywords: Experience Platform；激活；故障排除；护栏；指南；限制
title: 数据激活的默认护栏
solution: Experience Platform
product: experience platform
type: Documentation
description: 了解有关数据激活默认使用量和速率限制的更多信息。
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 2%

---

# 数据激活的护栏

>[!IMPORTANT]
>
>检查您的销售订单中的许可证权利以及相应的 [产品描述](https://helpx.adobe.com/legal/product-descriptions.html) 实际使用限制以及此护栏页面。

本页提供有关激活行为的默认使用量和速率限制。 查看以下护栏时，系统假定您已正确设置 [已连接到目标](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* 大多数客户不会超过这些默认限制。 如果您想了解自定义限制，请联系您的客户关怀代表。
>* 本文档中概述的限制不断得到改进。 请定期查看以获取最新信息。
>* 根据各个下游限制，某些目标的护栏可能会比此页面上记录的护栏更严格。 确保同时检查 [目录](/help/destinations/catalog/overview.md) 要连接并激活数据的目标页面。

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

以下护栏通常适用于以下激活： [所有目标类型](/help/destinations/destination-types.md#destination-types).

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 单个目标的最大受众数量 | 250 | 性能护栏 | 建议将最多250个受众映射到数据流中的单个目标。 <br><br> 如果您需要向某个目标激活超过250个受众，则可以： <ul><li> 取消映射您不想再激活的受众，或</li><li>创建到所需目标的新数据流，并将受众映射到此新数据流。</li></ul> <br> 请注意，对于某些目标，映射到目标的受众可能限制为250个以下。 这些目标将在页面中各自部分的下面进一步说明。 |
| 映射到目标的最大属性数 | 50 | 性能护栏 | 如果存在多个目标和目标类型，则可以选择要映射以导出的配置文件属性和身份。 为获得最佳性能，数据流中应将最多50个属性映射到目标。 |
| 最大目标数 | 100 | 系统强制的护栏 | 您最多可以创建100个可连接和激活数据的目标， *每个沙盒*. [Edge个性化目标（自定义个性化）](#edge-destinations-activation) 在100个推荐目的地中，最多可以包含10个。 |
| 激活到目标的数据类型 | 配置文件数据，包括身份和身份映射 | 系统强制的护栏 | 目前，只能导出 *配置文件记录属性* 到目标。 目前不支持导出描述事件数据的XDM属性。 |
| 激活到目标的数据类型 — 阵列和映射属性支持 | 不可用 | 系统强制的护栏 | 此时，它是 **非** 可以导出 *数组或映射属性* 到目标。 此规则的例外情况是 [身份映射](/help/xdm/field-groups/profile/identitymap.md)，它可以在流激活和基于文件的激活中导出。 |

{style="table-layout:auto"}

### 流激活 {#streaming-activation}

以下护栏适用于通过进行的激活 [流目标](/help/destinations/ui/activate-segment-streaming-destinations.md).

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每秒激活次数（包含配置文件导出的HTTP消息） | 不适用 | - | 当前每秒从Experience Platform发送到合作伙伴目标的API端点的消息数没有限制。 <br> 任何限制或延迟都由Experience Platform发送数据的端点决定。 确保同时检查 [目录](/help/destinations/catalog/overview.md) 要连接并激活数据的目标页面。 |

{style="table-layout:auto"}

### 批处理（基于文件）激活 {#batch-file-based-activation}

以下护栏适用于通过进行的激活 [批处理（基于文件）目标](/help/destinations/ui/activate-batch-profile-destinations.md).

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 激活频率 | 每日一次完全导出或更频繁的增量导出，每3、6、8或12小时一次。 | 系统强制的护栏 | 阅读 [导出完整文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [导出增量文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 文档部分，以了解有关批处理导出的频率递增的更多信息。 |
| 在给定小时可导出的最大受众数 | 100 | 性能护栏 | 建议向批处理目标数据流添加最多100个受众。 |
| 每个文件要激活的最大行数（记录） | 500万 | 系统强制的护栏 | Adobe Experience Platform会自动按每个文件500万条记录（行）拆分导出的文件。 每一行表示一个配置文件。 拆分文件名后附加一个数字，指示文件是较大导出的一部分，例如： `filename.csv`， `filename_2.csv`， `filename_3.csv`. 欲知更多信息，请参阅 [计划部分](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) “激活批次目标”教程的。 |

{style="table-layout:auto"}

### Ad-hoc activation {#ad-hoc-activation}

下面的护栏适用于 [临时激活](/help/destinations/api/ad-hoc-activation-api.md) 方法。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 根据临时激活作业激活的受众 | 80 | 系统强制的护栏 | 目前，每个临时激活作业最多可以激活80个受众。 尝试激活每个作业超过80个受众将导致作业失败。 此行为可能会在未来版本中发生更改。 |
| 每个受众的并发临时激活作业 | 1 | 系统强制的护栏 | 不要为每个受众运行多个并发临时激活作业。 |

{style="table-layout:auto"}

### Edge个性化目标激活 {#edge-destinations-activation}

以下护栏适用于通过进行的激活 [边缘个性化目标](/help/destinations/destination-types.md#streaming-profile-export).

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 最大数量 [自定义个性化](/help/destinations/catalog/personalization/custom-personalization.md) 目标 | 10 | 性能护栏 | 您可以将数据流设置为每个沙盒10个自定义个性化目标。 |
| 每个沙盒映射到个性化目标的最大属性数 | 30 | 系统强制的护栏 | 数据流中最多可以将30个属性映射到每个沙盒的个性化目标。 |
| 映射到单个的最大受众数 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 目标 | 50 | 性能护栏 | 在一个针对单个Adobe Target目标的激活流中，您最多可以激活50个受众。 |

{style="table-layout:auto"}

### 数据集导出 {#dataset-exports}

当前支持数据集导出 **[!UICONTROL 先完全备份，然后增量备份]** [模式](/help/destinations/ui/export-datasets.md#scheduling). 本节中介绍的护栏 *应用于第一次完全导出* 在设置数据集导出工作流后发生。

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### 数据集类型 {#dataset-types}

数据集导出护栏适用于从Experience Platform导出的两种类型的数据集，如下所述：

**基于XDM体验事件架构的数据集**
在基于XDM体验事件架构的数据集的情况下，数据集架构包括顶级 *时间戳* 列。 数据以仅追加方式摄取。

**基于XDM Individual Profile架构的数据集**
在基于XDM个人资料架构的数据集的情况下，数据集架构不包括顶级 *时间戳* 列。 数据以更新插入方式摄取。

以下软护栏适用于从Experience Platform中导出的所有数据集。 此外，还请查看下面针对不同数据集和压缩类型的硬护栏。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 导出数据集的大小 | 50亿条记录 | 性能护栏 | 此处所述的数据集导出限制为 *软护栏*. 例如，用户界面不会阻止您导出超过50亿条记录的数据集，但行为不可预测，导出可能会失败或导出延迟很长。 |

{style="table-layout:auto"}

#### 计划数据集导出的护栏

对于计划或定期数据集导出，以下护栏对于导出文件的两种格式（JSON或parquet）是相同的，并且按数据集类型分组。

>[!WARNING]
>
>仅在压缩模式下支持导出到JSON文件。

| 数据集类型 | 护栏 | 护栏类型 | 描述 |
---------|----------|---------|-------|
| 基于以下项的数据集 **XDM体验事件架构** | 最近365天的数据 | 系统强制的护栏 | 将导出上一个日历年的数据。 |
| 基于以下项的数据集 **XDM个人资料架构** | 数据流中所有导出文件的十亿条记录 | 系统强制的护栏 | 对于压缩的JSON或parquet文件，数据集的记录数必须少于100亿，对于未压缩的parquet文件，数据集的记录数必须少于100万，否则导出失败。 如果尝试导出的数据集大于允许的阈值，请减小该数据集的大小。 |

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

详细了解 [导出数据集](/help/destinations/ui/export-datasets.md).


### Destination SDK护栏 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) 是一套配置API，允许您配置目标集成模式，以便Experience Platform根据所选数据和身份验证格式向端点交付受众和配置文件数据。 以下护栏适用于您使用Destination SDK配置的目标。

| 护栏 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 最大数量 [专用自定义目标](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 性能护栏 | 您最多可以使用Destination SDK创建5个私有自定义流或批处理目标。 如果您需要创建5个以上的此类目标，请联系自定义关怀代表。 |
| Destination SDK的配置文件导出策略 | <ul><li>`maxBatchAgeInSecs` （最小1.800，最大3.600）</li><li>`maxNumEventsInBatch` （最小1.000，最大10.000）</li></ul> | 系统强制的护栏 | 使用时 [可配置聚合](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 目标选项，请注意确定HTTP消息发送到基于API的目标的频率以及消息应包含的用户档案数的最小值和最大值。 |

{style="table-layout:auto"}

### 目标限制和重试策略 {#destination-throttling-and-retry-policy}

有关给定目标的限制阈值或限制的详细信息。 此部分还提供了有关目标的重试策略的信息。

| 目标类型 | 描述 |
| --- | --- |
| 企业目标(HTTP API、Amazon Kinesis、Azure EventHubs) | 在95%的时间中，Experience Platform会尝试为成功发送的消息提供少于10分钟的吞吐量延迟，每个数据流到企业目标的请求速率低于每秒10,000次。 <br> 如果对您的企业目标的请求失败，Experience Platform将存储失败的请求，并重试两次以将请求发送到您的端点。 |

{style="table-layout:auto"}

## 后续步骤

请参阅Real-Time CDP产品描述文档中的以下文档，了解有关其他Experience Platform服务护栏、端到端延迟信息和许可信息的更多信息：

* [Real-Time CDP护栏](/help/rtcdp/guardrails/overview.md)
* [端到端延迟图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 用于各种Experience Platform服务。
* [Real-time Customer Data Platform （B2C版本 — Prime和Ultimate包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2P — 主要和最终包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform （B2B - Prime和Ultimate包）](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
