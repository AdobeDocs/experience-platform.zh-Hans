---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 重置沙箱
topic: developer guide
translation-type: tm+mt
source-git-commit: 974e93b1c24493734848151b9be00758f6a84578

---


# 重置沙箱

开发沙箱具有“工厂重置”功能，该功能会从沙箱中删除所有非默认资源。 可以通过发出PUT请求来重置沙箱，该请求在请 `name` 求路径中包含沙箱。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{SANDBOX_NAME}` | 要 `name` 重置的沙箱的属性。 |

**请求**

以下请求将重置名为“dev-2”的沙箱。

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
| `action` | 为了重置沙箱，必须在请求有效负荷中提供此参数，其值为“reset”。 |

**响应**

成功的响应会返回更新沙箱的详细信息，表明其 `state` 正在“重置”。

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

>[!NOTE] 重置沙箱后，系统需要大约15分钟才能进行设置。 设置沙箱后，沙箱的 `state` 变为“活动”或“失败”。