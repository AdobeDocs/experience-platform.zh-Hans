---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: 量度API端点
topic-legacy: developer guide
description: 了解如何使用Oncentibry Insights API在Experience Platform中检索可观测性指标。
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2054'
ht-degree: 4%

---

# 量度端点

可观察性指标可洞察Adobe Experience Platform中各种功能的使用情况统计、历史趋势和绩效指标。 [!DNL Observability Insights API]中的`/metrics`端点允许您以编程方式检索[!DNL Platform]中组织活动的量度数据。

## 入门指南

本指南中使用的API端点是[[!DNL Observability Insights] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)的一部分。 在继续之前，请查阅[快速入门指南](./getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南以及成功调用任何[!DNL Experience Platform] API所需标头的重要信息。

## 检索可观察性指标

有两种支持的方法可使用API检索量度数据：

* [版本1](#v1):使用查询参数指定量度。
* [版本2](#v2):使用JSON有效负荷指定过滤器并将其应用到量度。

### 版本1 {#v1}

您可以通过向`/metrics`端点发出GET请求，通过使用查询参数指定量度来检索量度数据。

**API格式**

`metric`参数中必须至少提供一个度量。 其他查询参数对于筛选结果是可选的。

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| 参数 | 描述 |
| --- | --- |
| `{METRIC}` | 要公开的量度。 在单次调用中组合多个量度时，必须使用和号(`&`)来分隔单个量度。 例如：`metric={METRIC_1}&metric={METRIC_2}`。 |
| `{ID}` | 要公开其量度的特定[!DNL Platform]资源的标识符。 此ID可能是可选的、必需的或不适用的，具体取决于所使用的量度。 有关可用量度的列表，包括每个量度支持的ID（必需和可选），请参阅[附录](#available-metrics)。 |
| `{DATE_RANGE}` | 要公开的量度的日期范围，ISO 8601格式（例如`2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`）。 |

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

成功的响应返回对象列表，每个对象都包含提供的`dateRange`中的时间戳和请求路径中指定的度量的相应值。 如果请求路径中包含[!DNL Platform]资源的`id`，则结果将仅应用于该特定资源。 如果省略`id`，则结果将应用于您IMS组织内的所有适用资源。

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

### 版本2 {#v2}

您可以通过向`/metrics`端点发出POST请求，指定要在有效负荷中检索的量度，来检索量度数据。

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
| `start` | 要检索量度数据的最早日期/时间。 |
| `end` | 要从中检索量度数据的最新日期/时间。 |
| `granularity` | 一个可选字段，指示要按量度数据除以的时间间隔。 例如，值`DAY`返回`start`和`end`日期之间每天的量度，而值`MONTH`将按月对量度结果进行分组。 使用此字段时，还必须提供相应的`downsample`属性以指示将数据分组时所使用的聚合函数。 |
| `metrics` | 对象数组，每个对象对应一个要检索的量度。 |
| `name` | 可观察性洞察所识别的量度名称。 有关已接受的量度名称的完整列表，请参见[附录](#available-metrics)。 |
| `filters` | 允许您按特定数据集筛选量度的可选字段。 该字段是对象的数组（每个滤镜各一个），每个对象包含以下属性： <ul><li>`name`:要筛选量度的实体类型。当前仅支持`dataSets`。</li><li>`value`:一个或多个数据集的ID。可以将多个数据集ID作为单个字符串提供，每个ID由垂直条字符(`|`)分隔。</li><li>`groupBy`:设置为true时，指示相应的表示 `value` 应单独返回其量度结果的多个数据集。如果设置为false，则这些数据集的量度结果将分组在一起。</li></ul> |
| `aggregator` | 指定应用于将多个时间序列记录分组为单个结果的聚合函数。 有关可用聚合器的详细信息，请参阅[OpenTSDB文档](http://opentsdb.net/docs/build/html/user_guide/query/aggregators.html)。 |
| `downsample` | 可选字段，允许您指定聚合函数，通过将字段按时间间隔（或“时段”）排序来降低量度数据的采样率。 缩减采样的间隔由`granularity`属性决定。 有关缩减采样的详细信息，请参阅[OpenTSDB文档](http://opentsdb.net/docs/build/html/user_guide/query/downsampling.html)。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回请求中指定的量度和过滤器的结果数据点。

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
| `metricResponses` | 一个数组，其对象表示请求中指定的每个量度。 每个对象都包含有关筛选器配置和返回量度数据的信息。 |
| `metric` | 请求中提供的量度之一的名称。 |
| `filters` | 指定量度的筛选器配置。 |
| `datapoints` | 一个数组，其对象表示指定量度和过滤器的结果。 数组中的对象数取决于请求中提供的筛选器选项。 如果未提供任何过滤器，则数组将仅包含一个表示所有数据集的对象。 |
| `groupBy` | 如果在某个量度的`filter`属性中指定了多个数据集，并且在请求中将`groupBy`选项设置为true，则此对象将包含相应`dps`属性所应用的数据集ID。<br><br>如果此对象在响应中显示为空，则相应的 `dps` 属性将应用于数组中提供的所 `filters` 有数据集(如果未提 [!DNL Platform] 供任何过滤器，则应用于中的所有数据集)。 |
| `dps` | 给定量度、过滤器和时间范围的返回数据。 此对象中的每个键都表示具有指定量度的相应值的时间戳。 每个数据点之间的时间段取决于请求中指定的`granularity`值。 |

{style=&quot;table-layout:auto&quot;}

## 附录

以下部分包含有关使用`/metrics`端点的其他信息。

### 可用量度{#available-metrics}

下表列表了由[!DNL Observability Insights]公开的所有量度，由[!DNL Platform]服务划分。 每个量度都包含一个描述和可接受的ID查询参数。

>[!NOTE]
>
>除非另有说明，否则所有列出的ID查询参数都是可选的。

#### [!DNL Data Ingestion] {#ingestion}

下表概述了Adobe Experience Platform [!DNL Data Ingestion]的量度。 **bold**&#x200B;中的量度是流式摄取量度。

| 洞察量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 创建的数据集总数。 | 不适用 |
| timeseries.ingestion.dataset.size | 为一个或多个数据集摄取的所有数据的累积大小。 | 数据集 ID |
| timeseries.ingestion.dataset.dailysize | 每日为一个数据集或所有数据集摄取的数据大小。 | 数据集 ID |
| timeseries.ingestion.dataset.batchfailed.count | 一个数据集或所有数据集失败的批次数。 | 数据集 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 为一个数据集或所有数据集摄取的批次数。 | 数据集 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 为一个数据集或所有数据集摄取的记录数。 | 数据集 ID |
| **timeseries.data.collection.validation.total.messages.rate** | 一个数据集或所有数据集的消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.messages.rate** | 一个数据集或所有数据集的有效消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.invalid.messages.rate** | 一个数据集或所有数据集的无效消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.类别.type.count** | 一个数据集或所有数据集的无效“类型”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.类别.range.count** | 一个数据集或所有数据集的无效“范围”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.类别.format.count** | 一个数据集或所有数据集的无效“格式”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.类别.pattern.count** | 一个数据集或所有数据集的无效“模式”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.类别.presence.count** | 一个数据集或所有数据集的无效“存在”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.类别.enum.count** | 一个数据集或所有数据集的无效“枚举”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.类别.unclassified.count** | 一个数据集或所有数据集的无效“未分类”消息总数。 | 数据集 ID |
| **timeseries.data.collection.validation.类别.unknown.count** | 一个数据集或所有数据集的无效“未知”消息总数。 | 数据集 ID |
| **timeseries.data.collection.inlet.total.messages.received** | 为一个数据入口或所有数据入口接收的消息总数。 | 入口ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | 为一个数据入口或所有数据入口接收的数据的总大小。 | 入口ID |
| **timeseries.data.collection.inlet.success** | 对一个数据入口或所有数据入口成功的HTTP调用总数。 | 入口ID |
| **timeseries.data.collection.inlet.failure** | 对一个数据入口或所有数据入口的失败HTTP调用总数。 | 入口ID |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Identity Service] {#identity}

下表概述了Adobe Experience Platform [!DNL Identity Service]的量度。

| 洞察量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 由[!DNL Identity Service]写入其数据源的记录数，用于一个数据集或所有数据集。 | 数据集 ID |
| timeseries.identity.dataset.recordfailed.count | [!DNL Identity Service]、一个数据集或所有数据集失败的记录数。 | 数据集 ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 为命名空间成功摄取的身份记录数。 | 命名空间ID（**必需**） |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 由命名空间失败的身份记录数。 | 命名空间ID（**必需**） |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 命名空间跳过的身份记录数。 | 命名空间ID（**必需**） |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 存储在IMS组织的标识图中的唯一标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 存储在命名空间标识图中的唯一标识数。 | 命名空间ID（**必需**） |
| timeseries.identity.graph.imsorg.numidgraphs.count | 存储在IMS组织的标识图中的唯一图标标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | IMS组织在标识图中存储的特定标识数，用于特定图强（“未知”、“弱”或“强”）。 | 图强度（**必需**） |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Privacy Service] {#privacy}

下表概述了Adobe Experience Platform [!DNL Privacy Service]的量度。

| 洞察量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | 从GDPR创建的作业总数。 | ENV（**必需**） |
| timeseries.gdpr.jobs.completedjobs.count | GDPR已完成的作业总数。 | ENV（**必需**） |
| timeseries.gdpr.jobs.errorjobs.count | GDPR中的错误作业总数。 | ENV（**必需**） |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Query Service] {#query}

下表概述了Adobe Experience Platform [!DNL Query Service]的量度。

| 洞察量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 非循环计划查询的总数。 | 不适用 |
| timeseries.queryservice.query.scheduledrecurring.count | 定期计划查询的总数。 | 不适用 |
| timeseries.queryservice.query.batchquery.count | 已执行的批查询总数。 | 不适用 |
| timeseries.queryservice.query.scheduledquery.count | 已执行的计划查询总数。 | 不适用 |
| timeseries.queryservice.query.interactivequery.count | 执行的交互式查询总数。 | 不适用 |
| timeseries.queryservice.query.batchfrompsqlquery.count | 来自PSQL的已执行批查询的总数。 | 不适用 |

{style=&quot;table-layout:auto&quot;}

#### [!DNL Real-time Customer Profile] {#profile}

下表概述了[!DNL Real-time Customer Profile]的量度。

| 洞察量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 由[!DNL Profile]从[!DNL Data Lake]读取的记录数，用于一个数据集或所有数据集。 | 数据集 ID |
| timeseries.profiles.dataset.recordsuccess.count | 由[!DNL Profile]、一个数据集或所有数据集写入其数据源的记录数。 | 数据集 ID |
| timeseries.profiles.dataset.recordfailed.count | [!DNL Profile]、一个数据集或所有数据集失败的记录数。 | 数据集 ID |
| timeseries.profiles.dataset.batchsuccess.count | 为数据集或所有数据集摄取的[!DNL Profile]批次数。 | 数据集 ID |
| timeseries.profiles.dataset.batchfailed.count | [!DNL Profile]批次数失败（对于一个数据集或所有数据集）。 | 数据集 ID |
| platform.ups.ingest.streaming.request.m1_rate | 传入请求率。 | IMS组织（**必需**） |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 摄取成功率。 | IMS组织（**必需**） |
| platform.ups.ingest.streaming.records.created.m15_rate | 为数据集摄取的新记录的速率。 | 数据集ID（**必需**） |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 为数据集创建请求的超时时间戳记录的速率。 | 数据集ID（**必需**） |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 数据集的上次创建记录请求的时间戳。 | 数据集ID（**必需**） |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 数据集的更新请求的超时时间戳记录的速率。 | 数据集ID（**必需**） |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 数据集的上次更新记录请求的时间戳。 | 数据集ID（**必需**） |
| platform.ups.ingest.streaming.record.size.m1_rate | 平均记录大小。 | IMS组织（**必需**） |
| platform.ups.ingest.streaming.records.updated.m15_rate | 为数据集摄取的记录的更新请求的速率。 | 数据集ID（**必需**） |

{style=&quot;table-layout:auto&quot;}

### 错误消息

在某些条件下，来自`/metrics`端点的响应可能会返回错误消息。 这些错误消息以以下格式返回：

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
| `title` | 一个字符串，其中包含错误消息以及可能发生错误消息的原因。 |
| `report` | 包含有关错误的上下文信息，包括触发该错误的操作中使用的沙箱和IMS组织。 |

{style=&quot;table-layout:auto&quot;}

下表列表了API可返回的不同错误代码：

| 错误代码 | 标题 | 描述 |
| --- | --- | --- |
| `INSGHT-1000-400` | 错误的请求有效负荷 | 请求负载有问题。 确保与上面[所示的有效负荷格式完全匹配。 ](#v2)任何可能的原因都可能触发此错误：<ul><li>缺少必填字段，如`aggregator`</li><li>无效的量度</li><li>请求包含无效的聚合器</li><li>开始日期在结束日期之后发生</li></ul> |
| `INSGHT-1001-400` | 量度查询失败 | 尝试查询量度数据库时出错，原因是请求错误或查询本身不可参与。 在重试之前，请确保您的请求格式正确。 |
| `INSGHT-1001-500` | 量度查询失败 | 由于服务器错误，尝试查询量度数据库时出错。 请重试请求，如果问题仍然存在，请与Adobe支持联系。 |
| `INSGHT-1002-500` | 服务错误 | 由于内部错误，无法处理该请求。 请重试请求，如果问题仍然存在，请与Adobe支持联系。 |
| `INSGHT-1003-401` | 沙箱验证错误 | 由于沙箱验证错误，无法处理该请求。 在再次尝试请求之前，请确保您在`x-sandbox-name`标头中提供的沙箱名称代表IMS组织的一个有效的已启用沙箱。 |

{style=&quot;table-layout:auto&quot;}
