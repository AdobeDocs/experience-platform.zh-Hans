---
keywords: Experience Platform；主页；热门主题；目录；API；替换对象
solution: Experience Platform
title: 替换目录对象
topic-legacy: developer guide
description: 您可以使用PUT请求覆盖Catalog对象的内容，其中整个资源将被请求有效负载替换。
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 替换目录对象

您可以覆盖 [!DNL Catalog] 对象，其中整个资源被请求有效负载替换。

>[!NOTE]
>
>如果您只需更新 [!DNL Catalog] 对象，则使用PATCH请求可能会更有效。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要替换的对象。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求使用有效负载中提供的值覆盖数据集。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的响应会返回一个包含被覆盖对象ID的数组。 此ID应与在PUT请求中发送的ID匹配。 现在，为此对象执行GET请求会显示其详细信息已替换为在上一个PUT请求的有效负荷中提供的详细信息。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
