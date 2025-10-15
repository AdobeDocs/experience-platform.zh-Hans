---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 实体（配置文件访问）API端点
type: Documentation
description: 通过Adobe Experience Platform，您可以使用RESTful API或用户界面访问实时客户配置文件数据。 本指南概述如何使用配置文件API访问实体（通常称为“配置文件”）。
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 193045d530d73d8a3e4f7ac3df4e1f43e8ad5b15
workflow-type: tm+mt
source-wordcount: '2141'
ht-degree: 2%

---

# 实体端点（配置文件访问）

Adobe Experience Platform允许您使用RESTful API或用户界面访问[!DNL Real-Time Customer Profile]数据。 本指南概述了如何使用API访问实体（通常称为“用户档案”）。 有关使用[!DNL Experience Platform] UI访问配置文件的详细信息，请参阅[配置文件用户指南](../ui/user-guide.md)。

## 快速入门

本指南中使用的API终结点是[[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 在继续之前，请查看[快速入门指南](getting-started.md)，以获取相关文档的链接、此文档中示例API调用的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需的所需标头的重要信息。

>[!BEGINSHADEBOX]

## 实体分辨率

作为架构升级的一部分，Adobe将引入针对客户和商机的实体解决方案，使用基于最新数据的确定性ID匹配。 实体解析作业在批量分段期间每天运行，然后再评估具有B2B属性的多实体受众。

此增强功能使Experience Platform能够识别和统一表示同一实体的多个记录，从而提高数据一致性并实现更准确的受众分段。

以前，“帐户”和“机会”依赖于基于身份图的解决方案，该解决方案将身份（包括所有历史引入）关联起来。 在新的实体解析方法中，标识仅根据最新数据进行链接

### 实体解析如何工作？

- **在**&#x200B;之前：如果将数据通用编号系统(DUNS)编号用作附加标识，并且在源系统（如CRM）中更新了帐户的DUNS编号，则帐户ID将同时链接到旧和新的DUNS编号。
- **After**：如果将DUNS编号用作附加标识，并且在源系统（如CRM）中更新了帐户的DUNS编号，则帐户ID将仅链接到新的DUNS编号，从而更准确地反映帐户的当前状态。

作为本次更新的结果，[!DNL Profile Access] API现在会在实体解析作业周期完成后反映最新的合并配置文件视图。 此外，一致数据提供了分段、激活和分析等用例，提高了数据准确性和一致性。

>[!ENDSHADEBOX]

## 检索实体 {#retrieve-entity}

>[!IMPORTANT]
>
>不再通过API支持以下B2B实体查找请求：**帐户 — 人员关系、机会 — 人员关系、营销活动、营销活动成员、营销列表和营销列表成员**。
>
>已不再支持这些实体。 如果您现有的集成或工作流依赖于访问这些实体，请更新它们以使用支持的实体类型，以确保功能可继续使用。

您可以通过向`/access/entities`端点发出GET请求以及所需的查询参数来检索配置文件实体。

>[!BEGINTABS]

>[!TAB 配置文件实体]

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

请求路径中提供的查询参数指定要访问的数据。 您可以包含多个参数，以&amp;分隔。

要访问配置文件实体，您&#x200B;**必须**&#x200B;提供以下查询参数：

- `schema.name`：实体的XDM架构的名称。 在此使用案例中，`schema.name=_xdm.context.profile`。
- `entityId`：您尝试检索的实体的ID。
- `entityIdNS`：您尝试检索的实体的命名空间。 如果`entityId`是&#x200B;**而不是** XID，则必须提供此值。

此外，强烈建议使用以下查询参数&#x200B;**：

- `mergePolicyId`：要用于筛选数据的合并策略的ID。 如果未指定合并策略，则将使用贵组织的默认合并策略。

附录的[查询参数](#query-parameters)部分提供了有效参数的完整列表。

**请求**

以下请求使用标识检索客户的电子邮件和名称。

+++ 使用标识检索实体的示例请求

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回包含所请求实体的HTTP状态200。

+++ 包含所请求实体的示例响应

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "johnsmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

+++

>[!NOTE]
>
>如果相关图形链接超过50个身份，此服务将返回HTTP状态422和消息“相关身份过多”。 如果收到此错误，请考虑添加更多查询参数以缩小搜索范围。

>[!TAB B2B帐户]

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

请求路径中提供的查询参数指定要访问的数据。 您可以包含多个参数，以&amp;分隔。

要访问B2B帐户数据，您&#x200B;**必须**&#x200B;提供以下查询参数：

- `schema.name`：实体的XDM架构的名称。 在此用例中，值为`schema.name=_xdm.context.account`。
- `entityId`：您尝试检索的实体的ID。
- `entityIdNS`：您尝试检索的实体的命名空间。 如果`entityId`是&#x200B;**而不是** XID，则必须提供此值。

此外，强烈建议使用以下查询参数&#x200B;**：

- `mergePolicyId`：要用于筛选数据的合并策略的ID。 如果未指定合并策略，则将使用贵组织的默认合并策略。

附录的[查询参数](#query-parameters)部分提供了有效参数的完整列表。

**请求**

+++ 检索B2B帐户的示例请求

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回包含所请求实体的HTTP状态200。

+++ 包含所请求实体的示例响应

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB B2B机会]

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

请求路径中提供的查询参数指定要访问的数据。 您可以包含多个参数，以&amp;分隔。

要访问B2B Opportunity实体，您&#x200B;**必须**&#x200B;提供以下查询参数：

- `schema.name`：实体的XDM架构的名称。 在此使用案例中，`schema.name=_xdm.context.opportunity`。
- `entityId`：您尝试检索的实体的ID。
- `entityIdNS`：您尝试检索的实体的命名空间。 如果`entityId`是&#x200B;**而不是** XID，则必须提供此值。

此外，强烈建议使用以下查询参数&#x200B;**：

- `mergePolicyId`：要用于筛选数据的合并策略的ID。 如果未指定合并策略，则将使用贵组织的默认合并策略。

附录的[查询参数](#query-parameters)部分提供了有效参数的完整列表。

**请求**

+++ 检索B2B Opportunity实体的示例请求

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回包含所请求实体的HTTP状态200。

+++ 包含所请求实体的示例响应

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## 检索多个实体 {#retrieve-entities}

您可以通过向`/access/entities`端点发出POST请求并在有效负载中提供标识来检索多个配置文件实体。

>[!BEGINTABS]

>[!TAB 配置文件实体]

**API格式**

```http
POST /access/entities
```

**请求**

以下请求按身份列表检索多个客户的名称和电子邮件地址。

+++检索多个实体的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp"
      }'
```

| 属性 | 类型 | 描述 |
| -------- |----- | ----------- |
| `schema.name` | 字符串 | **（必需）**&#x200B;实体所属的XDM架构的名称。 |
| `fields` | 数组 | 要作为字符串数组返回的XDM字段。 默认情况下，将返回所有字段。 |
| `identities` | 数组 | **（必需）**&#x200B;一个数组，其中包含您要访问的实体的标识列表。 |
| `identities.entityId` | 字符串 | 您希望访问的实体的ID。 |
| `identities.entityIdNS.code` | 字符串 | 您希望访问的实体ID的命名空间。 |
| `timeFilter.startTime` | 整数 | 指定筛选配置文件实体的开始时间（以毫秒为单位）。 默认情况下，此值设置为可用时间的开始。 |
| `timeFilter.endTime` | 整数 | 指定筛选配置文件实体的结束时间（以毫秒为单位）。 默认情况下，此值设置为可用时间的结束。 |
| `limit` | 整数 | 要返回的最大记录数。 默认情况下，此值设置为1000。 |
| `orderby` | 字符串 | 按时间戳检索的体验事件的排序顺序，写为`(+/-)timestamp`，默认值为`+timestamp`。 |

+++

**响应**

成功的响应返回HTTP状态200，请求正文中指定了实体的请求字段。

+++ 包含所请求实体的示例响应

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

+++

>[!TAB B2B帐户]

**API格式**

```http
POST /access/entities
```

**请求**

以下请求将检索请求的B2B帐户。

+++检索多个实体的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| 属性 | 类型 | 描述 |
| -------- |----- | ----------- |
| `schema.name` | 字符串 | **（必需）**&#x200B;实体所属的XDM架构的名称。 |
| `identities` | 数组 | **（必需）**&#x200B;一个数组，其中包含您要访问的实体的标识列表。 |
| `identities.entityId` | 字符串 | 您希望访问的实体的ID。 |
| `identities.entityIdNS.code` | 字符串 | 您希望访问的实体ID的命名空间。 |

+++

**响应**

成功的响应会返回包含所请求实体的HTTP状态200。

+++ 包含所请求实体的示例响应

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB B2B机会]

**API格式**

```http
POST /access/entities
```

**请求**

以下请求将检索请求的B2B机会。

+++ 检索多个实体的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| 属性 | 类型 | 描述 |
| -------- |----- | ----------- |
| `schema.name` | 字符串 | **（必需）**&#x200B;实体所属的XDM架构的名称。 |
| `identities` | 数组 | **（必需）**&#x200B;一个数组，其中包含您要访问的实体的标识列表。 |
| `identities.entityId` | 字符串 | 您希望访问的实体的ID。 |
| `identities.entityIdNS.code` | 字符串 | 您希望访问的实体ID的命名空间。 |

+++

**响应**

成功的响应会返回包含所请求实体的HTTP状态200。

+++ 包含所请求实体的示例响应

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### 访问结果的后续页面

检索时序事件时，结果将分页。 如果有后续结果页，则`_page.next`属性将包含ID。 此外，`_links.next.href`属性还提供用于检索下一页的请求URI。 要检索结果，请对`/access/entities`端点发出另一个GET请求，并使用提供的URI的值替换`/entities`。

>[!NOTE]
>
>请确保不要在请求路径中意外重复`/entities/`。 它只应出现一次，如`/access/entities?start=...`

**API格式**

```http
GET /access/{NEXT_URI}
```

| 参数 | 描述 |
|---|---|
| `{NEXT_URI}` | URI值取自`_links.next.href`。 |

**请求**

以下请求通过使用`_links.next.href` URI作为请求路径来检索结果的下一页。

+++ 用于访问下一页结果的示例请求

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应将返回结果的下一页。 此响应没有后续结果页，如`_page.next`和`_links.next.href`的空字符串值所指示。

+++ 包含下一页实体的示例响应

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

+++

## 删除实体 {#delete-entity}

>[!IMPORTANT]
>
>删除实体端点将在2025年10月底之前被弃用。 如果要执行记录删除操作，可以改用[数据生命周期记录删除API工作流](/help/hygiene/api/workorder.md)或[数据生命周期记录删除UI工作流](/help/hygiene/ui/record-delete.md)。
>
>此外，以下B2B实体的删除请求已被弃用：
>
>- 帐户
>- 帐户 — 人员关系
>- 机会
>- 机会 — 人员关系
>- Campaign
>- 营销活动成员
>- 营销列表
>- 营销列表成员

通过向`/access/entities`端点发出DELETE请求以及必需的查询参数，可以从配置文件存储中删除实体。

**API格式**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

请求路径中提供的查询参数指定要访问的数据。 您可以包含多个参数，以&amp;分隔。

要删除实体，您&#x200B;**必须**&#x200B;提供以下查询参数：

- `schema.name`：实体的XDM架构的名称。 在此使用案例中，您&#x200B;**只能**&#x200B;使用`schema.name=_xdm.context.profile`。
- `entityId`：您尝试检索的实体的ID。
- `entityIdNS`：您尝试检索的实体的命名空间。 如果`entityId`是&#x200B;**而不是** XID，则必须提供此值。
- `mergePolicyId`：实体的合并策略ID。 合并策略包含有关身份拼接和键值XDM对象合并的信息。 如果未提供此值，则将使用默认合并策略。

**请求**

以下请求删除指定的实体。

+++ 删除实体的示例请求

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回带有空响应正文的HTTP状态202。

## 后续步骤

按照本指南，您已成功访问[!DNL Real-Time Customer Profile]数据字段、配置文件和时序数据。 要了解如何访问存储在[!DNL Experience Platform]中的其他数据资源，请参阅[数据访问概述](../../data-access/home.md)。

## 附录 {#appendix}

以下部分提供有关使用API访问[!DNL Profile]数据的补充信息。

### 查询参数 {#query-parameters}

在`/access/entities`终结点的GET请求的路径中使用了以下参数。 它们用于标识要访问的配置文件实体，并筛选响应中返回的数据。 必填参数标有标签，其余参数为可选参数。

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `schema.name` | **（必需）**&#x200B;实体的XDM架构的名称。 | `schema.name=_xdm.context.profile` |
| `relatedSchema.name` | 如果`schema.name`是`_xdm.context.experienceevent`，则此值&#x200B;**必须**&#x200B;为时间序列事件相关的配置文件实体指定架构。 | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **（必需）**&#x200B;实体的ID。 如果此参数的值不是XID，则还必须提供标识命名空间参数(`entityIdNS`)。 | `entityId=janedoe@example.com` |
| `entityIdNS` | 如果未将`entityId`作为XID提供，则字段&#x200B;**必须**&#x200B;指定标识命名空间。 | `entityIdNS=email` |
| `relatedEntityId` | 如果`schema.name`是`_xdm.context.experienceevent`，则此值&#x200B;**必须**&#x200B;指定相关配置文件实体的ID。 此值遵循与`entityId`相同的规则。 | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | 如果`schema.name`是“_xdm.context.experienceevent”，此值必须为`relatedEntityId`中指定的实体指定身份命名空间。 | `relatedEntityIdNS=CRMID` |
| `fields` | 筛选响应中返回的数据。 使用此选项可指定要包含在检索的数据中的架构字段值。 对于多个字段，请使用逗号分隔值，且中间不应有空格。 | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | *推荐*&#x200B;标识用于管理返回数据的合并策略。 如果未在调用中指定架构，则将使用您组织对该架构的默认值。 如果没有为您请求的架构定义默认合并策略，则API将返回HTTP 422错误状态代码。 | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 按时间戳检索的实体的排序顺序。 此写为`(+/-)timestamp`，默认值为`+timestamp`。 | `orderby=-timestamp` |
| `startTime` | 指定筛选实体的开始时间（以毫秒为单位）。 | `startTime=1539838505` |
| `endTime` | 指定筛选实体的结束时间（以毫秒为单位）。 | `endTime=1539838510` |
| `limit` | 指定要返回的最大实体数。 默认情况下，此值设置为1000。 | `limit=100` |
| `property` | 按属性值筛选。 此查询参数支持以下计算器： =、！=， &lt;， &lt;=， >， >=。 这只能用于体验事件，最多支持三个属性。 | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
