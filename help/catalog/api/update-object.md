---
keywords: Experience Platform；主页；热门主题；目录；API；更新对象
solution: Experience Platform
title: 更新目录对象
description: 您可以通过在PATCH请求的路径中包含目录对象的ID来更新目录对象的一部分。 本文档介绍如何使用字段和使用JSON修补程序表示法来对目录对象执行PATCH操作。
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 296a988a67871933723ad0474c113cb93fdbf255
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 2%

---

# 更新目录对象

您可以通过在PATCH请求的路径中包含其ID来更新[!DNL Catalog]对象的一部分。 本文档介绍了对目录对象执行PATCH操作的两种方法：

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

## 使用JSON修补程序表示法更新

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
