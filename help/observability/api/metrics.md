---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 量度API端点
description: 了解如何使用可观测性分析API在Experience Platform中检索可观测性量度。
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 3%

---

# 量度端点

可观察性量度提供对Adobe Experience Platform中各项功能的使用情况统计信息、历史趋势和性能指标的洞察。 的 `/metrics` 的端点 [!DNL Observability Insights API] 允许您以编程方式在 [!DNL Platform].

>[!NOTE]
>
>已弃用量度端点的先前版本(V1)。 本文档专门介绍当前版本(V2)。 有关旧版实施的V1端点的详细信息，请参阅 [API参考](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## 快速入门

本指南中使用的API端点是 [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接、本文档中的API调用示例指南，以及有关成功调用任何代码所需标头的重要信息 [!DNL Experience Platform] API。

## 检索可观测性量度

您可以通过向 `/metrics` 端点，指定要在有效负载中检索的量度。

**API格式**

```http
POST /metrics
```

**请求**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `start` | 从中检索量度数据的最早日期/时间。 |
| `end` | 从中检索量度数据的最新日期/时间。 |
| `granularity` | 一个可选字段，指示用量度数据除以的时间间隔。 例如，值为 `DAY` 返回之间每天的量度 `start` 和 `end` 日期，而值为 `MONTH` 会按月对量度结果进行分组。 使用此字段时， `downsample` 还必须提供属性以指示数据分组所依据的聚合函数。 |
| `metrics` | 对象数组，每个要检索的量度对应一个对象。 |
| `name` | 可观测性分析所识别的量度的名称。 请参阅 [附录](#available-metrics) ，以获取已接受量度名称的完整列表。 |
| `filters` | 允许您按特定数据集过滤量度的可选字段。 该字段是一个对象数组（每个过滤器对应一个对象），每个对象都包含以下属性： <ul><li>`name`:要过滤量度的实体类型。 目前，仅 `dataSets` 支持。</li><li>`value`:一个或多个数据集的ID。 多个数据集ID可以作为单个字符串提供，每个ID由垂直条字符(`\|`)。</li><li>`groupBy`:当设置为true时，表示对应的 `value` 表示应单独返回其量度结果的多个数据集。 如果设置为false，则这些数据集的量度结果会分组在一起。</li></ul> |
| `aggregator` | 指定聚合函数，该函数应用于将多次序列记录分组为单个结果。 有关可用聚合器的详细信息，请参阅 [OpenTSDB文档](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |
| `downsample` | 可选字段，用于指定聚合函数，以通过将字段分类为间隔（或“分段”）来降低量度数据的采样率。 缩减采样的间隔由 `granularity` 属性。 有关缩减采样的详细信息，请参阅 [OpenTSDB文档](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |

{style="table-layout:auto"}

**响应**

成功的响应会返回在请求中指定的量度和过滤器的生成数据点。

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `metricResponses` | 一个数组，其对象表示请求中指定的每个量度。 每个对象都包含有关过滤器配置和返回的量度数据的信息。 |
| `metric` | 请求中提供的其中一个量度的名称。 |
| `filters` | 指定量度的过滤器配置。 |
| `datapoints` | 一个数组，其对象表示指定量度和过滤器的结果。 数组中的对象数取决于请求中提供的筛选器选项。 如果未提供过滤器，则数组将只包含表示所有数据集的单个对象。 |
| `groupBy` | 如果在 `filter` 属性， `groupBy` 选项在请求中设置为true，则此对象将包含对应 `dps` 属性。<br><br>如果此对象在响应中显示为空，则对应 `dps` 属性适用于中提供的所有数据集 `filters` 数组(或 [!DNL Platform] 如果未提供过滤器)。 |
| `dps` | 给定量度、过滤器和时间范围的返回数据。 此对象中的每个键都表示一个时间戳，其中包含指定量度的相应值。 每个数据点之间的时间段取决于 `granularity` 值。 |

{style="table-layout:auto"}

## 附录

以下部分包含有关使用的其他信息 `/metrics` 端点。

### 可用量度 {#available-metrics}

下表列出了所有公开的量度 [!DNL Observability Insights]，划分为 [!DNL Platform] 服务。 每个量度都包含一个描述和接受的ID查询参数。

>[!NOTE]
>
>除非另有说明，否则所有列出的ID查询参数都是可选的。

#### [!DNL Data Ingestion] {#ingestion}

下表概述了Adobe Experience Platform的量度 [!DNL Data Ingestion]. 中的量度 **粗体** 正在流式引入量度。

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | 为一个或多个数据集的一个数据集摄取的所有数据的累计大小。 | 数据集 ID |
| timeseries.ingestion.dataset.dailysize | 根据每日使用情况为一个数据集或所有数据集摄取的数据大小。 | 数据集 ID |
| timeseries.ingestion.dataset.batchfailed.count | 一个数据集或所有数据集的批次数失败。 | 数据集 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 为一个数据集或所有数据集批量摄取的次数。 | 数据集 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 为一个数据集或所有数据集摄取的记录数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.presence.count** | 一个数据集或所有数据集的无效“存在”消息总数。 | 数据集 ID |
| **timeseries.data.collection.inlet.total.messages.received** | 为一个数据入口或所有数据入口接收的消息总数。 | 入口ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | 为一个数据入口或所有数据入口接收的数据的总大小。 | 入口ID |
| **timeseries.data.collection.inlet.success** | 对一个数据入口或所有数据入口的成功HTTP调用总数。 | 入口ID |
| **timeseries.data.collection.inlet.failure** | 对一个数据入口或所有数据入口的失败HTTP调用总数。 | 入口ID |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

下表概述了Adobe Experience Platform的量度 [!DNL Identity Service].

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 写入其数据源的记录数，由 [!DNL Identity Service]，用于一个数据集或所有数据集。 | 数据集 ID |
| timeseries.identity.dataset.recordfailed.count | 失败的记录数 [!DNL Identity Service]，适用于一个数据集或所有数据集。 | 数据集 ID |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 命名空间失败的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 命名空间跳过的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 您组织的标识图中存储的唯一标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 命名空间的标识图中存储的唯一标识数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | 针对特定图表强度（“未知”、“弱”或“强”），存储在组织标识图中的唯一标识数。 | 图表强度(**必需**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

下表概述了 [!DNL Real-Time Customer Profile].

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 从 [!DNL Data Lake] by [!DNL Profile]，适用于一个数据集或所有数据集。 | 数据集 ID |
| timeseries.profiles.dataset.recordsuccess.count | 写入其数据源的记录数，由 [!DNL Profile]，适用于一个数据集或所有数据集。 | 数据集 ID |
| timeseries.profiles.dataset.batchsuccess.count | 数量 [!DNL Profile] 为数据集或所有数据集批量摄取。 | 数据集 ID |

{style="table-layout:auto"}

### 错误消息

来自 `/metrics` 端点在某些情况下可能会返回错误消息。 这些错误消息将以下格式返回：

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `title` | 包含错误消息的字符串以及可能发生该错误的原因。 |
| `report` | 包含有关错误的上下文信息，包括触发该错误的操作中使用的沙盒和组织。 |

{style="table-layout:auto"}

下表列出了API可返回的不同错误代码：

| 错误代码 | 标题 | 描述 |
| --- | --- | --- |
| `INSGHT-1000-400` | 请求负载错误 | 请求负载出现问题。 确保您完全按照所示的方式匹配有效负载格式 [以上](#v2). 任何可能的原因都可能触发此错误：<ul><li>缺少必填字段，例如 `aggregator`</li><li>无效的量度</li><li>请求包含无效的聚合器</li><li>开始日期在结束日期之后</li></ul> |
| `INSGHT-1001-400` | 量度查询失败 | 由于请求错误或查询本身不可解析，尝试查询量度数据库时出错。 在再次尝试之前，请确保请求的格式正确。 |
| `INSGHT-1001-500` | 量度查询失败 | 由于服务器错误，尝试查询量度数据库时出错。 请重试请求，如果问题仍然存在，请与Adobe支持联系。 |
| `INSGHT-1002-500` | 服务错误 | 由于内部错误，无法处理该请求。 请重试请求，如果问题仍然存在，请与Adobe支持联系。 |
| `INSGHT-1003-401` | 沙盒验证错误 | 由于沙盒验证错误，无法处理该请求。 确保您在 `x-sandbox-name` 标头表示贵组织在再次尝试请求之前已启用的有效沙盒。 |

{style="table-layout:auto"}
