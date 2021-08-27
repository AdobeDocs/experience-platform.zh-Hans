---
keywords: Experience Platform；配置文件；实时客户配置文件；疑难解答；API
title: 实体（配置文件访问）API端点
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform允许您使用RESTful API或用户界面访问实时客户资料数据。 本指南概述了如何使用配置文件API访问实体（通常称为“配置文件”）。
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 1%

---

# 实体端点（配置文件访问）

Adobe Experience Platform允许您使用RESTful API或用户界面访问[!DNL Real-time Customer Profile]数据。 本指南概述了如何使用API访问实体（通常称为“用户档案”）。 有关使用[!DNL Platform] UI访问用户档案的更多信息，请参阅[用户档案指南](../ui/user-guide.md)。

## 快速入门

本指南中使用的API端点是[[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 在继续操作之前，请查阅[快速入门指南](getting-started.md) ，以获取相关文档的链接、本文档中API调用示例的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需标头的重要信息。

## 按身份访问用户档案数据

您可以通过向`/access/entities`端点发出GET请求，并将实体的标识作为一系列查询参数来访问[!DNL Profile]实体。 此标识由ID值(`entityId`)和标识命名空间(`entityIdNS`)组成。

请求路径中提供的查询参数指定要访问的数据。 您可以包含多个参数，这些参数之间用与号(&amp;)分隔。 有效参数的完整列表见附录的[查询参数](#query-parameters)部分。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**请求**

以下请求会检索客户的电子邮件和使用身份的名称：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
>如果相关图链接的标识数超过50个，则此服务将返回HTTP状态422，并显示消息“相关标识过多”。 如果收到此错误，请考虑添加更多查询参数以缩小搜索范围。

## 按身份列表访问用户档案数据

您可以通过对`/access/entities`端点发出POST请求并在有效负载中提供标识，通过多个配置文件实体的标识来访问它们。 这些标识由ID值(`entityId`)和标识命名空间(`entityIdNS`)组成。

**API格式**

```http
POST /access/entities
```

**请求**

以下请求可按身份列表检索多个客户的名称和电子邮件地址：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `schema.name` | ***（必需）*** 实体所属的XDM架构的名称。 |
| `fields` | 要作为字符串数组返回的XDM字段。 默认情况下，将返回所有字段。 |
| `identities` | ***（必需）*** 一个数组，其中包含要访问的实体的标识列表。 |
| `identities.entityId` | 要访问的实体的ID。 |
| `identities.entityIdNS.code` | 要访问的实体ID的命名空间。 |
| `timeFilter.startTime` | 包含的时间范围过滤器的开始时间。 应以毫秒为粒度。 如果未指定，则默认值为可用时间的开始值。 |
| `timeFilter.endTime` | 排除的时间范围过滤器的结束时间。 应以毫秒为粒度。 如果未指定，则默认为可用时间的结束。 |
| `limit` | 要返回的记录数。 仅适用于返回的体验事件数。 默认：一千。 |
| `orderby` | 按时间戳列出的检索体验事件的排序顺序，编写为`(+/-)timestamp`，默认值为`+timestamp`。 |
| `withCA` | 用于启用计算属性以进行查找的功能标记。 默认：false。 |

****
响应成功响应会返回请求正文中指定的实体的请求字段。

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

您可以通过向`/access/entities`端点发出GET请求，通过其关联的配置文件实体的标识来访问时间系列事件。 此标识由ID值(`entityId`)和标识命名空间(`entityIdNS`)组成。

请求路径中提供的查询参数指定要访问的数据。 您可以包含多个参数，这些参数之间用与号(&amp;)分隔。 有效参数的完整列表见附录的[查询参数](#query-parameters)部分。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**请求**

以下请求按ID查找配置文件实体，并检索与实体关联的所有时间序列事件的属性`endUserIDs`、`web`和`channel`的值。

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回在请求查询参数中指定的时间系列事件和相关字段的分页列表。

>[!NOTE]
>
>请求指定了一个(`limit=1`)的限制，因此下面响应中的`count`为1，并且只返回一个实体。

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

### 访问后续的结果页面

在检索时间系列事件时，会对结果进行分页。 如果有后续的结果页，`_page.next`属性将包含ID。 此外， `_links.next.href`属性还提供用于检索下一页的请求URI。 要检索结果，请向`/access/entities`端点再次发出GET请求，但必须确保将`/entities`替换为提供的URI的值。

>[!NOTE]
>
>请确保不要意外地在请求路径中重复`/entities/`。 它应该只显示一次， `/access/entities?start=...`

**API格式**

```http
GET /access/{NEXT_URI}
```

| 参数 | 描述 |
|---|---|
| `{NEXT_URI}` | 从`_links.next.href`获取的URI值。 |

**请求**

以下请求使用`_links.next.href` URI作为请求路径来检索结果的下一页。

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回结果的下一页。 此响应没有后续的结果页，如`_page.next`和`_links.next.href`的空字符串值所示。

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

## 按身份访问多个用户档案的时间系列事件

您可以通过向`/access/entities`端点发出POST请求并在有效负载中提供配置文件标识，从多个关联的配置文件访问时间系列事件。 这些标识分别由ID值(`entityId`)和标识命名空间(`entityIdNS`)组成。

**API格式**

```http
POST /access/entities
```

**请求**

以下请求可检索与用户档案标识列表关联的时间系列事件的用户ID、本地时间和国家/地区代码：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `schema.name` | **（必需）** 要检索的实体的XDM架构 |
| `relatedSchema.name` | 如果`schema.name`为`_xdm.context.experienceevent`，则此值必须指定与时间系列事件相关的配置文件实体的架构。 |
| `identities` | **（必需）** 用于从中检索关联时间系列事件的配置文件数组列表。数组中的每个条目可通过以下两种方式之一进行设置：1)使用由ID值和命名空间组成的完全限定的身份，或2)提供XID。 |
| `fields` | 将返回的数据隔离到一组指定的字段。 使用此选项可筛选检索到的数据中包含的架构字段。 示例：personalEmail，person.name，person.gender |
| `mergePolicyId` | 确定用于管理返回数据的合并策略。 如果未在服务调用中指定某个架构，则将使用贵组织对该架构的默认设置。 如果尚未配置默认的合并策略，则默认值为“未合并配置文件”和“未拼合身份”。 |
| `orderby` | 按时间戳列出的检索体验事件的排序顺序，编写为`(+/-)timestamp`，默认值为`+timestamp`。 |
| `timeFilter.startTime` | 指定过滤时间系列对象的开始时间（以毫秒为单位）。 |
| `timeFilter.endTime` | 指定过滤时间系列对象的结束时间（以毫秒为单位）。 |
| `limit` | 指定要返回的最大对象数的数值。 默认：1000 |
| `withCA` | 用于启用计算属性以进行查找的功能标记。 默认：false |

**响应**

成功的响应会返回与请求中指定的多个用户档案关联的分页时间系列事件列表。

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

在此示例响应中，列出的第一个配置文件(&quot;GkouAW-yD9aoRCPhRROJ-TetAFW&quot;)为`_links.next.payload`提供了一个值，这表示此配置文件还有额外的结果页。 有关如何访问这些附加结果的详细信息，请参阅以下关于[访问其他结果](#access-additional-results)的部分。

### 访问其他结果 {#access-additional-results}

检索时间系列事件时，可能会返回许多结果，因此结果通常会进行分页。 如果某个特定配置文件有后续的结果页，则该配置文件的`_links.next.payload`值将包含有效负荷对象。

在请求正文中使用此有效负载，您可以对`access/entities`端点执行其他POST请求，以检索该配置文件的后续时间系列数据页。

## 访问多个架构实体中的时间系列事件

您可以访问通过关系描述符连接的多个实体。 以下示例API调用假定两个架构之间已定义关系。 有关关系描述符的更多信息，请阅读[!DNL Schema Registry] API开发人员指南[描述符终结点指南](../../xdm/api/descriptors.md)。

您可以在请求路径中包含查询参数，以指定要访问的数据。 您可以包含多个参数，这些参数之间用与号(&amp;)分隔。 有效参数的完整列表见附录的[查询参数](#query-parameters)部分。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**请求**

以下请求检索包含先前已建立的关系描述符的实体，以访问不同架构之间的信息。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应返回与多个实体相关联的时间系列事件的分页列表。

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

### 访问后续的结果页面

在检索时间系列事件时，会对结果进行分页。 如果有后续的结果页，`_page.next`属性将包含ID。 此外， `_links.next.href`属性通过向`access/entities`端点发出附加GET请求来提供用于检索后续页面的请求URI。

## 后续步骤

按照本指南，您已成功访问[!DNL Real-time Customer Profile]数据字段、配置文件和时间系列数据。 要了解如何访问存储在[!DNL Platform]中的其他数据资源，请参阅[数据访问概述](../../data-access/home.md)。

## 附录 {#appendix}

以下部分提供了有关使用API访问[!DNL Profile]数据的补充信息。

### 查询参数 {#query-parameters}

在`/access/entities`端点的GET请求路径中使用以下参数。 它们用于标识您希望访问的用户档案实体，并筛选响应中返回的数据。 必需的参数将进行标记，而其余参数则为可选参数。

| 参数 | 描述 | 示例 |
|---|---|---|
| `schema.name` | **（必需）** 要检索的实体的XDM架构 | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | 如果`schema.name`为“_xdm.context.experienceevent”，则此值必须指定与时间系列事件相关的配置文件实体架构。 | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **（必需）** 实体的ID。如果此参数的值不是XID，则还必须提供身份命名空间参数（请参阅下面的`entityIdNS`）。 | `entityId=janedoe@example.com` |
| `entityIdNS` | 如果未将`entityId`作为XID提供，则此字段必须指定身份命名空间。 | `entityIdNE=email` |
| `relatedEntityId` | 如果`schema.name`为“_xdm.context.experienceevent”，则此值必须指定相关配置文件实体的标识命名空间。 此值遵循与`entityId`相同的规则。 | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | 如果`schema.name`为“_xdm.context.experienceevent”，则此值必须为`relatedEntityId`中指定的实体指定标识命名空间。 | `relatedEntityIdNS=CRMID` |
| `fields` | 过滤响应中返回的数据。 使用此选项可指定要包含在检索数据中的架构字段值。 对于多个字段，用逗号分隔值，中间不带空格 | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | 确定用于管理返回数据的合并策略。 如果未在调用中指定某个架构，则将使用贵组织对该架构的默认设置。 如果尚未配置默认的合并策略，则默认值为“未合并配置文件”和“未拼合身份”。 | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 按时间戳列出的检索体验事件的排序顺序，编写为`(+/-)timestamp`，默认值为`+timestamp`。 | `orderby=-timestamp` |
| `startTime` | 指定过滤时间系列对象的开始时间（以毫秒为单位）。 | `startTime=1539838505` |
| `endTime` | 指定过滤时间系列对象的结束时间（以毫秒为单位）。 | `endTime=1539838510` |
| `limit` | 指定要返回的最大对象数的数值。 默认：1000 | `limit=100` |
| `property` | 按属性值过滤。 支持以下评估器：=, !=、&lt;、&lt;=、>、>=。 只能用于体验事件，最多支持三个属性。 | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | 用于启用计算属性以进行查找的功能标记。 默认：false | `withCA=true` |
