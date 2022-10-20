---
keywords: Experience Platform；激活；疑难解答；护栏；准则；限制
title: 激活数据的默认防护
solution: Experience Platform
product: experience platform
type: Documentation
description: 了解有关数据激活默认使用和速率限制的更多信息。
source-git-commit: 69496d2e00ce866413786160d4524cabd03ae350
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 3%

---

# 激活数据的防护

本页提供与激活行为有关的默认使用和费率限制。 在查看以下护栏时，我们假定您已正确 [连接到目标](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* 大多数客户未超出这些默认限制。 如果您想了解自定义限制，请联系您的客户关怀代表。
>* 本文档中概述的限制正在不断改进。 请定期查看以获取最新信息。
>* 根据单个下游限制，某些目标的防护可能比此页面中记录的目标紧。 另请务必检查 [目录](/help/destinations/catalog/overview.md) 连接并激活数据的目标页面。


## 限制类型 {#limit-types}

本文档中有两种类型的默认限制：

* **软限制：** 可以超出软限制，但软限制为系统性能提供了建议的准则。
* **硬限制：** 硬限制提供绝对最大值。 Experience PlatformUI或API不允许您超出此限制，或者，如果超出此限制，则会返回错误。


## 激活限制 {#activation-limits}

以下护栏在将实时客户资料数据激活到目标时提供建议的限制。

### 常规激活护栏 {#general-activation-guardrails}

以下护栏通常适用于通过 [所有目标类型](/help/destinations/destination-types.md#destination-types).

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 单个目标的最大区段数 | 250 | 柔和 | 建议在数据流中最多将250个区段映射到单个目标。 <br><br> 如果您需要将250个以上的区段激活到目标，则可以： <ul><li> 取消映射您不希望再激活的区段，或</li><li>创建到所需目标的新数据流，并将区段映射到此新数据流。</li></ul> <br> 请注意，对于某些目标，您可能限制为映射到该目标的区段少于250个。 这些目标在页面的下面各节中进一步标注。 |
| 最大目标数 | 100 | 柔和 | 建议最多创建100个目标，以便您将数据连接并激活到 *每个沙盒*. [边缘个性化目标（自定义个性化）](#edge-destinations-activation) 在100个推荐目标中，最多可以包含10个目标。 |
| 映射到目标的最大属性数 | 50 | 柔和 | 对于多个目标和目标类型，您可以选择要映射以供导出的配置文件属性和标识。 为了获得最佳性能，数据流中最多应映射50个属性到目标。 |
| 激活到目标的数据类型 | 用户档案数据，包括身份和身份映射 | 硬 | 目前，只能导出 *配置文件记录属性* 到目标。 目前不支持导出描述事件数据的XDM属性。 |
| 激活到目标的数据类型 — 阵列和映射属性支持 | 不可用 | 硬 | 此时，它 **not** 可导出 *数组或映射属性* 到目标。 此规则的例外是 [身份映射](/help/xdm/field-groups/profile/identitymap.md)，可在基于流和文件的激活中导出。 |

{style=&quot;table-layout:auto&quot;}

### 流激活 {#streaming-activation}

以下护栏适用于通过 [流目标](/help/destinations/ui/activate-segment-streaming-destinations.md).

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每秒激活次数（具有配置文件导出的HTTP消息） | 不适用 | - | 当前，从Experience Platform到合作伙伴目标的API端点每秒发送的消息数没有限制。 <br> 任何限制或延迟都由Experience Platform发送数据的端点规定。 另请务必检查 [目录](/help/destinations/catalog/overview.md) 连接并激活数据的目标页面。 |

{style=&quot;table-layout:auto&quot;}

### 批量（基于文件）激活 {#batch-file-based-activation}

以下护栏适用于通过 [批量（基于文件）目标](/help/destinations/ui/activate-batch-profile-destinations.md).

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 激活频率 | 每3、6、8或12小时进行一次每日完整出口或更频繁的增量出口。 | 硬 | 阅读 [导出完整文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [导出增量文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 文档章节，以了解有关批量导出的频率增量的更多信息。 |
| 在给定小时内可导出的区段的最大数量 | 100 | 柔和 | 建议向批处理目标数据流中添加最多100个区段。 |
| 每个文件要激活的最大行数（记录） | 500万 | 硬 | Adobe Experience Platform会自动将导出的文件拆分为每个文件500万条记录（行）。 每行表示一个用户档案。 拆分文件名后附加一个数字，表示该文件是较大导出的一部分，如下所示： `filename.csv`, `filename_2.csv`, `filename_3.csv`. 有关更多信息，请阅读 [调度节](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 的“激活批处理目标”教程的“受众”部分。 |

{style=&quot;table-layout:auto&quot;}

### 临时激活 {#ad-hoc-activation}

下面的护栏适用于 [临时激活](/help/destinations/api/ad-hoc-activation-api.md) 方法。

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 每个临时激活作业激活的区段 | 80 | 硬 | 目前，每个临时激活作业最多可激活80个区段。 尝试激活每个作业80个以上的区段将导致作业失败。 此行为可能会在未来版本中发生更改。 |
| 每个区段的并发临时激活作业 | 1 | 硬 | 每个区段不要运行多个并发的临时激活作业。 |

{style=&quot;table-layout:auto&quot;}

### 边缘个性化目标激活 {#edge-destinations-activation}

以下护栏适用于通过 [边缘个性化目标](/help/destinations/destination-types.md#streaming-profile-export).

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 最大数 [自定义个性化](/help/destinations/catalog/personalization/custom-personalization.md) 目标 | 10 | 柔和 | 您可以为每个沙盒将数据流设置为10个自定义个性化目标。 |
| 每个沙盒映射到个性化目标的最大属性数 | 20 | 硬 | 每个沙盒在数据流中最多可以将20个属性映射到个性化目标。 |
| 映射到单个区段的最大区段数 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 目标 | 50 | 柔和 | 在激活流程中，您最多可以激活50个区段，以到达一个Adobe Target目标。 |

{style=&quot;table-layout:auto&quot;}

### Destination SDK护栏 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) 是一套配置API，允许您配置目标集成模式，以便Experience Platform根据所选的数据和身份验证格式将受众和配置文件数据交付到端点。 以下护栏适用于您使用Destination SDK配置的目标。

| 瓜德拉伊 | 限制 | 限制类型 | 描述 |
| --- | --- | --- | --- |
| 最大数 [私有自定义目标](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 柔和 | 使用Destination SDK，您最多可以创建5个专用自定义流或批量目标。 如果您需要创建5个以上的此类目标，请联系自定义关怀代表。 |
| 用于Destination SDK的配置文件导出策略 | <ul><li>`maxBatchAgeInSecs` （最低1.800和最高3.600）</li><li>`maxNumEventsInBatch` （最小1.000，最大10.000）</li></ul> | 硬 | 使用 [可配置聚合](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation) 选项时，需要注意用于确定将HTTP消息发送到基于API的目标的频率以及消息应包含的用户档案数的最小值和最大值。 |

{style=&quot;table-layout:auto&quot;}

### 目标限制和重试策略 {#destination-throttling-and-retry-policy}

有关给定目标的限制阈值或限制的详细信息。 本节还提供有关目标的重试策略的信息。

| 目标类型 | 描述 |
| --- | --- |
| 企业目标(HTTP API、Amazon Kinesis、Azure EventHubs) | 在95%的时间内，Experience Platform尝试为成功发送的消息提供少于10分钟的吞吐量延迟，每个数据流的请求速率低于每秒10,000次，以此速率发送到企业目标。 <br> 如果向企业目标发出的请求失败，Experience Platform会存储失败的请求并重试两次，以将请求发送到您的端点。 |

{style=&quot;table-layout:auto&quot;}

## 其他Experience Platform服务的防护 {#guardrails-other-services}

查看其他Experience Platform服务的护栏信息：

* 的护栏 [数据摄取](/help/ingestion/guardrails.md)
* 的护栏 [[!DNL Identity Service] 数据](/help/identity-service/guardrails.md)
* 的护栏 [[!DNL Real-time Customer Profile] 数据](/help/profile/guardrails.md)
* 的护栏 [[!DNL Query Service] 数据](/help/query-service/guardrails.md)