---
keywords: Experience Platform；首页；热门话题
solution: Experience Platform
title: 量度API端点
description: 了解如何使用可观察性分析API在Experience Platform中检索可观察性指标。
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 3%

---

# 量度端点

可观察性量度可为Adobe Experience Platform中的各种功能提供使用统计信息、历史趋势和绩效指标见解。 [!DNL Observability Insights API]中的`/metrics`端点允许您以编程方式检索[!DNL Experience Platform]中组织活动的量度数据。

>[!NOTE]
>
>已弃用量度端点(V1)的先前版本。 本文档仅侧重于当前版本(V2)。 有关旧版实施的V1端点的详细信息，请参阅[API引用](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1)。

## 快速入门

本指南中使用的API端点是[[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、此文档中示例API调用的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需的所需标头的重要信息。

## 检索可观察性指标

您可以通过向`/metrics`端点发出POST请求，指定要在有效负载中检索的量度来检索量度数据。

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
  -H 'x-sandbox-id: {SANDBOX_ID}'
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
            "aggregator": "sum"
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
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `start` | 检索量度数据的最早日期/时间。 |
| `end` | 从中检索量度数据的最新日期/时间。 |
| `granularity` | 一个可选字段，它指明将度量数据除以的时间间隔。 例如，值`DAY`返回`start`到`end`日期之间每天的量度，而值`MONTH`将改为按月分组量度结果。 |
| `metrics` | 一个对象数组，您要检索的每个量度对应一个对象。 |
| `name` | 可观察性分析识别的指标的名称。 有关接受的量度名称的完整列表，请参阅[附录](#available-metrics)。 |
| `filters` | 一个可选字段，允许您按特定数据集筛选量度。 字段是一个对象数组（每个过滤器对应一个对象），每个对象包含以下属性： <ul><li>`name`：要筛选量度的实体类型。 当前仅支持`dataSets`。</li><li>`value`：一个或多个数据集的标识。 可以将多个数据集ID作为单个字符串提供，每个ID都用竖条字符(`\|`)分隔。</li><li>`groupBy`：当设置为true时，指示相应的`value`表示多个数据集，这些数据集的度量结果应单独返回。 如果设置为false，则将这些数据集的度量结果分组在一起。</li></ul> |
| `aggregator` | 指定应将多个时间序列记录分组为单个结果的聚合函数。 当前支持的聚合器包括最小值、最大值、总和以及平均值，具体取决于量度的定义。 |

{style="table-layout:auto"}

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
| `metricResponses` | 一个数组，其对象表示请求中指定的每个度量。 每个对象都包含有关过滤器配置和返回的量度数据的信息。 |
| `metric` | 请求中提供的某个指标的名称。 |
| `filters` | 指定度量的过滤器配置。 |
| `datapoints` | 一个数组，其对象表示指定量度和过滤器的结果。 数组中的对象数取决于请求中提供的过滤器选项。 如果未提供筛选器，则数组将仅包含表示所有数据集的单个对象。 |
| `groupBy` | 如果在一个量度的`filter`属性中指定了多个数据集，并且在请求中将`groupBy`选项设置为true，则此对象将包含对应`dps`属性应用于的数据集的ID。<br><br>如果此对象在响应中显示为空，则相应的`dps`属性适用于`filters`数组中提供的所有数据集（如果未提供筛选器，则适用于[!DNL Experience Platform]中的所有数据集）。 |
| `dps` | 为给定的量度、过滤器和时间范围返回的数据。 此对象中的每个键都表示一个时间戳，该时间戳具有指定度量的相应值。 每个数据点之间的时间段取决于请求中指定的`granularity`值。 |

{style="table-layout:auto"}

## 附录

以下部分包含有关使用`/metrics`终结点的其他信息。

### 可用量度 {#available-metrics}

下表列出了[!DNL Observability Insights]公开的所有指标，按[!DNL Experience Platform]服务进行划分。 每个量度都包括一个描述和接受的ID查询参数。

>[!NOTE]
>
>除非另有说明，否则列出的所有ID查询参数都是可选的。

#### [!DNL Data Ingestion] {#ingestion}

下表概述了Adobe Experience Platform [!DNL Data Ingestion]的指标。 **bold**&#x200B;中的量度是流式摄取量度。

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | 针对一个数据集或所有数据集摄取的所有数据的累积大小。 | 数据集 ID |
| timeseries.ingestion.dataset.dailysize | 针对一个数据集或所有数据集按每日使用情况摄取的数据大小。 | 数据集 ID |
| timeseries.ingestion.dataset.batchfailed.count | 一个数据集或所有数据集失败的批次数。 | 数据集 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 为一个数据集或所有数据集摄取的批次数。 | 数据集 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 为一个数据集或所有数据集摄取的记录数。 | 数据集 ID |
| **timeseries.data.collection.validation.category.presence.count** | 一个数据集或所有数据集的无效“存在”消息总数。 | 数据集 ID |
| **timeseries.data.collection.inlet.total.messages.received** | 为一个数据入口或所有数据入口接收的消息总数。 | 入口标识 |
| **timeseries.data.collection.inlet.total.messages.size.received** | 为一个数据入口或所有数据入口接收的数据总大小。 | 入口标识 |
| **timeseries.data.collection.inlet.success** | 成功调用一个数据入口或所有数据入口的HTTP总数。 | 入口标识 |
| **timeseries.data.collection.inlet.failure** | 对一个数据入口或所有数据入口失败的HTTP调用总数。 | 入口标识 |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

下表概述了Adobe Experience Platform [!DNL Identity Service]的指标。

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 一个数据集或所有数据集的[!DNL Identity Service]写入其数据源的记录数。 | 数据集 ID |
| timeseries.identity.dataset.recordfailed.count | [!DNL Identity Service]失败的记录数（针对一个数据集或所有数据集）。 | 数据集 ID |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 跳过的身份记录数。 | 组织 ID |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 存储在贵组织的身份图中的唯一身份数。 | 不适用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 存储在命名空间的身份图中的唯一身份数。 | 命名空间ID （**必需**） |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | 组织中针对特定图形强度（“未知”、“弱”或“强”）存储在身份图中的唯一身份数。 | 图形强度（**必需**） |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

下表概述了[!DNL Real-Time Customer Profile]的量度。

| 分析量度 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | [!DNL Profile]从[!DNL Data Lake]读取的记录数（针对一个数据集或所有数据集）。 | 数据集 ID |
| timeseries.profiles.dataset.recordsuccess.count | [!DNL Profile]写入其数据源的记录数（针对一个数据集或所有数据集）。 | 数据集 ID |
| timeseries.profiles.dataset.batchsuccess.count | 为数据集或所有数据集摄取的[!DNL Profile]批次数。 | 数据集 ID |

{style="table-layout:auto"}

### 错误消息

在某些条件下，来自`/metrics`终结点的响应可能会返回错误消息。 以下列格式返回这些错误消息：

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
| `title` | 一个字符串，其中包含错误消息及其可能发生的潜在原因。 |
| `report` | 包含有关错误的上下文信息，包括触发该错误的操作中使用的沙盒和组织。 |

{style="table-layout:auto"}

下表列出了API可返回的不同错误代码：

| 错误代码 | 标题 | 描述 |
| --- | --- | --- |
| `INSGHT-1000-400` | 请求有效负载无效 | 请求有效负载出错。 请确保与上面显示的[有效负载格式完全匹配](#v2)。 触发此错误的可能原因有：<ul><li>缺少必填字段，如`aggregator`</li><li>量度无效</li><li>请求包含无效汇总</li><li>开始日期发生在结束日期之后</li></ul> |
| `INSGHT-1001-400` | 量度查询失败 | 尝试查询量度数据库时出错，因为请求不正确或查询本身无法分析。 在重试之前，请确保您的请求格式正确。 |
| `INSGHT-1001-500` | 量度查询失败 | 由于服务器错误，尝试查询量度数据库时出错。 请重试该请求，如果问题依然存在，请联系Adobe支持部门。 |
| `INSGHT-1002-500` | 服务错误 | 由于内部错误，无法处理该请求。 请重试该请求，如果问题依然存在，请联系Adobe支持部门。 |
| `INSGHT-1003-401` | 沙盒验证错误 | 由于沙盒验证错误，无法处理请求。 在重试请求之前，请确保您在`x-sandbox-name`标头中提供的沙盒名称表示您的组织启用的有效沙盒。 |

{style="table-layout:auto"}
