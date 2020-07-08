---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 为受众区段强制实施数据使用合规性
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 1%

---


# 使用API为受众区段强制实施数据使用合规性

本教程介绍了使用API强制实时客户用户档案受众细分的数据使用合规性的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

- [实时客户用户档案](../../profile/home.md): 实时客户用户档案是通用的查找实体存储，用于管理平台内的体验数据模型(XDM)数据。 用户档案可以跨各种企业数据资产合并数据，并以统一的表示形式提供对该数据的访问。
   - [合并策略](../../profile/api/merge-policies.md): 实时客户用户档案使用的规则，确定哪些数据可以在特定条件下合并为一个统一视图。 可以为“数据管理”配置合并策略。
- [细分](../home.md): 实时用户档案如何将用户档案商店中包含的大量个人划分为具有相似特征并将对营销策略做出类似反应的较小群体。
- [数据治理](../../data-governance/home.md): Data Governance使用以下组件为数据使用标签和执行(DULE)提供了基础架构：
   - [数据使用标签](../../data-governance/labels/user-guide.md): 标签用于根据处理数据集和字段各自数据的敏感程度描述数据集和字段。
   - [数据使用策略](../../data-governance/policies/overview.md): 配置，指示允许对按特定数据使用标签分类的数据执行哪些营销操作。
   - [策略实施](../../data-governance/enforcement/overview.md): 允许您实施数据使用策略并防止构成违反策略的数据操作。
