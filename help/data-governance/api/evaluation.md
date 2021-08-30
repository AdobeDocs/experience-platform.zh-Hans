---
keywords: Experience Platform；主页；热门主题；策略执行；自动执行；基于API的执行；数据管理
solution: Experience Platform
title: 策略评估API端点
topic-legacy: developer guide
description: 创建营销操作并定义策略后，可以使用策略服务API来评估某些操作是否违反了任何策略。 返回的约束采用一组策略的形式，这些策略会尝试对包含数据使用标签的指定数据执行营销操作而违反。
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 1%

---

# 策略评估端点

创建营销操作并定义策略后，您可以使用[!DNL Policy Service] API评估某些操作是否违反了任何策略。 返回的约束采用一组策略的形式，这些策略会尝试对包含数据使用标签的指定数据执行营销操作而违反。

默认情况下，只有状态设置为`ENABLED`的策略才参与评估。 但是，您可以使用查询参数`?includeDraft=true`在评估中包含`DRAFT`策略。

评估请求可以采用以下三种方式之一：

1. 如果执行了营销操作和一组数据使用标签，该操作是否会违反任何策略？
1. 如果执行了营销操作并设置了一个或多个数据集，该操作是否会违反任何策略？
1. 如果执行营销操作、一个或多个数据集以及每个数据集中一个或多个字段的子集，该操作是否会违反任何策略？

## 快速入门

本指南中使用的API端点是[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)的一部分。 在继续操作之前，请查阅[快速入门指南](./getting-started.md) ，以获取相关文档的链接、本文档中API调用示例的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需标头的重要信息。

## 使用数据使用情况标签评估策略违规 {#labels}

