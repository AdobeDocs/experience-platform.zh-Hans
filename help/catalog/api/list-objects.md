---
keywords: Experience Platform；主页；热门主题；过滤器；过滤器；过滤数据；过滤数据
solution: Experience Platform
title: 列表目录对象
topic-legacy: developer guide
description: 您可以通过单个API调用检索特定类型的所有可用对象的列表，最佳实践是包含可限制响应大小的过滤器。
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 列表目录对象

您可以通过单个API调用检索特定类型的所有可用对象的列表，最佳实践是包含可限制响应大小的过滤器。

**API格式**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | 用于筛选响应中返回的结果的查询参数。 多个参数以与号(`&`)。 请参阅 [筛选目录数据](filter-data.md) 以了解更多信息。 |

**请求**

以下示例请求检索数据集列表，其中 `limit` 过滤器会减少对五个结果的响应，而 `properties` 过滤器，以限制每个数据集显示的属性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回 [!DNL Catalog] 键值对形式的对象，按请求中提供的查询参数进行筛选。 对于每个键值对，键表示 [!DNL Catalog] 对象，然后在对 [查看特定对象](look-up-object.md) 以了解更多详细信息。

>[!NOTE]
>
>如果返回的对象不包含由 `properties` 查询时，响应只返回它所包含的请求属性，如 ***`Sample Dataset 3`*** 和 ***`Sample Dataset 4`*** 下。

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
