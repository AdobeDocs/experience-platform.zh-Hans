---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API
title: 合并策略API端点
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform使您能够将来自多个来源的数据片段整合在一起，并将它们合并在一起，以全面视图每位客户。 整合这些数据时，合并策略是平台用来确定如何对数据进行优先级排序以及将哪些数据合并以创建统一视图的规则。
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2560'
ht-degree: 1%

---

# 合并策略端点

Adobe Experience Platform使您能够将来自多个来源的数据片段整合在一起，并将它们合并在一起，以全面视图每位客户。 合并策略是[!DNL Platform]用来确定如何对数据进行优先级排序以及将哪些数据合并以创建统一视图的规则。

例如，如果一个渠道跨多个用户档案与您的品牌互动，则您的组织将在多个数据集中显示与该单个客户相关的多个片段。 当这些片段被收录到平台中时，它们会合并在一起，以便为该客户创建单一用户档案。 当来自多个来源的列表发生冲突(例如，一个片段将客户为“单一”，而其他片段将客户列表为“已婚”)时，合并策略将确定要包含在个人用户档案中的信息。

使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 本指南提供了使用API处理合并策略的步骤。

要使用UI处理合并策略，请参阅[合并策略UI指南](../ui/merge-policies.md)。

## 入门指南

本指南中使用的API端点是[[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)的一部分。 在继续之前，请查阅[快速入门指南](getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南以及成功调用任何[!DNL Experience Platform] API所需标头的重要信息。

## 合并策略{#components-of-merge-policies}的组件

合并策略对您的IMS组织是私有的，允许您创建不同的策略以按您需要的特定方式合并模式。 访问[!DNL Profile]数据的任何API都需要合并策略，但如果未显式提供，则将使用默认策略。 [!DNL Platform] 为组织提供默认的合并策略，或者您可以为特定的体验数据模型(XDM)模式类创建合并策略，并将其标记为组织的默认策略。

虽然每个组织可能每个模式类有多个合并策略，但每个类只能有一个默认的合并策略。 如果提供了模式类的名称并且需要但未提供合并策略，则将使用任何设置为默认的合并策略。

>[!NOTE]
>
>当您将新合并策略设置为默认值时，之前设置为默认值的任何现有合并策略将自动更新为不再用作默认值。

### 完成合并策略对象

完整的合并策略对象表示一组控制合并用户档案片段方面的首选项。

**合并策略对象**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| 属性 | 描述 |
|---|---|
| `id` | 系统生成了在创建时分配的唯一标识符 |
| `name` | 在列表视图中标识合并策略的易记名称。 |
| `imsOrgId` | 此合并策略所属的组织ID |
| `identityGraph` | [标](#identity-graph) 识图对象，指示将从中获取相关标识的标识图。为所有相关身份找到的用户档案片段将合并。 |
| `attributeMerge` | [属](#attribute-merge) 性mergeobject，指示在发生用户档案冲突时合并策略将按何种方式优先处理数据属性。 |
| `schema.name` | 作为[`schema`](#schema)对象的一部分，`name`字段包含与合并策略相关的XDM模式类。 有关模式和类的详细信息，请阅读[XDM文档](../../xdm/home.md)。 |
| `default` | 指示此合并策略是否为指定模式的默认值的布尔值。 |
| `version` | [!DNL Platform] 维护的合并策略版本。只读值在更新合并策略时递增。 |
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

### 标识图{#identity-graph}

[Adobe Experience Platform Identity ](../../identity-service/home.md) Service管理全局使用的以及上每个组织的标识图 [!DNL Experience Platform]。合并策略的`identityGraph`属性定义如何确定用户的相关身份。

**identityGraph对象**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

其中`{IDENTITY_GRAPH_TYPE}`为以下内容之一：

* **“无”：不** 执行身份拼接。
* **“pdg”：根** 据您的个人身份图进行身份拼接。

**示例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 属性合并{#attribute-merge}

用户档案片段是特定用户所存在身份列表中仅一个身份的用户档案信息。 当使用标识图类型导致多个标识时，可能存在冲突的用户档案属性，必须指定优先级。 使用`attributeMerge`，您可以指定在“键值”（记录数据）类型数据集之间的合并冲突事件中排定优先级的用户档案属性。

**attributeMerge对象**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

其中`{ATTRIBUTE_MERGE_TYPE}`为以下内容之一：

* **`timestampOrdered`**:（默认）优先于上次更新的用户档案。使用此合并类型时，不需要`data`属性。 `timestampOrdered` 还支持在数据集内或跨数据集合并用户档案片段时优先使用的自定义时间戳。要了解详细信息，请参阅[上的“使用自定义时间戳](#custom-timestamps)”的附录部分。
* **`dataSetPrecedence`** :根据用户档案片段来自的数据集优先处理这些片段。当一个数据集中的信息优先于或信任于另一个数据集中的数据时，可以使用此选项。 使用此合并类型时，`order`属性是必需的，因为它按优先级顺序列表数据集。
   * **`order`**:当使用“dataSetPrecidence”时， `order` 必须向数组提供列表数据集。未包含在列表中的任何数据集都不会合并。 换句话说，必须显式列出数据集才能合并到用户档案中。 `order`数组按优先级列表数据集的ID。

#### 使用`dataSetPrecedence`类型的`attributeMerge`对象示例

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

#### 使用`timestampOrdered`类型的`attributeMerge`对象示例

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 架构 {#schema}

模式对象指定创建此合并策略的体验模式类。

**`schema`对象**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

其中，`name`的值是与合并策略关联的模式所基于的XDM类的名称。

**示例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

要进一步了解XDM并在Experience Platform中使用模式，请首先阅读[XDM系统概述](../../xdm/home.md)。

## 访问合并策略{#access-merge-policies}

使用[!DNL Real-time Customer Profile] API， `/config/mergePolicies`端点允许您执行查找请求以按其ID视图特定合并策略，或访问IMS组织中按特定条件过滤的所有合并策略。 您还可以使用`/config/mergePolicies/bulk-get`端点按多个合并策略的ID检索多个合并策略。 以下各节概述了执行这些呼叫的步骤。

### 按ID访问单个合并策略

通过向`/config/mergePolicies`端点发出GET请求并将`mergePolicyId`包含在请求路径中，可以通过其ID访问单个合并策略。

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

有关组成合并策略的各个元素的详细信息，请参阅本文档开头的合并策略[组件](#components-of-merge-policies)部分。

### 通过ID检索多个合并策略

可以通过向`/config/mergePolicies/bulk-get`端点发出POST请求并在请求主体中包含要检索的合并策略的ID来检索多个合并策略。

**API格式**

```http
POST /config/mergePolicies/bulk-get
```

**请求**

请求主体包括一个“ids”数组，其中各个对象包含您要检索其详细信息的每个合并策略的“id”。

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
          },
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
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
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
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
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
    }
}
```

有关组成合并策略的各个元素的详细信息，请参阅本文档开头的合并策略[组件](#components-of-merge-policies)部分。

### 列表按条件的多个合并策略

您可以列表IMS组织内的多个合并策略，方法是向`/config/mergePolicies`端点发出GET请求，并使用可选查询参数对响应进行筛选、排序和分页。 可以包含多个参数，用&amp;符号(&amp;)分隔。 调用不带参数的此端点将检索组织可用的所有合并策略。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 参数 | 描述 |
|---|---|
| `default` | 一个布尔值，通过过滤器合并策略是否是模式类的默认值来生成。 |
| `limit` | 指定页面大小限制以控制页面中包含的结果数。 默认值：20 |
| `orderBy` | 指定将结果排序为`orderBy=name`或`orderBy=+name`的字段，按名称按升序排序，或按降序排序。 `orderBy=-name`省略此值将导致按升序对`name`进行默认排序。 |
| `schema.name` | 要为其检索可用合并策略的模式的名称。 |
| `identityGraph.type` | 过滤器按标识图类型生成的结果。 可能的值包括“none”和“pdg”（专用图）。 |
| `attributeMerge.type` | 过滤器按使用的属性合并类型生成结果。 可能的值包括“timestampOrdered”和“dataSetPrecience”。 |
| `start` | 页面偏移 — 指定要检索的数据的起始ID。 默认值：0 |
| `version` | 如果要使用合并策略的特定版本，请指定此选项。 默认情况下，将使用最新版本。 |

有关`schema.name`、`identityGraph.type`和`attributeMerge.type`的详细信息，请参阅本指南前面提供的合并策略的[组件](#components-of-merge-policies)部分。


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

成功的响应返回符合请求中发送的查询参数所指定条件的合并策略的分页列表。

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
| `_links.next.href` | 结果下一页的URI地址。 使用此URI作为对同一端点的另一个API调用的请求参数，以视图页面。 如果不存在下一页，则此值将为空字符串。 |

## 创建合并策略

可以通过向`/config/mergePolicies`端点发出POST请求，为组织创建新的合并策略。

**API格式**

```http
POST /config/mergePolicies
```

**请**
求以下请求创建了新的合并策略，该策略由有效负荷中提供的属性值配置：

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
| `identityGraph.type` | 要从中获取要合并的相关身份的身份图类型。 可能的值：“none”或“pdg”（专用图）。 |
| `attributeMerge` | 在发生用户档案冲突时排定数据属性值优先级的方式。 |
| `schema` | 与合并策略关联的XDM模式类。 |
| `default` | 指定此合并策略是否为模式的默认策略。 |

有关详细信息，请参阅合并策略](#components-of-merge-policies)的[组件部分。

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

有关组成合并策略的各个元素的详细信息，请参阅本文档开头的合并策略[组件](#components-of-merge-policies)部分。

## 更新合并策略{#update}

您可以通过编辑单个属性(PATCH)或用新属性覆盖整个合并策略(PUT)来修改现有合并策略。 各示例如下。

### 编辑单个合并策略字段

可以通过向`/config/mergePolicies/{mergePolicyId}`端点发出PATCH请求，编辑合并策略的各个字段：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要删除的合并策略的标识符。 |

**请求**

以下请求将其`default`属性的值更改为`true`，以更新指定的合并策略：

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
| `op` | 指定要执行的操作。 其他PATCH操作的示例可在[JSON修补程序文档](http://jsonpatch.com)中找到 |
| `path` | 要更新的字段的路径。 接受的值为：&quot;/name&quot;、&quot;/identityGraph.type&quot;、&quot;/attributeMerge.type&quot;、&quot;/schema.name&quot;、&quot;/version&quot;、&quot;/default&quot; |
| `value` | 要将指定字段设置为的值。 |

有关详细信息，请参阅合并策略](#components-of-merge-policies)的[组件部分。


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

修改合并策略的另一种方法是使用PUT请求，该请求会覆盖整个合并策略。

**API格式**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要覆盖的合并策略的标识符。 |

**请求**

以下请求将覆盖指定的合并策略，将其属性值替换为负载中提供的属性值。 由于此请求完全替换现有的合并策略，因此您需要提供最初定义合并策略时所需的所有相同字段。 但是，这次您为要更改的字段提供了更新值。

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
| `identityGraph` | 要从中获取相关身份的身份图。 |
| `attributeMerge` | 在发生用户档案冲突时排定数据属性值优先级的方式。 |
| `schema` | 与合并策略关联的XDM模式类。 |
| `default` | 指定此合并策略是否为模式的默认策略。 |

有关详细信息，请参阅合并策略](#components-of-merge-policies)的[组件部分。


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

可以通过向`/config/mergePolicies`端点发出DELETE请求并在请求路径中包含要删除的合并策略的ID来删除合并策略。

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

成功的删除请求返回HTTP状态200(OK)和空的响应体。 要确认删除成功，您可以执行GET请求以按合并策略的ID视图该合并策略。 如果删除了合并策略，您将收到HTTP状态404（未找到）错误。

## 后续步骤

现在，您知道如何为组织创建和配置合并策略，可以使用这些策略来调整平台内客户用户档案的视图，并根据[!DNL Real-time Customer Profile]数据创建受众区段。 请参阅[Adobe Experience Platform Segmentation Service文档](../../segmentation/home.md)以开始定义和使用区段。

## 附录

本节提供与使用合并策略相关的补充信息。

### 使用自定义时间戳{#custom-timestamps}

当记录被摄入到Experience Platform中时，在摄取时获得系统时间戳并添加到记录中。 当选择`timestampOrdered`作为合并策略的`attributeMerge`类型时，将根据系统时间戳合并用户档案。 换句话说，合并是根据将记录引入平台的时间戳完成的。

有时可能会出现一些用例，如回填数据或确保在未按顺序摄取记录时事件的正确顺序，在这些情况下需要提供自定义时间戳并使合并策略遵守自定义时间戳而不是系统时间戳。

要使用自定义时间戳，必须将[[!DNL External Source System Audit Details Mixin]](#mixin-details)添加到您的用户档案模式。 添加后，可以使用`xdm:lastUpdatedDate`字段填充自定义时间戳。 当在摄取记录时填充`xdm:lastUpdatedDate`字段，Experience Platform将使用该字段在数据集内和跨数据集合并记录或用户档案片段。 如果`xdm:lastUpdatedDate`不存在或未填充，平台将继续使用系统时间戳。

>[!NOTE]
>
>必须确保在同一记录上发送PATCH时填充`xdm:lastUpdatedDate`时间戳。

有关使用模式 Registry API使用模式的分步说明(包括如何向模式添加混音)，请访问[教程，了解如何使用API](../../xdm/tutorials/create-schema-api.md)创建模式。

要使用UI使用自定义时间戳，请参阅[合并策略用户指南](../ui/merge-policies.md)中的[使用自定义时间戳](../ui/merge-policies.md#custom-timestamps)一节。

#### [!DNL External Source System Audit Details Mixin] 详细信息  {#mixin-details}

以下示例显示了[!DNL External Source System Audit Details Mixin]中正确填充的字段。 还可以在GitHub上的[公共体验数据模型(XDM)repo](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json)中查看完整的混合JSON。

```json
{
  "xdm:createdBy": "{CREATED_BY}",
  "xdm:createdDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastUpdatedBy": "{LAST_UPDATED_BY}",
  "xdm:lastUpdatedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastActivityDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastReferencedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastViewedDate": "2018-01-02T15:52:25+00:00"
 }
```
