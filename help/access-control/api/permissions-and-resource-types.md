---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列表权限和资源类型的名称
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 1%

---


# 列表权限和资源类型的名称

您可以通过向端点发出列表请求来GET所有权限和资源类型的 `/acl/reference` 名称。 然后，这些名称可用于API调用，以 [视图当前用户](./effective-policies.md) 的有效策略。

权 **限** 是通过Adobe Admin Console管理的策略，映射到零个或多个资源类型的策略。 资 **源类型** 是一种策略，它为特定类型的资源(如数据集或模式)启用读 [!DNL Platform] 取、写入和／或删除功能。

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

成功的响应返回 `permissions` 对象和对 `resource-types` 象，每个对象分别包含访问权限或资源类型名称的完整列表。

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
