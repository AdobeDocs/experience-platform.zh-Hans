---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 删除对象
topic: developer guide
translation-type: tm+mt
source-git-commit: 6c17351b04fedefd4b57b9530f1d957da8183a68

---


# 删除对象

可以通过在DELETE请求的路径中提供Catalog对象的ID来删除它。

>[!WARNING] 删除对象时要格外小心，因为此操作无法撤消，并且可能会在Experience Platform的其他位置产生破坏性更改。

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT] 端 `DELETE /batches/{ID}` 点已弃用。 要删除批，您应使用批 [摄取API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)。

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要删除的Catalog对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求将删除在请求路径中指定其ID的数据集。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200(OK)和包含已删除数据集ID的数组。 此ID应与在DELETE请求中发送的ID匹配。 对已删除的对象执行GET请求将返回HTTP状态404（未找到），确认已成功删除数据集。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE] 如果没有与请求中提供的ID匹配的Catalog对象，您仍可能收到HTTP状态代码200，但响应数组将为空。
