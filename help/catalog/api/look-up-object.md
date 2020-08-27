---
keywords: Experience Platform;home;popular topics;catalog;object lookup;api
solution: Experience Platform
title: 查找对象
topic: developer guide
description: '如果您知道特定Catalog对象的唯一标识符，则可以执行GET请求以视图该对象的详细信息。 '
translation-type: tm+mt
source-git-commit: dd1f508b93e8eac14e3c41fac9d8f49769d08f46
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 2%

---


# 查找对象

如果您知道特定对象的唯一标 [!DNL Catalog] 识符，则可以执行GET请求以视图该对象的详细信息。

>[!NOTE]
>
>查看特定对象时，仍最好按属 [性筛选](filter-data.md) ，并仅返回您感兴趣的属性。

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索 [!DNL Catalog] 的对象的类型。 有效对象有： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要检索的特定对象的标识符。 |

**请求**

以下请求按数据集的ID检索数据集，并 `name`返回 `description`其 `state`、 `tags`、和 `files` 属性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回的指定数据集中只有正文 `properties` 中请求的数据集。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE]
>
>其值前缀为相关对象 `@` 的属性。 有关如何视图这些对 [象详细信息](appendix.md#view-interrelated-objects) ，请参阅查看相关对象的附录部分。
