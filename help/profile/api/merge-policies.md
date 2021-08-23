---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 合并策略API端点
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform允许您从多个来源将数据片段合并在一起，以便查看各个客户的完整视图。 合并策略是Platform用来确定数据优先级以及合并哪些数据以创建统一视图的规则，将这些数据整合在一起。
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: acf88ba3c4181fce85ffec3b0041a30b7bb14cef
workflow-type: tm+mt
source-wordcount: '2263'
ht-degree: 1%

---

# 合并策略端点

Adobe Experience Platform允许您从多个来源将数据片段合并在一起，以便查看各个客户的完整视图。 合并策略是[!DNL Platform]用来确定数据的优先级以及将哪些数据合并以创建统一视图的规则。

例如，如果客户跨多个渠道与您的品牌进行交互，则您的组织将在多个数据集中显示与该单个客户相关的多个配置文件片段。 将这些片段摄取到Platform后，它们会合并在一起，以便为该客户创建单个配置文件。 当来自多个源的数据发生冲突（例如，一个片段将客户列为“单一”，而另一个片段将客户列为“已婚”）时，合并策略会确定要包含在个人配置文件中的信息。

使用RESTful API或用户界面，您可以创建新的合并策略、管理现有策略，并为您的组织设置默认的合并策略。 本指南提供了使用API处理合并策略的步骤。

要使用UI处理合并策略，请参阅[合并策略UI指南](../merge-policies/ui-guide.md)。 要进一步了解合并策略的一般情况及其在Experience Platform中的角色，请首先阅读[合并策略概述](../merge-policies/overview.md)。

## 快速入门

