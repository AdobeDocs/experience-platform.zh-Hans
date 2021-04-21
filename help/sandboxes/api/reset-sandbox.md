---
keywords: Experience Platform；主页；热门主题；重置沙箱
solution: Experience Platform
title: 在API中重置沙箱
topic-legacy: developer guide
description: 开发沙箱具有“工厂重置”功能，可从沙箱中删除所有非默认资源。 可以通过发出在请求路径中包含沙箱名称的PUT请求来重置沙箱。
exl-id: 3a82735d-a043-4fe4-9042-1eb373748d35
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 3%

---

# 在API中重置沙箱

开发沙箱具有“工厂重置”功能，可从沙箱中删除所有非默认资源。 可以通过发出PUT请求来重置沙箱，该请求在请求路径中包含沙箱的`name`。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要重置的沙箱的`name`属性。 |

**请求**

以下请求会重置名为“dev-2”的沙箱。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| 属性 | 描述 |
| --- | --- |
| `action` | 此参数必须在请求负载中提供值为“reset”的值，才能重置沙箱。 |

**响应**

成功的响应返回更新沙箱的详细信息，显示其`state`是“resetting”。

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>重置沙箱后，系统将需要大约15分钟才能设置沙箱。 设置后，沙箱的`state`将变为“活动”或“失败”。
