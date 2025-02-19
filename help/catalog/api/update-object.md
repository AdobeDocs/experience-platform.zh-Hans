---
keywords: Experience Platform；主页；热门主题；目录；API；更新对象
solution: Experience Platform
title: 更新目录对象
description: 您可以通过在PATCH请求的路径中包含目录对象的ID来更新该目录对象的一部分。 本文档介绍如何使用字段和使用JSON修补程序表示法来对目录对象执行PATCH操作。
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 更新目录对象

您可以通过在PATCH请求的路径中包含对象ID来更新[!DNL Catalog]对象的一部分。 本文档介绍了两种对目录对象执行PATCH操作的方法：

* 使用字段
* 使用JSON修补程序表示法

>[!NOTE]
>
>对对象的PATCH操作无法修改其可扩展字段，这些字段表示相互关联的对象。 必须直接对相关对象进行修改。

## 使用字段更新

以下示例调用演示了如何使用字段和值更新对象。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要更新的[!DNL Catalog]对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求将数据集的`name`和`description`字段更新为有效负载中提供的值。 可以从有效负载中排除不更新的对象字段。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**响应**

成功的响应会返回一个数组，其中包含已更新数据集的ID。 此ID应该与PATCH请求中发送的ID匹配。 现在，对此数据集执行GET请求会显示只有`name`和`description`已更新，而所有其他值保持不变。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用JSON修补程序表示法更新 {#patch-notation}

以下示例调用演示了如何使用JSON修补程序更新对象，如[RFC-6902](https://tools.ietf.org/html/rfc6902)中所述。

有关JSON修补程序语法的详细信息，请参阅[API基础指南](../../landing/api-fundamentals.md#json-patch)。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要更新的[!DNL Catalog]对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求将数据集的`name`和`description`字段更新为每个JSON修补程序对象中提供的值。 使用JSON修补程序时，还必须将Content-Type标头设置为`application/json-patch+json`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**响应**

成功的响应会返回一个数组，其中包含已更新对象的ID。 此ID应该与PATCH请求中发送的ID匹配。 现在，对此对象执行GET请求会显示只有`name`和`description`已更新，而所有其他值保持不变。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用PATCH v2表示法更新 {#patch-v2-notation}

`/v2/dataSets/{DATASET_ID}`端点提供了一种更灵活的方法来更新复杂或深度嵌套的数据集属性。

通常，在更新深度嵌套字段（如`a.b.c.d`）时，路径中的每个级别都必须已存在。 如果缺少任何级别，则必须先手动创建每个级别，然后再设置最终值。 这通常需要多次操作，这增加了复杂性并增加了出错的可能性。

`/v2/dataSets/{DATASET_ID}`端点会自动在路径中创建任何缺失的级别。 PATCH `v2`操作不是在设置`d`之前手动检查和添加`b`和`c`，而是为您执行此操作。

当您向`/v2/dataSets/{DATASET_ID}`端点发送PATCH请求时，您只需要发送最终结构，并且系统会在应用更新之前填充缺失的部分。

>[!NOTE]
>
>`If-Match`和`If-None-Match`标头对于`/v2/dataSets/{id}`终结点为可选标头。 对此端点的PATCH请求会动态合并更新，从而允许进行修改，而无需检索最新的数据集版本。 虽然这降低了并发更新丢失数据的风险，但您可以将`If-Match`与最新的`etag`一起使用，以确保更改仅应用于特定版本。 或者，如果数据集自上一个已知版本以来未发生更改，`If-None-Match`可阻止更新。

**API格式**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要更新的数据集的标识符。 |

**请求**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**响应**

成功的响应会返回一个数组，其中包含已更新数据集的ID，该ID应当与PATCH请求中发送的ID匹配。 现在，对此对象执行GET请求会显示`extensions.adobe_lakeHouse.rowExpiration`对象已创建，无需事先手动创建步骤。

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### 更新前后数据集示例

以下示例JSON说明了PATCH请求&#x200B;**之前**&#x200B;的数据集结构，其中`extensions.adobe_lakeHouse.rowExpiration`对象不在数据集中。

+++选择以查看示例

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

以下JSON显示了PATCH请求&#x200B;**之后的数据集结构**。 更新会自动创建缺少的`extensions.adobe_lakeHouse.rowExpiration`对象，而无需执行之前的手动创建步骤。 此示例演示了`/v2/` PATCH请求如何消除多次操作的需要，从而使更新更简单、更有效。


+++选择以查看示例

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++
