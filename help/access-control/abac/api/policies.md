---
keywords: Experience Platform；主页；热门主题；API；基于属性的访问控制；基于属性的访问控制
solution: Experience Platform
title: 访问控制策略API端点
description: 基于属性的访问控制API中的/policies端点允许您以编程方式管理Adobe Experience Platform中的策略。
role: Developer
exl-id: 07690f43-fdd9-4254-9324-84e6bd226743
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 2%

---

# 访问控制策略端点

>[!NOTE]
>
>如果传递的是用户令牌，则该令牌的用户必须具有所请求组织的“组织管理员”角色。

访问控制策略是将属性集合在一起以建立允许和不允许的操作的语句。 这些策略可以是本地策略或全局策略，也可以覆盖其他策略。 基于属性的访问控制API中的`/policies`端点允许您以编程方式管理策略，包括有关控制策略的规则及其相应主题条件的信息。

>[!IMPORTANT]
>
>不应将此端点与用于管理数据使用策略的[策略服务API](../../../data-governance/api/policies.md)中的`/policies`端点混淆。

## 快速入门

本指南中使用的API端点属于基于属性的访问控制API。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 检索策略列表 {#list}

向`/policies`端点发出GET请求，以列出组织中的所有现有策略。

**API格式**

```http
GET /policies
```

**请求**

以下请求检索现有策略的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应将返回现有策略的列表。

```json
{
  {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652892767559,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/xql/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.read",
                  "com.adobe.action.write",
                  "com.adobe.action.view"
              ]
          },
          {
              "effect": "Permit",
              "resource": "/orgs/{IMS_ORG}/sandboxes/*/schemas/*/schema-fields/*",
              "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
              "actions": [
                  "com.adobe.action.delete"
              ]
          },
          {
              "effect": "Deny",
              "resource": "/orgs/{IMS_ORG}/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
              "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
              "actions": [
                  "com.adobe.action.write"
              ]
          }
      ],
      "_etag": "\"0300593f-0000-0200-0000-62852ff80000\""
  },
  {
      "id": "13138ef6-c007-495d-837f-0a248867e219",
      "imsOrgId": "{IMS_ORG}",
      "createdBy": "{CREATED_BY}",
      "createdAt": 1652859368555,
      "modifiedBy": "{MODIFIED_BY}",
      "modifiedAt": 1652890780206,
      "name": "Documentation-Copy",
      "description": "xyz",
      "status": "active",
      "subjectCondition": null,
      "rules": [
          {
              "effect": "Permit",
              "resource": "orgs/{IMS_ORG}/sandboxes/ro-sand/schemas/*/schema-fields/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"and\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          },
          {
              "effect": "Deny",
              "resource": "orgs/{IMS_ORG}/sandboxes/*/segments/*",
              "condition": "{\"!\":[{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}]}",
              "actions": [
                  "com.adobe.action.read"
              ]
          }
      ],
      "_etag": "\"0300d43c-0000-0200-0000-62851c9c0000\""
  },
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与策略相对应的ID。 此标识符是自动生成的，可用于查找、更新和删除策略。 |
| `imsOrgId` | 查询的策略可访问的组织。 |
| `createdBy` | 创建策略的用户的ID。 |
| `createdAt` | 创建策略的时间。 `createdAt`属性以unix epoch时间戳显示。 |
| `modifiedBy` | 上次更新策略的用户的ID。 |
| `modifiedAt` | 上次更新策略的时间。 `modifiedAt`属性以unix epoch时间戳显示。 |
| `name` | 策略的名称。 |
| `description` | （可选）可以添加以提供有关特定策略的进一步信息的属性。 |
| `status` | 策略的当前状态。 此属性定义策略当前是`active`还是`inactive`。 |
| `subjectCondition` | 应用于主体的条件。 主体是具有特定属性的用户，请求访问资源以执行操作。 在这种情况下，`subjectCondition`是应用于主题属性的类似查询的条件。 |
| `rules` | 定义策略的一组规则。 规则定义了哪些属性组合已获授权，以便主体能够成功对资源执行操作。 |
| `rules.effect` | 考虑`action`、`condition`和`resource`的值后产生的效果。 可能的值包括： `permit`、`deny`或`indeterminate`。 |
| `rules.resource` | 主体可以或无法访问的资源或对象。  资源可以是文件、应用程序、服务器甚至API。 |
| `rules.condition` | 应用于资源的条件。 例如，如果资源是架构，则架构可以应用某些标签，这有助于确定针对该架构的操作是允许还是不允许的。 |
| `rules.action` | 允许主体对查询的资源执行的操作。 可能的值包括： `read`、`create`、`edit`和`delete`。 |

## 按ID查找策略详细信息 {#lookup}

在请求路径中提供策略ID以检索有关单个GET的信息时，向`/policies`端点发出策略请求。

**API格式**

```http
GET /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 要检索的策略的ID。 |

**请求**

以下请求检索有关单个策略的信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的请求会返回有关所查询的策略ID的信息。

```json
{
  "policies": [
    {
      "id": "7019068e-a3a0-48ce-b56b-008109470592",
      "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
      "createdBy": "example@AdobeID",
      "createdAt": 1652892767559,
      "modifiedBy": "example@AdobeID",
      "modifiedAt": 1652895736367,
      "name": "schema-field",
      "description": "schema-field",
      "status": "inactive",
      "subjectCondition": null,
      "rules": [
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/xql/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.read",
            "com.adobe.action.write",
            "com.adobe.action.view"
          ]
        },
        {
          "effect": "Permit",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/*/schemas/*/schema-fields/*",
          "condition": "{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}",
          "actions": [
            "com.adobe.action.delete"
          ]
        },
        {
          "effect": "Deny",
          "resource": "/orgs/5555467B5D8013E50A494220@AdobeOrg/sandboxes/delete-sandbox-adfengine-test-8/segments/*",
          "condition": "{\"!\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"custom/\",{\"var\":\"resource.labels\"}]}]}",
          "actions": [
            "com.adobe.action.write"
          ]
        }
      ],
      "etag": "\"0300593f-0000-0200-0000-62852ff80000\""
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与策略相对应的ID。 此标识符是自动生成的，可用于查找、更新和删除策略。 |
| `imsOrgId` | 查询的策略可访问的组织。 |
| `createdBy` | 创建策略的用户的ID。 |
| `createdAt` | 创建策略的时间。 `createdAt`属性以unix epoch时间戳显示。 |
| `modifiedBy` | 上次更新策略的用户的ID。 |
| `modifiedAt` | 上次更新策略的时间。 `modifiedAt`属性以unix epoch时间戳显示。 |
| `name` | 策略的名称。 |
| `description` | （可选）可以添加以提供有关特定策略的进一步信息的属性。 |
| `status` | 策略的当前状态。 此属性定义策略当前是`active`还是`inactive`。 |
| `subjectCondition` | 应用于主体的条件。 主体是具有特定属性的用户，请求访问资源以执行操作。 在这种情况下，`subjectCondition`是应用于主题属性的类似查询的条件。 |
| `rules` | 定义策略的一组规则。 规则定义了哪些属性组合已获授权，以便主体能够成功对资源执行操作。 |
| `rules.effect` | 考虑`action`、`condition`和`resource`的值后产生的效果。 可能的值包括： `permit`、`deny`或`indeterminate`。 |
| `rules.resource` | 主体可以或无法访问的资源或对象。  资源可以是文件、应用程序、服务器甚至API。 |
| `rules.condition` | 应用于资源的条件。 例如，如果资源是架构，则架构可以应用某些标签，这有助于确定针对该架构的操作是允许还是不允许的。 |
| `rules.action` | 允许主体对查询的资源执行的操作。 可能的值包括： `read`、`create`、`edit`和`delete`。 |


## 创建策略 {#create}

要创建新策略，请向`/policies`端点发出POST请求。

**API格式**

```http
POST /policies
```

**请求**

以下请求创建一个名为的新策略： `acme-integration-policy`。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "name": "acme-integration-policy",
      "description": "Policy for ACME",
      "imsOrgId": "{IMS_ORG}",
      "rules": [
        {
          "effect": "Permit",
          "resource": "/orgs/{IMS_ORG}/sandboxes/*",
          "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
          "actions": [
            "com.adobe.action.read"
          ]
        }
      ]
    }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 策略的名称。 |
| `description` | （可选）可以添加以提供有关特定策略的进一步信息的属性。 |
| `imsOrgId` | 包含策略的组织。 |
| `rules` | 定义策略的一组规则。 规则定义了哪些属性组合已获授权，以便主体能够成功对资源执行操作。 |
| `rules.effect` | 考虑`action`、`condition`和`resource`的值后产生的效果。 可能的值包括： `permit`、`deny`或`indeterminate`。 |
| `rules.resource` | 主体可以或无法访问的资源或对象。  资源可以是文件、应用程序、服务器甚至API。 |
| `rules.condition` | 应用于资源的条件。 例如，如果资源是架构，则架构可以应用某些标签，这有助于确定针对该架构的操作是允许还是不允许的。 |
| `rules.action` | 允许主体对查询的资源执行的操作。 可能的值包括： `read`、`create`、`edit`和`delete`。 |

**响应**

成功的请求会返回新创建的策略，包括其唯一策略ID和相关规则。

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988384458,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Policy for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与策略相对应的ID。 此标识符是自动生成的，可用于查找、更新和删除策略。 |
| `name` | 策略的名称。 |
| `rules` | 定义策略的一组规则。 规则定义了哪些属性组合已获授权，以便主体能够成功对资源执行操作。 |
| `rules.effect` | 考虑`action`、`condition`和`resource`的值后产生的效果。 可能的值包括： `permit`、`deny`或`indeterminate`。 |
| `rules.resource` | 主体可以或无法访问的资源或对象。  资源可以是文件、应用程序、服务器甚至API。 |
| `rules.condition` | 应用于资源的条件。 例如，如果资源是架构，则架构可以应用某些标签，这有助于确定针对该架构的操作是允许还是不允许的。 |
| `rules.action` | 允许主体对查询的资源执行的操作。 可能的值包括： `read`、`create`、`edit`和`delete`。 |


## 按策略ID更新策略 {#put}

要更新单个策略的规则，请在请求PUT中提供要更新的策略的ID时，向`/policies`端点发出请求请求。

**API格式**

```http
PUT /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 要更新的策略的ID。 |

**请求**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/8cf487d7-3642-4243-a8ea-213d72f694b9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
      "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
      "imsOrgId": "{IMS_ORG}",
      "name": "test-2",
      "rules": [
      {
        "effect": "Deny",
        "resource": "/orgs/{IMS_ORG}/sandboxes/*",
        "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
        "actions": [
          "com.adobe.action.read"
        ]
      }
    ]
  }'
