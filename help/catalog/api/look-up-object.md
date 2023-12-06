---
keywords: Experience Platform；主页；热门主题；目录；对象查找；API
solution: Experience Platform
title: 查找目录对象
description: 如果您知道特定目录对象的唯一标识符，则可以执行GET请求以查看该对象的详细信息。
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 0331b6bbd22255cab92c93070dda1ffaed5bbbcb
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# 查找目录对象

如果您知道特定的 [!DNL Catalog] 对象，您可以执行GET请求以查看该对象的详细信息。

>[!NOTE]
>
>查看特定对象时，最佳做法仍是 [按属性筛选](filter-data.md) 并且仅返回您感兴趣的资产。

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 要检索的特定对象的标识符。 |

**请求**

以下请求按数据集ID检索数据集，并返回其 `name`， `description`， `tags`、和 `files` 属性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回指定的数据集，但仅返回请求的数据集 `properties` 在身体里。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }
}
```

>[!NOTE]
>
>其值带有前缀的属性 `@` 表示相互关联的对象。 请参见附录中的 [查看相关对象](appendix.md#view-interrelated-objects) 有关如何查看这些对象的详细信息的步骤。
