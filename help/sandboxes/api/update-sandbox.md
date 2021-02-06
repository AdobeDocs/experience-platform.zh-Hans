---
keywords: Experience Platform；主页；热门主题；更新沙箱
solution: Experience Platform
title: 在API中更新沙箱
topic: developer guide
description: 您可以通过发出PATCH请求来更新沙箱中的一个或多个字段，该请求在请求路径中包含沙箱的名称，并在请求有效负荷中包含要更新的属性。
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---


# 更新API中的沙箱

您可以通过发出PATCH请求来更新沙箱中的一个或多个字段，该请求在请求路径中包含沙箱的`name`，并在请求负载中包含要更新的属性。

>[!NOTE]
>
>当前只能更新沙箱的`title`属性。

**API格式**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要更新的沙箱的`name`属性。 |

**请求**

以下请求更新名为“dev-2”的沙箱的`title`属性。

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
