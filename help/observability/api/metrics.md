---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 可用指标
topic: developer guide
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 2%

---


# 度量端点

可观察性指标可提供对Adobe Experience Platform各种功能的使用情况统计、历史趋势和绩效指标的洞察。 中 `/metrics` 的端点 [!DNL Observability Insights API] 允许您以编程方式检索组织活动的度量数据 [!DNL Platform]。

## 入门指南

本指南中使用的API端点是API的一 [[!DNL Observability Insights] 部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)。 在继续之前，请查 [看入门指南](./getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何API所需标头的重要信 [!DNL Experience Platform] 息。

## 检索可观性指标

您可以通过向API中的端点发出GET请求来检 `/metrics` 索可观测性 [!DNL Observability Insights] 指标。

**API格式**

使用端点 `/metrics` 时，必须至少提供一个度量请求参数。 其他查询参数是筛选结果的可选参数。

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| 参数 | 描述 |
| --- | --- |
| `{METRIC}` | 要公开的度量。 在一次调用中合并多个指标时，必须使用和号(`&`)来分隔单个指标。 例如：`metric={METRIC_1}&metric={METRIC_2}`。 |
| `{ID}` | 要公开其度 [!DNL Platform] 量的特定资源的标识符。 此ID可能是可选的、必需的或不适用的，具体取决于所使用的度量。 请参 [阅附录](#available-metrics) ，了解可用指标的列表以及每个指标支持的ID（必需和可选）。 |
| `{DATE_RANGE}` | 要公开的指标的日期范围，ISO 8601格式(例如 `2018-10-01T07:00:00.000Z/2018-10-09T07:00:00.000Z`)。 |

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

成功的响应返回对象列表，每个对象都包含提供的时间戳 `dateRange` 和请求路径中指定的度量的相应值。 如果 `id` 请求路 [!DNL Platform] 径中包含某个资源，则结果将仅应用于该特定资源。 如果忽 `id` 略，则结果将应用于IMS组织内的所有适用资源。

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

## 附录

以下部分包含有关使用端点的其他 `/metrics` 信息。

### 可用指标 {#available-metrics}

下表列表了由服务公开的所 [!DNL Observability Insights]有度量，按服务 [!DNL Platform] 划分。 每个度量都包括一个描述和一个接受的ID查询参数。

>[!NOTE]
>
>除非另有说明，否则所有列出的ID查询参数都是可选的。

#### [!DNL Data Ingestion] {#ingestion}

下表概述了Adobe Experience Platform的指标 [!DNL Data Ingestion]。 粗体的 **指标** 是流式摄取指标。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 创建的数据集总数。 | 不适用 |
| timeseries.ingestion.dataset.size | 为一个或多个数据集摄取的所有数据的累计大小。 | 数据集ID |
| timeseries.ingestion.dataset.dailysize | 根据每日使用情况摄取的数据大小，用于一个数据集或所有数据集。 | 数据集ID |
| timeseries.ingestion.dataset.batchfailed.count | 一个数据集或所有数据集失败的批次数。 | 数据集ID |
| timeseries.ingestion.dataset.batchsuccess.count | 为一个数据集或所有数据集摄取的批次数。 | 数据集ID |
| timeseries.ingestion.dataset.recordsuccess.count | 为一个数据集或所有数据集摄取的记录数。 | 数据集ID |
| **timeseries.data.collection.validation.total.messages.rate** | 一个数据集或所有数据集的消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.valid.messages.rate** | 一个数据集或所有数据集的有效消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.invalid.messages.rate** | 一个数据集或所有数据集的无效消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.类别.type.count** | 一个数据集或所有数据集的无效“类型”消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.类别.range.count** | 一个数据集或所有数据集的无效“范围”消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.类别.format.count** | 一个数据集或所有数据集的无效“格式”消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.类别.pattern.count** | 一个数据集或所有数据集的无效“模式”消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.类别.presence.count** | 一个数据集或所有数据集的无效“存在”消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.类别.enum.count** | 一个数据集或所有数据集的无效“枚举”消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.类别.unclassified.count** | 一个数据集或所有数据集的无效“未分类”消息总数。 | 数据集ID |
| **timeseries.data.collection.validation.类别.unknown.count** | 一个数据集或所有数据集的无效“未知”消息总数。 | 数据集ID |
| **timeseries.data.collection.inlet.total.messages.received** | 为一个数据入口或所有数据入口接收的消息总数。 | 入口ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | 为一个数据入口或所有数据入口接收的数据的总大小。 | 入口ID |
| **timeseries.data.collection.inlet.success** | 对一个数据入口或所有数据入口成功的HTTP调用总数。 | 入口ID |
| **timeseries.data.collection.inlet.failure** | 对一个数据入口或所有数据入口的失败HTTP调用总数。 | 入口ID |

#### [!DNL Identity Service] {#identity}

下表概述了Adobe Experience Platform的指标 [!DNL Identity Service]。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 为一个数据集或所有数据集写入 [!DNL Identity Service]其数据源的记录数。 | 数据集ID |
| timeseries.identity.dataset.recordfailed.count | 失败的记录数 [!DNL Identity Service]目依据、一个数据集或所有数据集。 | 数据集ID |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 为命名空间成功摄取的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 由命名空间失败的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 命名空间跳过的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | IMS组织的标识图中存储的唯一标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 存储在标识图中的命名空间的唯一标识数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | IMS组织的标识图中存储的唯一图形标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | IMS组织在标识图中存储的特定标识数，用于特定图形强度（“未知”、“弱”或“强”）。 | 图形强度(**必需**) |

#### [!DNL Privacy Service] {#privacy}

下表概述了Adobe Experience Platform的指标 [!DNL Privacy Service]。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | 从GDPR创建的作业总数。 | ENV(必&#x200B;**需**) |
| timeseries.gdpr.jobs.completedjobs.count | GDPR已完成的作业总数。 | ENV(必&#x200B;**需**) |
| timeseries.gdpr.jobs.errorjobs.count | GDPR中的错误作业总数。 | ENV(必&#x200B;**需**) |

#### [!DNL Query Service] {#query}

下表概述了Adobe Experience Platform的指标 [!DNL Query Service]。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 非重复计划查询的总数。 | 不适用 |
| timeseries.queryservice.query.scheduledrecurring.count | 定期计划查询总数。 | 不适用 |
| timeseries.queryservice.query.batchquery.count | 已执行的批查询总数。 | 不适用 |
| timeseries.queryservice.query.scheduledquery.count | 已执行的计划查询总数。 | 不适用 |
| timeseries.queryservice.query.interactivequery.count | 执行的交互式查询总数。 | 不适用 |
| timeseries.queryservice.query.batchfrompsqlquery.count | PSQL中执行的批查询总数。 | 不适用 |

#### [!DNL Real-time Customer Profile] {#profile}

下表概述了相关指标 [!DNL Real-time Customer Profile]。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 从中读取的记录数 [!DNL Data Lake] 量， [!DNL Profile]依据一个数据集或所有数据集。 | 数据集ID |
| timeseries.profiles.dataset.recordsuccess.count | 按、一个数据集或所有数据集 [!DNL Profile]写入其数据源的记录数。 | 数据集ID |
| timeseries.profiles.dataset.recordfailed.count | 失败的记录数 [!DNL Profile]目依据、一个数据集或所有数据集。 | 数据集ID |
| timeseries.profiles.dataset.batchsuccess.count | 为数据集 [!DNL Profile] 或所有数据集摄取的批次数。 | 数据集ID |
| timeseries.profiles.dataset.batchfailed.count | 一个数 [!DNL Profile] 据集或所有数据集失败的批次数。 | 数据集ID |
| platform.ups.ingest.streaming.request.m1_rate | 传入请求率。 | IMS组织(必&#x200B;**需**) |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 摄取成功率。 | IMS组织(必&#x200B;**需**) |
| platform.ups.ingest.streaming.records.created.m15_rate | 为数据集摄取的新记录的速率。 | 数据集ID(**必需**) |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 创建数据集请求的超时时间戳记录的速率。 | 数据集ID(**必需**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 数据集的上次创建记录请求的时间戳。 | 数据集ID(**必需**) |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 数据集更新请求的超时时间戳记录的速率。 | 数据集ID(**必需**) |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 数据集的上次更新记录请求的时间戳。 | 数据集ID(**必需**) |
| platform.ups.ingest.streaming.record.size.m1_rate | 平均记录大小。 | IMS组织(必&#x200B;**需**) |
| platform.ups.ingest.streaming.records.updated.m15_rate | 为数据集摄取的记录请求更新的速率。 | 数据集ID(**必需**) |