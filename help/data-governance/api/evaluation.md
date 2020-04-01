---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 策略
topic: developer guide
translation-type: tm+mt
source-git-commit: 2997243622a7483ae23e21487128cea6badecb80

---


# 策略评估

在创建营销操作并定义策略后，您可以使用策略服务API评估某些操作是否违反了任何策略。 返回的约束采用一组策略的形式，这些策略会尝试对包含数据使用标签的指定数据执行营销操作而违反这些策略。

默认情况下， **只有状态设置为“ENABLED”的策略才能参与评估**`?includeDraft=true` ，但是您可以使用查询参数将“DRAFT”策略包含在评估中。

评估请求可通过以下三种方式之一提出：

1. 如果有一组数据使用标签和营销操作，该操作是否违反了任何策略？
1. 如果有一个或多个数据集和营销操作，该操作是否违反了任何策略？
1. 如果给定一个或多个数据集以及每个数据集中一个或多个字段的子集，则该操作是否违反了任何策略？

## 使用数据使用标签和营销操作评估策略

根据数据使用标签的存在评估策略违规要求您指定请求期间数据上将显示的标签集。 这是通过使用查询参数实现的，其中数据使用标签以逗号分隔的值列表形式提供，如下例所示。

**API格式**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**请求**

以下示例请求对标签C1和C3评估营销操作。 在使用数据使用标签评估策略时，请牢记以下几点：
* **数据使用标签区分大小写。** 上述请求返回违反的策略，而使用小写标签发出相同的请求(例如， `"c1,c3"`, `"C1,c3"``"c1,C3"`)不会。
* **请注意您的政策`AND`表达式`OR`中的操作符和操作符。** 在此示例中，如果请求中单独显示了标签(`C1` 或 `C3`)，则营销操作不会违反本政策。 需要两个标签(`C1 AND C3`)才能返回违反的策略。 确保仔细评估政策，并平等地界定政策表达式。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应对象包括应 `duleLabels` 与请求中发送的标签相匹配的数组。 如果对数据使用标签执行指定的营销操作违反了策略，则阵列将包含受影响的策略（或策略）的详细信息。 `violatedPolicies` 如果未违反任何策略， `violatedPolicies` 则数组将显示为空(`[]`)。

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

您还可以通过指定可从中收集数据使用标签的一个或多个数据集的ID来评估策略违规。 这是通过对营销操作的核心端点或自定义端点执行POST请求并在请求主体中指定数据集ID来完成的，如下所示。 `/constraints`

**API格式**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**请求**

请求主体包含一个数组，其中每个数据集ID都有一个对象。 由于您发送的是请求主体，因此，“内容类型：application/json”请求标头是必需的，如以下示例中所示。

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

响应对象包括一个数 `duleLabels` 组，该数组包含在指定数据集内找到的所有标签的统一列表。 此列表在数据集内的所有字段上都包含数据集和字段级别标签。

响应还包括一个数组， `discoveredLabels` 其中包含每个数据集的对象，该数 `datasetLabels` 组显示分为数据集级别和字段级别标签。 每个字段级标签都显示包含该标签的特定字段的路径。

如果指定的营销操作违反了涉及数据集内 `duleLabels` 的策略，则阵列将 `violatedPolicies` 包含受影响的策略（或策略）的详细信息。 如果未违反任何策略， `violatedPolicies` 则数组将显示为空(`[]`)。

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

除了提供一个或多个数据集ID外，还可指定来自每个数据集内的字段子集，指示应仅评估这些字段上的数据使用标签。 与仅涉及数据集的POST请求类似，此请求会将每个数据集的特定字段添加到请求主体。

使用数据集字段评估策略时，请牢记以下几点：

* **字段名称区分大小写。** 提供字段时，必须完全按照它们在数据集中的显示方式编写这些字段(例如， `firstName` vs `firstname`)。
* **数据集标签继承。** 数据使用标签可以应用于多个级别，并可以向下继承。 如果策略评估没有按您所认为的方式返回，请务必检查从数据集到字段的继承标签以及在字段级别应用的标签。

**API格式**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**请求**

请求主体包含一个数组，其中每个数据集ID都有一个对象，该数据集中应用于评估的字段子集。 由于您发送的是请求主体，因此，“内容类型：application/json”请求标头是必需的，如以下示例中所示。

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

响应对象包括一个数 `duleLabels` 组，该数组包含在指定字段上找到的统一列表标签。 记住，这也包括数据集标签，因为它们会继承到字段。

如果对提供的字段中的数据执行指定的营销操作而违反了策略，则阵列将包含受影响的策略（或策略）的详细信息。 `violatedPolicies` 如果未违反任何策略， `violatedPolicies` 则数组将显示为空(`[]`)。

在以下响应中，您可以看到的列表现在更短，同每个数据集的一样，因为它只包括请求主体中指定的字段。 `duleLabels``discoveredLabels` 您还会注意到之前违反的策略“定位广告或内容”需要两个标签，因此 `C4 AND C6` 它不再违反，并且数组 `violatedPolicies` 显示为空。

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

## 实时客户用户档案的策略评估

策略服务API还可用于检查与使用实时客户用户档案段相关的策略违规。 有关详细信息，请参 [阅关于强制受众区段遵守数据使用](../../segmentation/tutorials/governance.md) 的教程。