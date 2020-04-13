---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform可观性洞察
topic: overview
translation-type: tm+mt
source-git-commit: d349ffab7c0de72d38b5195585c14a4a8f80e37c

---


# Adobe Experience Platform可观性洞察概述

可观性洞察是一个RESTful API，它允许您在Adobe Experience Platform中显示关键的可观性指标。 这些指标提供平台使用统计数据、平台服务运行状况检查、历史趋势以及各种平台功能的绩效指标的洞察。

此文档演示了对Opencibility Insights API的示例调用。 有关可观性端点的完整列表，请参阅可观 [性洞察API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/observability-insights.yaml)。

## 入门指南

要调用平台API，您必须首先完成身份验证 [教程](../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个头，它指定操作将在其中进行的沙箱的名称。 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../sandboxes/home.md)。

* x-sandbox-name: `{SANDBOX_NAME}`

## 检索可观测性指标

您可以通过在Opergibility Insights API中向端点发出GET请求来检 `/metrics` 索可观测性指标。

**API格式**

当使用端 `/metrics` 点时，必须提供至少一个度量请求参数。 其他查询参数对于筛选结果是可选的。

```http
GET /metrics?metric={METRIC}
GET /metrics?metric={METRIC}&metric={METRIC_2}
GET /metrics?metric={METRIC}&id={ID}
GET /metrics?metric={METRIC}&dateRange={DATE_RANGE}
GET /metrics?metric={METRIC}&metric={METRIC_2}&id={ID}&dateRange={DATE_RANGE}
```

| 参数 | 描述 |
| --- | --- |
| `{METRIC}` | 要公开的度量。 在单次调用中组合多个指标时，必须使用“和号”(`&`)分隔单个指标。 例如：`metric={METRIC_1}&metric={METRIC_2}`。 |
| `{ID}` | 要公开其度量的特定平台资源的标识符。 此ID可能是可选的、必需的或不适用的，具体取决于所使用的度量。 有关可用度量的列表以及每个度量的受支持ID（必需和可选），请参阅可用度量的参考 [文档](metrics.md)。 |
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

成功的响应返回对象列表，每个对象都包含提供的时间戳内的时间戳以及请求路径中指定 `dateRange` 的度量的相应值。 如果 `id` 请求路径中包含平台资源，则结果将仅应用于该特定资源。 如果忽略 `id` 了该选项，则结果将应用于IMS组织内的所有适用资源。

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

本文档概述了可观性洞察API。 有关可在 [API中使用的](metrics.md) 、完整列表的度量，请参阅可用度量的文档。