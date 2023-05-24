---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 實體（設定檔存取） API端點
type: Documentation
description: Adobe Experience Platform可讓您使用RESTful API或使用者介面存取即時客戶設定檔資料。 本指南概述如何使用設定檔API存取實體（通常稱為「設定檔」）。
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 1%

---

# 實體端點（設定檔存取）

Adobe Experience Platform可讓您存取 [!DNL Real-Time Customer Profile] 使用RESTful API或使用者介面的資料。 本指南概述如何使用API存取實體（通常稱為「設定檔」）。 有關使用存取設定檔的詳細資訊 [!DNL Platform] UI，請參閱 [設定檔使用手冊](../ui/user-guide.md).

## 快速入门

本指南中使用的API端點是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 在繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

## 依身分存取設定檔資料

您可以存取 [!DNL Profile] 向以下專案發出GET要求 `/access/entities` 端點，並將實體的身分識別提供為一連串查詢引數。 此身分包含ID值(`entityId`)和身分名稱空間(`entityIdNS`)。

請求路徑中提供的查詢引數會指定要存取哪些資料。 您可以包含多個引數，以&amp;分隔。 有效引數的完整清單提供於 [查詢引數](#query-parameters) 一節。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**请求**

以下請求會使用身分擷取客戶的電子郵件和名稱：

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
>如果相關圖表連結超過50個身分，此服務將傳回HTTP狀態422和「太多相關身分」訊息。 如果收到此錯誤，請考慮新增更多查詢引數來縮小搜尋範圍。

## 依身分清單存取設定檔資料

您可以透過向向發出POST請求，依多個設定檔實體的身分來存取它們 `/access/entities` 端點，並在裝載中提供身分。 這些身分識別包含ID值(`entityId`)和身分名稱空間(`entityIdNS`)。

**API格式**

```http
POST /access/entities
```

**请求**

以下請求會根據身分清單擷取多個客戶的名稱和電子郵件地址：

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
| `schema.name` | ***（必要）*** 實體所屬的XDM結構描述名稱。 |
| `fields` | 要以字串陣列形式傳回的XDM欄位。 依預設，將會傳回所有欄位。 |
| `identities` | ***（必要）*** 包含您要存取之實體身分清單的陣列。 |
| `identities.entityId` | 您要存取之實體的ID。 |
| `identities.entityIdNS.code` | 您要存取之實體ID的名稱空間。 |
| `timeFilter.startTime` | 時間範圍篩選器的開始時間，包括。 應為毫秒詳細程度。 如果未指定，預設值為可用時間的開始。 |
| `timeFilter.endTime` | 時間範圍篩選的結束時間，已排除。 應為毫秒詳細程度。 預設值（如果未指定）為可用時間的結尾。 |
| `limit` | 要傳回的記錄數。 僅適用於傳回的體驗事件數。 預設值： 1,000。 |
| `orderby` | 依時間戳記所擷取的體驗事件排序順序，寫成 `(+/-)timestamp` 預設為 `+timestamp`. |
| `withCA` | 啟用計算屬性以供查閱的功能標幟。 預設： false。 |

**回應**
成功的回應會傳回要求內文中指定之實體的要求欄位。

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

## 依身分存取設定檔的時間序列事件

您可以透過向以下專案發出GET要求，以透過相關設定檔實體的身分存取時間序列事件： `/access/entities` 端點。 此身分包含ID值(`entityId`)和身分名稱空間(`entityIdNS`)。

請求路徑中提供的查詢引數會指定要存取哪些資料。 您可以包含多個引數，以&amp;分隔。 有效引數的完整清單提供於 [查詢引數](#query-parameters) 一節。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**请求**

以下請求會依ID尋找設定檔實體，並擷取屬性的值 `endUserIDs`， `web`、和 `channel` 與實體相關聯的所有時間序列事件。

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回要求查詢引數中指定的時間序列事件和相關欄位的分頁清單。

>[!NOTE]
>
>請求指定了一個的限制(`limit=1`)，因此， `count` 在以下的回應中為1，且僅傳回一個實體。

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

### 存取後續結果頁面

擷取時間序列事件時，結果會分頁。 如果有後續結果頁面，則 `_page.next` 屬性將包含ID。 此外， `_links.next.href` 屬性提供擷取下一頁的要求URI。 GET若要擷取結果，請對 `/access/entities` 端點，不過您必須確定取代 `/entities` 以及所提供URI的值。

>[!NOTE]
>
>請確定不要不小心重複 `/entities/` 在請求路徑中。 它應該只會出現一次，例如， `/access/entities?start=...`

**API格式**

```http
GET /access/{NEXT_URI}
```

| 参数 | 描述 |
|---|---|
| `{NEXT_URI}` | URI值取自 `_links.next.href`. |

**请求**

以下請求會使用，擷取結果的下一頁 `_links.next.href` URI作為請求路徑。

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回結果的下一頁。 此回應沒有後續的結果頁面，如的空字串值所指示 `_page.next` 和 `_links.next.href`.

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

## 依身分存取多個設定檔的時間序列事件

您可以透過向發出POST請求，從多個關聯的設定檔存取時間序列事件 `/access/entities` 端點，並在裝載中提供設定檔身分。 這些身分分別包含一個ID值(`entityId`)和身分名稱空間(`entityIdNS`)。

**API格式**

```http
POST /access/entities
```

**请求**

以下請求會擷取與設定檔身分識別清單相關之時間序列事件的使用者ID、當地時間和國家/地區代碼：

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
| `schema.name` | **（必要）** 要擷取的實體的XDM結構描述 |
| `relatedSchema.name` | 若 `schema.name` 是 `_xdm.context.experienceevent` 此值必須指定與時間序列事件相關的設定檔實體的結構描述。 |
| `identities` | **（必要）** 要從中擷取關聯時間序列事件的設定檔清單。 陣列中的每個專案都是以下列兩種方式之一設定： 1)使用由ID值和名稱空間組成的完整身分識別，或2)提供XID。 |
| `fields` | 隔離傳回指定欄位集的資料。 使用此選項來篩選在擷取的資料中包含哪些結構描述欄位。 範例： personalEmail，person.name，person.gender |
| `mergePolicyId` | 識別用來控管傳回資料的合併原則。 如果服務呼叫中未指定架構，則會使用您組織對該架構的預設值。 如果尚未設定預設合併原則，預設值為無設定檔合併及無身分拼接。 |
| `orderby` | 依時間戳記所擷取的體驗事件排序順序，寫成 `(+/-)timestamp` 預設為 `+timestamp`. |
| `timeFilter.startTime` | 指定篩選時間序列物件的開始時間（毫秒）。 |
| `timeFilter.endTime` | 指定篩選時間序列物件的結束時間（毫秒）。 |
| `limit` | 指定要傳回之物件數目上限的數值。 預設： 1000 |
| `withCA` | 啟用計算屬性以供查閱的功能標幟。 預設： false |

