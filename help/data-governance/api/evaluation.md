---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 策略
topic: developer guide
translation-type: tm+mt
source-git-commit: 12c53122d84e145a699a2a86631dc37ee0073578
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 1%

---


# 策略评估端点

创建营销操作并定义策略后，您可以使用 [!DNL Policy Service] API评估某些操作是否违反了任何策略。 返回的约束采用一组策略的形式，这些策略会尝试对包含数据使用标签的指定数据执行营销操作而违反。

默认情况下，只有其状态设置为参与 `ENABLED` 评估的策略。 但是，您可以使用查询参数 `?includeDraft=true` 在评估 `DRAFT` 中包含策略。

评估请求可以通过以下三种方式之一进行：

1. 对于营销操作和一组数据使用标签，该操作是否违反了任何策略？
1. 如果您有营销操作和一个或多个数据集，该操作是否违反了任何策略？
1. 如果给定营销操作、一个或多个数据集以及每个数据集中一个或多个字段的子集，该操作是否违反了任何策略？

## 入门指南

本指南中使用的API端点是API的一 [[!DNL Policy Service] 部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。 在继续之前，请查 [看入门指南](./getting-started.md) ，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何API所需标头的重要信 [!DNL Experience Platform] 息。

## 使用数据使用标签评估策略违规 {#labels}

您可以使用GET请求中的查询参数，根据特定数据使用标签集的存在情况来评 `duleLabels` 估是否存在策略违规。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要根据一组数据使用标签测试的营销操作的名称。 您可以通过向营销活动端点发出列表请求来 [检索可用的营销活动GET](./marketing-actions.md#list)。 |
| `{LABELS_LIST}` | 以逗号分隔的列表数据使用标签名称，用于测试营销操作。 例如： `duleLabels=C1,C2,C3`<br><br>请注意，标签名称区分大小写。 确保在参数中列出它们时使用正确的 `duleLabels` 大小写。 |

**请求**

以下示例请求对标签C1和C3评估营销操作。

>[!IMPORTANT]
>
>注意策略表达式 `AND` 中 `OR` 的操作符和操作符。 在以下示例中，如果请求中只`C1` 显示 `C3`了标签（或），则营销操作不会违反本政策。 同时需要标签(`C1` 和 `C3`)才能返回违反的策略。 确保仔细评估政策，并平等地定义政策表达式。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应包 `violatedPolicies` 括一个数组，其中包含因对提供的标签执行营销操作而违反的策略的详细信息。 如果未违反任何策略， `violatedPolicies` 则阵列将为空。

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

您可以根据可从中收集数据使用标签的一组一个或多个数据集评估策略违规。 这是通过在请求主体内对特定营 `/constraints` 销操作的端点执行POST请求并提供列表数据集ID来完成的。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要针对一个或多个数据集测试的营销操作的名称。 您可以通过向营销活动端点发出列表请求来 [检索可用的营销活动GET](./marketing-actions.md#list)。 |

**请求**

以下请求对一组三 `crossSiteTargeting` 个数据集执行营销操作，以评估是否存在任何违反策略的情况。

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
| `entityType` | 在同级属性中指示其ID的实体的类 `entityId` 型。 目前，唯一接受的值是 `dataSet`。 |
| `entityId` | 测试其营销操作的数据集的ID。 通过在API中对端点发出列表请求，可以获得集及其 `/dataSets` 相应ID的 [!DNL Catalog Service] GET。 有关详细信 [ [!DNL Catalog] 息，请参](../../catalog/api/list-objects.md) 阅listingobjects指南。 |

**响应**

成功的响应包 `violatedPolicies` 括一个数组，其中包含由于对提供的数据集执行营销操作而违反的策略的详细信息。 如果未违反任何策略， `violatedPolicies` 则阵列将为空。

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
| `duleLabels` | 响应对象包括一个数 `duleLabels` 组，该数组包含指定数据集内找到的所有标签的统一列表。 此列表包括数据集中所有字段上的数据集和字段级别标签。 |
| `discoveredLabels` | 该响应还包含一个数 `discoveredLabels` 组，其中包含每个数据集的对象，该数 `datasetLabels` 组显示分为数据集级别和字段级别标签。 每个字段级标签都显示具有该标签的特定字段的路径。 |

## 使用特定数据集字段评估策略违规情况 {#fields}

您可以根据一个或多个数据集中的字段子集评估策略违规情况，以便只评估应用了这些字段的数据使用标签。

在使用数据集字段评估策略时，请注意以下事项：

* **字段名称区分大小写**:提供字段时，必须完全按照它们在数据集中的显示方式编写(例如， `firstName` vs `firstname`)。
* **数据集标签继承**:数据集中的单个字段将继承在数据集级别应用的任何标签。 如果策略评估未按预期返回，请务必检查除在字段级别应用的标签外，还可能从数据集级别继承到字段的任何标签。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 针对数据集字段子集测试的营销操作的名称。 您可以通过向营销活动端点发出列表请求来 [检索可用的营销活动GET](./marketing-actions.md#list)。 |

**请求**

以下请求将测试属于三个 `crossSiteTargeting` 数据集的特定字段集上的营销操作。 负载类似于仅涉及数 [据集的评估请求](#datasets)，为每个数据集添加特定字段以从中收集标签。

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
| `entityType` | 在同级属性中指示其ID的实体的类 `entityId` 型。 目前，唯一接受的值是 `dataSet`。 |
| `entityId` | 要根据营销操作评估其字段的数据集的ID。 通过在API中对端点发出列表请求，可以获得集及其 `/dataSets` 相应ID的 [!DNL Catalog Service] GET。 有关详细信 [ [!DNL Catalog] 息，请参](../../catalog/api/list-objects.md) 阅listingobjects指南。 |
| `entityMeta.fields` | 数据集模式中特定字段的路径数组，以JSON指针字符串形式提供。 有关这些字符串 [已接受的语法](../../landing/api-fundamentals.md#json-pointer) ，请参阅API基础知识指南中有关JSON指针的部分。 |

**响应**

成功的响应包 `violatedPolicies` 括一个数组，其中包含针对提供的数据集字段执行营销操作时违反的策略的详细信息。 如果未违反任何策略， `violatedPolicies` 则阵列将为空。

将下面的示例响应与仅涉 [及数据集的响应进行比较](#datasets)，请注意，收集的标签的列表更短。 每个 `discoveredLabels` 数据集的字段也已减少，因为它们只包含请求主体中指定的字段。 此外，以前违反的策略 `Targeting Ads or Content` 要求 `C4 AND C6` 同时显示标签，因此不再违反，如空数组所 `violatedPolicies` 示。

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

端点 `/bulk-eval` 允许您在单个API调用中运行多个评估作业。

**API格式**

```http
POST /bulk-eval
```

**请求**

批量评估请求的有效负荷应是一组对象；每个要执行的评估作业各执行一个。 对于根据数据集和字段进行评估的作业，必 `entityList` 须提供数组。 对于根据数据使用标签进行评估的作业，必 `labels` 须提供数组。

>[!WARNING]
>
>如果列出的任何评估作业都 `entityList` 包含数 `labels` 组和数组，则将导致错误。 如果要根据数据集和标签评估同一营销操作，则必须为该营销操作包含单独的评估作业。

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
| `includeDraft` | 默认情况下，只有启用的策略才会参与评估。 如果 `includeDraft` 设置为 `true`，则处于状态的 `DRAFT` 策略也将参与。 |
| `labels` | 用于测试营销操作的一组数据使用标签。<br><br>**重要说明**:使用此属性时， `entityList` 不能将属性包含在同一对象中。 要使用数据集和／或字段评估相同的营销操作，必须在包含数组的请求有效负荷中包含一个单独的 `entityList` 对象。 |
| `entityList` | 数据集中的一组数据集和（可选）特定字段，用于测试针对的营销操作。<br><br>**重要说明**:使用此属性时， `labels` 不能将属性包含在同一对象中。 要使用特定数据使用标签评估同一营销操作，您必须在包含数组的请求有效负荷中包含一个单独的 `labels` 对象。 |
| `entityType` | 要测试其营销操作的实体类型。 目前，仅 `dataSet` 受支持。 |
| `entityId` | 测试其营销操作的数据集的ID。 |
| `entityMeta.fields` | （可选）数据集中特定字段的列表，以测试针对的营销操作。 |

**响应**

成功的响应会返回一系列评估结果；请求中发送的每个策略评估作业对应一个。

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

## 策略评估 [!DNL Real-time Customer Profile]

该 [!DNL Policy Service] API还可用于检查与使用区段相关的策略违 [!DNL Real-time Customer Profile] 规情况。 有关详细信息，请参 [阅关于强制受众段符合数据使用](../../segmentation/tutorials/governance.md) 规范的教程。