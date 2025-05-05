---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 合并策略API端点
type: Documentation
description: Adobe Experience Platform允许您从多个来源将数据片段整合在一起并组合它们，以便查看每个客户的完整视图。 在汇总此数据时，合并策略是Experience Platform用于确定数据优先顺序的规则以及将合并哪些数据以创建统一视图。
role: Developer
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 1%

---

# 合并策略端点

Adobe Experience Platform允许您从多个来源将数据片段整合在一起并组合它们，以便查看每个客户的完整视图。 在汇总此数据时，合并策略是[!DNL Experience Platform]用于确定数据优先顺序的规则以及将合并哪些数据以创建统一视图。

例如，如果客户跨多个渠道与您的品牌互动，则您的组织将在多个数据集中显示多个与该单个客户相关的配置文件片段。 将这些片段摄取到Experience Platform后，会合并在一起，以便为该客户创建一个配置文件。 当来自多个源的数据发生冲突时（例如，一个片段将客户列为“单身”，而另一个片段将客户列为“已婚”），合并策略会确定要将哪些信息包含在个人的配置文件中。

使用RESTful API或用户界面，您可以创建新的合并策略、管理现有策略以及为组织设置默认合并策略。 本指南提供了使用API处理合并策略的步骤。

要使用UI处理合并策略，请参阅[合并策略UI指南](../merge-policies/ui-guide.md)。 要了解有关合并策略的一般信息及其在Experience Platform中的角色的更多信息，请从阅读[合并策略概述](../merge-policies/overview.md)开始。

## 快速入门

