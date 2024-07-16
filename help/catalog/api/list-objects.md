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
| `{OBJECT_TYPE}` | 要列出的[!DNL Catalog]对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{FILTER}` | 用于筛选响应中返回结果的查询参数。 多个参数由&amp;符号(`&`)分隔。 有关详细信息，请参阅[筛选目录数据](filter-data.md)指南。 |

**请求**

下面的示例请求检索数据集列表，使用`limit`筛选器减少对5个结果的响应，使用`properties`筛选器限制为每个数据集显示的属性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应以键值对的形式返回[!DNL Catalog]对象的列表，该列表按请求中提供的查询参数进行筛选。 对于每个键值对，该键代表所讨论的[!DNL Catalog]对象的唯一标识符，该唯一标识符随后可用于对[查看特定对象](look-up-object.md)的另一调用，以了解更多详细信息。

>[!NOTE]
>
>如果返回的对象不包含`properties`查询指示的一个或多个请求属性，则响应仅返回它包含的一个或多个请求属性，如下面的&#x200B;***`Sample Dataset 3`***&#x200B;和&#x200B;***`Sample Dataset 4`***&#x200B;所示。

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
