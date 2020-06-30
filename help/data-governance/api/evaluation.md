---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 策略
topic: developer guide
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---


# 策略评估

创建市场营销操作并定义策略后，您可以使用策略服务API评估某些操作是否违反了任何策略。 返回的约束采用一组策略的形式，这些策略会尝试对包含数据使用标签的指定数据执行营销操作而违反。

默认情 **况下，只有状态设置为“ENABLED”的策略才能参与评估**，但您可以使用查询参数 `?includeDraft=true` 在评估中包括“DRAFT”策略。

评估请求可以通过以下三种方式之一进行：

1. 如果有一组数据使用标签和营销操作，该操作是否违反了任何策略？
1. 如果有一个或多个数据集和一个营销操作，该操作是否违反了任何策略？
1. 给定一个或多个数据集以及每个数据集中一个或多个字段的子集，该操作是否违反任何策略？

## 使用数据使用标签和营销操作评估策略

根据存在数据使用标签来评估违反策略的情况需要您指定在请求期间数据上可能显示的标签集。 这是通过使用查询参数来完成的，其中数据使用标签以逗号分隔的值列表形式提供，如以下示例所示。

**API格式**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**请求**

以下示例请求对标签C1和C3评估营销操作。 在使用数据使用标签评估策略时，请注意以下事项：
* **数据使用标签区分大小写。** 上面显示的请求返回违反的策略，而使用小写标签发出相同的请求(例如， `"c1,c3"`, `"C1,c3"`) `"c1,C3"`不会。
* **注意策略表达式`AND`中`OR`的操作符和操作符。** 在此示例中，如果请求中只`C1` 显示 `C3`了标签（或），则市场营销操作不会违反本政策。 需要两个标签(`C1 AND C3`)才能返回违反的策略。 确保仔细评估政策，并平等地定义政策表达式。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象包括 `duleLabels` 应与请求中发送的标签匹配的数组。 如果对数据使用标签执行指定的营销操作违反了策略， `violatedPolicies` 阵列将包含受影响的策略（或策略）的详细信息。 如果未违反任何策略， `violatedPolicies` 阵列将显示为空`[]`()。

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

## 使用数据集和营销操作评估策略

您还可以通过指定可从中收集数据使用标签的一个或多个数据集的ID来评估策略违规。 这是通过对营销操作的核心或自定义端点执行 `/constraints` POST请求并在请求主体中指定数据集ID来完成的，如下所示。

**API格式**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**请求**

请求主体包含一个数组，其中每个数据集ID都有一个对象。 由于您正在发送请求正文，因此，“Content-Type: application/json”请求标头是必需的，如以下示例所示。

```SHELL
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

**响应**

响应对象包括一个数 `duleLabels` 组，该数组包含指定数据集内找到的所有标签的统一列表。 此列表包括数据集中所有字段上的数据集和字段级别标签。

该响应还包含一个数 `discoveredLabels` 组，其中包含每个数据集的对象，该数 `datasetLabels` 组显示分为数据集级别和字段级别标签。 每个字段级标签都显示具有该标签的特定字段的路径。

如果指定的营销操作违反了涉及数据集 `duleLabels` 中的策略，则阵 `violatedPolicies` 列将包含受影响的策略（或策略）的详细信息。 如果未违反任何策略， `violatedPolicies` 阵列将显示为空`[]`()。

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

## 使用数据集、字段和营销操作评估策略

除了提供一个或多个数据集ID外，还可以指定每个数据集内字段的子集，指示只应评估这些字段上的数据使用标签。 与仅涉及数据集的POST请求相似，此请求会将每个数据集的特定字段添加到请求主体。

在使用数据集字段评估策略时，请注意以下事项：

* **字段名称区分大小写。** 提供字段时，必须完全按照它们在数据集中的显示方式编写(例如， `firstName` vs `firstname`)。
* **数据集标签继承。** 数据使用标签可以应用于多个级别，并可向下继承。 如果策略评估没有按您认为的方式返回，请务必检查除字段级别应用的标签外，从数据集到字段的继承标签。

**API格式**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**请求**

请求主体包含一个数组，其中每个数据集ID都有一个对象，该数据集中应用于评估的字段子集。 由于您正在发送请求正文，因此，“Content-Type: application/json”请求标头是必需的，如以下示例所示。

```SHELL
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

**响应**

响应对象包括一 `duleLabels` 个数组，它包含在指定字段上找到的标签的统一列表。 请记住，这也包括数据集标签，因为它们继承到字段。

如果对提供的字段中的数据执行指定的营销操作而违反策略， `violatedPolicies` 则阵列将包含受影响的策略（或策略）的详细信息。 如果未违反任何策略， `violatedPolicies` 阵列将显示为空`[]`()。

在下面的响应中，您可以看到列表的 `duleLabels` 现在更短，因为每个 `discoveredLabels` 数据集只包含请求主体中指定的字段。 您还会注意到之前违反的策略“定位广告或内容”需要两个标 `C4 AND C6` 签，因此不再违反该策略，并且数 `violatedPolicies` 组显示为空。

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

## 策略评估 [!DNL Real-time Customer Profile]

该 [!DNL Policy Service] API还可用于检查与使用区段相关的策略违 [!DNL Real-time Customer Profile] 规情况。 有关详细信息，请参 [阅关于强制受众段符合数据使用](../../segmentation/tutorials/governance.md) 规范的教程。