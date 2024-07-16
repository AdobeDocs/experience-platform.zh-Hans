---
keywords: Experience Platform；主页；热门主题；目录；API；替换对象
solution: Experience Platform
title: 替换目录对象
description: 您可以使用PUT请求覆盖目录对象的内容，其中整个资源将替换为请求有效负载。
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 2d6167ee7aaa0b79514be6e532e61602ae5cc640
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 替换目录对象

您可以使用PUT请求覆盖[!DNL Catalog]对象的内容，其中整个资源将替换为请求有效负载。

>[!NOTE]
>
>如果只需要更新[!DNL Catalog]对象中的几个特定字段，则使用PATCH请求可能会更有效。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要替换的[!DNL Catalog]对象的类型。 有效对象为： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
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
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    }'
```

**响应**

成功的响应会返回一个包含被覆盖对象ID的数组。 此ID应该与PUT请求中发送的ID匹配。 现在，为此对象执行GET请求时，会显示其详细信息已替换为上一个PUT请求的有效负载中提供的详细信息。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
