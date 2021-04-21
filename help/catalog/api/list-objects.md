---
keywords: Experience Platform；主页；热门主题；过滤器；过滤器；过滤数据；过滤数据
solution: Experience Platform
title: 列表目录对象
topic-legacy: developer guide
description: 您可以通过单个API调用检索特定类型的所有可用对象的列表，最佳实践是包括限制响应大小的过滤器。
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 列表 Catalog对象

您可以通过单个API调用检索特定类型的所有可用对象的列表，最佳实践是包括限制响应大小的过滤器。

**API格式**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要列出的[!DNL Catalog]对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | 用于筛选在响应中返回的结果的查询参数。 多个参数用&amp;符号(`&`)分隔。 有关详细信息，请参阅[筛选目录数据](filter-data.md)指南。 |

**请求**

下面的示例请求检索数据集的列表，其中`limit`过滤器将响应减少到五个结果，而`properties`过滤器将限制每个数据集显示的属性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应以键值对的形式返回[!DNL Catalog]对象的列表，该键值对由请求中提供的查询参数筛选。 对于每个键值对，键表示有关[!DNL Catalog]对象的唯一标识符，然后该标识符可用于对特定对象](look-up-object.md)的视图的另一个调用，以获取更多详细信息。[

>[!NOTE]
>
>如果返回的对象不包含由`properties`查询指示的一个或多个请求属性，则响应只返回它包含的请求属性，如下面的&#x200B;***`Sample Dataset 3`***&#x200B;和&#x200B;***`Sample Dataset 4`***&#x200B;所示。

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