您可以使用GET请求中的`duleLabels`查询参数，根据存在一组特定的数据使用标签来评估是否存在策略违规。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要针对一组数据使用情况标签进行测试的营销操作的名称。 您可以通过向营销操作端点发出[GET请求](./marketing-actions.md#list)来检索可用营销操作的列表。 |
| `{LABELS_LIST}` | 以逗号分隔的数据使用标签名称列表，用于测试针对的营销操作。 例如：`duleLabels=C1,C2,C3`<br><br>请注意，标签名称区分大小写。 在`duleLabels`参数中列出这些参数时，请确保使用正确的大小写。 |

**请求**

以下示例请求会评估针对标签C1和C3的营销操作。

>[!IMPORTANT]
>
>请注意策略表达式中的`AND`和`OR`运算符。 在以下示例中，如果请求中单独显示了标签（`C1`或`C3`），则营销操作不会违反此策略。 需要两个标签（`C1`和`C3`）才能返回违反的策略。 请确保您仔细评估策略并同等谨慎地定义策略表达式。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包含`violatedPolicies`数组，其中包含因对提供的标签执行营销操作而违反的策略的详细信息。 如果未违反任何策略，则`violatedPolicies`阵列将为空。

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
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
            "created": 1550703519823,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## 使用数据集评估策略违规情况 {#datasets}

您可以根据可从中收集数据使用情况标签的一组一个或多个数据集来评估是否存在策略违规。 这是通过向特定营销操作的`/constraints`端点执行POST请求并在请求正文中提供数据集ID列表来完成的。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要针对一个或多个数据集测试的营销操作的名称。 您可以通过向营销操作端点发出[GET请求](./marketing-actions.md#list)来检索可用营销操作的列表。 |

**请求**

以下请求对一组三个数据集执行`crossSiteTargeting`营销操作，以评估是否存在任何策略违规。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
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
| `entityType` | 其ID在同级`entityId`属性中指示的实体类型。 目前，唯一接受的值是`dataSet`。 |
| `entityId` | 测试针对的营销操作的数据集的ID。 通过向[!DNL Catalog Service] API中的`/dataSets`端点发出GET请求，可以获取数据集及其相应ID的列表。 有关更多信息，请参阅[listing [!DNL Catalog] objects](../../catalog/api/list-objects.md)上的指南。 |

**响应**

成功响应包含`violatedPolicies`数组，其中包含对提供的数据集执行营销操作时违反的策略的详细信息。 如果未违反任何策略，则`violatedPolicies`阵列将为空。

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
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
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `duleLabels` | 响应对象包括一个`duleLabels`数组，其中包含在指定数据集中找到的所有标签的统一列表。 此列表包含数据集内所有字段的数据集级别和字段级别标签。 |
| `discoveredLabels` | 响应中还包含一个`discoveredLabels`数组，其中包含每个数据集的对象，该数组显示了按数据集和字段级别标签划分的`datasetLabels`。 每个字段级别的标签都显示带有该标签的特定字段的路径。 |

## 使用特定数据集字段评估策略违规情况 {#fields}

您可以根据一个或多个数据集中的字段子集评估策略违规情况，以便仅评估应用了这些字段的数据使用标签。

在使用数据集字段评估策略时，请牢记以下几点：

* **字段名称区分大小写**:提供字段时，必须完全按照数据集中显示的方式写入它们(例如， `firstName` 与 `firstname`)。
* **数据集标签继承**:数据集中的单个字段将继承在数据集级别应用的任何标签。如果策略评估未按预期返回，请务必检查除字段级别应用的标签外，是否还有可能从数据集级别继承到字段的任何标签。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要针对数据集字段子集进行测试的营销操作的名称。 您可以通过向营销操作端点发出[GET请求](./marketing-actions.md#list)来检索可用营销操作的列表。 |

**请求**

以下请求会对属于三个数据集的特定字段集测试营销操作`crossSiteTargeting`。 负载类似于[评估请求，仅涉及数据集](#datasets)，用于为每个数据集添加特定字段以从中收集标签。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| 属性 | 描述 |
| --- | --- |
| `entityType` | 其ID在同级`entityId`属性中指示的实体类型。 目前，唯一接受的值是`dataSet`。 |
| `entityId` | 要针对营销操作评估其字段的数据集的ID。 通过向[!DNL Catalog Service] API中的`/dataSets`端点发出GET请求，可以获取数据集及其相应ID的列表。 有关更多信息，请参阅[listing [!DNL Catalog] objects](../../catalog/api/list-objects.md)上的指南。 |
| `entityMeta.fields` | 数据集架构中特定字段的路径数组，以JSON指针字符串形式提供。 有关这些字符串已接受语法的详细信息，请参阅API基础知识指南中[JSON指针](../../landing/api-fundamentals.md#json-pointer)部分。 |

**响应**

成功的响应包含一个`violatedPolicies`数组，其中包含对提供的数据集字段执行营销操作时违反的策略的详细信息。 如果未违反任何策略，则`violatedPolicies`阵列将为空。

将下面的示例响应与仅涉及数据集](#datasets)的[响应进行比较，请注意收集的标签列表会比较短。 每个数据集的`discoveredLabels`也已减少，因为它们只包含请求正文中指定的字段。 此外，之前违反的策略`Targeting Ads or Content`要求同时显示`C4 AND C6`标签，因此不再违反空`violatedPolicies`数组所指示的标签。

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
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
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
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
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## 批量评估策略 {#bulk}

`/bulk-eval`端点允许您在单个API调用中运行多个评估作业。

**API格式**

```http
POST /bulk-eval
```

**请求**

批量评估请求的有效负载应为对象数组；每个要执行的评估作业各执行一个。 对于根据数据集和字段进行评估的作业，必须提供`entityList`数组。 对于根据数据使用标签评估的作业，必须提供`labels`数组。

>[!WARNING]
>
>如果列出的任何评估作业同时包含`entityList`和`labels`数组，则会导致错误。 如果您要根据数据集和标签来评估同一营销操作，则必须为该营销操作包含单独的评估作业。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| 属性 | 描述 |
| --- | --- |
| `evalRef` | 针对标签或数据集测试策略违规的营销操作的URI。 |
| `includeDraft` | 默认情况下，只有启用的策略才会参与评估。 如果将`includeDraft`设置为`true`，则处于`DRAFT`状态的策略也将参与。 |
| `labels` | 用于测试营销操作的数据使用标签数组。<br><br>**重要信息**:使用此属性时， `entityList` 属性不得包含在同一对象中。要使用数据集和/或字段评估同一营销操作，必须在包含`entityList`数组的请求有效负载中包含一个单独的对象。 |
| `entityList` | 数据集中的数据集数组和（可选）特定字段，用于测试针对的营销操作。<br><br>**重要信息**:使用此属性时， `labels` 属性不得包含在同一对象中。要使用特定数据使用标签评估同一营销操作，必须在包含`labels`数组的请求有效负载中包含一个单独的对象。 |
| `entityType` | 要测试其营销操作的实体类型。 目前仅支持`dataSet`。 |
| `entityId` | 测试针对的营销操作的数据集的ID。 |
| `entityMeta.fields` | （可选）数据集中用于测试营销操作的特定字段列表。 |

**响应**

成功的响应返回一组评估结果；请求中发送的每个策略评估作业各一个。

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{IMS_ORG}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## [!DNL Real-time Customer Profile]的策略评估

[!DNL Policy Service] API还可用于检查是否存在与使用[!DNL Real-time Customer Profile]区段有关的策略违规。 有关更多信息，请参阅关于[强制受众区段符合数据使用要求的教程](../../segmentation/tutorials/governance.md)。
