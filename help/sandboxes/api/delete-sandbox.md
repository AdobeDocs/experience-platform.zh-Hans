---
keywords: Experience Platform;home;popular topics;delete sandbox
solution: Experience Platform
title: 删除沙箱
topic: developer guide
description: 可以通过发出DELETE请求来删除沙箱，该请求在请求路径中包含沙箱的名称。
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 3%

---


# 删除沙箱

可以通过发出DELETE请求来删除沙箱，该请求将沙箱 `name` 包含在请求路径中。

>[!NOTE]
>
>发出此API调用会将沙箱的属 `status` 性更新为“已删除”并将其停用。 GET请求在删除沙箱后仍可以检索其详细信息。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要 `name` 删除的沙箱的位置。 |

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

成功的响应返回沙箱的更新详细信息，显示其 `state` 已“删除”。

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
