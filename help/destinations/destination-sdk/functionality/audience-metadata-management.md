---
description: 使用對象中繼資料範本，以程式設計方式在您的目的地建立、更新或刪除對象。 Adobe提供可擴充的對象中繼資料範本，您可以根據行銷API的規格進行設定。 定義、測試及提交範本後，Adobe會使用範本來建構對目的地的API呼叫。
title: 對象中繼資料管理
source-git-commit: e69bd819fb8ef6c2384a2b843542d1ddcea0661f
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 0%

---


# 對象中繼資料管理

使用對象中繼資料範本，以程式設計方式在您的目的地建立、更新或刪除對象。 Adobe提供可擴充的對象中繼資料範本，您可以根據行銷API的規格進行設定。 定義、測試及提交設定後，Adobe會使用該設定來建構對目的地的API呼叫。

您可以使用設定本檔案中描述的功能 `/authoring/audience-templates` api端點。 讀取 [建立中繼資料範本](../metadata-api/create-audience-template.md) 如需您可以在端點上執行的操作的完整清單。

## 何時使用對象中繼資料管理端點 {#when-to-use}

根據您的API設定，當您在Experience Platform中設定目的地時，不一定需要使用對象中繼資料管理端點。 使用下方的決策樹圖表，瞭解何時應使用對象中繼資料端點，以及如何為目的地設定對象中繼資料範本。

![決策樹圖表](../assets/functionality/audience-metadata-decision-tree.png)

## 受眾中繼資料管理支援的使用案例 {#use-cases}

透過Destination SDK中的受眾中繼資料支援，當您設定Experience Platform目的地時，可以為Platform使用者提供下列其中一個選項，讓他們將區段對應及啟用至您的目的地。 您可以透過中的引數控制使用者可用的選項 [對象中繼資料設定](../functionality/destination-configuration/audience-metadata-configuration.md) 目的地設定的區段。

### 使用案例1 — 您有第三方API，使用者不需要輸入對應ID

如果您有建立/更新/刪除區段或受眾的API端點，則可以使用受眾中繼資料範本設定Destination SDK，以符合區段建立/更新/刪除端點的規格。 Experience Platform能以程式設計方式建立/更新/刪除區段，並將中繼資料同步回Experience Platform。

在Experience Platform使用者介面(UI)中將區段啟用至您的目的地時，使用者不需要手動填寫啟用工作流程中的區段對應ID欄位。

### 使用案例2 — 使用者需要先在您的目的地中建立區段，並需要手動輸入對應ID

如果您的目的地需要合作夥伴或使用者手動建立區段和其他中繼資料，則使用者必須在啟動工作流程中手動填寫區段對應ID欄位，以在目的地和Experience Platform之間同步區段中繼資料。

![輸入對應ID](../assets/functionality/input-mapping-id.png)

### 使用案例3 — 您的目的地接受Experience Platform區段ID，使用者不需要手動輸入對應ID

如果您的目的地系統接受Experience Platform區段ID，您可以在對象中繼資料範本中加以設定。 使用者啟用區段時，不必填入區段對應ID。

## 通用且可擴充的對象範本 {#generic-and-extensible}

為了支援上面列出的使用案例，Adobe提供您一個通用範本，您可以根據您的API規格來自訂該範本。

您可以使用通用範本來 [建立新的受眾範本](../metadata-api/create-audience-template.md) 如果您的API支援：

* HTTP方法：POST、GET、PUT、DELETE、PATCH
* 驗證型別：OAuth 1、具有重新整理權杖的OAuth 2、具有持有人權杖的OAuth 2
* 函式：建立對象、更新對象、取得對象、刪除對象、驗證認證

如果您的使用案例需要，Adobe工程團隊可以與您合作，使用自訂欄位展開通用範本。

## 設定範例 {#configuration-examples}

本節包含三個一般受眾中繼資料設定的範例，以供您參考，以及設定的主要區段說明。 請注意三個設定範例之間的URL、標頭、請求和回應內文差異。 這是因為三個範例平台行銷API的規格不同。

請注意，在一些範例中，巨集欄位如 `{{authData.accessToken}}` 或 `{{segment.name}}` 用於URL，而在其他範例中，這些會用於標頭或請求內文。 這確實取決於您的行銷API規格。

| 範本區段 | 描述 |
|--- |--- |
| `create` | 包含對API進行HTTP呼叫的所有必要元件（URL、HTTP方法、標題、要求與回應內文），以程式設計方式在您的平台中建立區段/對象，並將資訊同步回Adobe Experience Platform。 |
| `update` | 包含對API進行HTTP呼叫的所有必要元件（URL、HTTP方法、標頭、要求與回應內文），以程式設計方式更新您平台中的區段/對象，並將資訊同步回Adobe Experience Platform。 |
| `delete` | 包含對API進行HTTP呼叫的所有必要元件（URL、HTTP方法、標頭、要求與回應內文），以便以程式設計方式刪除平台中的區段/對象。 |
| `validate` | 在呼叫合作夥伴API之前，執行範本設定中任何欄位的驗證。 例如，您可以驗證使用者的帳戶ID是否正確輸入。 |
| `notify` | 僅適用於以檔案為基礎的目的地。 包含對API進行HTTP呼叫的所有必要元件（URL、HTTP方法、標頭、請求和回應內文），以通知您檔案匯出成功。 |

{style="table-layout:auto"}