```

**响应**

成功的响应将返回更新的策略。

```json
{
    "id": "8cf487d7-3642-4243-a8ea-213d72f694b9",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "{CREATED_BY}",
    "createdAt": 1652988866647,
    "modifiedBy": "{MODIFIED_BY}",
    "modifiedAt": 1652989297287,
    "name": "test-2",
    "description": null,
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Deny",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## 更新策略属性 {#patch}

要更新单个策略的属性，请在请求PATCH中提供要更新的策略的ID时，向`/policies`端点发出请求请求。

**API格式**

```http
PATCH /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 要更新的策略的ID。 |

**请求**

以下请求替换策略ID `c3863937-5d40-448d-a7be-416e538f955e`中的`/description`值。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -d'{
    "operations": [
      {
        "op": "replace",
        "path": "/description",
        "value": "Pre-set policy to be applied for ACME"
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

成功的响应会返回查询的策略ID，并包含更新的描述。

```json
{
    "id": "c3863937-5d40-448d-a7be-416e538f955e",
    "imsOrgId": "{IMS_ORG}",
    "createdBy": "acp_accessControlService",
    "createdAt": 1652988384458,
    "modifiedBy": "acp_accessControlService",
    "modifiedAt": 1652988384458,
    "name": "acme-integration-policy",
    "description": "Pre-set policy to be applied for ACME",
    "status": "active",
    "subjectCondition": null,
    "rules": [
        {
            "effect": "Permit",
            "resource": "/orgs/{IMS_ORG}/sandboxes/*",
            "condition": "{\"or\":[{\"adobe.match_any_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]},{\"!\":[{\"adobe.match_all_labels_by_prefix\":[{\"var\":\"subject.roles.labels\"},\"core/\",{\"var\":\"resource.labels\"}]}]}]}",
            "actions": [
                "com.adobe.action.read"
            ]
        }
    ],
    "_etag": null
}
```

## 删除策略 {#delete}

要删除策略，请在提供要删除的策略的ID时向`/policies`端点发出DELETE请求。

**API格式**

```http
DELETE /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 要删除的策略的ID。 |

**请求**

以下请求删除ID为`c3863937-5d40-448d-a7be-416e538f955e`的策略。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。

您可以通过尝试对策略进行查找(GET)请求来确认删除。 您将收到HTTP状态404 （未找到），因为策略已从管理中删除。
