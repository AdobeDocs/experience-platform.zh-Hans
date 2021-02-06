---
keywords: Experience Platform；主页；热门主题；删除沙箱
solution: Experience Platform
title: 删除API中的沙箱
topic: developer guide
description: 可以通过发出DELETE请求来删除沙箱，该请求在请求路径中包含沙箱的名称。
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 3%

---


# 删除API中的沙箱

可以通过发出DELETE请求删除沙箱，该请求在请求路径中包含沙箱的`name`。

>[!NOTE]
>
>发出此API调用会将沙箱的`status`属性更新为“deleted”并将其停用。 GET请求在删除沙箱后仍可以检索其详细信息。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要删除的沙箱的`name`。 |

**请求**

以下请求将删除名为“dev-2”的沙箱。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回沙箱的更新详细信息，显示其`state`为“deleted”。

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
