---
keywords: Experience Platform；主页；热门主题；API；基于属性的访问控制；基于属性的访问控制
solution: Experience Platform
title: 策略API端点
description: 基于属性的访问控制API中的/policys端点允许您以编程方式管理Adobe Experience Platform中的策略。
hide: true
hidefromtoc: true
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 2%

---

# 策略端点

>[!IMPORTANT]
>
>目前，基于属性的访问控制在面向美国医疗保健客户的有限版本中提供。 此功能在完全发布后将可供所有Real-time Customer Data Platform客户使用。

政策是将属性集合在一起以确立允许和不允许的行动的声明。 策略可以是本地策略，也可以是全局策略，并且可以覆盖其他策略。 的 `/policies` 基于属性的访问控制API中的端点允许您以编程方式管理策略，包括有关控制策略的规则及其各自的主题条件的信息。

## 快速入门

本指南中使用的API端点是基于属性的访问控制API的一部分。 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索策略列表 {#list}

向发送GET请求 `/policies` 端点来列出您组织中的所有现有策略。

**API格式**

```http
GET /policies
```

**请求**

以下请求可检索现有策略的列表。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应会返回现有策略的列表。

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
| `id` | 与策略对应的ID。 此标识符是自动生成的，可用于查找、更新和删除策略。 |
| `imsOrgId` | 可访问查询策略的组织。 |
| `createdBy` | 创建策略的用户的ID。 |
| `createdAt` | 策略的创建时间。 的 `createdAt` 属性以unix纪元时间戳显示。 |
| `modifiedBy` | 上次更新策略的用户的ID。 |
| `modifiedAt` | 上次更新策略的时间。 的 `modifiedAt` 属性以unix纪元时间戳显示。 |
| `name` | 策略的名称。 |
| `description` | （可选）可添加以提供有关特定策略的更多信息的属性。 |
| `status` | 策略的当前状态。 此属性定义策略当前是否为 `active` 或 `inactive`. |
| `subjectCondition` | 适用于主题的条件。 主体是具有特定属性的用户，请求访问资源以执行操作。 在这种情况下， `subjectCondition` 是应用于主题属性的类似查询的条件。 |
| `rules` | 定义策略的规则集。 规则定义哪些属性组合被授权，以便主体成功对资源执行操作。 |
| `rules.effect` | 考虑 `action`, `condition` 和 `resource`. 可能的值包括： `permit`, `deny`或 `indeterminate`. |
| `rules.resource` | 主体可以或不能访问的资产或对象。  资源可以是文件、应用程序、服务器，甚至API。 |
| `rules.condition` | 应用于资源的条件。 例如，如果资源是模式，则模式可以应用某些标签，从而有助于针对该模式的操作是允许还是不允许。 |
| `rules.action` | 允许主体对查询的资源执行的操作。 可能的值包括： `read`, `create`, `edit`和 `delete`. |

## 按ID查找策略详细信息 {#lookup}

向发送GET请求 `/policies` 端点时，在请求路径中提供策略ID以检索有关该单个策略的信息。

**API格式**

```http
GET /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 要检索的策略的ID。 |

**请求**

以下请求可检索有关单个策略的信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/13138ef6-c007-495d-837f-0a248867e219 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的请求返回有关查询的策略ID的信息。

```json
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
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与策略对应的ID。 此标识符是自动生成的，可用于查找、更新和删除策略。 |
| `imsOrgId` | 可访问查询策略的组织。 |
| `createdBy` | 创建策略的用户的ID。 |
| `createdAt` | 策略的创建时间。 的 `createdAt` 属性以unix纪元时间戳显示。 |
| `modifiedBy` | 上次更新策略的用户的ID。 |
| `modifiedAt` | 上次更新策略的时间。 的 `modifiedAt` 属性以unix纪元时间戳显示。 |
| `name` | 策略的名称。 |
| `description` | （可选）可添加以提供有关特定策略的更多信息的属性。 |
| `status` | 策略的当前状态。 此属性定义策略当前是否为 `active` 或 `inactive`. |
| `subjectCondition` | 适用于主题的条件。 主体是具有特定属性的用户，请求访问资源以执行操作。 在这种情况下， `subjectCondition` 是应用于主题属性的类似查询的条件。 |
| `rules` | 定义策略的规则集。 规则定义哪些属性组合被授权，以便主体成功对资源执行操作。 |
| `rules.effect` | 考虑 `action`, `condition` 和 `resource`. 可能的值包括： `permit`, `deny`或 `indeterminate`. |
| `rules.resource` | 主体可以或不能访问的资产或对象。  资源可以是文件、应用程序、服务器，甚至API。 |
| `rules.condition` | 应用于资源的条件。 例如，如果资源是模式，则模式可以应用某些标签，从而有助于针对该模式的操作是允许还是不允许。 |
| `rules.action` | 允许主体对查询的资源执行的操作。 可能的值包括： `read`, `create`, `edit`和 `delete`. |


## 创建策略 {#create}

要创建新策略，请向 `/policies` 端点。

**API格式**

```http
POST /policies
```

**请求**

以下请求会创建一个名为的新策略： `acme-integration-policy`.

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
            "read"
          ]
        }
      ]
    }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 策略的名称。 |
