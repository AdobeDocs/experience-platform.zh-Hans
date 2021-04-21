---
keywords: Experience Platform；主页；热门主题；目录；api；替换对象
solution: Experience Platform
title: 替换目录对象
topic-legacy: developer guide
description: 您可以使用PUT请求覆盖Catalog对象的内容，其中整个资源将替换为请求有效负荷。
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 替换Catalog对象

您可以使用PUT请求覆盖[!DNL Catalog]对象的内容，其中整个资源将替换为请求有效负荷。

>[!NOTE]
>
>如果您只需要更新[!DNL Catalog]对象中的几个特定字段，使用PATCH请求可能会更高效。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要替换的[!DNL Catalog]对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求使用在负载中提供的值覆盖数据集。

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

成功的响应返回包含被覆盖对象ID的数组。 此ID应与在PUT请求中发送的ID匹配。 现在，对此对象执行GET请求时显示，其详细信息已替换为之前PUT请求的有效负荷中提供的详细信息。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
