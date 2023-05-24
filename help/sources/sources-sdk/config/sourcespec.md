---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: 設定自助式來源的來源規格（批次SDK）
description: 本檔案提供使用Self-Serve Sources (Batch SDK)所需準備的設定概觀。
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1687'
ht-degree: 1%

---

# 設定自助式來源的來源規格（批次SDK）

來源規格包含來源的特定資訊，包括與來源類別、測試版狀態和目錄圖示相關的屬性。 它們也包含有用的資訊，例如URL引數、內容、標題和排程。 來源規格也說明從基本連線建立來源連線所需之引數的結構。 若要建立來源連線，結構描述是必要的。

請參閱 [附錄](#source-spec) 以完全填入的來源規格為例。


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "host",
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `sourceSpec.attributes` | 包含UI或API專屬來源的資訊。 |
| `sourceSpec.attributes.uiAttributes` | 顯示UI特定來源的資訊。 |
| `sourceSpec.attributes.uiAttributes.isBeta` | 布林值屬性，指出來源是否需要客戶提供更多意見回饋才能新增至其功能。 | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | 定義來源的類別。 | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | 定義在Platform UI中用於呈現來源的圖示。 | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | 顯示來源的簡短說明。 |
| `sourceSpec.attributes.uiAttributes.label` | 顯示用於在Platform UI中呈現來源的標籤。 |
| `sourceSpec.attributes.spec.properties.urlParams` | 包含有關URL資源路徑、方法和支援的查詢引數的資訊。 |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | 定義從何處擷取資料的來源資源路徑。 | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | 定義用於向資源發出擷取資料之請求的HTTP方法。 | `GET`、`POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | 定義支援的查詢引數，可在提出擷取資料的請求時，用於附加來源URL。 **注意**：任何使用者提供的引數值都必須格式化為預留位置。 例如：`${USER_PARAMETER}`。 | `"queryParams" : {"key" : "value", "key1" : "value1"}` 將會附加至來源URL作為： `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | 定義擷取資料時，必須在來源URL的HTTP請求中提供的標頭。 | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | 此屬性可設定為透過POST要求傳送HTTP內文。 |
| `sourceSpec.attributes.spec.properties.contentPath` | 定義包含需要擷取至Platform的專案清單的節點。 此屬性應遵循有效的JSON路徑語法，且必須指向特定陣列。 | 檢視 [其他資源區段](#content-path) 內容路徑中包含的資源範例。 |
| `sourceSpec.attributes.spec.properties.contentPath.path` | 指向要擷取至Platform的集合記錄的路徑。 | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | 此屬性可讓您從在內容路徑中識別的資源中，識別要排除以避免內嵌的特定專案。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | 此屬性可讓您明確指定要保留的個別屬性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | 此屬性可讓您覆寫您在中指定的屬性名稱值 `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | 此屬性可讓您平面化兩個陣列，並將資源資料轉換為Platform資源。 |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | 指向您要平面化的集合記錄的路徑。 | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | 此屬性可讓您從實體路徑中識別的資源中，識別要排除以防止內嵌的特定專案。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | 此屬性可讓您明確指定要保留的個別屬性。 | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | 此屬性可讓您覆寫您在中指定的屬性名稱值 `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | 定義必須提供的引數或欄位，才能從使用者目前的頁面回應或建立下一頁URL時，取得下一頁的連結。 |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 顯示您的來源支援的分頁型別型別。 | <ul><li>`OFFSET`：此分頁型別可讓您透過指定從何處開始產生陣列以及限制傳回的結果來剖析結果。</li><li>`POINTER`：此分頁型別可讓您使用 `pointer` 變數來指向需要隨請求傳送的特定專案。 指標型別分頁需要在裝載中指向下一頁的路徑。</li><li>`CONTINUATION_TOKEN`：此分頁型別可讓您將查詢或標頭引數附加一個接續Token，以從來源擷取剩餘的傳回資料（由於預先決定的最大值，這些資料最初並未傳回）。</li><li>`PAGE`：此分頁型別可讓您將查詢引數附加至分頁引數，以便依頁面周遊傳回資料，從第0頁開始。</li><li>`NONE`：此分頁型別可用於不支援任何可用分頁型別的來源。 分頁型別 `NONE` 會在要求後傳回整個回應資料。</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | 限制的名稱，API可透過該名稱指定要在頁面中擷取的記錄數。 | `limit` 或 `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 要在頁面中擷取的記錄數。 | `limit=10` 或 `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 位移屬性名稱。 如果分頁型別設定為，則必須執行此設定 `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 指標屬性名稱。 這需要指向下一頁之屬性的json路徑。 如果分頁型別設定為，則必須執行此設定 `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 包含定義來源支援之排程格式的引數。 排程引數包括 `startTime` 和 `endTime`，兩者皆可讓您設定批次執行的特定時間間隔，進而確保不會再次擷取先前批次執行中擷取的記錄。 |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 定義開始時間引數名稱 | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 定義結束時間引數名稱 | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | 定義支援的格式 `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | 定義支援的格式 `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 定義使用者提供的引數，以擷取資源值。 | 請參閱 [其他資源](#user-input) 例如，使用者輸入的引數範例 `spec.properties`. |

{style="table-layout:auto"}

## 其他资源 {#appendix}

以下小節提供您可以對進行其他設定的相關資訊 `sourceSpec`，包括進階排程和自訂結構描述。

### 內容路徑範例 {#content-path}

以下範例為 `contentPath` 中的屬性 [!DNL MailChimp Members] 連線規格。

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` 使用者輸入範例 {#user-input}

以下是使用者提供的範例 `spec.properties` 使用 [!DNL MailChimp Members] 連線規格。

在此範例中， `listId` 作為的一部分提供 `urlParams.path`. 如果您需要擷取 `listId` 來自客戶，則您也必須將其定義為的一部分 `spec.properties`.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### 來源規格範例 {#source-spec}

以下為已完成的來源規格，使用 [!DNL MailChimp Members]：

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "host": "https://{domain}.api.mailchimp.com",
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### 為您的來源設定不同的分頁型別 {#pagination}

以下是自助來源（批次SDK）支援的其他分頁型別範例：

#### `CONTINUATION_TOKEN`

分頁的繼續權杖型別會傳回字串權杖，表示由於單一回應中可傳回的專案數量已預先設定上限，因此存在更多無法傳回的專案。

支援繼續記號型別分頁的來源可能有類似下列的分頁引數：

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| 属性 | 描述 |
| --- | --- |
| `type` | 用來傳回資料的分頁型別。 |
| `continuationTokenPath` | 必須附加至查詢引數的值，才能移至傳回結果的下一頁。 |
| `parameterType` | 此 `parameterType` 屬性會定義 `parameterName` 必須新增。 此 `QUERYPARAM` type可讓您將查詢附加 `parameterName`. 此 `HEADERPARAM` 可讓您新增 `parameterName` 至您的標頭請求。 |
| `parameterName` | 用於合併接續權杖的引數名稱。 格式如下： `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | 此 `delayRequestMillis` 分頁屬性可讓您控制向來源提出要求的速率。 有些來源會限制每分鐘可提出的請求數。 例如， [!DNL Zendesk] 具有每分鐘100個請求的限制，並定義  `delayRequestMillis` 至 `850` 可讓您將來源設定為每分鐘發出約80個請求，遠低於每分鐘100個請求的臨界值。 |

以下範例為使用接續權杖型別分頁傳回的回應：

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

#### `PAGE`

此 `PAGE` 分頁型別可讓您依從零開始的頁數遍歷傳回資料。 使用時 `PAGE` 輸入分頁，您必須提供單一頁面中給定的記錄數。

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| 属性 | 描述 |
| --- | --- |
| `type` | 用來傳回資料的分頁型別。 |
| `limitName` | 限制的名稱，API可透過該名稱指定要在頁面中擷取的記錄數。 |
| `limitValue` | 要在頁面中擷取的記錄數。 |
| `pageParamName` | 您必須附加至查詢引數的引數名稱，才能在傳回資料的不同頁面中周遊。 例如， `https://abc.com?pageIndex=1` 會傳回API傳回裝載的第二頁。 |
| `maximumRequest` | 來源可為指定的增量執行提出的最大請求數。 目前的預設限製為10000。 |

#### `NONE`

此 `NONE` 分頁型別可用於不支援任何可用分頁型別的來源。 使用下列分頁型別的來源： `NONE` 提出GET要求時，只需傳回所有可擷取的記錄即可。

```json
"paginationParams": {
  "type": "NONE"
}
```

### 自助式來源的進階排程（批次SDK）

使用進階排程來設定來源的增量與回填排程。 此 `incremental` 屬性可讓您設定排程，讓來源僅擷取新記錄或已修改的記錄，而 `backfill` 屬性可讓您建立排程來擷取歷史資料。

透過進階排程，您可以使用來源特定的運算式和函式來設定增量排程和回填排程。 在以下範例中， [!DNL Zendesk] 來源需要將增量排程格式化為 `type:user updated > {START_TIME} updated < {END_TIME}` 和回填為 `type:user updated < {END_TIME}`.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| 属性 | 描述 |
| --- | --- |
| `scheduleParams.type` | 您的來源將使用的排程型別。 將此值設定為 `ADVANCE` 以使用進階排程型態。 |
| `scheduleParams.paramFormat` | 排程引數的定義格式。 此值可與您來源的 `scheduleStartParamFormat` 和 `scheduleEndParamFormat` 值。 |
| `scheduleParams.incremental` | 來源的增量查詢。 增量是指只擷取新資料或修改過的資料的擷取方法。 |
| `scheduleParams.backfill` | 來源的回填查詢。 回填是指擷取歷史資料的擷取方法。 |

設定進階排程後，您必須參考 `scheduleParams` 在URL、內文或標頭引數區段中，視您的特定來源支援而定。 在以下範例中， `{SCHEDULE_QUERY}` 是用來指定增量與回填排程運算式使用位置的預留位置。 若是 [!DNL Zendesk] 來源， `query` 用於 `queryParams` 以指定進階排程。

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### 新增自訂結構描述以定義來源的動態屬性

您可以包含自訂結構描述至 `sourceSpec` 定義來源所需的所有屬性，包括您可能需要的動態屬性。 您可以透過向以下專案發出PUT請求，更新來源對應的連線規格： `/connectionSpecs` 的端點 [!DNL Flow Service] API，同時在中提供您的自訂結構 `sourceSpec` 區段。

以下是您可以新增至來源連線規格的自訂結構描述範例：

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## 后续步骤

填入您的來源規格後，您可以繼續設定您要整合至平台的來源之瀏覽規格。 檢視檔案： [設定瀏覽規格](./explorespec.md) 以取得詳細資訊。
