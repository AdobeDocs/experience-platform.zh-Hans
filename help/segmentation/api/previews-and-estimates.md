---
solution: Experience Platform
title: 预览和估算API端点
description: 在开发区段定义时，您可以使用Adobe Experience Platform中的评估和预览工具来查看摘要级别的信息，从而帮助您隔离预期的受众。
role: Developer
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: a374d261e3b34b30869f1a9e8486d52f5bd658cb
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 2%

---

# 预览和估计端点

在开发区段定义时，您可以使用Adobe Experience Platform中的评估和预览工具来查看摘要级别的信息，从而帮助确保隔离您预期的受众。

* **预览**&#x200B;提供符合区段定义资格的用户档案的分页列表，允许您比较结果与预期结果。

* **估算值**&#x200B;提供有关区段定义的统计信息，例如预计受众大小、置信区间和误差标准偏差。

>[!NOTE]
>
>要访问与实时客户个人资料数据相关的类似量度，如特定命名空间或个人资料数据存储中的个人资料片段和合并个人资料的总数，请参阅个人资料API开发人员指南中的[个人资料预览（预览样本状态）端点指南](../../profile/api/preview-sample-status.md)。

## 快速入门

本指南中使用的端点是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 如何生成估算

当将记录摄取到配置文件存储中增加或减少总配置文件计数超过3%时，将触发取样作业以更新计数。 数据采样的触发方式取决于摄取方法：

* **批次摄取：**&#x200B;对于批次摄取，在成功将批次摄取到配置文件存储区后15分钟内，如果满足3%的增加或减少阈值，将运行作业以更新计数。
* **流式摄取：**&#x200B;对于流式数据工作流，每小时进行一次检查，以确定是否已达到3%的增加或减少阈值。 如果超过100次，则会自动触发作业以更新计数。

扫描的样本大小取决于配置文件存储区中的实体总数。 下表显示了这些样本量：

| 配置文件存储中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 少于100万 | 完整数据集 |
| 100万到2000万 | 100万 |
| 超过2000万 | 占总数的5% |

>[!NOTE]
>
>估计值通常需要10到15秒来运行，从粗略估计开始，并随着读取更多记录而优化。

## 新建预览 {#create-preview}

您可以通过向`/preview`端点发出POST请求来创建新的预览。

>[!NOTE]
>
>创建预览作业时，将自动创建评估作业。 这两个作业将共享相同的ID。

**API格式**

```http
POST /preview
```

**请求**

+++ 创建预览的示例请求。

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `predicateExpression` | 作为数据查询依据的PQL表达式。 |
| `predicateType` | `predicateExpression`下的查询表达式的谓词类型。 当前，此属性的唯一接受值为`pql/text`。 |
| `predicateModel` | 配置文件数据所基于的[!DNL Experience Data Model] (XDM)架构类的名称。 |
| `graphType` | 您希望从中获取集群的图形类型。 支持的值为`none`（不执行身份拼接）和`pdg`（根据您的专用身份图形执行身份拼接）。 |

+++

**响应**

成功的响应返回HTTP状态201（已创建）以及新创建的预览的详细信息。

+++ 创建预览时的示例响应。

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
| `state` | 预览作业的当前状态。 最初创建时，它将处于“NEW”状态。 随后，它将处于“正在运行”状态，直到处理完成，此时它将变为“RESULT_READY”或“FAILED”。 |
| `previewId` | 预览作业的ID，用于在查看估计或预览时查找，如下节所述。 |

+++

## 检索特定预览的结果 {#get-preview}

您可以通过向`/preview`端点发出GET请求并在请求路径中提供预览ID，来检索有关特定预览的详细信息。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 要检索的预览的`previewId`值。 |

**请求**

+++ 用于检索预览的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

+++ 检索预览时的示例响应。

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
| `results` | 实体ID及其相关标识的列表。 提供的链接可用于使用[配置文件访问API终结点](../../profile/api/entities.md)查找指定的实体。 |

+++

## 检索特定估算作业的结果 {#get-estimate}

创建预览作业后，您可以在GET请求到`previewId`端点的路径中使用其`/estimate`查看有关区段定义的统计信息，包括预计受众大小、置信区间和错误标准偏差。

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 仅在创建预览作业且两个作业共享同一ID值以进行查找时，才会触发估计作业。 具体而言，这是创建预览作业时返回的`previewId`值。 |

**请求**

以下请求检索特定估计作业的结果。

+++ 用于检索估计作业的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200以及估计作业的详细信息。

+++ 检索估计作业时的示例响应。

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
| `estimatedNamespaceDistribution` | 一个对象数组，显示区段定义中按身份命名空间划分的配置文件数。 按命名空间列出的配置文件总数（将每个命名空间显示的值相加）可能高于配置文件计数量度，因为一个配置文件可能与多个命名空间关联。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个人客户关联。 |
| `state` | 预览作业的当前状态。 状态将为“正在运行”，直到处理完成，此时状态将变为“RESULT_READY”或“FAILED”。 |
| `_links.preview` | 当`state`为“RESULT_READY”时，此字段提供一个URL以查看估计值。 |

+++

## 后续步骤

阅读本指南后，您应该更好地了解如何使用分段API进行预览和评估。 要了解如何访问与实时客户配置文件数据相关的量度，如特定命名空间内的配置文件片段和合并配置文件总数或配置文件数据存储的总量，请访问[配置文件预览(`/previewsamplestatus`)端点指南](../../profile/api/preview-sample-status.md)。
