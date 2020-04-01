---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 更新对象
topic: developer guide
translation-type: tm+mt
source-git-commit: 4361032b419622d7decc02194d38885b114749e4

---


# 更新对象

通过在PATCH请求的路径中包含Catalog对象的ID，可以更新其部分。 本文档介绍了对Catalog对象执行PATCH操作的两种方法：

* 使用字段
* 使用JSON修补程序表示法

>[!NOTE] 对象上的PATCH操作无法修改其可扩展字段，这些字段表示相关对象。  必须直接修改相关对象。

## 使用字段更新

以下示例调用演示了如何使用字段和值更新对象。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要更新的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求将数据集 `name` 的 `description` 和字段更新为有效负荷中提供的值。 不要更新的对象字段可以从有效负荷中排除。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**响应**

成功的响应会返回一个包含已更新数据集ID的数组。 此ID应与在PATCH请求中发送的ID匹配。 对此数据集执行GET请求现在显示，只有和 `name` 已更 `description` 新，而所有其他值保持不变。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用JSON修补符号进行更新

以下示例调用演示了如何使用JSON修补程序更新对象，如 [RFC-6902中所述](https://tools.ietf.org/html/rfc6902)。

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要更新的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求将数据集 `name` 的 `description` 和字段更新为每个JSON修补对象中提供的值。 使用JSON修补程序时，还必须将Content-Type头设置为 `application/json-patch+json`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**响应**

成功的响应会返回一个包含已更新对象ID的数组。 此ID应与在PATCH请求中发送的ID匹配。 对此对象执行GET请求现在表明，只有和 `name` 已更 `description` 新，而所有其他值保持不变。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
