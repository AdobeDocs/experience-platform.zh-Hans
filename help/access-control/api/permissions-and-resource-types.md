---
keywords: Experience Platform；主页；热门主题；访问控制权限；访问控制资源类型；访问控制api
solution: Experience Platform
title: 引用API端点
description: 访问控制API中的引用端点允许您查看可用权限和资源类型的名称，然后可以使用它们查看当前用户的有效访问控制策略。
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# 引用端点

>[!NOTE]
>
>如果传递的是用户令牌，则该令牌的用户必须具有所请求组织的“组织管理员”角色。

您可以通过对以下项发出GET请求，列出所有权限和资源类型的名称： `/acl/reference` 端点。 然后，这些名称可用于对发起的API调用 [查看有效的访问控制策略](./effective-policies.md) 当前用户。

权限是通过Adobe Admin Console管理的策略，可映射到零个或多个资源类型策略。 资源类型是一种策略，它针对特定类型的资源启用读取、写入和/或删除功能 [!DNL Platform] 资源（如数据集或架构）。

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

成功响应将返回 `permissions` 对象和 `resource-types` 对象，每个对象分别包含访问权限或资源类型的完整名称列表。

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
