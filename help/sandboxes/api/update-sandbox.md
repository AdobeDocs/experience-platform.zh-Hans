---
keywords: Experience Platform;home;popular topics;update sandbox
solution: Experience Platform
title: 更新沙箱
topic: developer guide
description: 您可以通过发出PATCH请求来更新沙箱中的一个或多个字段，该请求在请求路径中包含沙箱的名称，并在请求有效负荷中包含要更新的属性。
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---


# 更新沙箱

您可以通过发出PATCH请求来更新沙箱中的一个或多个字段，该请求在请求路径中包含沙 `name` 箱的请求，并在请求有效负荷中包含要更新的属性。

>[!NOTE]
>
>当前只能更新沙 `title` 箱的属性。

**API格式**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要 `name` 更新的沙箱的属性。 |

**请求**

以下请求更新 `title` 名为“dev-2”的沙箱的属性。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "title": "Development B"
  }'
```

**响应**

成功的响应会返回HTTP状态200(OK)，其中包含最新更新的沙箱的详细信息。

```json
{
    "name": "dev-2",
    "title": "Development B",
    "state": "active",
    "type": "development",
    "region": "VA7"
}
```
