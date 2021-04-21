---
keywords: Experience Platform；主页；热门主题；访问控制权限；访问控制资源类型；访问控制api
solution: Experience Platform
title: 引用API端点
topic-legacy: developer guide
description: Adobe Experience Platform中的访问控制允许您使用Adobe Admin Console管理各种平台功能的角色和权限。 您可以通过向访问控制 API中的/acl/reference端点发出GET请求，列表所有权限和资源类型的名称。 然后，这些名称可用于API调用，以视图当前用户的有效策略。
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---

# 引用端点

您可以通过向`/acl/reference`端点发出GET请求来列表所有权限和资源类型的名称。 然后，这些名称可用于对当前用户的[视图有效策略](./effective-policies.md)的API调用。

权限是通过Adobe Admin Console管理的策略，映射到零个或多个资源类型策略。 资源类型是一种策略，它为特定类型的[!DNL Platform]资源(如数据集或模式)启用读、写和/或删除功能。

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

成功的响应返回`permissions`对象和`resource-types`对象，每个对象分别包含访问权限或资源类型名称的完整列表。

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
