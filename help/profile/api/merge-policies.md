---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案API开发人员指南
topic: guide
translation-type: tm+mt
source-git-commit: 33091568c850375b399435f375e854667493152c
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 1%

---


# 合并策略

Adobe Experience Platform使您能够将多个来源的数据整合在一起并加以整合，从而全面了解每位客户的视图。 整合这些数据时，合并策略是平台用来确定数据的优先级以及将哪些数据合并以创建统一视图的规则。 使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 本指南显示了使用API处理合并策略的步骤。 要使用UI处理合并策略，请参阅合 [并策略用户指南](../ui/merge-policies.md)。

## 入门指南

本指南中使用的API端点是实时客户用户档案API的一部分。 在继续之前，请查 [看实时客户用户档案API开发人员指南](getting-started.md)。 特别是，用户档案开 [发人员指南的](getting-started.md#getting-started) “入门”部分包括相关主题的链接、阅读此文档中示例API调用的指南，以及成功调用任何Experience Platform API所需标头的重要信息。

## 合并策略的组件 {#components-of-merge-policies}

合并策略是IMS组织专用的策略，允许您创建不同的策略，以便以您需要的特定方式合并模式。 访问用户档案数据的任何API都需要合并策略，但如果未明确提供合并策略，则将使用默认策略。 平台提供默认的合并策略，或者您可以为特定模式创建合并策略并将其标记为组织的默认策略。 每个组织可能具有每个模式的多个合并策略，但每个模式只能有一个默认的合并策略。 在提供模式名和需要但未提供合并策略的情况下，将使用任何设置为默认的合并策略。 当您将合并策略设置为默认策略时，之前设置为默认策略的任何现有合并策略都将自动更新为不再用作默认策略。

### 完整合并策略对象

完整的合并策略对象表示控制合并用户档案片段方面的一组首选项。

**合并策略对象**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": {BOOLEAN},
        "updateEpoch": {UPDATE_TIME}
    }
