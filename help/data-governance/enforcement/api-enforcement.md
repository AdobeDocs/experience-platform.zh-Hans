---
keywords: Experience Platform；主页；热门主题；策略执行；自动执行；基于API的执行；数据管理；测试
solution: Experience Platform
title: 使用策略服务API强制实施数据使用策略
type: Tutorial
description: 为数据创建数据使用标签并针对这些标签创建营销操作的使用策略后，您可以使用策略服务API来评估对数据集或任意标签组执行的营销操作是否构成策略违规。 然后，您可以设置自己的内部协议，以根据API响应处理策略违规。
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# 使用 [!DNL Policy Service] API

为数据创建数据使用情况标签并为针对这些标签的营销操作创建使用策略后，您便可以使用 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) 评估对数据集或任意标签组执行的营销操作是否构成策略违规。 然后，您可以设置自己的内部协议，以根据API响应处理策略违规。

>[!NOTE]
>
>默认情况下，只有状态设置为 `ENABLED` 可以参与评估。 允许 `DRAFT` 要参与评估的策略，必须包含查询参数 `includeDraft=true` 在请求路径中。

本文档提供了有关如何使用 [!DNL Policy Service] 用于检查不同情况下是否存在策略违规的API。

## 快速入门

本教程需要对实施数据使用策略时涉及的以下关键概念有一定的了解：

* [数据管理](../home.md):框架 [!DNL Platform] 强制实施数据使用合规性。
   * [数据使用标签](../labels/overview.md):数据使用情况标签会应用于数据集（和/或这些数据集中的各个字段），从而指定数据使用方式的限制。
   * [数据使用策略](../policies/overview.md):数据使用策略是描述针对某些数据使用标签集允许或限制的营销操作类型的规则。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

在启动本教程之前，请查看 [开发人员指南](../api/getting-started.md) 以了解成功调用 [!DNL Policy Service] API，包括所需的标头以及如何读取示例API调用。

## 使用标签和营销操作进行评估

您可以通过测试针对数据集中假设存在的一组数据使用标签的营销操作来评估策略。 这是通过使用 `duleLabels` 查询参数，其中以逗号分隔的值列表形式提供标签，如以下示例所示。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 与您评估的数据使用策略关联的营销操作的名称。 |
| `{LABEL_1}` | 用于测试营销操作的数据使用标签。 必须至少提供一个标签。 提供多个标签时，必须用逗号分隔这些标签。 |

**请求**

以下请求测试 `exportToThirdParty` 针对标签的营销行动 `C1` 和 `C3`. 由于您在本教程前面创建的数据使用策略定义了 `C1` 标签为 `deny` 条件时，营销操作应触发策略违规。

>[!NOTE]
>
>数据使用情况标签区分大小写。 仅当策略表达式中定义的标签与其策略表达式完全匹配时，才会发生策略违规。 在本例中， `C1` 标签会触发违规，而 `c1` 标签不会。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回营销操作的URL、测试该操作所针对的使用情况标签，以及由于针对这些标签测试该操作而违反的任何策略的列表。 在此示例中，“将数据导出到第三方”策略显示在 `violatedPolicies` 数组，指示营销操作触发了预期的策略违规。

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{ORG_ID}",
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
| `violatedPolicies` | 列出测试营销操作(在 `marketingActionRef`) `duleLabels`. |

## 使用数据集评估

您可以通过针对一个或多个可从中收集标签的数据集测试营销操作来评估数据使用策略。 这是通过向 `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` 和在请求正文中提供数据集ID，如以下示例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 与您评估的策略关联的营销操作的名称。 |

**请求**

以下请求测试 `exportToThirdParty` 营销操作。 数据集由有效负载中提供的数组中的类型和ID引用。

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
      "entityId": "5c423dc25f2f2e00005e2319"
    },
    {
      "entityType": "dataSet",
      "entityId": "5cc323e15410ef14b749481e"
    },
    {
      "entityType": "dataSet",
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `entityType` | 有效负载数组中的每个项目必须指示正在定义的实体类型。 对于此用例，值将始终为“dataSet”。 |
| `entityId` | 有效负载数组中的每个项目都必须提供数据集的唯一ID。 |
| `entityMeta.fields` | （可选） [JSON指针](../../landing/api-fundamentals.md#json-pointer) 字符串，引用数据集架构中的特定字段。 如果包含此数组，则只有数组中包含的字段会参与评估。 阵列中未包含的任何架构字段将不会参与评估。<br><br>如果未包含此字段，则数据集架构内的所有字段都将包含在评估中。 |

**响应**

成功的响应会返回营销操作的URL、从提供的数据集收集的使用情况标签，以及由于针对这些标签测试操作而违反的任何策略的列表。 在此示例中，“将数据导出到第三方”策略显示在 `violatedPolicies` 数组，指示营销操作触发了预期的策略违规。

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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
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
| `duleLabels` | 从请求有效负载中提供的数据集提取的数据使用标签列表。 |
| `discoveredLabels` | 请求有效负载中提供的数据集列表，其中显示了在每个请求中找到的数据集级别和字段级别标签。 |
| `violatedPolicies` | 列出测试营销操作(在 `marketingActionRef`) `duleLabels`. |

## 后续步骤

通过阅读本文档，您可以在对数据集或一组数据使用标签执行营销操作时成功检查是否存在策略违规。 使用API响应中返回的数据，您可以在体验应用程序中设置协议，以在发生策略违规时相应地强制执行这些协议。

有关Platform如何为激活的区段自动提供策略强制的信息，请参阅 [自动执行](./auto-enforcement.md).
