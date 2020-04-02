---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建区段
topic: tutorial
translation-type: tm+mt
source-git-commit: a6a1ecd9ce49c0a55e14b0d5479ca7315e332904

---


# 创建区段

本文档提供了一个教程，用于使用分段API开发、测试、预览和保存段 [定义](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

有关如何使用用户界面构建区段的信息，请参阅“区段生成 [器指南”](../ui/overview.md)。

## 入门指南

本教程需要对创建受众细分时涉及的各种Adobe Experience Platform服务有充分的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
- [Adobe Experience Platform Segmentation Service](../home.md):允许您根据实时客户用户档案数据构建受众细分。
- [体验数据模型(XDM)](../../xdm/home.md):平台通过标准化框架组织客户体验数据。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

## 制定细分定义

分段的第一步是定义段，在称为段定义的构造中 **表示**。 段定义是封装以用户档案查询语言(PQL)编写的查询的对象。 此对象也称为 **PQL谓词**。 PQL谓词根据与您提供给实时客户用户档案的任何记录或时间序列数据相关的条件为区段定义规则。 有关编写 [PQL查询的更多信息](../pql/overview.md) ，请参阅PQL指南。

您可以通过在实时客户用户档案API中向端点发 `/segment/definitions` 出POST请求来创建新的区段定义。 以下示例概述了如何设置定义请求的格式，包括成功定义区段所需的信息。

可以通过两种方式评估区段定义——批量分段和流分段。 批分段根据预设计划或手动触发评估时评估区段，而流分段则在数据被收录到平台后立即评估区段。 本教程将使用批 **量细分**。 有关流分段的更多信息，请阅读有关流 [分段的概述](../api/streaming-segmentation.md)。

**API格式**

```http
POST /segment/definitions
```

**请求**

以下请求为名为“MyProfile”的模式创建新的区段定义。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| 属性 | 描述 |
| --------- | ------------ | 
| `name` | **必需.** 引用区段的唯一名称。 |
| `schema` | **必需.** 与分部内实体相关的模式。 由或字段 `id` 组 `name` 成。 |
| `expression` | **必需.** 包含有关区段定义的字段信息的实体。 |
| `expression.type` | 指定表达式类型。 目前，仅支持“PQL”。 |
| `expression.format` | 以值表示表达式的结构。 目前，支持以下格式： <ul><li>`pql/text`:根据发布的PQL语法，段定义的文本表示。  例如：`workAddress.stateProvince = homeAddress.stateProvince`。</li></ul> |
| `expression.value` | 符合中指示的类型的表达式 `expression.format`。 |
| `mergePolicyId` | 用于导出数据的合并策略的标识符。 有关详细信息，请阅读合 [并策略配置文档](../../profile/api/merge-policies.md)。 |
| `description` | 定义的可读描述。 |

**响应**

成功的响应会返回新创建的区段定义的详细信息，包括其系统生成的只读定义， `id` 该定义将在本教程的稍后部分使用。

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## 估计和预览受众

在开发细分定义时，您可以使用实时客户用户档案中的估计和预览工具来视图摘要级别信息，以帮助确保隔离预期受众。 估计提供关于区段定义的统计信息，例如预测受众大小和置信区间。 预览为区段定义提供符合条件的用户档案的分页列表，允许您将结果与预期结果进行比较。

通过评估和预览受众，您可以测试和优化PQL谓词，直到它们产生可预期的结果，然后在更新的段定义中使用这些谓词。

预览或评估您的细分有两个必需的步骤：

1. [创建预览作业](#create-a-preview-job)
2. [视图估计或预览](#view-an-estimate-or-preview) ，使用预览作业的ID

### 如何生成估计

数据范例用于评估分类及估计合资格用户档案之数目。 每天早晨将新数据加载到内存中(在上午12点到凌晨2点（即UTC），上午7点到上午9点之间)，并且使用当天的样本数据来估计所有细分查询。 因此，所添加的任何新字段或收集的其他数据都将反映在次日的估计中。

样本大小取决于用户档案商店中的实体总数。 下表显示了这些样本大小：

| 用户档案商店中的实体 | 样本大小 |
| ------------------------- | ----------- |
| 不到100万 | 完整数据集 |
| 1000万到2000万 | 100万 |
| 超过2000万 | 总共5% |

估计通常在10-15秒之间，从粗略估计开始，并随着读取更多记录而优化。

### 创建预览作业

您可以通过向端点发出POST请求来创建新的预览 `/preview` 作业。

**API格式**

```http
POST /preview
```

**请求**

以下请求将创建新的预览作业。 请求主体包含与段相关的查询信息。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `predicateExpression` | 用于查询数据的PQL表达式。 |
| `predicateModel` | 用户档案数据所基于的XDM模式的名称。 |

**响应**

成功的响应会返回新创建的预览作业的详细信息，包括其ID和当前处理状态。

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `state` | 预览作业的当前状态。 它将处于“RUNNING”状态，直到处理完成，此时它将变为“RESULT_READY”或“FAILED”。 |
| `previewId` | 预览作业的ID，用于查看估计或预览时的查找目的，如下节所述。 |

### 视图估计或预览

评估和预览进程以异步方式运行，因为不同的查询可能需要不同的时间来完成。 启动查询后，您可以使用API调用来检索(GET)评估或预览的当前状态（当它进行时）。

使用实时客户用户档案API，您可以通过预览作业的ID查找该作业的当前状态。 如果状态为“RESULT_READY”，则可以视图结果。 根据您是要视图估计还是预览，每个API都有各自的端点。 下面提供了两者的示例。

### 视图估计

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{PREVIEW_ID}` | 要预览的视图作业的ID。 |

**请求**

以下请求使用在上一步中创建的 `previewId` 值检索估计值。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回估计的详细信息。

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `state` | 预览作业的当前状态。 在处理完成之前，将一直为“RUNNING”（正在运行），此时它将变为“RESULT_READY”或“FAILED”（失败）。 |
| `_links.preview` | 当预览作业的当前状态为“RESULT_READY”时，此属性提供一个URL以视图估计值。 |

### 视图预览

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{PREVIEW_ID}` | 要预览的视图作业的ID。 |

**请求**

以下请求使用在上一步中创 `previewId` 建的预览检索。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回预览的详细信息。

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
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## 后续步骤

开发、测试和保存区段定义后，您便可以创建区段作业，以使用实时客户用户档案API构建受众。 有关如何完成此 [操作的详细步骤](./evaluate-a-segment.md) ，请参阅有关评估和访问区段结果的教程。