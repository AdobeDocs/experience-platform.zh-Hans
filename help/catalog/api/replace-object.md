---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 替换对象
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# 替换对象

您可以使用PUT请求覆 [!DNL Catalog] 盖对象的内容，其中整个资源将替换为请求有效负荷。

>[!NOTE]
>
>如果您只需要更新对象中的几个特定字 [!DNL Catalog] 段，使用PATCH请求可能会更高效。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要替换 [!DNL Catalog] 的对象类型。 有效对象有： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求使用有效负荷中提供的值覆盖数据集。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**响应**

成功的响应会返回包含被覆盖对象ID的数组。 此ID应与PUT请求中发送的ID匹配。 现在，为此对象执行GET请求时显示，其详细信息已替换为之前PUT请求的有效负荷中提供的详细信息。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
