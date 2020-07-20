---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 预览和估计端点
topic: developer guide
translation-type: tm+mt
source-git-commit: b3e6a6f1671a456b2ffa61139247c5799c495d92
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 2%

---


# 预览和估计端点

在开发细分定义时，您可以使用中的估计和预览工具来 [!DNL Adobe Experience Platform] 视图摘要级别信息，以帮助确保隔离预期受众。 **预览** 为区段定义提供符合条件的列表的分页用户档案，使您能够将结果与预期进行比较。 **估计** 提供关于区段定义的统计信息，如预测受众大小、置信区间和误差标准偏差。

## 入门指南

本指南中使用的端点是API的一 [!DNL Adobe Experience Platform Segmentation Service] 部分。 在继续之前，请查 [看入门指南](./getting-started.md) ，了解成功调用API需要了解的重要信息，包括必需的头以及如何读取示例API调用。

## 估计的生成方式

数据采样的触发方式取决于摄取的方法。

对于批量摄取，用户档案存储区每十五分钟自动扫描一次，以查看自上次采样作业运行以来是否成功摄取了新批量。 如果是这样，随后扫描用户档案存储，以查看记录数是否至少有5%的变化。 如果满足这些条件，将触发新的采样作业。

对于流式摄取，每小时自动扫描用户档案商店，以查看记录数是否至少有5%的变化。 如果满足此条件，将触发新的采样作业。

扫描的样本大小取决于用户档案存储中的实体总数。 下表显示了这些示例大小：

| 用户档案商店中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 不到100万 | 完整数据集 |
| 1000万到2000万 | 100万 |
| 2000多万 | 总共5% |

>[!NOTE] 估计通常需要10到15秒才能运行，首先是粗略估计，然后随着读取更多记录而优化。

## Create a new preview {#create-preview}

可以通过向端点发出POST请求来创建新 `/preview` 预览。

>[!NOTE] 在创建预览作业时，会自动创建评估作业。 这两个作业将共享同一ID。

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
| `predicateType` | 查询表达式的谓词类型 `predicateExpression`。 当前，此属性唯一接受的值是 `pql/text`。 |
| `predicateModel` | 模式用户档案数据的体验数据模型(XDM)的名称。 |

**响应**

成功的响应会返回HTTP状态201（已创建），其中包含新创建预览的详细信息。

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

## 检索特定预览的结果 {#get-preview}

您可以通过向端点发出GET请求并在请求路径中提 `/preview` 供预览ID来检索有关特定预览的详细信息。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 要 `previewId` 检索的预览的值。 |

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
        },
        "state": "RESULT_READY",
        "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
        }
    }],
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `results` | 实体ID的列表及其相关身份。 提供的链接可用于使用用户档案访问API查找指定 [的实体](../../profile/api/entities.md)。 |

## 检索特定评估作业的结果 {#get-estimate}

创建预览作业后，可以在GET请求到端点的路径中使 `previewId` 用它来有关段定义的 `/estimate` 视图统计信息，包括预计受众大小、置信间隔和错误标准偏差。

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 仅当创建预览作业，并且两个作业共享相同的ID值以用于查找时，才会触发估计作业。 具体而言，这是 `previewId` 创建预览作业时返回的值。 |

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

成功的响应会返回HTTP状态200，其中包含估计作业的详细信息。

```json
{
    "estimatedSize": 0,
    "numRowsToRead": 1,
    "state": "RESULT_READY",
    "profilesReadSoFar": 1,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 0,
    "totalRows": 1,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `state` | 预览作业的当前状态。 在处理完成之前，将一直为“RUNNING”，此时它将变为“RESULT_READY”或“FAILED”。 |
| `_links.preview` | 当预览作业的当前状态为“RESULT_READY”时，此属性提供一个URL来视图估计。 |

## 后续步骤

阅读本指南后，您现在可以更好地了解如何处理预览和评估。 要进一步了解其他Segmentation Service API端点，请阅读Segmentation Service开 [发人员指南概述](./overview.md)。