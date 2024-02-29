---
keywords: Experience Platform；主页；热门主题；策略实施；自动实施；基于API的实施；数据治理
solution: Experience Platform
title: 策略评估API端点
description: 创建营销操作和定义策略后，您可以使用策略服务API来评估某些操作是否违反了任何策略。 返回的约束采用一组策略的形式，通过尝试对包含数据使用标签的指定数据执行营销操作，将违反这些策略。
role: Developer
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 1%

---

# 策略评估端点

在创建营销操作和定义数据使用策略后，您可以使用 [!DNL Policy Service] 用于评估某些操作是否违反了任何策略的API。 返回的约束采用一组策略的形式，通过尝试对包含数据使用标签的指定数据执行营销操作，将违反这些策略。

默认情况下，仅策略状态设置为 `ENABLED` 参与评估。 但是，您可以使用查询参数 `?includeDraft=true` 要包含 `DRAFT` 正在评估中的策略。

可通过以下三种方式之一发出评估请求：

1. 给定一个营销操作和一组数据使用标签，该操作是否违反任何策略？
1. 给定营销操作和一个或多个数据集，该操作是否违反任何策略？
1. 给定营销操作、一个或多个数据集以及每个数据集内一个或多个字段的子集，该操作是否违反任何策略？

## 快速入门

本指南中使用的API端点是 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关相关文档的链接、阅读本文档中的示例API调用的指南，以及有关成功调用任何组件所需的所需标头的重要信息 [!DNL Experience Platform] API。

## 使用数据使用标签评估策略违规 {#labels}