本指南中使用的API终结点是[[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 在继续之前，请查看[快速入门指南](getting-started.md)，以获取相关文档的链接、此文档中示例API调用的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需的所需标头的重要信息。

## 合并策略的组件 {#components-of-merge-policies}

合并策略是贵组织专有的，允许您创建不同的策略以按照所需的特定方式合并架构。 任何访问[!DNL Profile]数据的API都需要合并策略，但如果未明确提供合并策略，则将使用默认策略。 [!DNL Experience Platform]为组织提供默认合并策略，或者您可以为特定体验数据模型(XDM)架构类创建合并策略并将其标记为组织的默认策略。

虽然每个组织可能具有每个架构类的多个合并策略，但每个类只能有一个默认合并策略。 如果提供了架构类的名称，并且需要但未提供合并策略，则将使用任何设置为默认值的合并策略。

>[!NOTE]
>
>当您将新合并策略设置为默认策略时，之前设置为默认策略的任何现有合并策略都将自动更新为不再用作默认值。

要确保所有配置文件使用者在边缘上使用相同的视图，可以将合并策略标记为在边缘上处于活动状态。 为了在Edge上激活受众（标记为Edge受众），必须将其绑定到在Edge上标记为“活动”的合并策略。 如果受众未与在Edge上标记为“活动”的合并策略绑定&#x200B;**&#x200B;**，则该受众不会在Edge上标记为“活动”，而是会标记为流式受众。

此外，每个组织只能有&#x200B;**一个**&#x200B;在边缘上处于活动状态的合并策略。 如果合并策略在Edge上处于活动状态，则该策略可用于Edge上的其他系统，例如Edge用户档案、Edge分段和Edge上的目标。

### 完成合并策略对象

完整的合并策略对象表示一组首选项，用于控制合并配置文件片段的各个方面。

**合并策略对象**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| 属性 | 描述 |
|---|---|
| `id` | 创建时分配的系统生成的唯一标识符 |
| `name` | 在列表视图中用于标识合并策略的友好名称。 |
| `imsOrgId` | 此合并策略所属的组织ID |
| `schema.name` | 作为[`schema`](#schema)对象的一部分，`name`字段包含与合并策略相关的XDM架构类。 有关架构和类的详细信息，请阅读[XDM文档](../../xdm/home.md)。 |
| `version` | [!DNL Experience Platform]维护了合并策略的版本。 每当更新合并策略时，此只读值都会递增。 |
| `identityGraph` | [标识图](#identity-graph)对象，指示将从其中获取相关标识的标识图。 将合并为所有相关身份找到的配置文件片段。 |
| `attributeMerge` | [属性合并](#attribute-merge)对象，它指明在数据冲突的情况下合并策略优先处理配置文件属性的方式。 |
| `isActiveOnEdge` | 布尔值，指示是否可在Edge上使用此合并策略。 默认情况下，此值为`false`。 |
| `default` | 布尔值，指示此合并策略是否为指定架构的默认值。 |
| `updateEpoch` | 上次更新合并策略的日期。 |

**示例合并策略**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### 身份标识图 {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md)管理[!DNL Experience Platform]上每个组织全局使用的身份图。 合并策略的`identityGraph`属性定义如何确定用户的相关标识。

**identityGraph对象**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

其中`{IDENTITY_GRAPH_TYPE}`是以下任一项：

* **“无”：**&#x200B;不执行标识拼接。
* **&quot;pdg&quot;：**&#x200B;根据您的专用身份图执行身份拼合。

**示例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 属性合并 {#attribute-merge}

配置文件片段是特定用户存在的身份列表中只有一个身份的个人资料信息。 当使用的身份图形类型导致多个身份时，可能会出现配置文件属性冲突，必须指定优先级。 使用`attributeMerge`，您可以指定在键值（记录数据）类型数据集之间发生合并冲突时优先处理哪些配置文件属性。

**attributeMerge对象**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

其中`{ATTRIBUTE_MERGE_TYPE}`是以下任一项：

* **`timestampOrdered`**： （默认）为上次更新的配置文件赋予优先权。 使用此合并类型，`data`特性不是必需的。
* **`dataSetPrecedence`**：根据配置文件片段来自的数据集为其赋予优先级。 当某个数据集中呈现的信息优于或受信任于另一个数据集中的数据时，可以使用此功能。 使用此合并类型时，`order`属性是必需的，因为它按优先级列出了数据集。
   * **`order`**：当使用“dataSetPrecedence”时，`order`数组必须随数据集列表一起提供。 任何未包含在此列表中的数据集都不会被合并。 换言之，数据集必须明确列出以合并到配置文件中。 `order`数组按优先级列出了数据集的ID。

#### 使用`dataSetPrecedence`类型的示例`attributeMerge`对象

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### 使用`timestampOrdered`类型的示例`attributeMerge`对象

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 架构 {#schema}

架构对象指定为其创建此合并策略的体验数据模型(XDM)架构类。

**`schema`对象**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

其中`name`的值是与合并策略关联的架构所基于的XDM类的名称。

**示例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

要了解有关XDM以及在Experience Platform中使用架构的更多信息，请从阅读[XDM系统概述](../../xdm/home.md)开始。

## 访问合并策略 {#access-merge-policies}

通过使用[!DNL Real-Time Customer Profile] API，`/config/mergePolicies`端点允许您执行查找请求，以按其ID查看特定合并策略，或访问组织中按特定条件筛选的所有合并策略。 您还可以使用`/config/mergePolicies/bulk-get`端点按ID检索多个合并策略。 以下各节概述了执行上述每种调用的步骤。

### 按ID访问单一合并策略

您可以通过向`/config/mergePolicies`端点发出GET请求并在请求路径中包含`mergePolicyId`来通过单合并策略的ID访问它。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**响应**

成功的响应将返回合并策略的详细信息。

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

有关构成合并策略的每个单独元素的详细信息，请参阅本文档开头的[合并策略组件](#components-of-merge-policies)部分。

### 按其ID检索多个合并策略

您可以通过向`/config/mergePolicies/bulk-get`端点发出POST请求来检索多个合并策略，并在请求正文中包含要检索的合并策略的ID。

**API格式**

```http
POST /config/mergePolicies/bulk-get
```

**请求**

请求正文包含一个“ids”数组，其中的各个对象包含要检索其详细信息的每个合并策略的“id”。

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的响应返回HTTP状态207（多状态）以及POST请求中提供了ID的合并策略的详细信息。

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

有关构成合并策略的每个单独元素的详细信息，请参阅本文档开头的[合并策略组件](#components-of-merge-policies)部分。

### 按条件列出多个合并策略

您可以列出组织内的多个合并策略，方法是向`/config/mergePolicies`端点发出GET请求，并使用可选的查询参数来筛选、排序和分页响应。 可以包含多个参数，以&amp;分隔。 在不使用参数的情况下对此端点进行调用将检索对您的组织可用的所有合并策略。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 参数 | 描述 |
|---|---|
| `default` | 一个布尔值，它根据合并策略是否为架构类的默认策略来筛选结果。 |
| `limit` | 指定页大小限制，以控制页中包含的结果数。 默认值：20 |
| `orderBy` | 指定要按其排序结果的字段，如`orderBy=name`或`orderBy=+name`中要按名称升序排序，或`orderBy=-name`中要按降序排序。 省略此值将导致默认排序`name`按升序排列。 |
| `isActiveOnEdge` | 一个布尔值，用于根据合并策略在Edge上是否处于活动状态来筛选结果。 |
| `schema.name` | 要检索其可用合并策略的架构的名称。 |
| `identityGraph.type` | 按身份图类型过滤结果。 可能的值包括“none”和“pdg”（专用图）。 |
| `attributeMerge.type` | 按使用的属性合并类型筛选结果。 可能的值包括“timestampOrdered”和“dataSetPrecedence”。 |
| `start` | 页面偏移 — 为要检索的数据指定起始ID。 默认值： 0 |
| `version` | 如果要使用特定版本的合并策略，请指定此项。 默认情况下，将使用最新版本。 |

有关`schema.name`、`identityGraph.type`和`attributeMerge.type`的详细信息，请参阅本指南前面提供的[合并策略组件](#components-of-merge-policies)部分。


**请求**

以下请求列出了给定架构的所有合并策略：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**响应**

成功的响应会返回一个分页的合并策略列表，该列表符合在请求中发送的查询参数所指定的标准。

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
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "isActiveOnEdge": false,
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
| `_links.next.href` | 下一页结果的URI地址。 将此URI用作对同一端点的其他API调用的请求参数，以查看页面。 如果下一页不存在，则此值将为空字符串。 |

## 创建合并策略

您可以通过向`/config/mergePolicies`端点发出POST请求来为组织创建新的合并策略。

**API格式**

```http
POST /config/mergePolicies
```

**请求**
以下请求创建新的合并策略，该策略由有效负载中提供的属性值配置：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "isActiveOnEdge": true,
    "default": true
}'
```

| 属性 | 描述 |
|---|---|
| `name` | 便于识别的名称，通过该名称可以在列表视图中标识合并策略。 |
| `identityGraph.type` | 从中获取要合并的相关身份的身份图类型。 可能的值：“none”或“pdg”（专用图）。 |
| `attributeMerge` | 在数据冲突的情况下优先处理配置文件属性值的方式。 |
| `schema` | 与合并策略关联的XDM架构类。 |
| `isActiveOnEdge` | 指定此合并策略在Edge上是否处于活动状态。 |
| `default` | 指定此合并策略是否为架构的默认策略。 |

有关详细信息，请参阅合并策略[&#128279;](#components-of-merge-policies)的组件部分。

**响应**

成功的响应将返回新创建的合并策略的详细信息。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

有关构成合并策略的每个单独元素的详细信息，请参阅本文档开头的[合并策略组件](#components-of-merge-policies)部分。

## 更新合并策略 {#update}

您可以通过编辑单个属性(PATCH)或使用新属性覆盖整个合并策略(PUT)来修改现有合并策略。 下面显示了每种功能的示例。

### 编辑单个合并策略字段

您可以通过向`/config/mergePolicies/{mergePolicyId}`端点发出PATCH请求来编辑合并策略的各个字段：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要删除的合并策略的标识符。 |

**请求**

以下请求通过将指定合并策略的`default`属性的值更改为`true`来更新该策略：

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | 指定要执行的操作。 其他PATCH操作的示例可在[JSON修补程序文档](https://datatracker.ietf.org/doc/html/rfc6902)中找到 |
| `path` | 要更新的字段的路径。 接受的值为：“/name”、“/identityGraph.type”、“/attributeMerge.type”、“/schema.name”、“/version”、“/default”、“/isActiveOnEdge” |
| `value` | 将指定字段设置为的值。 |

有关详细信息，请参阅合并策略[&#128279;](#components-of-merge-policies)的组件部分。


**响应**

成功的响应将返回新更新的合并策略的详细信息。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
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

以下请求将覆盖指定的合并策略，并将其属性值替换为有效负载中提供的属性值。 由于此请求完全替换了现有的合并策略，因此您需要提供最初定义合并策略时所需的所有相同字段。 但是，这次您要为要更改的字段提供更新的值。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
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
        "isActiveOnEdge": true,
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| 属性 | 描述 |
|---|---|
| `name` | 便于识别的名称，通过该名称可以在列表视图中标识合并策略。 |
| `identityGraph` | 从中获取要合并的相关身份的身份图。 |
| `attributeMerge` | 在数据冲突的情况下优先处理配置文件属性值的方式。 |
| `schema` | 与合并策略关联的XDM架构类。 |
| `isActiveOnEdge` | 指定此合并策略在Edge上是否处于活动状态。 |
| `default` | 指定此合并策略是否为架构的默认策略。 |

有关详细信息，请参阅合并策略[&#128279;](#components-of-merge-policies)的组件部分。

**响应**

成功的响应将返回已更新合并策略的详细信息。

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## 删除合并策略

通过向`/config/mergePolicies`端点发出DELETE请求，并在请求路径中包含要删除的合并策略的ID，可以删除合并策略。

>[!NOTE]
>
>如果合并策略的`isActiveOnEdge`设置为true，则无法删除合并策略&#x200B;**&#x200B;**。 使用[PATCH](#edit-individual-merge-policy-fields)或[PUT](#overwrite-a-merge-policy)端点更新合并策略，然后再删除它。

**API格式**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要删除的合并策略的标识符。 |

**请求**

以下请求删除合并策略。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的删除请求返回HTTP状态200 （正常）和空响应正文。 要确认删除成功，您可以执行GET请求以按其ID查看合并策略。 如果删除了合并策略，您将收到HTTP状态404（未找到）错误。

## 后续步骤

现在您已经知道如何为组织创建和配置合并策略，可以使用这些策略在Experience Platform中调整客户配置文件视图，并根据您的[!DNL Real-Time Customer Profile]数据创建受众。

请参阅[Adobe Experience Platform Segmentation Service文档](../../segmentation/home.md)以开始定义和使用受众。
