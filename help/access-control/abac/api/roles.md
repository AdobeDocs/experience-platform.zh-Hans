---
keywords: Experience Platform；主页；热门主题；API；基于属性的访问控制；基于属性的访问控制
solution: Experience Platform
title: 角色API端点
description: 基于属性的访问控制API中的/roles端点允许您以编程方式管理Adobe Experience Platform中的角色。
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: 16d85a2a4ee8967fc701a3fe631c9daaba9c9d70
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 3%

---

# 角色端点

>[!NOTE]
>
>如果传递了用户令牌，则令牌的用户必须对请求的组织具有“组织管理员”角色。

角色定义管理员、专家或最终用户对您组织中的资源的访问权限。 在基于角色的访问控制环境中，用户访问设置是通过共同的责任和需求进行分组的。 角色具有一组给定的权限，并且可以根据角色需要的查看或写入权限，将组织的成员分配给一个或多个角色。

的 `/roles` 基于属性的访问控制API中的端点允许您以编程方式管理组织中的角色。

## 快速入门

本指南中使用的API端点是基于属性的访问控制API的一部分。 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索角色列表 {#list}

您可以通过向 `/roles` 端点。

**API格式**

```http
GET /roles/
```

**请求**

以下请求可检索属于贵组织的角色列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应会返回组织中的角色列表，包括有关其各自的角色类型、权限集和主体属性的信息。

```json
{
  "roles": [
    {
      "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "name": "Administrator Role",
      "description": "Role for administrator type of responsibilities and access",
      "roleType": "user-defined",
      "permissionSets": [
        "manage-datasets",
        "manage-schemas"
      ],
      "sandboxes": [
        "prod"
      ],
      "subjectAttributes": {
        "labels": [
          "core/S1"
        ]
      },
      "createdBy": "{CREATED_BY}",
      "createdAt": 1648153201825,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1648153201825,
      "etag": null
    }
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "next": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    },
    "subjects": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
      "templated": true
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与角色对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | 描述属性提供有关您角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织内为特定角色配置的沙箱。 |
| `subjectAttributes` | 指示主题与他们有权访问的平台资源之间的关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用情况标签。 |

## 查找角色 {#lookup}

您可以通过发出包含相应GET的 `roleId` 在请求路径中。

**API格式**

```http
GET /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 要查找的角色的ID。 |

**请求**

以下请求检索 `{ROLE_ID}`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应会返回查询的角色ID的详细信息，包括有关其角色类型、权限集和主体属性的信息。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与角色对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | 描述属性提供有关您角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织内为特定角色配置的沙箱。 |
| `subjectAttributes` | 指示主题与他们有权访问的平台资源之间的关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用情况标签。 |

## 按角色ID查找主体

您还可以通过向 `/roles` 提供{ROLE_ID}时的端点。

**API格式**

```http
GET /roles/{ROLE_ID}/subjects
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 与要查找的主体关联的角色的ID。 |

**请求**

以下请求检索与 `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应返回与查询的角色ID关联的主题，包括相应的主题ID和主题类型。

```json
{
  "items": [
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "PIRJ7WE5T3QT9Z4TCLVH86DE@AdobeID"
      },
      {
          "roleId": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
          "subjectType": "user",
          "subjectId": "WHPWE00MC26SHZ7AKBFG403D@AdobeID"
      },
  ]
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
      "self": {
          "href": "/roles/{ROLE_ID}/subjects",
          "templated": false,
          "type": null,
          "method": null
      },
      "page": {
          "href": "/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
          "templated": true,
          "type": null,
          "method": null
      }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `roleId` | 与查询的主题关联的角色ID。 |
| `subjectType` | 查询的主题的类型。 |
| `subjectId` | 与查询的主题对应的ID。 |

## 创建角色 {#create}

要创建新角色，请向 `/roles` 端点，同时为角色的名称、描述和角色类型提供值。

**API格式**

```http
POST /roles/
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator Role",
    "description": "Role for administrator type of responsibilities and access",
    "roleType": "user-defined"
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 您的角色的名称。 确保角色的名称具有描述性，因为您可以使用该名称查找有关您角色的信息。 |
| `description` | （可选）可包含的描述性值，用于提供有关您角色的更多信息。 |
| `roleType` | 角色的指定类型。 角色类型的可能值包括： `user-defined` 和 `system-defined`. |

**响应**

成功的响应会返回您新创建的角色（具有相应的角色ID）以及有关其角色类型、权限集和主体属性的信息。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role for administrator type of responsibilities and access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与角色对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | 描述属性提供有关您角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织内为特定角色配置的沙箱。 |
| `subjectAttributes` | 指示主题与他们有权访问的平台资源之间的关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用情况标签。 |

## 更新角色 {#patch}

您可以通过向 `/roles` 端点，同时为要应用的操作提供相应的角色ID和值。

**API格式**

```http
PATCH /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 要更新的角色的ID。 |

**请求**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/description",
        "value": "Role with permission sets for admin type of access"
      }
    ]
  }'
```

| 操作 | 描述 |
| --- | --- |
| `op` | 操作调用，用于定义更新角色所需的操作。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 要更新的参数的路径。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回更新的角色，包括您选择更新的属性的新值。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与角色对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | 描述属性提供有关您角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织内为特定角色配置的沙箱。 |
| `subjectAttributes` | 指示主题与他们有权访问的平台资源之间的关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用情况标签。 |

## 按角色ID更新角色 {#put}

您可以通过向 `/roles` 端点，并指定与要更新的角色对应的角色ID。

**API格式**

```http
PUT /roles/{ROLE_ID}
```

**请求**

以下请求更新角色ID的名称、描述和角色类型： `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "name": "Administrator role for ACME",
    "description": "New administrator role for ACME",
    "roleType": "user-defined"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 角色的更新名称。 |
| `description` | 角色的更新描述。 |
| `roleType` | 角色的指定类型。 角色类型的可能值包括： `user-defined` 和 `system-defined`. |

**响应**

成功后，将返回您更新的角色，包括其名称、描述和角色类型的新值。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator Role",
  "description": "Role with permission sets for admin type of access",
  "roleType": "user-defined",
  "permissionSets": [
    "manage-datasets",
    "manage-schemas"
  ],
  "sandboxes": [
    "prod"
  ],
  "subjectAttributes": {
    "labels": [
      "core/S1"
    ]
  },
  "createdBy": "{CREATED_BY}",
  "createdAt": 1648153201825,
  "modifiedBy": "{MODIFIED_BY}",
  "modifiedAt": 1648153201825,
  "etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与角色对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | 描述属性提供有关您角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型的可能值包括： `user-defined` 和 `system-defined`. |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织内为特定角色配置的沙箱。 |
| `subjectAttributes` | 指示主题与他们有权访问的平台资源之间的关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用情况标签。 |

## 按角色ID更新主体

要更新与角色关联的主体，请向 `/roles` 端点，同时提供要更新的主体的角色ID。

**API格式**

```http
PATCH /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 与您要更新的主体关联的角色ID。 |

**请求**

以下请求更新了与 `{ROLE_ID}`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "add",
        "path": "/subjects",
        "value": "New subjects"
      }
    ]
  }'
```

| 操作 | 描述 |
| --- | --- |
| `op` | 操作调用，用于定义更新角色所需的操作。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 要更新的参数的路径。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回与查询的角色ID关联的更新主体。

```json
{
  "subjects": [
    {
      "subjectId": "string",
      "subjectType": "user"
    }
  ],
  "_page": {
    "limit": 0,
    "count": 0
  },
  "_links": {
    "next": {
      "href": "string",
      "templated": true
    },
    "page": {
      "href": "string",
      "templated": true
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `subjectId` | 主题的ID。 |
| `subjectType` | 主题的类型。 |

## 删除角色 {#delete}

要删除角色，请向 `/roles` 端点。

**API格式**

```http
DELETE /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 要删除的角色的ID。 |

**请求**

以下请求会删除ID为的角色 `{ROLE_ID}`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功响应会返回HTTP状态204（无内容）和空白正文。

您可以通过尝试对角色进行查找(GET)请求来确认删除。 您将收到HTTP状态404（未找到），因为该角色已从管理中删除。