**响应**

成功的回應會傳回與請求中指定的多個設定檔相關聯的時間序列事件分頁清單。

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

在此範例回應中，列出的第一個設定檔(「GkouAW-yD9aoRCPhRYROJ-TetAFW」)會提供 `_links.next.payload`，表示此設定檔還有其他結果頁面。 請參閱以下章節： [存取其他結果](#access-additional-results) 以取得如何存取這些其他結果的詳細資訊。

### 存取其他結果 {#access-additional-results}

擷取時間序列事件時，可能會傳回許多結果，因此結果通常會分頁。 如果特定設定檔有後續結果頁面，則 `_links.next.payload` 該設定檔的值將包含裝載物件。

POST在請求內文中使用此裝載，您可以對 `access/entities` 端點以擷取該設定檔的後續時間序列資料頁面。

## 存取多個結構描述實體中的時間序列事件

您可以存取透過關係描述項連線的多個實體。 以下範例API呼叫假設兩個結構描述之間已定義關係。 如需關係描述元的詳細資訊，請閱讀 [!DNL Schema Registry] API開發人員指南 [描述項端點指南](../../xdm/api/descriptors.md).

您可以在請求路徑中包含查詢引數，以指定要存取哪些資料。 您可以包含多個引數，以&amp;分隔。 有效引數的完整清單提供於 [查詢引數](#query-parameters) 一節。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**请求**

以下請求會擷取包含先前已建立關係描述項的實體，以存取不同結構描述中的資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的回應會傳回與多個實體相關聯的時間序列事件分頁清單。

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

### 存取後續結果頁面

擷取時間序列事件時，結果會分頁。 如果有後續結果頁面，則 `_page.next` 屬性將包含ID。 此外， `_links.next.href` 屬性透過向提出其他GET請求，提供用於擷取後續頁面的請求URI。 `access/entities` 端點。

## 后续步骤

依照本指南，您已成功存取 [!DNL Real-Time Customer Profile] 資料欄位、設定檔和時間序列資料。 瞭解如何存取中儲存的其他資料資源 [!DNL Platform]，請參閱 [資料存取總覽](../../data-access/home.md).

## 附录 {#appendix}

下節提供有關存取的補充資訊 [!DNL Profile] 使用API的資料。

### 查詢引數 {#query-parameters}

以下引數用於向發出之GET請求的路徑 `/access/entities` 端點。 它們用於識別您要存取的設定檔實體，並篩選回應中傳回的資料。 必要引數會加上標籤，其餘引數則為選用。

| 参数 | 描述 | 示例 |
|---|---|---|
| `schema.name` | **（必要）** 要擷取的實體的XDM結構描述 | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | 若 `schema.name` 為「_xdm.context.experienceevent」，此值必須指定時間序列事件相關的設定檔實體架構。 | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **（必要）** 實體的識別碼。 如果此引數的值不是XID，則必須同時提供身分名稱空間引數(請參閱 `entityIdNS` 下)。 | `entityId=janedoe@example.com` |
| `entityIdNS` | 若 `entityId` 不是以XID提供，此欄位必須指定身分名稱空間。 | `entityIdNE=email` |
| `relatedEntityId` | 若 `schema.name` 為「_xdm.context.experienceevent」，此值必須指定相關設定檔實體的身分名稱空間。 此值遵循與相同的規則 `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | 若 `schema.name` 為「_xdm.context.experienceevent」，此值必須指定中指定的實體的身分名稱空間 `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | 篩選回應中傳回的資料。 使用此專案來指定要包含在擷取之資料中的結構描述欄位值。 若為多個欄位，請用逗號分隔值，且中間不應有空格 | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | 識別用來控管傳回資料的合併原則。 如果呼叫中未指定其中一個結構描述，則會使用您組織對該結構描述的預設值。 如果尚未設定預設合併原則，預設值為無設定檔合併及無身分拼接。 | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 依時間戳記所擷取的體驗事件排序順序，寫成 `(+/-)timestamp` 預設為 `+timestamp`. | `orderby=-timestamp` |
| `startTime` | 指定篩選時間序列物件的開始時間（毫秒）。 | `startTime=1539838505` |
| `endTime` | 指定篩選時間序列物件的結束時間（毫秒）。 | `endTime=1539838510` |
| `limit` | 指定要傳回之物件數目上限的數值。 預設： 1000 | `limit=100` |
| `property` | 依屬性值篩選。 支援下列求值器：=、！=， &lt;， &lt;=， >， >=。 只能用於體驗事件，最多支援三個屬性。 | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | 啟用計算屬性以供查閱的功能標幟。 預設： false | `withCA=true` |
