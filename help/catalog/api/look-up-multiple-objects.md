---
keywords: Experience Platform;home;popular topics;catalog;multiple object lookup;api
solution: Experience Platform
title: 查找多个对象
topic: developer guide
description: 如果您希望视图多个特定对象，而不是对每个对象发出一个请求，目录为请求同一类型的多个对象提供了一个简单的快捷方式。 您可以通过包含以逗号分隔的IDGET，使用单个列表请求返回多个特定对象。
translation-type: tm+mt
source-git-commit: dd1f508b93e8eac14e3c41fac9d8f49769d08f46
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# 查找多个对象

如果您希望视图多个特定对象，而不是对每个对象发出一个请求，则 [!DNL Catalog] 为请求同一类型的多个对象提供了一个简单的快捷方式。 您可以通过包含以逗号分隔的IDGET，使用单个列表请求返回多个特定对象。

>[!NOTE]
>
>即使请求特定 [!DNL Catalog] 对象，也最好 `properties` 查询参数以仅返回所需的属性。

**API格式**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| `{OBJECT_TYPE}` |要检索的 [!DNL Catalog] 对象的类型。 有效对象有： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` |要检索的特定对象的标识符。 |

**请求**

以下请求包括以逗号分隔的列表集ID以及要为每个数据集返回的属性的以逗号分隔的列表。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回指定数据集的列表，其中只包含每个数据集所`name`请求的 `description`属性( `files`、和)。

>[!NOTE]
>
>如果返回的对象不包含查询所指示的一个或多个请求属性， `properties` 则响应将仅返回其确实包含的请求属性，如 ***`Sample Dataset 3`*** 下 ***`Sample Dataset 4`*** 所示。

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
