---
keywords: Experience Platform；主页；热门主题；目录；对象查找；API
solution: Experience Platform
title: 查找目录对象
topic-legacy: developer guide
description: 如果您知道特定Catalog对象的唯一标识符，则可以执行GET请求以查看该对象的详细信息。
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# 查找目录对象

如果您知道特定 [!DNL Catalog] 对象时，您可以执行GET请求以查看该对象的详细信息。

>[!NOTE]
>
>查看特定对象时，最佳做法仍是 [按属性筛选](filter-data.md) 并仅返回您感兴趣的资产。

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要检索的对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要检索的特定对象的标识符。 |

**请求**

以下请求会按数据集的ID检索数据集，并返回其 `name`, `description`, `state`, `tags`和 `files` 属性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回仅包含请求的指定数据集 `properties` 在身体里。

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
>其值以前缀的属性 `@` 表示相互关联的对象。 请参阅 [查看相关对象](appendix.md#view-interrelated-objects) 以了解有关如何查看这些对象详细信息的步骤。