### 串流範例1 {#example-1}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

### 串流範例2 {#example-2}

```json
{
   "instanceId":"12c78017-5af3-4d4e-8f9c-d330c547c482",
   "createdDate":"2021-07-20T13:27:37.029490Z",
   "lastModifiedDate":"2021-07-20T18:53:03.622306Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v1.0/{{customerData.accountId}}/customaudiences?fields=name,description,account_id&subtype=CUSTOM&name={{segment.name}}&customer_file_source={{segment.metadata.customer_file_source}}&access_token={{authData.accessToken}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?field=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}&&name={{segment.name}}&description={{segment.description}}&customer_file_source={{segment.metadata.customer_file_source}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v1.0/{{segment.alias}}?fields=name,description,account_id&access_token={{authData.accessToken}}&customerAudienceId={{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      },
      "validate":{
         "url":"https://api.moviestar.com/v1.0/permissions?access_token={{authData.accessToken}}",
         "httpMethod":"GET",
         "headers":[
            {
               "value":"application/x-www-form-urlencoded",
               "header":"Content-Type"
            }
         ],
         "responseFields":[
            {
               "value":"{{response.data[0].permission}}",
               "name":"Id"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{error.message}}",
               "name":"message"
            }
         ]
      }
   }
}
```

### 串流範例3 {#example-3}

```json
{
   "instanceId":"12a3238f-b509-4a40-b8fb-0a5006e7901d",
   "createdDate":"2021-07-20T13:30:30.843054Z",
   "lastModifiedDate":"2021-07-21T16:33:05.787472Z",
   "metadataTemplate":{
      "create":{
         "url":"https://api.moviestar.com/v2/dmpSegments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{authData.accessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "name":"{{segment.name}}",
               "type":"USER",
               "account":"{{customerData.accountId}}",
               "accessPolicy":"PRIVATE",
               "destinations":[
                  {
                     "destination":"MOVIESTAR"
                  }
               ],
               "sourcePlatform":"ADOBE"
            }
         },
         "responseFields":[
            {
               "value":"{{headers.x-moviestar-id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{message}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{authData.accessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "patch":{
                  "$set":{
                     "name":"{{segment.name}}"
                  }
               }
            }
         },
         "responseErrorFields":[
            {
               "value":"{{message}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://api.moviestar.com/v2/dmpSegments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{authData.accessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{message}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar audience template - Third example"
   }
}
```


### 檔案型範例 {#example-file-based}

```json
{
   "instanceId":"34ab9cc2-2536-44a5-9dc5-b2fea60b3bd6",
   "createdDate":"2021-07-26T19:30:52.012490Z",
   "lastModifiedDate":"2021-07-27T21:25:42.763478Z",
   "metadataTemplate":{
      "create":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments",
         "httpMethod":"POST",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}",
                     "source_type":"FIRST_PARTY",
                     "ad_account_id":"{{customerData.accountId}}",
                     "retention_in_days":180
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "update":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "notify":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"PUT",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "requestBody":{
            "json":{
               "segments":[
                  {
                     "id":"{{segment.alias}}",
                     "name":"{{segment.name}}",
                     "description":"{{segment.description}}"
                  }
               ]
            }
         },
         "responseFields":[
            {
               "value":"{{body.segments[0].segment.id}}",
               "name":"externalAudienceId"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "delete":{
         "url":"https://adsapi.moviestar.com/v1/adaccounts/{{customerData.accountId}}/segments/{{segment.alias}}",
         "httpMethod":"DELETE",
         "headers":[
            {
               "value":"application/json",
               "header":"Content-Type"
            },
            {
               "value":"Bearer {{oauth2ServiceAccessToken}}",
               "header":"Authorization"
            }
         ],
         "responseErrorFields":[
            {
               "value":"{{root}}",
               "name":"message"
            }
         ]
      },
      "name":"Moviestar destination audience template - Example 1"
   }
}
```

在中尋找範本中所有引數的說明 [建立對象範本](../metadata-api/create-audience-template.md) API參考。

## 對象中繼資料範本中使用的巨集

若要在Experience Platform與API之間傳遞區段ID、存取權杖、錯誤訊息等資訊，受眾範本包含您可使用的巨集。 請閱讀以下本頁面三個設定範例中所使用的巨集說明：

| 巨集 | 描述 |
|--- |--- |
| `{{segment.alias}}` | 可讓您存取Experience Platform中的區段別名。 |
| `{{segment.name}}` | 可讓您存取Experience Platform中的區段名稱。 |
| `{{segment.id}}` | 可讓您存取Experience Platform中的區段ID。 |
| `{{customerData.accountId}}` | 可讓您存取在目的地設定中設定的帳戶ID欄位。 |
| `{{oauth2ServiceAccessToken}}` | 可讓您根據您的OAuth 2設定動態產生存取權杖。 |
| `{{authData.accessToken}}` | 可讓您將存取Token傳遞至API端點。 使用 `{{authData.accessToken}}` 如果Experience Platform應使用不會到期的Token來連線至您的目的地，否則請使用 `{{oauth2ServiceAccessToken}}` 以產生存取Token。 |
| `{{body.segments[0].segment.id}}` | 傳回已建立對象的唯一識別碼，作為索引鍵的值 `externalAudienceId`. |
| `{{error.message}}` | 傳回將在Experience PlatformUI中向使用者顯示的錯誤訊息。 |

{style="table-layout:auto"}