```

| 属性 | 描述 |
|---|---|
| `id` | 在创建时分配的系统生成的唯一标识符 |
| `name` | 友好名称，在列表视图中可通过它标识合并策略。 |
| `imsOrgId` | 此合并策略所属的组织ID |
| `identityGraph` | [标识图对象](#identity-graph) ，指示将从中获取相关标识的标识图。 为所有相关身份找到的用户档案片段将被合并。 |
| `attributeMerge` | [属性合并](#attribute-merge) 对象，指示在发生用户档案冲突时合并策略优先处理属性值的方式。 |
| `schema` | 可 [以使用](#schema) 合并策略的模式对象。 |
| `default` | 指示此合并策略是否为指定模式的默认值的布尔值。 |
| `version` | 平台维护的合并策略版本。 只读值在更新合并策略时递增。 |
| `updateEpoch` | 合并策略的上次更新日期。 |

**合并策略示例**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### 身份图 {#identity-graph}

[Adobe Experience Platform Identity Service管理全球](../../identity-service/home.md) 、Experience Platform上每个组织使用的标识图。 合并 `identityGraph` 策略的属性定义如何确定用户的相关标识。

**identityGraph对象**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

其 `{IDENTITY_GRAPH_TYPE}` 中是下列项之一：

* **“无”:** 不进行身份拼接。
* **“pdg”:** 根据您的个人身份图执行身份拼接。

**示例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 属性合并 {#attribute-merge}

用户档案片段是特定用户所存在身份列表中仅一个身份的用户档案信息。 当使用的标识图类型导致多个标识时，用户档案属性的值可能会发生冲突，并且必须指定优先级。 使 `attributeMerge`用，您可以指定在合并冲突事件中排定优先级的数据集用户档案值。

**attributeMerge对象**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

其 `{ATTRIBUTE_MERGE_TYPE}` 中是下列项之一：

* **&quot;timestampOrdered&quot;**: （默认）优先考虑最后更新的用户档案，以防发生冲突。 使用此合并类型， `data` 不需要属性。
* **&quot;dataSetPrecedence&quot;** : 根据用户档案片段的来源数据集优先处理这些片段。 当一个数据集中的信息优先于或信任另一个数据集中的数据时，可以使用此选项。 使用此合并类型时，属 `order` 性是必需的，因为它按优先级顺序列表数据集。
   * **“order”**: 当使用“dataSetPrecedency”时， `order` 必须向数组提供一列表数据集。 列表中未包含的任何数据集都不会合并。 换言之，必须明确列出数据集才能合并到用户档案中。 数 `order` 组按优先级列表数据集的ID。

**使用dataSetPrecedence类型的attributeMerge对象示例**

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

**使用timestampOrdered类型的attributeMerge对象示例**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 模式 {#schema}

模式对象指定为其创建此合并策略的XDM模式。

**`schema`对象&#x200B;**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

其中，值 `name` 是与合并策略关联的模式所基于的XDM类的名称。

**示例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

## 访问合并策略 {#access-merge-policies}

使用实时用户档案API，端点允许您执行查找请求，以按其ID视图特定的合并策略，或访问IMS组织中按特定条件筛选的所有合并策略。 `/config/mergePolicies` 您还可以使用端点 `/config/mergePolicies/bulk-get` 来通过其ID检索多个合并策略。 以下各节概述了执行这些调用的步骤。

### 按ID访问单个合并策略

通过向端点发出GET请求并在请求路径中包含，可以通 `/config/mergePolicies` 过其ID访 `mergePolicyId` 问单个合并策略。

**API格式**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要删除的合并策略的标识符。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**响应**

成功的响应会返回合并策略的详细信息。

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

有关组成 [合并策略的](#components-of-merge-policies) 各个元素的详细信息，请参阅此文档开头的合并策略的组件部分。

### 按多个合并策略的ID检索多个合并策略

通过向端点发出POST请求并在请求主体中 `/config/mergePolicies/bulk-get` 包括要检索的合并策略的ID，可以检索多个合并策略。

**API格式**

```http
POST /config/mergePolicies/bulk-get
```

**请求**

请求主体包含一个“ids”数组，其中各个对象包含每个合并策略的“id”，您要为其检索详细信息。

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          }
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**响应**

成功的响应会返回“HTTP状态207（多状态）”和其ID在POST请求中提供的合并策略的详细信息。

```json
{
    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
    "name": "Profile Default Merge Policy",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": true,
    "updateEpoch": 1552086578
},
{
    "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
    "name": "Dataset Precedence Merge Policy",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": false,
    "updateEpoch": 1576099719
}
```

有关组成 [合并策略的](#components-of-merge-policies) 各个元素的详细信息，请参阅此文档开头的合并策略的组件部分。

### 列表多个按标准合并策略

您可以列表IMS组织内的多个合并策略，方法是向端点发出GET请求 `/config/mergePolicies` ，并使用可选的查询参数来筛选、排序和分页响应。 可以包括多个参数，用和号(&amp;)分隔。 调用此端点（不含参数）将检索组织可用的所有合并策略。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 参数 | 描述 |
|---|---|
| `default` | 一个布尔值，过滤器通过合并策略是否是模式类的默认值来生成。 |
| `limit` | 指定页面大小限制以控制页面中包含的结果数。 默认值： 20 |
| `orderBy` | 指定按该字段对结果进行排序， `orderBy=name` 或按 `orderBy=+name` 名称按升序排序，或 `orderBy=-name`按降序排序。 省略此值将导致按升序进行 `name` 默认排序。 |
| `schema.name` | 要检索可用合并策略的模式的名称。 |
| `identityGraph.type` | 过滤器按标识图类型生成结果。 可能的值包括“none”和“pdg”（专用图）。 |
| `attributeMerge.type` | 过滤器按使用的属性合并类型生成结果。 可能的值包括“timestampOrdered”和“dataSetPrecedence”。 |
| `start` | 页面偏移——指定要检索数据的起始ID。 默认值： 0 |
| `version` | 如果要使用合并策略的特定版本，请指定此选项。 默认情况下，将使用最新版本。 |

有关、和的 `schema.name`详细 `identityGraph.type`信息， `attributeMerge.type`请参阅本指 [南前面提供的合](#components-of-merge-policies) 并策略的组件一节。


**请求**

以下请求列表给定模式的所有合并策略：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**响应**

成功的响应会返回合并策略的分页列表，该查询符合在请求中发送的合并参数指定的条件。

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| 属性 | 描述 |
|---|---|
| `_links.next.href` | 结果下一页的URI地址。 将此URI用作对同一端点的另一个API调用的请求参数，以视图页面。 如果不存在下一页，则此值将为空字符串。 |

## 创建合并策略

您可以通过向端点发出POST请求，为组织创建新的合并策 `/config/mergePolicies` 略。

**API格式**

```http
POST /config/mergePolicies
```

**请**&#x200B;求以下请求创建新的合并策略，该策略由有效负荷中提供的属性值配置：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| 属性 | 描述 |
|---|---|
| `name` | 在列表视图中标识合并策略的人性化名称。 |
| `identityGraph.type` | 要从中获得要合并的相关标识的标识图类型。 可能的值： “none”或“pdg”（专用图）。 |
| `attributeMerge` | 在数据冲突时排定用户档案属性值优先级的方式。 |
| `schema` | 与合并策略关联的XDM模式类。 |
| `default` | 指定此合并策略是否为模式的默认策略。 |

有关详细信 [息，请参阅合并策](#components-of-merge-policies) 略的组件部分。

**响应**

成功的响应会返回新创建的合并策略的详细信息。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

有关组成 [合并策略的](#components-of-merge-policies) 各个元素的详细信息，请参阅此文档开头的合并策略的组件部分。

## 更新合并策略 {#update}

您可以通过编辑单个属性(PATCH)或用新属性(PUT)覆盖整个合并策略来修改现有的合并策略。 各示例如下。

### 编辑单个合并策略字段

通过向端点发出PATCH请求，可以编辑合并策略的各个字 `/config/mergePolicies/{mergePolicyId}` 段：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要删除的合并策略的标识符。 |

**请求**

以下请求将其属性的值更改为，以更新指定 `default` 的合并策 `true`略：

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| 属性 | 描述 |
|---|---|
| `op` | 指定要执行的操作。 JSON修补程序文档中可找到其他PATCH [操作的示例](http://jsonpatch.com) |
| `path` | 要更新的字段的路径。 接受的值为： &quot;/name&quot;、&quot;/identityGraph.type&quot;、&quot;/attributeMerge.type&quot;、&quot;/schema.name&quot;、&quot;/version&quot;、&quot;/default&quot; |
| `value` | 要将指定字段设置为的值。 |

有关详细信 [息，请参阅合并策](#components-of-merge-policies) 略的组件部分。


**响应**

成功的响应会返回新更新的合并策略的详细信息。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### 覆盖合并策略

修改合并策略的另一种方法是使用PUT请求，该请求覆盖整个合并策略。

**API格式**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要覆盖的合并策略的标识符。 |

**请求**

以下请求将覆盖指定的合并策略，将其属性值替换为有效负荷中提供的属性值。 由于此请求完全替换现有的合并策略，因此您需要提供最初定义合并策略时所需的所有相同字段。 但是，这次您为要更改的字段提供了更新值。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| 属性 | 描述 |
|---|---|
| `name` | 在列表视图中标识合并策略的人性化名称。 |
| `identityGraph` | 要从中获得相关身份的身份图合并。 |
| `attributeMerge` | 在数据冲突时排定用户档案属性值优先级的方式。 |
| `schema` | 与合并策略关联的XDM模式类。 |
| `default` | 指定此合并策略是否为模式的默认策略。 |

有关详细信 [息，请参阅合并策](#components-of-merge-policies) 略的组件部分。


**响应**

成功的响应会返回更新的合并策略的详细信息。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## 删除合并策略

可以通过向端点发出DELETE请求并在请 `/config/mergePolicies` 求路径中包含要删除的合并策略的ID，来删除合并策略。

**API格式**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要删除的合并策略的标识符。 |

**请求**

以下请求将删除合并策略。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功删除请求将返回HTTP状态200(OK)和空的响应主体。 要确认删除成功，您可以执行GET请求，按合并策略的ID视图该策略。 如果合并策略被删除，您将收到HTTP状态404（找不到）错误。

## 后续步骤

现在，您知道如何为IMS组织创建和配置合并策略，可以使用它们根据实时受众用户档案数据创建细分。 请参阅Adobe [Experience Platform Segmentation Service文档](../../segmentation/home.md) ，开始定义和使用区段。



