---
keywords: Experience Platform；配置文件；实时客户配置文件；故障排除；API
title: 实体（配置文件访问）API端点
type: Documentation
description: 通过Adobe Experience Platform，您可以使用RESTful API或用户界面访问实时客户配置文件数据。 本指南概述如何使用配置文件API访问实体（通常称为“配置文件”）。
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 1%

---

# 实体端点（配置文件访问）

Adobe Experience Platform允许您使用RESTful API或用户界面访问[!DNL Real-Time Customer Profile]数据。 本指南概述了如何使用API访问实体（通常称为“用户档案”）。 有关使用[!DNL Platform] UI访问配置文件的详细信息，请参阅[配置文件用户指南](../ui/user-guide.md)。

## 快速入门

本指南中使用的API终结点是[[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 在继续之前，请查看[快速入门指南](getting-started.md)，以获取相关文档的链接、此文档中示例API调用的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需的所需标头的重要信息。

## 按身份访问配置文件数据

通过向`/access/entities`端点发出GET请求并提供实体标识作为一系列查询参数，您可以访问[!DNL Profile]实体。 此身份包含ID值(`entityId`)和身份命名空间(`entityIdNS`)。

请求路径中提供的查询参数指定要访问的数据。 您可以包含多个参数，以&amp;分隔。 附录的[查询参数](#query-parameters)部分提供了有效参数的完整列表。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**请求**

以下请求使用标识检索客户的电子邮件和名称：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

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

>[!NOTE]
>
>如果相关图形链接超过50个身份，此服务将返回HTTP状态422和消息“相关身份过多”。 如果收到此错误，请考虑添加更多查询参数以缩小搜索范围。

## 按身份列表访问配置文件数据

您可以通过向`/access/entities`端点发出POST请求并在有效负载中提供身份，按身份访问多个配置文件实体。 这些身份包含ID值(`entityId`)和身份命名空间(`entityIdNS`)。

**API格式**

```http
POST /access/entities
```

**请求**

以下请求按标识列表检索多个客户的名称和电子邮件地址：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
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
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| 属性 | 描述 |
|---|---|
| `schema.name` | ***（必需）***&#x200B;实体所属的XDM架构的名称。 |
| `fields` | 要作为字符串数组返回的XDM字段。 默认情况下，将返回所有字段。 |
| `identities` | ***（必需）***&#x200B;一个数组，其中包含您要访问的实体的标识列表。 |
| `identities.entityId` | 您希望访问的实体的ID。 |
| `identities.entityIdNS.code` | 您希望访问的实体ID的命名空间。 |
| `timeFilter.startTime` | 时间范围过滤器的开始时间，包括。 应为毫秒粒度。 如果未指定，则默认值为可用时间的开始。 |
| `timeFilter.endTime` | 时间范围过滤器的结束时间，已排除。 应为毫秒粒度。 如果未指定，则默认值为可用时间的结束。 |
| `limit` | 要返回的记录数。 仅适用于返回的体验事件数。 默认值：1,000。 |
| `orderby` | 按时间戳检索的体验事件的排序顺序，写为`(+/-)timestamp`，默认值为`+timestamp`。 |
| `withCA` | 用于启用计算属性进行查找的功能标志。 默认值： false。 |

**响应**
成功的响应将返回请求正文中指定的实体的请求字段。

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

## 按身份访问用户档案的时间系列事件

通过向`/access/entities`端点发出GET请求，您可以按其关联的配置文件实体的标识访问时间序列事件。 此身份包含ID值(`entityId`)和身份命名空间(`entityIdNS`)。

请求路径中提供的查询参数指定要访问的数据。 您可以包含多个参数，以&amp;分隔。 附录的[查询参数](#query-parameters)部分提供了有效参数的完整列表。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**请求**

以下请求按ID查找配置文件实体，并检索与该实体关联的所有时间序列事件的属性`endUserIDs`、`web`和`channel`的值。

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回在请求查询参数中指定的时间序列事件和相关字段的分页列表。

>[!NOTE]
>
>请求指定了一个(`limit=1`)的限制，因此以下响应中的`count`为1，并且只返回了一个实体。

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

### 访问结果的后续页面

检索时序事件时，结果将分页。 如果有后续结果页，则`_page.next`属性将包含ID。 此外，`_links.next.href`属性还提供用于检索下一页的请求URI。 要检索结果，请对`/access/entities`终结点发出另一个GET请求，但您必须确保使用提供的URI的值替换`/entities`。

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

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回结果的下一页。 此响应没有后续结果页，如`_page.next`和`_links.next.href`的空字符串值所指示。

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

## 按身份访问多个配置文件的时间序列事件

通过向`/access/entities`端点发出POST请求并在有效负载中提供配置文件标识，您可以从多个关联的配置文件访问时间序列事件。 这些标识每个都包含ID值(`entityId`)和标识命名空间(`entityIdNS`)。

**API格式**

```http
POST /access/entities
```

**请求**

以下请求可检索与用户档案身份列表关联的时间系列事件的用户ID、本地时间和国家/地区代码：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
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
    "limit": 10
}'
```

| 属性 | 描述 |
|---|---|
| `schema.name` | **（必需）**&#x200B;要检索的实体的XDM架构 |
| `relatedSchema.name` | 如果`schema.name`为`_xdm.context.experienceevent`，该值必须为时间序列事件相关的配置文件实体指定架构。 |
| `identities` | **（必需）**&#x200B;从中检索关联时间序列事件的配置文件数组列表。 数组中的每个条目均通过以下两种方式之一进行设置：1)使用由ID值和命名空间组成的完全限定的标识，或者2)提供XID。 |
| `fields` | 隔离返回到指定字段集的数据。 使用此选项可筛选在检索的数据中包含的架构字段。 示例： personalEmail，person.name，person.gender |
| `mergePolicyId` | 标识用于管理返回数据的合并策略。 如果未在服务调用中指定架构，则将使用贵组织对该架构的默认值。 如果尚未配置默认合并策略，则默认设置是无配置文件合并和无身份拼接。 |
| `orderby` | 按时间戳检索的体验事件的排序顺序，写为`(+/-)timestamp`，默认值为`+timestamp`。 |
| `timeFilter.startTime` | 指定过滤时间序列对象的开始时间（以毫秒为单位）。 |
| `timeFilter.endTime` | 指定过滤时间序列对象的结束时间（以毫秒为单位）。 |
| `limit` | 指定要返回的最大对象数的数值。 默认值：1000 |
| `withCA` | 用于启用计算属性进行查找的功能标志。 默认值： false |

**响应**

成功的响应将返回与请求中指定的多个配置文件关联的时间系列事件的分页列表。

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

在此示例响应中，列出的第一个配置文件(“GkouAW-yD9aoRCPhRYROJ-TetAFW”)为`_links.next.payload`提供了一个值，这意味着此配置文件还有其他结果页。 有关如何访问这些附加结果的详细信息，请参阅以下有关[访问附加结果](#access-additional-results)的部分。

### 访问其他结果 {#access-additional-results}

检索时间序列事件时，可能会返回许多结果，因此结果通常会分页。 如果特定配置文件有后续结果页面，则该配置文件的`_links.next.payload`值将包含一个有效负荷对象。

在请求正文中使用此有效负载，您可以对`access/entities`端点执行额外的POST请求，以检索该配置文件的后续时间序列数据页。

## 访问多个架构实体中的时间序列事件

您可以访问通过关系描述符连接的多个实体。 以下示例API调用假定已在两个架构之间定义了关系。 有关关系描述符的详细信息，请阅读[!DNL Schema Registry] API开发人员指南[描述符终结点指南](../../xdm/api/descriptors.md)。

您可以在请求路径中包含查询参数，以指定要访问的数据。 您可以包含多个参数，以&amp;分隔。 附录的[查询参数](#query-parameters)部分提供了有效参数的完整列表。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**请求**

以下请求检索包含先前建立的关系描述符的实体，以访问不同架构的信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的响应将返回与多个实体关联的时间系列事件的分页列表。

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### 访问结果的后续页面

检索时序事件时，结果将分页。 如果有后续结果页，则`_page.next`属性将包含ID。 此外，`_links.next.href`属性通过向`access/entities`端点发出其他GET请求来提供用于检索后续页面的请求URI。

## 后续步骤

按照本指南，您已成功访问[!DNL Real-Time Customer Profile]数据字段、配置文件和时序数据。 要了解如何访问存储在[!DNL Platform]中的其他数据资源，请参阅[数据访问概述](../../data-access/home.md)。

## 附录 {#appendix}

以下部分提供有关使用API访问[!DNL Profile]数据的补充信息。

### 查询参数 {#query-parameters}

在`/access/entities`终结点的GET请求路径中使用了以下参数。 它们用于标识要访问的配置文件实体，并筛选响应中返回的数据。 必填参数标有标签，其余参数为可选参数。

| 参数 | 描述 | 示例 |
|---|---|---|
| `schema.name` | **（必需）**&#x200B;要检索的实体的XDM架构 | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | 如果`schema.name`是“_xdm.context.experienceevent”，该值必须指定与时间序列事件相关的配置文件实体的架构。 | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **（必需）**&#x200B;实体的ID。 如果此参数的值不是XID，则还必须提供标识命名空间参数（请参阅下面的`entityIdNS`）。 | `entityId=janedoe@example.com` |
| `entityIdNS` | 如果未将`entityId`作为XID提供，则此字段必须指定标识命名空间。 | `entityIdNE=email` |
| `relatedEntityId` | 如果`schema.name`是“_xdm.context.experienceevent”，该值必须指定相关配置文件实体的标识命名空间。 此值遵循与`entityId`相同的规则。 | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | 如果`schema.name`是“_xdm.context.experienceevent”，此值必须为`relatedEntityId`中指定的实体指定身份命名空间。 | `relatedEntityIdNS=CRMID` |
| `fields` | 筛选响应中返回的数据。 使用此选项可指定要包含在检索的数据中的架构字段值。 对于多个字段，请使用逗号分隔值，且中间不应有空格 | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | 标识用于管理返回数据的合并策略。 如果未在调用中指定架构，则将使用您组织对该架构的默认值。 如果尚未配置默认合并策略，则默认设置是无配置文件合并和无身份拼接。 | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 按时间戳检索的体验事件的排序顺序，写为`(+/-)timestamp`，默认值为`+timestamp`。 | `orderby=-timestamp` |
| `startTime` | 指定过滤时间序列对象的开始时间（以毫秒为单位）。 | `startTime=1539838505` |
| `endTime` | 指定过滤时间序列对象的结束时间（以毫秒为单位）。 | `endTime=1539838510` |
| `limit` | 指定要返回的最大对象数的数值。 默认值：1000 | `limit=100` |
| `property` | 按属性值筛选。 支持以下计算器： =、！=， &lt;， &lt;=， >， >=。 只能与体验事件一起使用，最多支持三个属性。 | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | 用于启用计算属性进行查找的功能标志。 默认值： false | `withCA=true` |
