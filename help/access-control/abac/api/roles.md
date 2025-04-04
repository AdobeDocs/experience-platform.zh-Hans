---
keywords: Experience Platform；主页；热门主题；API；基于属性的访问控制；基于属性的访问控制
solution: Experience Platform
title: 角色API端点
description: 基于属性的访问控制API中的/roles端点允许您以编程方式管理Adobe Experience Platform中的角色。
role: Developer
exl-id: 049f7a18-7d06-437b-8ce9-25d7090ba782
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 6%

---

# 角色端点

>[!NOTE]
>
>如果传递的是用户令牌，则该令牌的用户必须具有所请求组织的“组织管理员”角色。

角色定义了管理员、专家或最终用户对组织中的资源的访问权限。在基于角色的访问控制环境中，用户访问设置是通过共同的责任和需求进行分组的。 一个角色具有一组给定的权限，可将您组织的成员分配给一个或多个角色，具体取决于他们需要的查看或写入访问权限的范围。

基于属性的访问控制API中的`/roles`端点允许您以编程方式管理组织中的角色。

## 快速入门

本指南中使用的API端点属于基于属性的访问控制API。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience Platform API所需的所需标头的重要信息。

## 检索角色列表 {#list}

您可以通过向`/roles`端点发出GET请求来列出属于您组织的所有现有角色。

**API格式**

```http
GET /roles/
```

**请求**

以下请求检索属于您组织的角色列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应将返回组织中的角色列表，包括有关其各自角色类型、权限集和主题属性的信息。

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
| `id` | 与角色相对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | description属性提供有关您的角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型可能的值为： `user-defined`和`system-defined`。 |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织中为特定角色配置的沙箱。 |
| `subjectAttributes` | 表示主题与其有权访问的Experience Platform资源之间关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用标签。 |

## 查找角色 {#lookup}

您可以通过在请求路径中包含相应`roleId`的GET请求来查找单个角色。

**API格式**

```http
GET /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 要查找的角色的ID。 |

**请求**

以下请求检索`{ROLE_ID}`的信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应将返回查询的角色ID的详细信息，包括其角色类型、权限集和主题属性的信息。

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
| `id` | 与角色相对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | description属性提供有关您的角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型可能的值为： `user-defined`和`system-defined`。 |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织中为特定角色配置的沙箱。 |
| `subjectAttributes` | 表示主题与其有权访问的Experience Platform资源之间关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用标签。 |

## 按角色ID查找主题

您还可以在提供{ROLE_ID}的同时通过向`/roles`端点发出GET请求来检索主题。

**API格式**

```http
GET /roles/{ROLE_ID}/subjects
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 与要查找的主题关联的角色的ID。 |

**请求**

以下请求检索与`3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`关联的主题。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809/subjects \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功响应将返回与查询的角色ID关联的主题，包括相应的主题ID和主题类型。

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
| `subjectType` | 查询对象的类型。 |
| `subjectId` | 与查询的主题相对应的ID。 |

## 创建角色 {#create}

要创建新角色，请在提供角色名称、描述和角色类型的值的同时，向`/roles`端点发出POST请求。

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
| `name` | 您的角色的名称。 确保您的角色名称是描述性的，因为您可以使用此名称查找有关您的角色的信息。 |
| `description` | （可选）可包含的描述性值，用于提供有关角色的更多信息。 |
| `roleType` | 角色的指定类型。 角色类型可能的值为： `user-defined`和`system-defined`。 |

**响应**

成功的响应将返回您新创建的角色，以及相应的角色ID，以及有关角色类型、权限集和主题属性的信息。

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
| `id` | 与角色相对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | description属性提供有关您的角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型可能的值为： `user-defined`和`system-defined`。 |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织中为特定角色配置的沙箱。 |
| `subjectAttributes` | 表示主题与其有权访问的Experience Platform资源之间关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用标签。 |

## 更新角色 {#patch}

您可以通过对`/roles`端点发出PATCH请求来更新角色的属性，同时为要应用的操作提供相应的角色ID和值。

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
| `op` | 用于定义更新角色所需的操作的操作调用。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 要更新的参数的路径。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回更新的角色，包括您选择更新的属性的新值。

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
| `id` | 与角色相对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | description属性提供有关您的角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型可能的值为： `user-defined`和`system-defined`。 |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织中为特定角色配置的沙箱。 |
| `subjectAttributes` | 表示主题与其有权访问的Experience Platform资源之间关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用标签。 |

