---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: 使用策略服务API实施数据使用策略
topic: enforcement
description: 为数据创建数据使用标签并针对这些标签创建市场营销操作的使用策略后，您可以使用策略服务API评估对数据集或任意标签组执行的市场营销操作是否构成策略违规。 然后，您可以设置自己的内部协议，根据API响应处理策略违规。
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---


# 使用API实施数据使用策 [!DNL Policy Service] 略

为数据创建数据使用标签并针对这些标签创建市场营销操作的使用策略后，您可以使用 [[!DNL策略服务API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) ，评估对数据集或任意标签组执行的营销操作是否构成策略违规。 然后，您可以设置自己的内部协议，根据API响应处理策略违规。

>[!NOTE]
>
>默认情况下，只有状态设置为的策略才 `ENABLED` 能参与评估。 要允许 `DRAFT` 策略参与评估，必须在请求路径中包含 `includeDraft=true` 查询参数。

此文档提供了如何使用API检查 [!DNL Policy Service] 不同情况下是否存在策略违规的步骤。

## 入门指南

本教程需要对实施数据使用策略涉及的下列主要概念有一个有效的了解：

* [数据治理](../home.md):强制执行数据使 [!DNL Platform] 用合规性的框架。
   * [数据使用标签](../labels/overview.md):数据使用标签被应用到数据集（和／或这些数据集中的单个字段），从而指定如何使用该数据的限制。
   * [数据使用策略](../policies/overview.md):数据使用策略是描述某些数据使用标签集允许或限制的营销操作类型的规则。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

在开始本教程之前，请查阅开发 [人员指南](../api/getting-started.md) ，了解成功调用API所需的重要信息，包括必需的头 [!DNL Policy Service] 以及如何读取示例API调用。

## 使用标签和营销操作进行评估

您可以根据数据集中假设存在的一组数据使用标签测试营销操作，从而评估策略。 这是通过使用查询参数来完 `duleLabels` 成的，其中标签以逗号分隔的值列表形式提供，如下例所示。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 与您正在评估的数据使用策略关联的营销操作的名称。 |
| `{LABEL_1}` | 用于测试营销操作的数据使用标签。 必须至少提供一个标签。 提供多个标签时，必须用逗号分隔。 |

**请求**

以下请求会根据标 `exportToThirdParty` 签和测试营销 `C1` 操作 `C3`。 由于您在本教程前面创建的数据使用策略将标 `C1` 签定义为其策略表达式 `deny` 中的一个条件，因此营销操作应触发策略违规。

>[!NOTE]
>
>数据使用标签区分大小写。 只有在策略表达式中定义的标签完全匹配时，才会发生策略违规。 在此示例中，标 `C1` 签将触发违规，而标 `c1` 签则不会触发。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回营销操作的URL、测试所针对的使用标签以及测试针对这些标签的操作而违反的任何策略的列表。 在此示例中，阵列中显示“将数据导出到第三方”策 `violatedPolicies` 略，表明营销操作触发了预期的策略违规。

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
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
| `violatedPolicies` | 一个数组，其中列出了根据提供的测试营销操作（在中指定） `marketingActionRef`所违反的任何策略 `duleLabels`。 |

## 使用数据集进行评估

您可以通过针对一个或多个可从中收集标签的数据集测试营销操作来评估数据使用策略。 这是通过向请求主体发出POST `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` 请求并在请求主体中提供数据集ID来完成的，如下例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 与要评估的策略关联的营销操作的名称。 |

**请求**

以下请求针对三个不 `exportToThirdParty` 同的数据集测试营销操作。 数据集由负载中提供的数组中的类型和ID引用。

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
      "entityId": "5c423dc25f2f2e00005e2319"
    },
    {
      "entityType": "dataSet",
      "entityId": "5cc323e15410ef14b749481e"
    },
    {
      "entityType": "dataSet",
      "entityId": "5cc1fb685410ef14b748c55f"
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `entityType` | 有效负荷数组中的每个项目都必须指示所定义实体的类型。 对于此用例，值将始终为“dataSet”。 |
| `entityId` | 有效负荷数组中的每个项目都必须为数据集提供唯一ID。 |

**响应**

成功的响应会返回营销操作的URL、从提供的数据集收集的使用标签以及针对这些标签测试操作而违反的任何策略的列表。 在此示例中，阵列中显示“将数据导出到第三方”策 `violatedPolicies` 略，表明营销操作触发了预期的策略违规。

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
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
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
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
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
            "entityId": "5cc1fb685410ef14b748c55f",
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
| `duleLabels` | 从请求有效负荷中提供的数据集提取的列表数据使用标签。 |
| `discoveredLabels` | 请求有效负荷中提供的数据集的列表，显示在每个数据集中找到的数据集级别和字段级别标签。 |
| `violatedPolicies` | 一个数组，其中列出了根据提供的测试营销操作（在中指定） `marketingActionRef`所违反的任何策略 `duleLabels`。 |

## 后续步骤

通过阅读此文档，您已成功检查在数据集或数据集使用标签集上执行营销操作时是否存在策略违规。 使用API响应中返回的数据，您可以在体验应用程序中设置协议以在发生策略违规时相应地强制实施这些违规。

有关如何为中的受众段实施数据使用策略的 [!DNL Real-time Customer Profile]步骤，请参阅以下 [教程](../../segmentation/tutorials/governance.md)。