您可以使用以下工具根据特定数据使用标签集的存在来评估策略违规 `duleLabels` GET查询参数。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要针对一组数据使用标签进行测试的营销操作的名称。 您可以通过以下方式检索可用营销操作的列表 [对营销操作端点的GET请求](./marketing-actions.md#list). |
| `{LABELS_LIST}` | 要针对其测试营销操作的数据使用标签名称的逗号分隔列表。 例如： `duleLabels=C1,C2,C3`<br><br>请注意，标签名称区分大小写。 在中列出这些组件时，请确保您使用正确的大小写 `duleLabels` 参数。 |

**请求**

以下示例请求针对标签C1和C3评估营销操作。

>[!IMPORTANT]
>
>请注意 `AND` 和 `OR` 策略表达式中的运算符。 在以下示例中，如果任意标签(`C1` 或 `C3`)单独出现在请求中，营销操作不会违反此策略。 它需要两个标签(`C1` 和 `C3`)返回违反的策略。 确保仔细评估策略并同等谨慎地定义策略表达式。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包括 `violatedPolicies` 数组，其中包含对提供的标签执行营销操作而违反的策略的详细信息。 如果未违反任何策略，则 `violatedPolicies` 数组将为空。

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## 使用数据集评估策略违规 {#datasets}

您可以根据一个或多个数据集集评估策略违规，可以从这些数据集收集数据使用标签。 POST这是通过对 `/constraints` 特定营销操作的端点，并在请求正文中提供数据集ID列表。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 针对一个或多个数据集测试的营销操作的名称。 您可以通过以下方式检索可用营销操作的列表 [对营销操作端点的GET请求](./marketing-actions.md#list). |

**请求**

以下请求执行 `crossSiteTargeting` 针对一组三个数据集执行营销操作，以评估任何策略违规。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | ID在同级中指示的实体的类型 `entityId` 属性。 目前，唯一接受的值是 `dataSet`. |
| `entityId` | 测试营销操作所针对的数据集的ID。 GET通过向 `/dataSets` 中的端点 [!DNL Catalog Service] API。 请参阅指南，网址为 [列表 [!DNL Catalog] 对象](../../catalog/api/list-objects.md) 以了解更多信息。 |

**响应**

成功的响应包括 `violatedPolicies` 数组，其中包含对提供的数据集执行营销操作所违反的策略的详细信息。 如果未违反任何策略，则 `violatedPolicies` 数组将为空。

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `duleLabels` | 响应对象包括 `duleLabels` 数组，其中包含指定数据集中找到的所有标签的统一列表。 此列表在数据集中的所有字段上包含数据集级别和字段级别的标签。 |
| `discoveredLabels` | 响应还包括 `discoveredLabels` 包含每个数据集的对象的数组，显示 `datasetLabels` 细分为数据集级别和字段级别标签。 每个字段级标签都显示了带有该标签的特定字段的路径。 |

## 使用特定数据集字段评估策略违规 {#fields}

您可以基于一个或多个数据集中的字段子集评估策略违规，以便仅评估应用这些字段的数据使用标签。

在使用数据集字段评估策略时，请牢记以下几点：

* **字段名称区分大小写**：提供字段时，必须完全按照数据集中的显示方式编写它们(例如， `firstName` 对比 `firstname`)。
* **数据集标签继承**：数据集中的各个字段会继承已在数据集级别应用的任何标签。 如果策略评估未按预期返回，请务必检查任何可能从数据集级别向下继承到字段的标签，以及在字段级别应用的标签。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 针对数据集字段子集进行测试的营销操作的名称。 您可以通过以下方式检索可用营销操作的列表 [对营销操作端点的GET请求](./marketing-actions.md#list). |

**请求**

以下请求测试营销操作 `crossSiteTargeting` 属于三个数据集的特定字段集上。 有效负载类似于 [仅涉及数据集的评估请求](#datasets)，为每个要从中收集标签的数据集添加特定字段。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | ID在同级中指示的实体的类型 `entityId` 属性。 目前，唯一接受的值是 `dataSet`. |
| `entityId` | 要根据营销操作评估其字段的数据集的ID。 GET通过向 `/dataSets` 中的端点 [!DNL Catalog Service] API。 请参阅指南，网址为 [列表 [!DNL Catalog] 对象](../../catalog/api/list-objects.md) 以了解更多信息。 |
| `entityMeta.fields` | 数据集架构中特定字段的路径数组，以JSON指针字符串形式提供。 请参阅以下部分 [JSON指针](../../landing/api-fundamentals.md#json-pointer) API基础知识指南中，以了解有关这些字符串的接受语法的详细信息。 |

**响应**

成功的响应包括 `violatedPolicies` 数组，其中包含对提供的数据集字段执行营销操作所违反策略的详细信息。 如果未违反任何策略，则 `violatedPolicies` 数组将为空。

将下面的示例响应与 [仅涉及数据集的响应](#datasets)，请注意，收集的标签列表较短。 此 `discoveredLabels` 还减少了每个数据集的数量，因为它们仅包含在请求正文中指定的字段。 此外，以前违反的策略 `Targeting Ads or Content` 需要两者 `C4 AND C6` 标签存在，因此不再违反（如空所示） `violatedPolicies` 数组。

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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

此 `/bulk-eval` 端点允许您在一个API调用中运行多个评估作业。

**API格式**

```http
POST /bulk-eval
```

**请求**

批量评估请求的有效负载应为一组对象；每个评估作业执行一个对象。 对于基于数据集和字段进行评估的作业，应 `entityList` 必须提供数组。 对于根据数据使用标签进行评估的作业， `labels` 必须提供数组。

>[!WARNING]
>
>如果列出的任何评估作业同时包含 `entityList` 和 `labels` 数组，这将导致错误。 如果您要根据数据集和标签来评估相同的营销操作，则必须为该营销操作包含单独的评估作业。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `evalRef` | 营销操作的URI，用于针对违反策略的标签或数据集进行测试。 |
| `includeDraft` | 默认情况下，只有启用的策略才参与评估。 如果 `includeDraft` 设置为 `true`，策略位于 `DRAFT` 状态也将参与。 |
| `labels` | 用于测试营销操作的数据使用标签数组。<br><br>**重要**：使用此属性时，应 `entityList` 属性不得包含在同一对象中。 要使用数据集和/或字段评估相同的营销操作，您必须在请求有效负荷中包含一个单独的对象，该对象包含 `entityList` 数组。 |
| `entityList` | 这些数据集内用于测试营销操作的数据集和（可选）特定字段的数组。<br><br>**重要**：使用此属性时， `labels` 属性不得包含在同一对象中。 要使用特定数据使用标签评估相同的营销操作，您必须在请求有效载荷中包含一个单独的对象，该对象应 `labels` 数组。 |
| `entityType` | 测试营销操作的实体类型。 当前，仅限 `dataSet` 受支持。 |
| `entityId` | 测试营销操作所针对的数据集的ID。 |
| `entityMeta.fields` | （可选）数据集中用于测试营销操作的特定字段的列表。 |

**响应**

成功的响应将返回一系列评估结果；请求中发送的每个策略评估作业各一个。

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
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
      "imsOrg": "{ORG_ID}",
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
          "imsOrg": "{ORG_ID}",
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

## 策略评估 [!DNL Real-Time Customer Profile]

此 [!DNL Policy Service] API还可用于检查涉及使用的策略违规 [!DNL Real-Time Customer Profile] 区段。 请参阅上的教程 [强制实施受众区段的数据使用合规性](../../segmentation/tutorials/governance.md) 以了解更多信息。
