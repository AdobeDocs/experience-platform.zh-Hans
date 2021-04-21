---
keywords: Experience Platform；主页；热门主题；删除对象；目录服务；api
solution: Experience Platform
title: 删除API中的对象
topic-legacy: developer guide
description: 可以通过在DELETE请求的路径中提供Catalog对象的ID来删除它。
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# 删除API中的对象

可以通过在DELETE请求的路径中提供[!DNL Catalog]对象的ID来删除该对象。

>[!WARNING]
>
>删除对象时要格外小心，因为此操作无法撤消，并且可能会在[!DNL Experience Platform]的其他位置产生破坏更改。

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>`DELETE /batches/{ID}`终结点已弃用。 要删除批，您应使用[批摄取API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)。

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要删除的[!DNL Catalog]对象的类型。 有效对象包括： <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

>[!NOTE]
>
>如果没有与请求中提供的ID匹配的[!DNL Catalog]对象，您仍可能收到HTTP状态代码200，但响应数组将为空。