- [沙箱](../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的章节。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型： application/json

## 查找区段定义的合并策略 {#merge-policy}

此工作流首先访问已知的受众段。 在实时客户用户档案中启用的区段在其区段定义中包含一个合并策略ID。 此合并策略包含有关区段中要包含哪些数据集的信息，这些数据集又包含任何适用的数据使用标签。

使用 [分段API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)，您可以按其ID查找段定义以找到其关联的合并策略。

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
| `mergePolicyId` | 用于段定义的合并策略的ID。 此操作将用于下一步。 |

## 从合并策略中查找源数据集 {#datasets}

合并策略包含有关其源数据集的信息，而源数据集又包含数据使用标签。 您可以通过在GET请求中向用户档案API提供合并策略ID来查找合并策略的详细信息。

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在上一步中获取的合并策略 [的ID](#merge-policy)。 |

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
| `attributeMerge.type` | 合并策略的数据优先级配置类型。 如果值为， `dataSetPrecedence`则与此合并策略关联的数据集将列在 `attributeMerge > data > order`下。 如果值为， `timestampOrdered`则与中引用的模式关联的所 `schema.name` 有数据集将由合并策略使用。 |
| `attributeMerge.data.order` | 如果 `attributeMerge.type` 为 `dataSetPrecedence`，则此属性将是包含此合并策略所使用数据集的ID的数组。 这些ID将用于下一步。 |

## 评估数据集中是否存在策略违规

>[!NOTE]
>
> 此步骤假定您至少有一个活动数据使用策略，该策略可阻止对包含特定标签的数据执行特定营销操作。 如果您对要评估的数据集没有任何适用的使用策略，请按照策略 [创建教程](../../data-governance/policies/create.md) ，先创建一个策略，然后继续此步骤。

获得合并策略的源数据集的ID后，您可以使用 [DULE Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) API根据特定营销操作评估这些数据集，以检查数据使用策略违规。

要评估数据集，您必须在POST请求路径中提供营销操作的名称，同时在请求主体中提供数据集ID，如下例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 与要评估数据集的数据使用策略关联的营销操作的名称。 根据策略是由Adobe还是您的组织定义，您必须分别使 `/marketingActions/core` 用 `/marketingActions/custom`或使用。 |

**请求**

以下请求将针对上 `exportToThirdParty` 一步中获取的数据集测试 [营销操作](#datasets)。 请求有效负荷是包含每个数据集ID的数组。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780"
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df"
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `entityType` | 有效负荷数组中的每个项目都必须指示所定义实体的类型。 对于此用例，值将始终为“dataSet”。 |
| `entityID` | 有效负荷数组中的每个项目都必须为数据集提供唯一ID。 |

**响应**

成功的响应会返回营销操作的URI、从提供的数据集收集的数据使用标签，以及测试针对这些标签的操作而违反的任何数据使用策略的列表。 在此示例中，阵列中显示“将数据导出到第三方” `violatedPolicies` 策略，表明营销操作触发了策略违规。

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{IMS_ORG}",
  "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
  "duleLabels": [
    "C1",
    "C2",
    "C4",
    "C5"
  ],
  "discoveredLabels": [
    {
      "entityType": "dataSet",
      "entityId": "5b95b155419ec801e6eee780",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C2",
            ],
            "path": "/properties/_customer"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/geoUnit"
          },
          {
            "labels": [
              "C1"
            ],
            "path": "/properties/identityMap"
          }
        ]
      }
    },
    {
      "entityType": "dataSet",
      "entityId": "5b7c86968f7b6501e21ba9df",
      "dataSetLabels": {
        "connection": {
          "labels": []
        },
        "dataSet": {
          "labels": [
            "C5"
          ]
        },
        "fields": [
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/createdByBatchID"
          },
          {
            "labels": [
              "C5"
            ],
            "path": "/properties/faxPhone"
          }
        ]
      }
    }
  ],
  "violatedPolicies": [
    {
      "name": "Export Data to Third Party",
      "status": "ENABLED",
      "marketingActionRefs": [
        "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
      ],
      "description": "Conditions under which data cannot be exported to a third party",
      "deny": {
        "operator": "OR",
        "operands": [
          {
            "label": "C1"
          },
          {
            "operator": "AND",
            "operands": [
              {
                "label": "C3"
              },
              {
                "label": "C7"
              }
            ]
          }
        ]
      },
      "imsOrg": "{IMS_ORG}",
      "created": 1565651746693,
      "createdClient": "{CREATED_CLIENT}",
      "createdUser": "{CREATED_USER",
      "updated": 1565723012139,
      "updatedClient": "{UPDATED_CLIENT}",
      "updatedUser": "{UPDATED_USER}",
      "_links": {
        "self": {
          "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
        }
      },
      "id": "5d51f322e553c814e67af1a3"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `duleLabels` | 从提供的数据集提取的列表数据使用标签。 |
| `discoveredLabels` | 请求有效负荷中提供的数据集的列表，显示在每个数据集中找到的数据集级别和字段级别标签。 |
| `violatedPolicies` | 一个数组，其中列出了根据提供的测试营销操作（在中指定）所违反 `marketingActionRef`的任何数据使用策略 `duleLabels`。 |

使用API响应中返回的数据，您可以在体验应用程序中设置协议以在发生策略违规时相应地强制实施这些违规。

## 筛选数据字段

如果您的受众细分未通过评估，您可以通过以下两种方法之一调整该细分中包含的数据。

### 更新段定义的合并策略

更新区段定义的合并策略将调整运行区段作业时将包含的数据集和字段。 有关详细信息， [请参阅API合并策略教程](../../profile/api/merge-policies.md#update) 中有关更新现有合并策略的部分。

### 导出区段时限制特定数据字段

使用实时客户用户档案API将区段导出到数据集时，可以使用参数过滤导出中包含的 `fields` 数据。 添加到此参数的所有数据字段都将包含在导出中，而所有其他数据字段将被排除。

考虑具有名为“A”、“B”和“C”的数据字段的区段。 如果只希望导出字段“C”，则参 `fields` 数将仅包含字段“C”。 通过执行此操作，导出区段时将排除字段“A”和“B”。

有关详细信息，请 [参阅分段教程](./evaluate-a-segment.md#export) 中有关导出区段的部分。

## 后续步骤

通过遵循本教程，您查找了与受众区段关联的数据使用标签，并测试了它们是否存在针对特定营销操作的违反策略的情况。 有关Experience Platform中的数据治理的更多信息，请参阅 [数据治理概述](../../data-governance/home.md)。
