---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform可观性洞察
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 2%

---


# Adobe Experience Platform可观性洞察概述

可观性洞察是一个REST风格的API，它允许您在Adobe Experience Platform中显示关键可观性指标。 这些指标可提供对使 [!DNL Platform] 用统计数据的洞察、服务运行 [!DNL Platform] 状况检查、历史趋势和各种功能的性能 [!DNL Platform] 指标。

此文档演示了对Oncenbility Insights API的示例调用。 有关可观性端点的完整列表，请参阅可观 [性洞察API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)。

## 入门指南

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作所在沙箱的名称。 有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../sandboxes/home.md)。

* x-sandbox-name: `{SANDBOX_NAME}`

## 检索可观性指标

您可以通过在Opencibility Insights API中向端点发出GET请求， `/metrics` 来检索可观测性指标。

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
| `{ID}` | 要公开其度 [!DNL Platform] 量的特定资源的标识符。 此ID可能是可选的、必需的或不适用的，具体取决于所使用的度量。 有关可用度量的列表以及每个度量的受支持ID（必需和可选），请参阅可用度量的引用 [文档](metrics.md)。 |
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

## 后续步骤

本文档概述了Oncebirity Insights API。 查看可 [用量度文档](metrics.md) ，获得可在API中使用的完整列表。