## 按角色ID更新角色 {#put}

您可以通过向`/roles`端点发出PUT请求并指定与要更新的角色对应的角色ID来更新角色。

**API格式**

```http
PUT /roles/{ROLE_ID}
```

**请求**

以下请求更新角色ID的名称、描述和角色类型： `3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809`。

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
| `roleType` | 角色的指定类型。 角色类型可能的值为： `user-defined`和`system-defined`。 |

**响应**

成功的响应将返回您更新的角色，包括其名称、描述和角色类型的新值。

```json
{
  "id": "3dfa045d-de58-4dfd-8ea9-e4e2c1b6d809",
  "name": "Administrator role for ACME",
  "description": "New administrator role for ACME",
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
| `id` | 与角色相对应的ID。 此ID是自动生成的。 |
| `name` | 您的角色的名称。 |
| `description` | description属性提供有关您的角色的其他信息。 |
| `roleType` | 角色的指定类型。 角色类型可能的值为： `user-defined`和`system-defined`。 |
| `permissionSets` | 权限集表示管理员可以应用于角色的一组权限。 管理员可以为角色分配权限集，而不是分配单个权限。 这允许您从包含一组权限的预定义角色创建自定义角色。 |
| `sandboxes` | 此属性显示组织中为特定角色配置的沙箱。 |
| `subjectAttributes` | 表示主题与其有权访问的Experience Platform资源之间关联的属性。 |
| `subjectAttributes.labels` | 显示应用于查询角色的数据使用标签。 |

## 按角色ID更新主题

要更新与角色关联的主体，请在提供要更新的主体的角色ID的同时，向`/roles`端点发出PATCH请求。

**API格式**

```http
PATCH /roles/{ROLE_ID}/subjects
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 与要更新的主体关联的角色ID。 |

**请求**

以下请求更新与`{ROLE_ID}`关联的主题。

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/user",
        "value": "{USER ID}"
    }
]' 
```

| 操作 | 描述 |
| --- | --- |
| `op` | 用于定义更新角色所需的操作的操作调用。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 要更新的参数的路径。 |
| `value` | 要用于更新参数的新值。 |

**响应**

成功的响应将返回您更新的角色，包括主题的新值。

```json
{
  "subjects": [
    [
      {
        "subjectId": "03Z07HFQCCUF3TUHAX274206@AdobeID",
        "subjectType": "user"
      }
    ]
  ],
  "_page": {
    "limit": 1,
    "count": 1
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects",
      "templated": true
    },
    "page": {
      "href": "https://platform.adobe.io:443/data/foundation/access-control/administration/roles/{ROLE_ID}/subjects?limit={limit}&start={start}&orderBy={orderBy}&property={property}",
      "templated": true
    }
  }
}
```

## 删除角色 {#delete}

要删除角色，请在指定要删除的DELETE的ID时向`/roles`端点发出角色请求。

**API格式**

```http
DELETE /roles/{ROLE_ID}
```

| 参数 | 描述 |
| --- | --- |
| {ROLE_ID} | 要删除的角色的ID。 |

**请求**

以下请求删除ID为`{ROLE_ID}`的角色。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/roles/{ROLE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。

您可以通过尝试向角色发送查找(GET)请求来确认删除。 您将收到HTTP状态404 （未找到），因为角色已从管理中删除。

## 添加API凭据 {#apicredential}

要添加API凭据，请在提供主体的角色ID的同时向`/roles`端点发出PATCH请求。

**API格式**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/access-control/administration/roles/<ROLE_ID>/subjects' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '[
    {
        "op": "add",
        "path": "/api-integration",
        "value": "{TECHNICAL ACCOUNT ID}"
    }
]'   
```

| 操作 | 描述 |
| --- | --- |
| `op` | 用于定义更新角色所需的操作的操作调用。 操作包括： `add`、`replace`和`remove`。 |
| `path` | 要添加参数的路径。 |
| `value` | 要添加参数的值。 |

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。
