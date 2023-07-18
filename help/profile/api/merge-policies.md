---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API
title: 合并策略API端点
type: Documentation
description: 通过Adobe Experience Platform，您可以将多个源中的数据片段放在一起并组合它们，以便查看每个客户的完整视图。 在汇总此数据时，合并策略是Platform用来确定数据优先顺序的方式以及合并哪些数据以创建统一视图的规则。
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '2467'
ht-degree: 1%

---

# 合并策略端点

通过Adobe Experience Platform，您可以将多个源中的数据片段放在一起并组合它们，以便查看每个客户的完整视图。 在汇总此数据时，合并策略是指 [!DNL Platform] 使用确定数据的优先级以及将合并哪些数据以创建统一视图。

例如，如果客户跨多个渠道与您的品牌互动，则您的组织将有多个与该单个客户相关的配置文件片段出现在多个数据集中。 将这些片段摄取到Platform后，会将其合并在一起，以便为该客户创建一个配置文件。 当来自多个源的数据发生冲突时（例如，一个片段将客户列为“单身”，而另一个片段将客户列为“已婚”），合并策略会确定个人资料中要包含哪些信息。

使用RESTful API或用户界面，您可以创建新的合并策略、管理现有策略以及为组织设置默认合并策略。 本指南提供了使用API处理合并策略的步骤。

要使用UI使用合并策略，请参阅 [合并策略UI指南](../merge-policies/ui-guide.md). 要了解有关合并策略的一般信息及其在Experience Platform中的角色的更多信息，请从阅读 [合并策略概述](../merge-policies/overview.md).

## 快速入门

本指南中使用的API端点是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 在继续之前，请查看 [快速入门指南](getting-started.md) 有关相关文档的链接，请参阅本文档中的示例API调用指南，以及有关成功调用任何组件所需的所需标头的重要信息 [!DNL Experience Platform] API。

## 合并策略的组件 {#components-of-merge-policies}

合并策略是贵组织专用的，允许您创建不同的策略以按所需的特定方式合并架构。 任何API访问 [!DNL Profile] 数据需要合并策略，但如果没有明确提供合并策略，则将使用默认策略。 [!DNL Platform] 为组织提供默认合并策略，或者您可以为特定Experience Data Model (XDM)架构类创建合并策略并将其标记为组织的默认值。

虽然每个组织可能每个架构类具有多个合并策略，但每个类只能有一个默认合并策略。 在提供了架构类的名称并且需要但未提供合并策略的情况下，将使用任何设置为默认值的合并策略。

>[!NOTE]
>
>当您将新合并策略设置为默认策略时，之前设置为默认策略的任何现有合并策略都将自动更新为不再用作默认值。

要确保所有配置文件使用者在边缘上使用相同的视图，可以将合并策略标记为在边缘上处于活动状态。 为了在Edge上激活受众（标记为Edge受众），必须将其绑定到在Edge上标记为“活动”的合并策略。 如果受众为 **非** 与在edge上标记为“活动”的合并策略绑定，受众将不会在edge上标记为“活动”，并且将标记为流式受众。

