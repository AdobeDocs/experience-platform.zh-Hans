---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 量度API端点
topic-legacy: developer guide
description: 了解如何使用可观测性分析API在Experience Platform中检索可观测性量度。
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 5%

---

# 量度端点

可观察性量度提供对Adobe Experience Platform中各项功能的使用情况统计信息、历史趋势和性能指标的洞察。 [!DNL Observability Insights API]中的`/metrics`端点允许您以编程方式检索[!DNL Platform]中组织活动的量度数据。

## 快速入门

本指南中使用的API端点是[[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/)的一部分。 在继续操作之前，请查阅[快速入门指南](./getting-started.md) ，以获取相关文档的链接、本文档中API调用示例的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需标头的重要信息。

## 检索可观测性量度

使用API检索量度数据时支持以下两种方法：

* [版本1](#v1):使用查询参数指定量度。
* [版本2](#v2):使用JSON有效负载指定过滤器并将其应用于量度。

### 版本 1 {#v1}

您可以通过向`/metrics`端点发出GET请求，并通过使用查询参数指定量度来检索量度数据。

**API格式**

`metric`参数中必须至少提供一个量度。 其他查询参数是筛选结果的可选参数。

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| 参数 | 描述 |
| --- | --- |
| `{METRIC}` | 要显示的量度。 在一次调用中组合多个量度时，必须使用与号(`&`)来分隔各个量度。 例如：`metric={METRIC_1}&metric={METRIC_2}`。 |
| `{ID}` | 要公开其量度的特定[!DNL Platform]资源的标识符。 此ID可能是可选的、必需的，也可能不适用，具体取决于所使用的量度。 有关可用量度的列表，请参阅[附录](#available-metrics)，包括每个量度支持的ID（必需ID和可选ID）。 |
| `{DATE_RANGE}` | 要显示的量度的日期范围，采用ISO 8601格式（例如`2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`）。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics?metric=timeseries.ingestion.dataset.size&metric=timeseries.ingestion.dataset.recordsuccess.count&id=5cf8ab4ec48aba145214abeb&dateRange=2018-10-01T07:00:00.000Z/2019-06-06T07:00:00.000Z \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回对象列表，每个对象都包含提供的`dateRange`内的时间戳和请求路径中指定的量度的相应值。 如果[!DNL Platform]资源的`id`包含在请求路径中，则结果将仅适用于该特定资源。 如果忽略`id`，则结果将应用于IMS组织内的所有适用资源。

```json
{
  "id": "5cf8ab4ec48aba145214abeb",
  "imsOrgId": "{IMS_ORG}",
  "timeseries": {
    "granularity": "MONTH",
    "items": [
      {
        "timestamp": "2019-06-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1125,
          "timeseries.ingestion.dataset.size": 32320
        }
      },
      {
        "timestamp": "2019-05-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 1003,
          "timeseries.ingestion.dataset.size": 31409
        }
      },
      {
        "timestamp": "2019-04-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-03-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 740,
          "timeseries.ingestion.dataset.size": 25809
        }
      },
      {
        "timestamp": "2019-02-01T00:00:00Z",
        "metrics": {
          "timeseries.ingestion.dataset.recordsuccess.count": 390,
          "timeseries.ingestion.dataset.size": 16801
        }
      }
    ],
    "_page": null,
    "_links": null
  },
  "stats": {}
}
```

### 版本 2 {#v2}

您可以通过向`/metrics`端点发出POST请求，并指定要在有效负载中检索的量度来检索量度数据。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `granularity` | 一个可选字段，用于指示用量度数据除以的时间间隔。 例如，值`DAY`返回`start`和`end`日期之间每天的量度，而值`MONTH`将按月对量度结果进行分组。 使用此字段时，还必须提供相应的`downsample`属性，以指示数据分组所依据的聚合函数。 |
| `metrics` | 对象数组，每个要检索的量度对应一个对象。 |
| `name` | 可观测性分析所识别的量度的名称。 有关已接受的量度名称的完整列表，请参阅[附录](#available-metrics)。 |
| `filters` | 允许您按特定数据集过滤量度的可选字段。 该字段是一个对象数组（每个过滤器对应一个对象），每个对象都包含以下属性： <ul><li>`name`:要过滤量度的实体类型。目前仅支持`dataSets`。</li><li>`value`:一个或多个数据集的ID。多个数据集ID可以作为单个字符串提供，每个ID由垂直条字符(`|`)分隔。</li><li>`groupBy`:当设置为true时，表示对应的表示 `value` 应单独返回其量度结果的多个数据集。如果设置为false，则这些数据集的量度结果会分组在一起。</li></ul> |
| `aggregator` | 指定聚合函数，该函数应用于将多次序列记录分组为单个结果。 有关可用聚合器的详细信息，请参阅[OpenTSDB文档](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html)。 |
| `downsample` | 可选字段，用于指定聚合函数，以通过将字段分类为间隔（或“分段”）来降低量度数据的采样率。 缩减采样的间隔由`granularity`属性决定。 有关缩减采样的详细信息，请参阅[OpenTSDB文档](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html)。 |

{style=&quot;table-layout:auto&quot;}

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
| `groupBy` | 如果在某个量度的`filter`属性中指定了多个数据集，并且在请求中将`groupBy`选项设置为true，则此对象将包含相应`dps`属性所应用的数据集的ID。<br><br>如果此对象在响应中显示为空，则相应的属 `dps` 性将应用于数组中提供的所有数据集( `filters` 如果未提供过滤器，则 [!DNL Platform] 也会应用中的所有数据集)。 |
| `dps` | 给定量度、过滤器和时间范围的返回数据。 此对象中的每个键都表示一个时间戳，其中包含指定量度的相应值。 每个数据点之间的时间段取决于请求中指定的`granularity`值。 |

{style=&quot;table-layout:auto&quot;}

## 附录

以下部分包含有关使用`/metrics`端点的其他信息。

### 可用量度 {#available-metrics}

下表列出了[!DNL Observability Insights]公开的所有量度，按[!DNL Platform]服务划分。 每个量度都包含一个描述和接受的ID查询参数。

>[!NOTE]
>
>除非另有说明，否则所有列出的ID查询参数都是可选的。

#### [!DNL Data Ingestion] {#ingestion}

下表概述了Adobe Experience Platform [!DNL Data Ingestion]的量度。 **粗体**&#x200B;中的量度是流式摄取量度。

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 创建的数据集总数。 | 不适用 |
| timeseries.ingestion.dataset.size | 为一个或多个数据集的一个数据集摄取的所有数据的累计大小。 | 数据集 ID |
| timeseries.ingestion.dataset.dailysize | 根据每日使用情况为一个数据集或所有数据集摄取的数据大小。 | 数据集 ID |
| timeseries.ingestion.dataset.batchfailed.count | 一个数据集或所有数据集的批次数失败。 | 数据集 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 为一个数据集或所有数据集批量摄取的次数。 | 数据集 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 为一个数据集或所有数据集摄取的记录数。 | 数据集 ID |
| **timeseries.data.collection.validation.total.messages.rate** | 一个数据集或所有数据集的消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.valid.messages.rate** | 一个数据集或所有数据集的有效消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.invalid.messages.rate** | 一个数据集或所有数据集的无效消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.type.count** | 一个数据集或所有数据集的无效“type”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.range.count** | 一个数据集或所有数据集的无效“范围”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.format.count** | 一个数据集或所有数据集的无效“format”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.pattern.count** | 一个数据集或所有数据集的无效“模式”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.presence.count** | 一个数据集或所有数据集的无效“存在”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.enum.count** | 一个数据集或所有数据集的无效“枚举”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.unclassified.count** | 一个数据集或所有数据集的无效“未分类”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.unknown.count** | 一个数据集或所有数据集的无效“未知”消息总数。 | 数据集 ID |
| **timeseries.data.collection.inlet.total.messages.received** | 为一个数据入口或所有数据入口接收的消息总数。 | 入口ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | 为一个数据入口或所有数据入口接收的数据的总大小。 | 入口ID |
| **timeseries.data.collection.inlet.success** | 对一个数据入口或所有数据入口的成功HTTP调用总数。 | 入口ID |
| **timeseries.data.collection.inlet.failure** | 对一个数据入口或所有数据入口的失败HTTP调用总数。 | 入口ID |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Identity Service] {#identity}

下表概述了Adobe Experience Platform [!DNL Identity Service]的量度。

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | [!DNL Identity Service]针对一个数据集或所有数据集写入其数据源的记录数。 | 数据集 ID |
| timeseries.identity.dataset.recordfailed.count | 对于一个数据集或所有数据集，记录数按[!DNL Identity Service]失败。 | 数据集 ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 为命名空间成功摄取的身份记录数。 | 命名空间ID（**必需**） |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 命名空间失败的身份记录数。 | 命名空间ID（**必需**） |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 命名空间跳过的身份记录数。 | 命名空间ID（**必需**） |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 存储在IMS组织的标识图中的唯一标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 命名空间的标识图中存储的唯一标识数。 | 命名空间ID（**必需**） |
| timeseries.identity.graph.imsorg.numidgraphs.count | 存储在IMS组织的标识图中的唯一图标标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | IMS组织的标识图中存储的特定图强度（“未知”、“弱”或“强”）的唯一标识数。 | 图表强度（**必需**） |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Privacy Service] {#privacy}

下表概述了Adobe Experience Platform [!DNL Privacy Service]的量度。

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | 根据GDPR创建的作业总数。 | ENV（**必需**） |
| timeseries.gdpr.jobs.completedjobs.count | 来自GDPR的已完成作业总数。 | ENV（**必需**） |
| timeseries.gdpr.jobs.errorjobs.count | 来自GDPR的错误作业总数。 | ENV（**必需**） |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Query Service] {#query}

下表概述了Adobe Experience Platform [!DNL Query Service]的量度。

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 非定期计划查询的总数。 | 不适用 |
| timeseries.queryservice.query.scheduledrecurring.count | 定期计划查询的总数。 | 不适用 |
| timeseries.queryservice.query.batchquery.count | 已执行的批处理查询总数。 | 不适用 |
| timeseries.queryservice.query.scheduledquery.count | 已执行的计划查询总数。 | 不适用 |
| timeseries.queryservice.query.interactivequery.count | 执行的交互式查询总数。 | 不适用 |
| timeseries.queryservice.query.batchfrompsqlquery.count | 从PSQL执行的批处理查询的总数。 | 不适用 |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Real-time Customer Profile] {#profile}

下表概述了[!DNL Real-time Customer Profile]的量度。

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 从[!DNL Data Lake]中读取的[!DNL Profile]、一个数据集或所有数据集的记录数。 | 数据集 ID |
| timeseries.profiles.dataset.recordsuccess.count | 由[!DNL Profile]、一个数据集或所有数据集写入其数据源的记录数。 | 数据集 ID |
| timeseries.profiles.dataset.recordfailed.count | 对于一个数据集或所有数据集，记录数按[!DNL Profile]失败。 | 数据集 ID |
| timeseries.profiles.dataset.batchsuccess.count | 为数据集或所有数据集批量摄取的[!DNL Profile]次数。 | 数据集 ID |
| timeseries.profiles.dataset.batchfailed.count | 一个数据集或所有数据集的[!DNL Profile]批次数失败。 | 数据集 ID |
| platform.ups.ingest.streaming.request.m1_rate | 传入请求速率。 | IMS组织（**必需**） |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 摄取成功率。 | IMS组织（**必需**） |
| platform.ups.ingest.streaming.records.created.m15_rate | 为数据集摄取的新记录的速率。 | 数据集ID（**必需**） |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 为数据集创建请求而加盖超时时间戳的记录的速率。 | 数据集ID（**必需**） |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 数据集的上次创建记录请求的时间戳。 | 数据集ID（**必需**） |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 数据集更新请求的带有超时时间戳的记录的速率。 | 数据集ID（**必需**） |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 数据集的上次更新记录请求的时间戳。 | 数据集ID（**必需**） |
| platform.ups.ingest.streaming.record.size.m1_rate | 平均记录大小。 | IMS组织（**必需**） |
| platform.ups.ingest.streaming.records.updated.m15_rate | 为数据集摄取的记录的更新请求的速率。 | 数据集ID（**必需**） |

{style=&quot;table-layout:auto&quot;}

### 错误消息

来自`/metrics`端点的响应在某些情况下可能会返回错误消息。 这些错误消息将以下格式返回：

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{IMS_ORG}"
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
| `report` | 包含有关错误的上下文信息，包括在触发该错误的操作中使用的沙盒和IMS组织。 |

{style=&quot;table-layout:auto&quot;}

下表列出了API可返回的不同错误代码：

| 错误代码 | 标题 | 描述 |
| --- | --- | --- |
| `INSGHT-1000-400` | 请求负载错误 | 请求负载出现问题。 确保有效负载格式与上面[所示的](#v2)完全匹配。 任何可能的原因都可能触发此错误：<ul><li>缺少必填字段，如`aggregator`</li><li>无效的量度</li><li>请求包含无效的聚合器</li><li>开始日期在结束日期之后</li></ul> |
| `INSGHT-1001-400` | 量度查询失败 | 由于请求错误或查询本身不可解析，尝试查询量度数据库时出错。 在再次尝试之前，请确保请求的格式正确。 |
| `INSGHT-1001-500` | 量度查询失败 | 由于服务器错误，尝试查询量度数据库时出错。 请重试请求，如果问题仍然存在，请与Adobe支持联系。 |
| `INSGHT-1002-500` | 服务错误 | 由于内部错误，无法处理该请求。 请重试请求，如果问题仍然存在，请与Adobe支持联系。 |
| `INSGHT-1003-401` | 沙盒验证错误 | 由于沙盒验证错误，无法处理该请求。 在再次尝试请求之前，请确保您在`x-sandbox-name`标头中提供的沙盒名称是IMS组织的有效已启用沙盒。 |

{style=&quot;table-layout:auto&quot;}
