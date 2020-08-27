---
keywords: Experience Platform;home;popular topics;delete an object;catalog service;api
solution: Experience Platform
title: 删除对象
topic: developer guide
description: 您可以通过在DELETE请求的路径中提供目录对象的ID来删除该对象。
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 2%

---


# 删除对象

您可以通过 [!DNL Catalog] 在DELETE请求的路径中提供对象ID来删除对象。

>[!WARNING]
>
>删除对象时要格外小心，因为此操作无法撤消，并且可能会在其他位置产生破坏性的更改 [!DNL Experience Platform]。

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>终 `DELETE /batches/{ID}` 结点已弃用。 要删除批，您应使用批 [摄取API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch)。

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 要删除 [!DNL Catalog] 的对象类型。 有效对象有： <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 要更新的特定对象的标识符。 |

**请求**

以下请求将删除在请求路径中指定ID的数据集。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200(OK)和包含已删除数据集ID的数组。 此ID应与在DELETE请求中发送的ID匹配。 对已删除的对象执行GET请求将返回HTTP状态404（未找到），确认已成功删除数据集。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>如果没 [!DNL Catalog] 有与请求中提供的ID匹配的对象，您仍可能收到HTTP状态代码200，但响应数组为空。
