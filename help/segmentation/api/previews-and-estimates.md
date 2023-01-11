---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；预览；估计；预览和估计；估计和预览；API;API;
solution: Experience Platform
title: 预览和估算API端点
description: 在开发区段定义时，您可以使用Adobe Experience Platform中的估计和预览工具来查看摘要级别的信息，以帮助确保隔离预期受众。
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# 预览和估算端点

在开发区段定义时，您可以使用Adobe Experience Platform中的评估和预览工具来查看摘要级别的信息，以帮助确保隔离您预期的受众。

* **预览** 为区段定义提供符合条件的用户档案的分页列表，以便将结果与预期结果进行比较。

* **估计** 提供有关区段定义的统计信息，如预计受众规模、置信区间和误差标准偏差。

>[!NOTE]
>
>要访问与实时客户配置文件数据相关的类似量度，例如特定命名空间或配置文件数据存储中的配置文件片段和合并配置文件的总数，请参阅 [配置文件预览（预览示例状态）端点指南](../../profile/api/preview-sample-status.md)，是配置文件API开发人员指南的一部分。

## 快速入门

本指南中使用的端点是 [!DNL Adobe Experience Platform Segmentation Service] API。 在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括所需的标头以及如何读取示例API调用。

## 如何生成估计

当将记录摄取到用户档案存储区时，总用户档案计数增加或减少5%以上，则会触发取样作业以更新计数。 数据采样的触发方式取决于摄取方法：

* **批量摄取：** 对于批量摄取，在将批成功摄取到用户档案存储的15分钟内，如果满足5%的增加或减少阈值，则将运行一个作业以更新计数。
* **流式摄取：** 对于流数据工作流，每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果已执行，则会自动触发作业以更新计数。

扫描的样本大小取决于配置文件存储中的实体总数。 下表显示了这些样本大小：

| 配置文件存储中的实体 | 示例大小 |
| ------------------------- | ----------- |
| 不到100万 | 完整数据集 |
| 1到2000万 | 100万 |
| 2000多万 | 总共5% |

>[!NOTE]
>
>估计值通常需要10到15秒才能运行，从粗略估计开始，随着读取更多记录，将进行优化。

## 创建新预览 {#create-preview}

您可以通过向 `/preview` 端点。

>[!NOTE]
>
>在创建预览作业时，将自动创建评估作业。 这两个作业将共享相同的ID。

**API格式**

```http
POST /preview
```

**请求**

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
| `predicateExpression` | 用于查询数据的PQL表达式。 |
| `predicateType` | 下查询表达式的谓词类型 `predicateExpression`. 目前，此属性唯一接受的值是 `pql/text`. |
| `predicateModel` | 的名称 [!DNL Experience Data Model] (XDM)配置文件数据所基于的架构类。 |
| `graphType` | 要从中获取群集的图形类型。 支持的值包括 `none` （不执行身份拼合）和 `pdg` （根据您的专用身份图执行身份拼合）。 |

**响应**

成功响应会返回HTTP状态201（已创建），其中包含新创建预览的详细信息。

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
| `state` | 预览作业的当前状态。 最初创建时，该变量将处于“NEW”状态。 随后，它将处于“正在运行”状态，直到处理完成，此时它将变为“RESULT_READY”或“失败”。 |
| `previewId` | 预览作业的ID，在查看预估或预览时用于查找目的，如下一节中所述。 |

## 检索特定预览的结果 {#get-preview}

您可以通过向 `/preview` 端点和在请求路径中提供预览ID。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 的 `previewId` 要检索的预览的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关指定预览的详细信息。

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
| `results` | 实体ID及其相关标识的列表。 提供的链接可用于使用 [配置文件访问API端点](../../profile/api/entities.md). |

## 检索特定评估作业的结果 {#get-estimate}

创建预览作业后，即可使用 `previewId` 在GET请求的路径中 `/estimate` 用于查看有关区段定义的统计信息的端点，包括预计受众大小、置信区间和错误标准偏差。

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 仅当创建了预览作业，并且两个作业共享相同的ID值以进行查找时，才会触发估计作业。 具体而言，这是 `previewId` 创建预览作业时返回的值。 |

**请求**

以下请求检索特定估计作业的结果。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含估计作业的详细信息。

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
| `estimatedNamespaceDistribution` | 一个对象数组，显示区段内按身份命名空间划分的配置文件数。 按命名空间划分的配置文件总数（将每个命名空间显示的值相加）可能高于配置文件计数量度，因为一个配置文件可能与多个命名空间关联。 例如，如果客户在多个渠道上与您的品牌进行交互，则多个命名空间将与该个别客户关联。 |
| `state` | 预览作业的当前状态。 在处理完成之前，状态将为“正在运行”，此时状态将变为“RESULT_READY”或“失败”。 |
| `_links.preview` | 当 `state` 为“RESULT_READY”，则此字段提供一个用于查看预估的URL。 |

## 后续步骤

阅读本指南后，您应该更好地了解如何使用分段API进行预览和评估。 要了解如何访问与实时客户配置文件数据相关的量度，例如特定命名空间或配置文件数据存储中的配置文件片段和合并配置文件总数，请访问 [配置文件预览(`/previewsamplestatus`)endpoint指南](../../profile/api/preview-sample-status.md).