| `description` | （可选）可添加以提供有关特定策略的更多信息的属性。 |
| `imsOrgId` | 包含策略的组织。 |
| `rules` | 定义策略的规则集。 规则定义哪些属性组合被授权，以便主体成功对资源执行操作。 |
| `rules.effect` | 考虑 `action`, `condition` 和 `resource`. 可能的值包括： `permit`, `deny`或 `indeterminate`. |
| `rules.resource` | 主体可以或不能访问的资产或对象。  资源可以是文件、应用程序、服务器，甚至API。 |
| `rules.condition` | 应用于资源的条件。 例如，如果资源是模式，则模式可以应用某些标签，从而有助于针对该模式的操作是允许还是不允许。 |
| `rules.action` | 允许主体对查询的资源执行的操作。 可能的值包括： `read`, `create`, `edit`和 `delete`. |

**响应**

成功的请求会返回新创建的策略，包括其唯一策略ID和关联的规则。

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
                "read"
            ]
        }
    ],
    "_etag": null
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与策略对应的ID。 此标识符是自动生成的，可用于查找、更新和删除策略。 |
| `name` | 策略的名称。 |
| `rules` | 定义策略的规则集。 规则定义哪些属性组合被授权，以便主体成功对资源执行操作。 |
| `rules.effect` | 考虑 `action`, `condition` 和 `resource`. 可能的值包括： `permit`, `deny`或 `indeterminate`. |
| `rules.resource` | 主体可以或不能访问的资产或对象。  资源可以是文件、应用程序、服务器，甚至API。 |
| `rules.condition` | 应用于资源的条件。 例如，如果资源是模式，则模式可以应用某些标签，从而有助于针对该模式的操作是允许还是不允许。 |
| `rules.action` | 允许主体对查询的资源执行的操作。 可能的值包括： `read`, `create`, `edit`和 `delete`. |


## 按策略ID更新策略 {#put}

要更新单个策略的规则，请向 `/policies` 端点，同时提供要在请求路径中更新的策略的ID。

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
          "read"
        ]
      }
    ]
  }'
```

**响应**

成功的响应会返回更新的策略。

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
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## 更新策略属性 {#patch}

要更新单个策略的属性，请向 `/policies` 端点，同时提供要在请求路径中更新的策略的ID。

**API格式**

```http
PATCH /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 要更新的策略的ID。 |

**请求**

以下请求将替换 `/description` 在策略ID中 `c3863937-5d40-448d-a7be-416e538f955e`.

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
| `op` | 操作调用，用于定义更新角色所需的操作。 操作包括： `add`, `replace`和 `remove`. |
| `path` | 要更新的参数的路径。 |
| `value` | 要使用更新参数的新值。 |

**响应**

成功的响应会返回查询的策略ID，其中包含更新的描述。

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
                "read"
            ]
        }
    ],
    "_etag": null
}
```

## 删除策略 {#delete}

要删除策略，请向 `/policies` 端点。

**API格式**

```http
DELETE /policies/{POLICY_ID}
```

| 参数 | 描述 |
| --- | --- |
| {POLICY_ID} | 要删除的策略的ID。 |

**请求**

以下请求将删除ID为的策略 `c3863937-5d40-448d-a7be-416e538f955e`.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/access-control/administration/policies/c3863937-5d40-448d-a7be-416e538f955e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功响应会返回HTTP状态204（无内容）和空白正文。

您可以通过尝试对策略进行查询(GET)请求来确认删除。 您将收到HTTP状态404（未找到），因为该策略已从管理中删除。
