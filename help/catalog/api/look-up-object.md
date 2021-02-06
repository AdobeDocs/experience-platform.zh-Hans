---
keywords: Experience Platform；主页；热门主题；目录；对象查找；api
solution: Experience Platform
title: 查找目录对象
topic: developer guide
description: '如果您知道特定Catalog对象的唯一标识符，则可以执行GET请求以视图该对象的详细信息。 '
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# 查找目录对象

如果您知道特定[!DNL Catalog]对象的唯一标识符，则可以执行GET请求以视图该对象的详细信息。

>[!NOTE]
>
>查看特定对象时，仍最好按属性](filter-data.md)进行[过滤，只返回您感兴趣的属性。

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要检索的[!DNL Catalog]对象的类型。 有效对象有： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要检索的特定对象的标识符。 |

**请求**

以下请求按其ID检索数据集，并返回其`name`、`description`、`state`、`tags`和`files`属性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回的指定数据集中只有请求的主体`properties`。

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
>其值前缀为`@`的属性表示相关对象。 有关如何视图这些对象详细信息的步骤，请参见[查看相关对象](appendix.md#view-interrelated-objects)的附录部分。
