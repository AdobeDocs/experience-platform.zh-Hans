---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API
title: 实体（配置文件访问）API端点
type: Documentation
description: 通过Adobe Experience Platform，您可以使用RESTful API或用户界面访问实时客户配置文件数据。 本指南概述如何使用配置文件API访问实体（通常称为“配置文件”）。
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 9f9823a23c488e63b8b938cb885f050849836e36
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 3%

---

# 实体端点（配置文件访问）

Adobe Experience Platform允许您使用RESTful API或用户界面访问[!DNL Real-Time Customer Profile]数据。 本指南概述了如何使用API访问实体（通常称为“用户档案”）。 有关使用[!DNL Platform] UI访问配置文件的详细信息，请参阅[配置文件用户指南](../ui/user-guide.md)。

## 快速入门

本指南中使用的API终结点是[[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 在继续之前，请查看[快速入门指南](getting-started.md)，以获取相关文档的链接、此文档中示例API调用的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需的所需标头的重要信息。

## 检索实体 {#retrieve-entity}

通过向`/access/entities`端点发出GET请求以及必需的查询参数，您可以检索配置文件实体或其时序数据。

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

>[!TAB 时间序列事件]

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

请求路径中提供的查询参数指定要访问的数据。 您可以包含多个参数，以&amp;分隔。

要访问时间序列事件数据，您&#x200B;**必须**&#x200B;提供以下查询参数：

- `schema.name`：实体的XDM架构的名称。 在此用例中，值为`schema.name=_xdm.context.experienceevent`。
- `relatedSchema.name`：相关架构的名称。 由于架构名称为Experience Event，因此&#x200B;**的值必须**&#x200B;为`relatedSchema.name=_xdm.context.profile`。
- `relatedEntityId`：相关实体的ID。
- `relatedEntityIdNS`：相关实体的命名空间。 如果`relatedEntityId`是&#x200B;**而不是** XID，则必须提供此值。

附录的[查询参数](#query-parameters)部分提供了有效参数的完整列表。

**请求**

以下请求按ID查找配置文件实体，并检索与该实体关联的所有时间序列事件的属性`endUserIDs`、`web`和`channel`的值。

+++ 用于检索与实体关联的时间系列事件的示例请求

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回HTTP状态200，其中包含以分页方式列出的时序事件以及在请求查询参数中指定的关联字段。

>[!NOTE]
>
>请求指定了一个(`limit=1`)的限制，因此以下响应中的`count`为1，并且只返回了一个实体。

+++ 包含所请求的时间系列事件数据的示例响应

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
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
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

+++

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

您可以通过向`/access/entities`端点发出POST请求并在有效负载中提供标识来检索多个配置文件实体或时序事件。

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

>[!TAB 时间序列事件]

**API格式**

```http
POST /access/entities
```

**请求**

以下请求可检索与用户档案身份列表关联的时间系列事件的用户ID、本地时间和国家/地区代码。

+++ 用于检索时间序列数据的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10,
    "orderby": "-timestamp"
}'
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `schema.name` | 字符串 | **（必需）**&#x200B;实体所属的XDM架构的名称。 |
| `relatedSchema.name` | 字符串 | 如果`schema.name`为`_xdm.context.experienceevent`，该值必须为时间序列事件相关的配置文件实体指定架构。 |
| `identities` | 数组 | **（必需）**&#x200B;从中检索关联时间序列事件的配置文件数组列表。 数组中的每个条目均通过以下两种方式之一进行设置： <ol><li>使用由ID值和命名空间组成的完全限定的身份</li><li>提供XID</li></ol> |
| `fields` | 字符串 | 要作为字符串数组返回的XDM字段。 默认情况下，将返回所有字段。 |
| `orderby` | 字符串 | 按时间戳检索的体验事件的排序顺序，写为`(+/-)timestamp`，默认值为`+timestamp`。 |
| `timeFilter.startTime` | 整数 | 指定过滤时间序列对象的开始时间（以毫秒为单位）。 默认情况下，此值设置为可用时间的开始。 |
| `timeFilter.endTime` | 整数 | 指定过滤时间序列对象的结束时间（以毫秒为单位）。 默认情况下，此值设置为可用时间的结束。 |
| `limit` | 整数 | 要返回的最大记录数。 默认情况下，此值设置为1,000。 |

+++

**响应**

成功的响应会返回HTTP状态200，其中包含与请求中指定的多个配置文件关联的时间系列事件的分页列表。

+++ 包含时间序列事件的示例响应

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

+++

>[!NOTE]
>
>在此示例响应中，列出的第一个配置文件(“GkouAW-yD9aoRCPhRYROJ-TetAFW”)为`_links.next.payload`提供了一个值，这意味着此配置文件还有其他结果页。
>
>要访问这些结果，您可以对`/access/entities`端点执行额外的POST请求，并将列出的有效负载作为请求正文。

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

检索时序事件时，结果将分页。 如果有后续结果页，则`_page.next`属性将包含ID。 此外，`_links.next.href`属性还提供用于检索下一页的请求URI。 要检索结果，请对`/access/entities`终结点发出另一个GET请求，并使用提供的URI的值替换`/entities`。

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

按照本指南，您已成功访问[!DNL Real-Time Customer Profile]数据字段、配置文件和时序数据。 要了解如何访问存储在[!DNL Platform]中的其他数据资源，请参阅[数据访问概述](../../data-access/home.md)。

## 附录 {#appendix}

以下部分提供有关使用API访问[!DNL Profile]数据的补充信息。

### 查询参数 {#query-parameters}

在`/access/entities`终结点的GET请求路径中使用了以下参数。 它们用于标识要访问的配置文件实体，并筛选响应中返回的数据。 必填参数标有标签，其余参数为可选参数。

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `schema.name` | **（必需）**&#x200B;实体的XDM架构的名称。 | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | 如果`schema.name`是`_xdm.context.experienceevent`，则此值&#x200B;**必须**&#x200B;为时间序列事件相关的配置文件实体指定架构。 | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **（必需）**&#x200B;实体的ID。 如果此参数的值不是XID，则还必须提供标识命名空间参数(`entityIdNS`)。 | `entityId=janedoe@example.com` |
| `entityIdNS` | 如果未将`entityId`作为XID提供，则字段&#x200B;**必须**&#x200B;指定标识命名空间。 | `entityIdNS=email` |
| `relatedEntityId` | 如果`schema.name`是`_xdm.context.experienceevent`，则此值&#x200B;**必须**&#x200B;指定相关配置文件实体的ID。 此值遵循与`entityId`相同的规则。 | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | 如果`schema.name`是“_xdm.context.experienceevent”，此值必须为`relatedEntityId`中指定的实体指定身份命名空间。 | `relatedEntityIdNS=CRMID` |
| `fields` | 筛选响应中返回的数据。 使用此选项可指定要包含在检索的数据中的架构字段值。 对于多个字段，请使用逗号分隔值，且中间不应有空格。 | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | 标识用来管理返回数据的合并策略。 如果未在调用中指定架构，则将使用您组织对该架构的默认值。 如果尚未配置默认合并策略，则默认设置是无配置文件合并和无身份拼接。 | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 按时间戳检索的实体的排序顺序。 此写为`(+/-)timestamp`，默认值为`+timestamp`。 | `orderby=-timestamp` |
| `startTime` | 指定筛选实体的开始时间（以毫秒为单位）。 | `startTime=1539838505` |
| `endTime` | 指定筛选实体的结束时间（以毫秒为单位）。 | `endTime=1539838510` |
| `limit` | 指定要返回的最大实体数。 默认情况下，此值设置为1000。 | `limit=100` |
| `property` | 按属性值筛选。 此查询参数支持以下计算器： =、！=， &lt;， &lt;=， >， >=。 这只能用于体验事件，最多支持三个属性。 | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
