---
keywords: Experience Platform；主页；热门主题；目录；多个对象查找；API
solution: Experience Platform
title: 查找多个目录对象
description: 如果要查看多个特定对象，而不是为每个对象发出一个请求，则Catalog提供了简单的快捷方式，用于请求同一类型的多个对象。 您可以使用单个GET请求，通过包含以逗号分隔的ID列表来返回多个特定对象。
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# 查找多个目录对象

如果您希望查看多个特定对象，而不是为每个对象发出一个请求， [!DNL Catalog] 为请求同一类型的多个对象提供了简单的快捷方式。 您可以使用单个GET请求，通过包含以逗号分隔的ID列表来返回多个特定对象。

>[!NOTE]
>
>即使请求特定 [!DNL Catalog] 对象，最佳做法仍是 `properties` 查询参数以仅返回所需的属性。

**API格式**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | 要检索的特定对象之一的标识符。 |

**请求**

以下请求包含以逗号分隔的数据集ID列表以及要为每个数据集返回的以逗号分隔的属性列表。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回指定数据集的列表，其中仅包含请求的属性(`name`， `description`、和 `files`)。

>[!NOTE]
>
>如果返回的对象不包含由指定的一个或多个请求属性， `properties` 查询时，响应仅返回所请求的属性，如中所示 ***`Sample Dataset 3`*** 和 ***`Sample Dataset 4`*** 下。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
