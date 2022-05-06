---
keywords: Experience Platform；主页；热门主题；目录；API；更新对象
solution: Experience Platform
title: 更新目录对象
topic-legacy: developer guide
description: 您可以通过在目录请求的路径中包含Catalog对象的ID来更新该对象的部分PATCH。 本文档介绍如何使用字段和使用JSON修补程序符号对目录对象执行PATCH操作。
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# 更新目录对象

您可以更新 [!DNL Catalog] 对象，方法是在PATCH请求的路径中包含其ID。 本文档介绍了对目录对象执行PATCH操作的两种方法：

* 使用字段
* 使用JSON修补程序符号

>[!NOTE]
>
>对对象的PATCH操作无法修改其表示相关对象的可扩展字段。 必须直接修改相关对象。

## 使用字段更新

以下示例调用演示了如何使用字段和值更新对象。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要更新的对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求更新了 `name` 和 `description` 数据集的字段映射到有效负载中提供的值。 可以从有效负载中排除不要更新的对象字段。

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

成功的响应会返回一个包含已更新数据集ID的数组。 此ID应与在PATCH请求中发送的ID匹配。 现在，为此GET集执行请求时，仅显示 `name` 和 `description` 已更新，而所有其他值保持不变。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用JSON修补程序符号进行更新

以下示例调用演示了如何使用JSON修补程序更新对象，如 [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要更新的对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求更新了 `name` 和 `description` 数据集的字段，指向每个JSON修补程序对象中提供的值。 使用JSON修补程序时，还必须将Content-Type标头设置为 `application/json-patch+json`.

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

成功的响应会返回一个包含已更新对象ID的数组。 此ID应与在PATCH请求中发送的ID匹配。 现在，为此对象执行GET请求时，仅显示 `name` 和 `description` 已更新，而所有其他值保持不变。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
