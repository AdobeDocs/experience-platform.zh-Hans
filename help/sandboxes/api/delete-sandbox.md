---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 删除沙箱
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# 删除沙箱

可以通过发出DELETE请求来删除沙箱，该请求在请求路径 `name` 中包含沙箱。

>[!NOTE] 发出此API调用会将沙箱的属 `status` 性更新为“已删除”并将其停用。 GET请求在删除沙箱后仍可检索其详细信息。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要 `name` 删除的沙箱的沙箱。 |

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

成功的响应将返回沙箱的更新详细信息，显示其 `state` 已“删除”。

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