此外，每个组织只能具有 **一** 在Edge上处于活动状态的合并策略。 如果合并策略在Edge上处于活动状态，则它可用于Edge上的其他系统，例如Edge Profile、Edge Segmentation和Destinations on Edge。

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
| `id` | 系统生成的唯一标识符，在创建时分配 |
| `name` | 可在列表视图中标识合并策略的友好名称。 |
| `imsOrgId` | 此合并策略所属的组织ID |
| `schema.name` | 的一部分 [`schema`](#schema) 对象， `name` 字段包含与合并策略相关的XDM架构类。 有关架构和类的更多信息，请阅读 [XDM文档](../../xdm/home.md). |
| `version` | [!DNL Platform] 维护的合并策略版本。 每当更新合并策略时，此只读值都会递增。 |
| `identityGraph` | [身份图](#identity-graph) 指示将从其中获取相关身份的身份图的对象。 将合并为所有相关身份找到的配置文件片段。 |
| `attributeMerge` | [属性合并](#attribute-merge) 对象指明在数据冲突的情况下，合并策略优先处理配置文件属性的方式。 |
| `isActiveOnEdge` | 指示此合并策略是否可以在Edge上使用的布尔值。 默认情况下，此值为 `false`. |
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

### 身份图 {#identity-graph}

[Adobe Experience Platform Identity服务](../../identity-service/home.md) 管理用于全局的标识图，以及 [!DNL Experience Platform]. 此 `identityGraph` 合并策略的属性定义如何确定用户的相关身份。

**identityGraph对象**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

位置 `{IDENTITY_GRAPH_TYPE}` 是以下项之一：

* **&quot;none&quot;：** 不执行身份拼接。
* **&quot;pdg&quot;：** 根据您的专用身份图执行身份拼合。

**示例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 属性合并 {#attribute-merge}

配置文件片段是指某个特定用户存在的身份列表中只有一个身份的配置文件信息。 当使用的身份图形类型导致多个身份时，可能会出现配置文件属性冲突，必须指定优先级。 使用 `attributeMerge`中，您可以指定在键值（记录数据）类型数据集之间发生合并冲突时优先处理的配置文件属性。

**attributeMerge对象**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

位置 `{ATTRIBUTE_MERGE_TYPE}` 是以下项之一：

* **`timestampOrdered`**：（默认）为上次更新的用户档案指定优先级。 使用此合并类型， `data` 属性不是必需的。
* **`dataSetPrecedence`**：根据片段来自的数据集为其赋予优先级。 当某个数据集中呈现的信息优于或受信任于另一个数据集中的数据时，可以使用此功能。 使用此合并类型时， `order` 属性是必需的，因为它按优先级列出了数据集。
   * **`order`**：当使用“dataSetPrecedence”时， `order` 数组必须随数据集列表一起提供。 任何未包含在此列表中的数据集都不会被合并。 换言之，数据集必须明确列出才能合并到配置文件中。 此 `order` array按优先级列出了数据集的ID。

#### 示例 `attributeMerge` 对象使用 `dataSetPrecedence` type

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

#### 示例 `attributeMerge` 对象使用 `timestampOrdered` type

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### 架构 {#schema}

架构对象指定为其创建此合并策略的Experience Data Model (XDM)架构类。

**`schema`对象**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

其中， `name` 是与合并策略关联的架构所基于的XDM类的名称。

**示例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

要了解有关XDM以及在Experience Platform中使用架构的更多信息，请从阅读 [XDM系统概述](../../xdm/home.md).

## 访问合并策略 {#access-merge-policies}

使用 [!DNL Real-Time Customer Profile] API、 `/config/mergePolicies` 端点允许您执行查找请求，以按其ID查看特定合并策略，或访问组织中按特定条件筛选的所有合并策略。 您还可以使用 `/config/mergePolicies/bulk-get` 端点以按其ID检索多个合并策略。 以下各节概述了执行每个调用的步骤。

### 按ID访问单合并策略

GET您可以通过对策略的ID来访问单合并策略，方法是向 `/config/mergePolicies` 端点并包括 `mergePolicyId` 在请求路径中。

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

成功响应将返回合并策略的详细信息。

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

请参阅 [合并策略的组件](#components-of-merge-policies) 部分，以了解有关构成合并策略的每个单独元素的详细信息。

### 按其ID检索多个合并策略

您可以通过向以下对象发出POST请求来检索多个合并策略： `/config/mergePolicies/bulk-get` 端点，并包括要在请求正文中检索的合并策略的ID。

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

成功的响应会返回HTTP状态207（多状态）以及POST请求中提供了其ID的合并策略的详细信息。

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

请参阅 [合并策略的组件](#components-of-merge-policies) 部分，以了解有关构成合并策略的每个单独元素的详细信息。

### 按条件列出多个合并策略

您可以通过向以下网站发出GET请求，列出公司内的多个合并策略 `/config/mergePolicies` 端点，并使用可选的查询参数筛选、排序和分页响应。 可以包含多个参数，以&amp;分隔。 在不使用参数的情况下对此端点进行调用将检索对您的组织可用的所有合并策略。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 参数 | 描述 |
|---|---|
| `default` | 一个布尔值，用于根据合并策略是否为架构类的默认值来筛选结果。 |
| `limit` | 指定页面大小限制，以控制页面中包含的结果数。 默认值：20 |
| `orderBy` | 指定排序结果所依据的字段，如下所示 `orderBy=name` 或 `orderBy=+name` 按名称升序排序，或 `orderBy=-name`，以按降序排序。 省略此值会导致默认排序 `name` 按升序排列。 |
| `isActiveOnEdge` | 一个布尔值，用于根据合并策略在Edge上是否处于活动状态来筛选结果。 |
| `schema.name` | 要检索其可用合并策略的架构的名称。 |
| `identityGraph.type` | 按身份图类型筛选结果。 可能的值包括“none”和“pdg”（专用图）。 |
| `attributeMerge.type` | 按使用的属性合并类型筛选结果。 可能的值包括“timestampOrdered”和“dataSetPrecedence”。 |
| `start` | 页面偏移 — 指定要检索的数据的起始ID。 默认值： 0 |
| `version` | 如果要使用特定版本的合并策略，请指定此项。 默认情况下，将使用最新版本。 |

有关以下内容的更多信息： `schema.name`， `identityGraph.type`、和 `attributeMerge.type`，请参阅 [合并策略的组件](#components-of-merge-policies) 章节。


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

成功的响应将返回一个分页的合并策略列表，该列表符合由请求中发送的查询参数指定的标准。

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

您可以向以下对象发出POST请求，以便为贵组织创建新的合并策略： `/config/mergePolicies` 端点。

**API格式**

```http
POST /config/mergePolicies
```

**请求**
以下请求将创建新的合并策略，该策略由有效负载中提供的属性值配置：

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
| `name` | 便于识别的名称，通过该名称，可以在列表视图中标识合并策略。 |
| `identityGraph.type` | 从中获取要合并的相关标识的标识图类型。 可能的值：“none”或“pdg”（专用图）。 |
| `attributeMerge` | 在数据冲突的情况下对配置文件属性值优先化的方式。 |
| `schema` | 与合并策略关联的XDM架构类。 |
| `isActiveOnEdge` | 指定此合并策略是否在Edge上处于活动状态。 |
| `default` | 指定此合并策略是否为架构的默认值。 |

请参阅 [合并策略的组件](#components-of-merge-policies) 部分以了解更多信息。

**响应**

成功响应将返回新创建的合并策略的详细信息。

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

请参阅 [合并策略的组件](#components-of-merge-policies) 部分，以了解有关构成合并策略的每个单独元素的详细信息。

## 更新合并策略 {#update}

您可以通过编辑单个属性（策略）或使用新属性(PATCH)覆盖整个合并PUT来修改现有合并策略。 下面显示了每种功能的示例。

### 编辑单个合并策略字段

您可以通过向以下对象发出PATCH请求来编辑合并策略的各个字段： `/config/mergePolicies/{mergePolicyId}` 端点：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要删除的合并策略的标识符。 |

**请求**

以下请求通过更改指定合并策略的值来更新其值 `default` 属性至 `true`：

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
| `op` | 指定要执行的操作。 其他PATCH操作的示例可在 [JSON修补程序文档](https://datatracker.ietf.org/doc/html/rfc6902) |
| `path` | 要更新的字段的路径。 接受的值为：“/name”、“/identityGraph.type”、“/attributeMerge.type”、“/schema.name”、“/version”、“/default”、“/isActiveOnEdge” |
| `value` | 将指定字段设置为的值。 |

请参阅 [合并策略的组件](#components-of-merge-policies) 部分以了解更多信息。


**响应**

成功响应将返回新更新的合并策略的详细信息。

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

以下请求将覆盖指定的合并策略，并将其属性值替换为有效负载中提供的属性值。 由于此请求完全替换了现有的合并策略，因此您需要提供最初定义合并策略时所需的所有相同字段。 但是，这次您需要为要更改的字段提供更新的值。

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
| `name` | 便于识别的名称，通过该名称，可以在列表视图中标识合并策略。 |
| `identityGraph` | 从中获取要合并的相关身份的身份图。 |
| `attributeMerge` | 在数据冲突的情况下对配置文件属性值优先化的方式。 |
| `schema` | 与合并策略关联的XDM架构类。 |
| `isActiveOnEdge` | 指定此合并策略是否在Edge上处于活动状态。 |
| `default` | 指定此合并策略是否为架构的默认值。 |

请参阅 [合并策略的组件](#components-of-merge-policies) 部分以了解更多信息。

**响应**

成功响应将返回已更新合并策略的详细信息。

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

可以通过向发出合并策略请求来删除DELETE `/config/mergePolicies` 端点并在请求路径中包含要删除的合并策略的ID。

>[!NOTE]
>
>如果合并策略具有 `isActiveOnEdge` 设置为true，则合并策略 **无法** 将被删除。 使用 [PATCH](#edit-individual-merge-policy-fields) 或 [PUT](#overwrite-a-merge-policy) 端点以更新合并策略，然后再删除它。

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

成功的删除请求会返回HTTP状态200 （正常）和空响应正文。 要确认删除成功，您可以执行GET请求，以按合并策略的ID查看合并策略。 如果删除了合并策略，您将收到HTTP状态404 （未找到）错误。

## 后续步骤

现在您已经知道如何为组织创建和配置合并策略，可以使用这些策略调整Platform中客户配置文件的视图，以及从创建受众 [!DNL Real-Time Customer Profile] 数据。

请查看 [Adobe Experience Platform分段服务文档](../../segmentation/home.md) 开始定义和使用受众。
