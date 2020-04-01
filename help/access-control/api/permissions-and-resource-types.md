---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列表权限和资源类型的名称
topic: developer guide
translation-type: tm+mt
source-git-commit: 7b354a96d70332cf7a7e9eff322cd3d6ee0fc96a

---


# 列表权限和资源类型的名称

您可以通过向端点发出GET请求来列表所有权限和资源类型的 `/acl/reference` 名称。 然后，这些名称可用于API调用中，以 [视图当前用户的有](./effective-policies.md) 效策略。

权 **限是通过** Adobe Admin Console管理的策略，并映射到零个或多个资源类型策略。 资 **源类型** ，是一种为特定类型的平台资源(如数据集或模式)启用读、写和／或删除功能的策略。

**API格式**

```http
GET /acl/reference
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**响应**

成功的响应会返回一 `permissions` 个对象和一个对 `resource-types` 象，每个对象分别包含访问权限或资源类型名称的完整列表。

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
