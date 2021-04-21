---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；预览；估计；预览和估计；估计和预览;api;API;
solution: Experience Platform
title: 预览和评估API端点
topic-legacy: developer guide
description: 在开发细分定义时，您可以使用Adobe Experience Platform中的估计和预览工具来视图摘要级信息，以帮助确保隔离预期受众。
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 2%

---

# 预览和估计端点

在开发区段定义时，您可以使用Adobe Experience Platform中的估计和预览工具来视图摘要级信息，以帮助确保隔离您期望的受众。

* **预** 览为区段定义提供符合条件的用户档案的分页列表，使您能够将结果与预期结果进行比较。

* **估** 计提供有关区段定义的统计信息，如预测受众大小、置信区间和误差标准偏差。

>[!NOTE]
>
>要访问与实时客户用户档案数据相关的类似指标，如特定命名空间或用户档案数据存储中的用户档案片段和合并用户档案的总数，请参阅用户档案API开发人员指南的[用户档案预览(预览示例状态)终结点指南](../../profile/api/preview-sample-status.md)。

## 入门指南

本指南中使用的端点是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需的重要信息，包括必需的标头以及如何读取示例API调用。

## 估计的生成方式

当将记录引入用户档案存储中时，将总用户档案计数增加或减少5%以上时，将触发采样作业以更新该计数。 数据采样的触发方式取决于摄取方法：

* **批摄取：** 对于批摄取，在成功将批摄入用户档案存储区的15分钟内，如果达到5%的增加或减少阈值，则运行一个作业以更新计数。
* **流摄取：** 对于流式数据工作流，会每小时检查一次，以确定是否达到5%的增加或减少阈值。如果已触发，则会自动触发作业以更新计数。

扫描的样本大小取决于用户档案存储中的实体总数。 下表显示了这些样本大小：

| 用户档案存储中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 不到100万 | 完整数据集 |
| 1到2000万 | 100万 |
| 2000多万 | 总共5% |

>[!NOTE]
>
>估计通常需要10到15秒才能运行，首先是粗略估计，然后随着读取更多记录而优化。

## 新建预览{#create-preview}

可以通过向`/preview`端点发出POST请求来创建新预览。

>[!NOTE]
>
>在创建预览作业时，会自动创建评估作业。 这两个作业将共享同一ID。

**API格式**

```http
POST /preview
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile"
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `predicateExpression` | 查询数据的PQL表达式。 |
| `predicateType` | `predicateExpression`下查询表达式的谓词类型。 当前，此属性唯一可接受的值为`pql/text`。 |
| `predicateModel` | 用户档案数据所基于的[!DNL Experience Data Model](XDM)模式类的名称。 |

**响应**

成功的响应会返回HTTP状态201（已创建），其中包含您新创建的预览的详细信息。

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `state` | 预览作业的当前状态。 最初创建时，它将处于“NEW”状态。 随后，它将处于“RUNNING”状态，直到处理完成，此时它将变为“RESULT_READY”或“FAILED”。 |
| `previewId` | 预览作业的ID，用于查看评估或预览时的查找目的，如下一节所述。 |

## 检索特定预览{#get-preview}的结果

您可以通过向`/preview`端点发出GET请求并在请求路径中提供预览ID来检索有关特定预览的详细信息。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 要检索的预览的`previewId`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关指定预览的详细信息。

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `results` | 实体ID的列表及其相关身份。 提供的链接可用于使用[用户档案访问API端点](../../profile/api/entities.md)查找指定的实体。 |

## 检索特定估计作业{#get-estimate}的结果

创建预览作业后，您可以在到`/estimate`端点的GET请求路径中使用其`previewId`来视图有关段定义的统计信息，包括预测受众大小、置信区间和误差标准偏差。

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 只有在创建预览作业时才会触发估计作业，并且这两个作业共享相同的ID值以用于查找目的。 具体而言，这是创建预览作业时返回的`previewId`值。 |

**请求**

以下请求检索特定估计作业的结果。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含估计作业的详细信息。

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | 一组对象，显示区段内按标识命名空间划分的用户档案数。 按命名空间划分的用户档案总数(将每个命名空间显示的值相加)可能高于用户档案计数量度，因为一个用户档案可能与多个命名空间关联。 例如，如果一个客户在多个渠道上与您的品牌互动，则多个命名空间将与该个别客户关联。 |
| `state` | 预览作业的当前状态。 状态将为“RUNNING”，直到处理完成，此时状态将变为“RESULT_READY”或“FAILED”。 |
| `_links.preview` | 当`state`为“RESULT_READY”时，此字段提供一个URL以视图估计。 |

## 后续步骤

阅读本指南后，您应该更好地了解如何使用分段API的预览和估计。 要了解如何访问与实时客户用户档案数据相关的指标，如特定命名空间或用户档案数据存储中的用户档案片段和合并用户档案总数，请访问[用户档案预览(`/previewsamplestatus`)端点指南](../../profile/api/preview-sample-status.md)。
