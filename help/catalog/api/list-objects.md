---
keywords: Experience Platform；主页；热门主题；过滤器；过滤器；过滤器数据；过滤器数据
solution: Experience Platform
title: 列出目录对象
description: 您可以通过单个API调用检索特定类型的所有可用对象列表，最佳做法是包含限制响应大小的过滤器。
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 409d052c119814a1cf6b79ff4448d1100b18e199
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 列出目录对象

您可以通过单个API调用检索特定类型的所有可用对象列表，最佳做法是包含限制响应大小的过滤器。

**API格式**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要列出的对象。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{FILTER}` | 用于筛选响应中返回结果的查询参数。 多个参数用&amp;符号(`&`)。 请参阅指南，网址为 [筛选目录数据](filter-data.md) 以了解更多信息。 |

**请求**

下面的示例请求检索数据集列表，使用 `limit` 筛选条件将响应减少到五个结果，以及 `properties` 该过滤器限制为每个数据集显示的属性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回列表 [!DNL Catalog] 键值对形式的对象，按请求中提供的查询参数进行筛选。 对于每个键值对，键表示 [!DNL Catalog] 有问题的对象，随后可以在对的调用中使用 [查看该特定对象](look-up-object.md) 以了解更多详细信息。

>[!NOTE]
>
>如果返回的对象不包含请求的一个或多个属性，这些属性由 `properties` 查询时，响应仅返回所请求的属性，如中所示 ***`Sample Dataset 3`*** 和 ***`Sample Dataset 4`*** 下。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSetFiles?dataSetId=5bda3a4228babc0000126377"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bde21511dd27b0000d24e95"
    }
}
```
