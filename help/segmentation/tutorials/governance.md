---
solution: Experience Platform
title: 使用API对受众区段强制执行数据使用合规性
type: Tutorial
description: 本教程介绍了使用API实施数据使用合规性区段定义的步骤。
exl-id: 2299328c-d41a-4fdc-b7ed-72891569eaf2
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 1%

---

# 使用API强制区段定义的数据使用合规性

本教程介绍了使用API为区段定义强制实施数据使用合规性的步骤。

## 快速入门

本教程需要对以下组件有一定的了解 [!DNL Adobe Experience Platform]：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)： [!DNL Real-Time Customer Profile] 是一个通用查找实体存储，用于管理 [!DNL Experience Data Model (XDM)] 数据范围 [!DNL Platform]. 配置文件可以跨各种企业数据资产合并数据，并在统一的演示文稿中提供对这些数据的访问。
   - [合并策略](../../profile/api/merge-policies.md)：使用的规则 [!DNL Real-Time Customer Profile] 以确定在特定条件下可以将哪些数据合并到统一视图中。 可以为数据管理目的配置合并策略。
- [[!DNL Segmentation]](../home.md)：方法 [!DNL Real-Time Customer Profile] 将个人资料存储中包含的大量个人划分为较小的个人群组，这些个人群组具有相似的特征，并且将对营销策略的响应类似。
- [数据管理](../../data-governance/home.md)：数据管理使用以下组件为数据使用标签和强制执行提供基础架构：
   - [数据使用情况标签](../../data-governance/labels/user-guide.md)：用于根据处理数据集和字段各自数据的敏感度级别描述数据集和字段的标签。
   - [数据使用策略](../../data-governance/policies/overview.md)：指示允许对按特定数据使用标签分类的数据执行哪些营销操作的配置。
   - [策略实施](../../data-governance/enforcement/overview.md)：用于实施数据使用策略并阻止构成策略违规的数据操作。
- [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功调用 [!DNL Platform] API。

### 正在读取示例API调用

本教程提供了示例API调用来演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

- Content-Type： application/json

## 查找区段定义的合并策略 {#merge-policy}

此工作流从访问已知的区段定义开始。 已启用以便在中使用的区段定义 [!DNL Real-Time Customer Profile] 在其区段定义中包含合并策略ID。 此合并策略包含有关区段定义中将包含哪些数据集的信息，而这些数据集又包含任何适用的数据使用标签。

使用 [!DNL Segmentation] API中，您可以根据区段的ID查找区段定义，以查找与其关联的合并策略。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回区段定义的详细信息。

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{ORG_ID}",
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
| `mergePolicyId` | 用于区段定义的合并策略的ID。 这将在下一步中使用。 |

## 从合并策略中查找源数据集 {#datasets}

合并策略包含有关其源数据集的信息，而这些源数据集又包含数据使用标签。 您可以通过在向提供的GET请求中提供合并策略ID来查找合并策略的详细信息 [!DNL Profile] API。 有关合并策略的更多信息，请参阅 [合并策略端点指南](../../profile/api/merge-policies.md).

**API格式**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | 在中获取的合并策略的ID [上一步](#merge-policy). |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回合并策略的详细信息。

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{ORG_ID}",
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
            "order": ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `schema.name` | 与合并策略关联的架构的名称。 |
| `attributeMerge.type` | 合并策略的数据优先配置类型。 如果值为 `dataSetPrecedence`，则与此合并策略关联的数据集将列在 `attributeMerge > data > order`. 如果值为 `timestampOrdered`，然后是与中引用的架构关联的所有数据集 `schema.name` 由合并策略使用。 |
| `attributeMerge.data.order` | 如果 `attributeMerge.type` 是 `dataSetPrecedence`，则此属性将是一个数组，其中包含此合并策略所使用的数据集的ID。 这些ID将在下一步中使用。 |

## 评估策略违规的数据集

>[!NOTE]
>
> 此步骤假定您至少有一个有效的数据使用策略，该策略阻止对包含特定标签的数据执行特定营销操作。 如果您对于正在评估的数据集没有任何适用的使用策略，请按照 [策略创建教程](../../data-governance/policies/create.md) ，以便在继续此步骤之前创建一个。

获取合并策略的源数据集的ID后，您可以使用 [策略服务API](https://www.adobe.io/experience-platform-apis/references/policy-service/) 根据特定的营销操作评估这些数据集，以检查是否存在数据使用策略违规。

要评估数据集，必须在POST请求的路径中提供营销操作的名称，同时在请求正文中提供数据集ID，如以下示例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 与作为数据集评估依据的数据使用策略关联的营销操作的名称。 根据策略是由Adobe还是贵组织定义，您必须使用 `/marketingActions/core` 或 `/marketingActions/custom`，则不会显示任何内容。 |

**请求**

以下请求将测试 `exportToThirdParty` 针对中获取的数据集执行营销操作 [上一步](#datasets). 请求有效负载是一个数组，其中包含每个数据集的ID。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | 有效负载数组中的每个项目都必须指示所定义的实体类型。 对于此用例，值将始终为“dataSet”。 |
| `entityID` | 有效负载数组中的每一项都必须提供数据集的唯一ID。 |

**响应**

成功响应将返回营销操作的URI、从提供的数据集收集的数据使用标签，以及由于针对这些标签测试操作而违反的任何数据使用策略的列表。 在此示例中，“将数据导出到第三方”策略显示在 `violatedPolicies` 数组，指示营销操作触发了策略冲突。

```json
{
  "timestamp": 1556324277895,
  "clientId": "{CLIENT_ID}",
  "userId": "{USER_ID}",
  "imsOrg": "{ORG_ID}",
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
      "imsOrg": "{ORG_ID}",
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
| `duleLabels` | 从提供的数据集中提取的数据使用标签列表。 |
| `discoveredLabels` | 请求有效负载中提供的数据集列表，显示可在每个有效负载中找到的数据集级别和字段级别标签。 |
| `violatedPolicies` | 一个数组，其中列出了测试营销操作所违反的任何数据使用策略(在 `marketingActionRef`)根据提供的 `duleLabels`. |

使用API响应中返回的数据，您可以在体验应用程序中设置协议，以便在发生策略违规时适当地实施这些违规。

## 筛选数据字段

如果区段定义未通过评估，则可通过下面列出的两种方法之一调整区段定义中包含的数据。

### 更新区段定义的合并策略

更新区段定义的合并策略将调整运行区段作业时将包含的数据集和字段。 请参阅以下部分： [更新现有合并策略](../../profile/api/merge-policies.md#update) 有关更多信息，请参阅API合并策略教程。

### 导出区段定义时限制特定数据字段

使用将区段定义导出到数据集时 [!DNL Segmentation] API中，您可以使用来筛选导出中包含的数据 `fields` 参数。 添加到此参数的任何数据字段都将包含在导出中，而所有其他数据字段将被排除。

考虑具有名为“A”、“B”和“C”的数据字段的区段定义。 如果您只想导出字段“C”，则 `fields` 参数将仅包含字段“C”。 这样，在导出区段定义时将排除字段“A”和“B”。

请参阅以下部分： [导出区段定义](./evaluate-a-segment.md#export) 有关更多信息，请参阅分段教程。

## 后续步骤

通过阅读本教程，您已查找与区段定义关联的数据使用标签，并测试它们是否存在违反特定营销操作的策略。 有关“数据管理”的更多信息，请参阅 [!DNL Experience Platform]，请阅读 [数据管理](../../data-governance/home.md).
