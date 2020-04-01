---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 为受众细分强制实施数据使用合规性
topic: tutorial
translation-type: tm+mt
source-git-commit: 76032cca825eb75f7a8056cbbbc230343bed27a0

---


# 使用API为受众细分强制实施数据使用合规性

本教程介绍了使用API强制实时客户用户档案受众细分的数据使用合规性的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [实时客户用户档案](../../profile/home.md):实时客户用户档案是通用的查找实体存储，用于管理平台内的体验数据模型(XDM)数据。 用户档案将各种企业数据资产中的数据合并在一起，并以统一的形式提供对这些数据的访问。
   - [合并策略](../../profile/api/merge-policies.md):实时客户用户档案用来确定哪些数据在特定条件下可以合并到统一视图的规则。 可以为数据管理目的配置合并策略。
- [细分](../home.md):实时客户用户档案如何将用户档案商店中包含的大量个人分成小组，这些小组具有相似的特征并将对营销策略作出类似的响应。
- [数据管理](../../data-governance/home.md):Data Governance使用以下组件为数据使用标签和强制实施(DULE)提供了基础架构：
   - [数据使用标签](../../data-governance/labels/user-guide.md):用于根据处理数据集和字段各自数据的敏感程度描述数据集和字段的标签。
   - [数据使用策略](../../data-governance/api/getting-started.md):指示允许对按特定数据使用标签分类的数据执行哪些营销操作的配置。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

> [!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

## 查找区段定义的合并策略

此工作流首先访问已知的受众区段。 在实时客户用户档案中启用的区段在其区段定义中包含合并策略ID。 此合并策略包含有关区段中要包含哪些数据集的信息，这些数据集又包含任何适用的数据使用标签。

使用实 [时客户用户档案API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)，您可以按其ID查找区段定义以查找其关联的合并策略。

**API格式**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 要查找的区段定义的ID。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回区段定义的详细信息。

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{IMS_ORG}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `mergePolicyId` | 用于区段定义的合并策略的ID。 此选项将用于下一步。 |

## 从合并策略中查找源数据集

合并策略包含有关其源数据集的信息，这些信息又包含DULE标签。 通过向用户档案API提供GET请求中的合并策略ID，可以查找合并策略的详细信息。

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在上一步中获取的合并策略 [的ID](#lookup-a-merge-policy-for-a-segment-definition)。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回合并策略的详细信息。

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `schema.name` | 与合并策略关联的模式的名称。 |
| `attributeMerge.type` | 合并策略的数据优先级配置类型。 如果值为， `dataSetPrecedence`则与此合并策略关联的数据集将列在下 `attributeMerge > data > order`。 如果值为， `timestampOrdered`则与中引用的模式关联的所有数据集 `schema.name` 都将被合并策略使用。 |
| `attributeMerge.data.order` | 如果 `attributeMerge.type` 为， `dataSetPrecedence`则此属性将是包含此合并策略所使用的数据集ID的数组。 这些ID将用于下一步。 |

## 查找源数据集的数据使用标签

收集合并策略的源数据集的ID后，您可以使用这些ID查找为数据集本身配置的数据使用标签以及其中包含的任何特定数据字段。

以下对 [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catalog Service API的调用通过在请求路径中提供单个数据集的ID来检索与单个数据集关联的数据使用标签：

**API格式**

```http
GET /dataSets/{DATASET_ID}/dule
```

| 属性 | 描述 |
| -------- | ----------- |
| `{DATASET_ID}` | 要查找其数据使用标签的数据集的ID。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回与整个数据集相关联的数据使用标签的列表，以及与源模式相关联的任何特定数据字段。

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `dataset` | 一个对象，其中包含应用于整个数据集的数据使用标签。 |
| `schemaFields` | 表示已应用数据使用标签的特定模式字段的对象数组。 |
| `schemaFields.path` | 其数据使用标签列在同一对象中的模式字段的路径。 |

## 过滤数据字段

> [!NOTE] 此步骤是可选的。 如果您不希望根据您在查找数据使用标签的上一步中的发现调整区段中包含的数据 [](#lookup-data-usage-labels-for-the-source-datasets)，您可以跳到评估数据是否违反策略的最 [后一步](#evaluate-data-for-policy-violations)。

如果您希望调整包含在受众区段中的数据，可以使用以下两种方法之一进行调整：

### 更新区段定义的合并策略

更新区段定义的合并策略将调整运行区段作业时将包含的数据集和字段。 有关详细信息，请 [参阅合并策略教程中有关更新现有合并策略的部分](../../profile/api/merge-policies.md) 。

### 导出区段时限制特定数据字段

使用实时客户用户档案API将区段导出到数据集时，您可以使用参数过滤导出中包含的数 `fields` 据。 添加到此参数的所有数据字段都将包含在导出中，而所有其他数据字段将被排除。

请考虑具有名为“A”、“B”和“C”的数据字段的区段。 如果您希望仅导出字段“C”，则该参 `fields` 数将仅包含字段“C”。 通过执行此操作，导出区段时将排除字段“A”和“B”。

有关详细信息，请 [参阅分段教程中](./evaluate-a-segment.md#export-a-segment) ，有关导出区段的部分。

## 评估违反策略的数据

现在，您已收集了与您的受众细分关联的数据使用标签，可以根据营销操作测试这些标签，以评估是否存在任何数据使用策略违规。 有关如何使用 [DULE Policy Service API执行策略评估的详细步骤](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)，请参阅策略评估 [文档](../../data-governance/enforcement/overview.md)。

## 后续步骤

通过本教程，您查找了与受众细分关联的数据使用标签，并测试了这些标签是否存在针对特定营销操作的策略违规。 有关Experience Platform中的数据管理的详细信息，请参阅数 [据管理概述](../../data-governance/home.md)。