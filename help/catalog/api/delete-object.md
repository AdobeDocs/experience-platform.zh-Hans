---
keywords: Experience Platform；主页；热门主题；删除对象；目录服务；API
solution: Experience Platform
title: 删除API中的对象
topic-legacy: developer guide
description: 您可以通过在目录请求的路径中提供Catalog对象ID来删除该DELETE对象。
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# 删除API中的对象

您可以删除 [!DNL Catalog] 对象，方法是在DELETE请求的路径中提供其ID。

>[!WARNING]
>
>删除对象时请格外小心，因为此操作无法撤消，并且可能会在 [!DNL Experience Platform].

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>的 `DELETE /batches/{ID}` 终结点已弃用。 要删除批处理，您应使用 [批量摄取API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 类型 [!DNL Catalog] 要删除的对象。 有效对象包括： <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求会删除请求路径中指定了ID的数据集。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200（确定）和一个包含已删除数据集ID的数组。 此ID应与在DELETE请求中发送的ID匹配。 对已删除的对象执行GET请求时，会返回HTTP状态404（未找到），以确认已成功删除数据集。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>如果否 [!DNL Catalog] 对象与请求中提供的ID匹配，您仍可能收到HTTP状态代码200，但响应数组将为空。
