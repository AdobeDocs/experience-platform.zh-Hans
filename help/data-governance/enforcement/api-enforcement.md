---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Policy Service API强制实施数据使用策略
topic: enforcement
translation-type: tm+mt
source-git-commit: 3e5245a718295cc5318c277a5cf9ee71da2a911b

---


# 使用Policy Service API强制实施数据使用策略

为数据创建数据使用标签并针对这些标签创建市场营销操作的使用策略后，您便可以使用 [DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) ，评估对数据集或任意标签组执行的营销操作是否构成策略违规。 然后，您可以设置自己的内部协议，以根据API响应处理策略违规。

>[!NOTE] 默认情况下，只有状态设置为的策略才 `ENABLED` 能参与评估。 要允许 `DRAFT` 策略参与评估，您必须在请求路径中包 `includeDraft=true` 含查询参数。

本文档提供了如何使用策略服务API检查不同情况下的策略违规的步骤。

## 入门指南

本教程需要对实施DULE策略涉及的下列主要概念有充分的了解：

* [数据管理](../home.md):平台执行数据使用合规性的框架。
   * [数据使用标签](../labels/overview.md):数据使用标签被应用到数据集（和／或这些数据集中的单个字段），从而指定数据的使用方式限制。
   * [数据使用策略](../policies/overview.md):数据使用策略是描述某些DULE标签集允许或限制的营销操作类型的规则。
* [沙箱](../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

在开始本教程之前，请查看开发人员指 [南](../api/getting-started.md) ，了解成功调用DULE Policy Service API需要了解的重要信息，包括必需的标题以及如何读取示例API调用。

## 使用DULE标签和营销操作进行评估

您可以根据数据集中假设存在的一组DULE标签测试营销操作，从而评估策略。 这是通过使用 `duleLabels` 查询参数实现的，其中DULE标签以逗号分隔的值列表提供，如下例所示。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 与您评估的DULE策略关联的营销操作的名称。 |
| `{LABEL_1}` | 用于测试营销操作的数据使用标签。 必须提供至少一个标签。 提供多个标签时，必须用逗号分隔。 |

**请求**

以下请求会针对标签 `exportToThirdParty` 和测试营销 `C1` 操作 `C3`。 由于您在本教程前面创建的数据使用策略将标签定义为其策略表达式中的一个条件 `C1``deny` ，因此营销操作应触发策略违规。

>[!NOTE] 数据使用标签区分大小写。 仅当策略表达式中定义的标签完全匹配时，才会发生策略违规。 在此示例中，标签 `C1` 将触发违规，而标签则 `c1` 不会触发违规。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回营销操作的URL、测试所针对的DULE标签以及测试针对这些标签的操作而违反的任何DULE策略的列表。 在此示例中，“将数据导出到第三方”策略显示在数组中，表 `violatedPolicies` 明营销操作触发了预期的策略违规。

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
| `violatedPolicies` | 一个数组，列出了根据提供的内容测试营销操作（在中指定）所违反 `marketingActionRef`的任何DULE策略 `duleLabels`。 |

## 使用数据集评估

您可以通过针对一个或多个数据集测试营销操作来评估DULE策略，这些数据集可以从中收集DULE标签。 这是通过向请求主体中的POST请 `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` 求和提供数据集ID来完成的，如下例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 与您评估的DULE策略关联的营销操作的名称。 |

**请求**

以下请求针对三个不 `exportToThirdParty` 同的数据集测试营销操作。 数据集按有效负荷中提供的数组中的类型和ID引用。

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
| `entityId` | 有效负荷数组中的每个项目都必须提供数据集的唯一ID。 |

**响应**

成功的响应会返回营销操作的URL、从提供的数据集收集的DULE标签以及因针对这些标签测试操作而违反的任何DULE策略的列表。 在此示例中，“将数据导出到第三方”策略显示在数组中，表 `violatedPolicies` 明营销操作触发了预期的策略违规。

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
| `duleLabels` | 从请求有效负荷中提供的数据集提取的DULE标签列表。 |
| `discoveredLabels` | 请求有效负荷中提供的数据集的列表，显示在每个数据集级别和字段级别DULE标签中找到的数据集级别。 |
| `violatedPolicies` | 一个数组，列出了根据提供的内容测试营销操作（在中指定）所违反 `marketingActionRef`的任何DULE策略 `duleLabels`。 |

## 后续步骤

通过阅读此文档，您成功检查了在数据集或一组DULE标签上执行营销操作时是否有策略违规。 使用API响应中返回的数据，您可以在体验应用程序中设置协议，以在发生策略违规时相应地强制执行这些违规。

有关如何在实时客户用户档案中为受众区段实施数据使用策略的步骤，请参阅以下教 [程](../../segmentation/tutorials/governance.md)。