本指南中使用的API端点是[[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)的一部分。 在继续操作之前，请查阅[快速入门指南](getting-started.md) ，以获取相关文档的链接、本文档中API调用示例的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需标头的重要信息。

## 合并策略的组件 {#components-of-merge-policies}

合并策略是IMS组织的专用策略，允许您创建不同的策略以按照所需的特定方式合并架构。 任何访问[!DNL Profile]数据的API都需要合并策略，但如果未明确提供，则将使用默认策略。 [!DNL Platform] 为组织提供默认的合并策略，或者，您可以为特定体验数据模型(XDM)架构类创建合并策略，并将其标记为组织的默认策略。

虽然每个组织可能在每个架构类中具有多个合并策略，但每个类只能有一个默认的合并策略。 如果提供了架构类的名称并且需要但未提供合并策略，则将使用设置为默认设置的任何合并策略。

>[!NOTE]
>
>当您将新合并策略设置为默认策略时，之前设置为默认策略的任何现有合并策略将自动更新为不再用作默认值。

### 完成合并策略对象

完整的合并策略对象表示一组控制合并配置文件片段各方面的首选项。

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
| `id` | 系统生成的唯一标识符在创建时分配 |
| `name` | 用于在列表视图中标识合并策略的易记名称。 |
| `imsOrgId` | 此合并策略所属的组织ID |
| `identityGraph` | [标](#identity-graph) 识图对象，用于指示将从中获取相关标识的标识图。将合并找到的所有相关身份的配置文件片段。 |
| `attributeMerge` | [属性](#attribute-merge) mergeobject ，指示在发生数据冲突时合并策略优先处理配置文件属性的方式。 |
| `schema.name` | 在[`schema`](#schema)对象中， `name`字段包含与合并策略相关的XDM架构类。 有关架构和类的更多信息，请阅读[XDM文档](../../xdm/home.md)。 |
| `default` | 布尔值，指示此合并策略是否是指定架构的默认策略。 |
| `version` | [!DNL Platform] 维护的合并策略版本。每当更新合并策略时，此只读值都会递增。 |
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

[Adobe Experience Platform Identity Service](../../identity-service/home.md) 可管理全局性地使用的标识图，以及上每个组织的 [!DNL Experience Platform]标识图。合并策略的`identityGraph`属性定义如何确定用户的相关身份。

**identityGraph对象**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

其中`{IDENTITY_GRAPH_TYPE}`是以下任一值：

* **“无”：** 不执行身份拼合。
* **“pdg”：** 根据您的专用身份图执行身份拼合。

**示例`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### 属性合并 {#attribute-merge}

配置文件片段是特定用户在身份列表中仅包含一个身份的配置文件信息。 如果使用的标识图形类型导致多个标识，则可能存在冲突的配置文件属性，并且必须指定优先级。 使用`attributeMerge`，您可以指定在键值（记录数据）类型数据集之间发生合并冲突时要优先排序的配置文件属性。

**attributeMerge对象**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

其中`{ATTRIBUTE_MERGE_TYPE}`是以下任一值：

* **`timestampOrdered`**:（默认）优先于上次更新的用户档案。使用此合并类型时，不需要`data`属性。
* **`dataSetPrecedence`** :根据来自的数据集，优先考虑配置文件片段。当一个数据集中存在的信息比另一个数据集中的数据更可取或更可信时，可以使用此方法。 使用此合并类型时，需要`order`属性，因为它会按优先级顺序列出数据集。
   * **`order`**:使用“dataSetPreperance”时，必须为数 `order` 组提供数据集列表。列表中未包含的任何数据集都将不会合并。 换言之，必须明确列出数据集才能将其合并到用户档案中。 `order`数组按优先级顺序列出数据集的ID。

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

架构对象指定为其创建此合并策略的体验数据模型(XDM)架构类。

**`schema`对象**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

其中，值`name`是与合并策略关联的架构所基于的XDM类的名称。

**示例`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

要进一步了解XDM并在Experience Platform中使用架构，请首先阅读[XDM系统概述](../../xdm/home.md)。

## 访问合并策略 {#access-merge-policies}

使用[!DNL Real-time Customer Profile] API， `/config/mergePolicies`端点允许您执行查找请求以按其ID查看特定合并策略，或访问IMS组织中按特定条件过滤的所有合并策略。 您还可以使用`/config/mergePolicies/bulk-get`端点通过其ID检索多个合并策略。 以下各节概述了执行这些调用的步骤。

### 按ID访问单个合并策略

您可以通过向`/config/mergePolicies`端点发出GET请求并在请求路径中包含`mergePolicyId`来通过其ID访问单个合并策略。

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

有关构成合并策略的各个元素的详细信息，请参阅本文档开头的合并策略的[组件](#components-of-merge-policies)部分。

### 按ID检索多个合并策略

您可以通过向`/config/mergePolicies/bulk-get`端点发出POST请求并在请求正文中包含要检索的合并策略的ID来检索多个合并策略。

**API格式**

```http
POST /config/mergePolicies/bulk-get
```

**请求**

请求正文包含一个“ids”数组，其中包含您要检索其详细信息的每个合并策略的各个对象的“id”。

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

成功响应会返回HTTP状态207（多状态）以及在POST请求中提供ID的合并策略的详细信息。

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

有关构成合并策略的各个元素的详细信息，请参阅本文档开头的合并策略的[组件](#components-of-merge-policies)部分。

### 按条件列出多个合并策略

您可以在IMS组织内列出多个合并策略，方法是向`/config/mergePolicies`端点发出GET请求，并使用可选的查询参数对响应进行筛选、排序和分页。 可以包含多个参数，并以与号(&amp;)分隔。 在没有参数的情况下调用此端点将检索适用于贵组织的所有合并策略。

**API格式**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| 参数 | 描述 |
|---|---|
| `default` | 一个布尔值，用于按合并策略是否是架构类的默认策略来筛选结果。 |
| `limit` | 指定页面大小限制以控制页面中包含的结果数。 默认值：20 |
| `orderBy` | 指定将结果排序为`orderBy=name`或`orderBy=+name`的字段，以按名称升序排序，或按`orderBy=-name`降序排序。 省略此值会导致默认按升序排序`name`。 |
| `schema.name` | 用于检索可用合并策略的架构的名称。 |
| `identityGraph.type` | 按身份图表类型筛选结果。 可能的值包括“无”和“pdg”（专用图）。 |
| `attributeMerge.type` | 按使用的属性合并类型筛选结果。 可能的值包括“timestampOrdered”和“dataSetPreperance”。 |
| `start` | 页面偏移 — 指定要检索数据的起始ID。 默认值：0 |
| `version` | 如果要使用合并策略的特定版本，请指定此选项。 默认情况下，将使用最新版本。 |

有关`schema.name`、`identityGraph.type`和`attributeMerge.type`的更多信息，请参阅本指南前面提供的合并策略的[组件](#components-of-merge-policies)部分。


**请求**

以下请求列出了给定架构的所有合并策略：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**响应**

成功的响应会返回符合请求中发送的查询参数所指定条件的合并策略分页列表。

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
| `_links.next.href` | 结果下一页的URI地址。 使用此URI作为对同一端点的另一API调用的请求参数，以查看页面。 如果不存在下一页，则此值将为空字符串。 |

## 创建合并策略

您可以通过向`/config/mergePolicies`端点发出POST请求，为组织创建新的合并策略。

**API格式**

```http
POST /config/mergePolicies
```

****
请求以下请求会创建一个新的合并策略，该策略由有效负载中提供的属性值进行配置：

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
| `name` | 在列表视图中标识合并策略的人类易记名称。 |
| `identityGraph.type` | 要从中获取要合并的相关标识的标识图类型。 可能值：“无”或“pdg”（专用图）。 |
| `attributeMerge` | 在发生数据冲突时优先配置文件属性值的方式。 |
| `schema` | 与合并策略关联的XDM架构类。 |
| `default` | 指定此合并策略是否为架构的默认策略。 |

有关更多信息，请参阅合并策略的[组件](#components-of-merge-policies)一节。

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

有关构成合并策略的各个元素的详细信息，请参阅本文档开头的合并策略的[组件](#components-of-merge-policies)部分。

## 更新合并策略 {#update}

您可以通过编辑单个属性(PATCH)或使用新属性(PUT)覆盖整个合并策略来修改现有合并策略。 下面显示了每个示例。

### 编辑单个合并策略字段

通过向`/config/mergePolicies/{mergePolicyId}`端点发出PATCH请求，可以编辑合并策略的各个字段：

**API格式**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要删除的合并策略的标识符。 |

**请求**

以下请求通过将其`default`属性的值更改为`true`来更新指定的合并策略：

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
| `path` | 要更新的字段路径。 接受的值包括：&quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | 将指定字段设置为的值。 |

有关更多信息，请参阅合并策略的[组件](#components-of-merge-policies)一节。


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

以下请求将覆盖指定的合并策略，将其属性值替换为有效负载中提供的属性值。 由于此请求完全替换了现有的合并策略，因此您需要提供最初定义合并策略时所需的所有相同字段。 但是，这次您为要更改的字段提供了更新的值。

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
| `name` | 在列表视图中标识合并策略的人类易记名称。 |
| `identityGraph` | 要从中获取要合并的相关标识的标识图。 |
| `attributeMerge` | 在发生数据冲突时优先配置文件属性值的方式。 |
| `schema` | 与合并策略关联的XDM架构类。 |
| `default` | 指定此合并策略是否为架构的默认策略。 |

有关更多信息，请参阅合并策略的[组件](#components-of-merge-policies)一节。


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

通过向`/config/mergePolicies`端点发出DELETE请求并在请求路径中包含要删除的合并策略的ID，可以删除合并策略。

**API格式**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| 参数 | 描述 |
|---|---|
| `{mergePolicyId}` | 要删除的合并策略的标识符。 |

**请求**

以下请求会删除合并策略。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的删除请求会返回HTTP状态200（确定）和空的响应正文。 要确认删除成功，您可以执行GET请求以按其ID查看合并策略。 如果删除了合并策略，您将收到HTTP状态404（未找到）错误。

## 后续步骤

现在，您已了解如何为组织创建和配置合并策略，接下来可以使用这些策略来调整Platform中客户配置文件的视图，并根据[!DNL Real-time Customer Profile]数据创建受众区段。

请参阅[Adobe Experience Platform Segmentation Service文档](../../segmentation/home.md)以开始定义和使用区段。
