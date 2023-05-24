---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK建立對象範本的API呼叫的範例。
title: 建立對象範本
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---


# 建立對象範本

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/audience-templates`

對於使用Destination SDK建立的一些目的地，您需要建立對象中繼資料設定，以程式設計方式在目的地中建立、更新或刪除區段中繼資料。 此頁面說明如何使用 `/authoring/audience-templates` API端點以建立設定。

如需可透過此端點設定的功能的詳細說明，請參閱 [對象中繼資料管理](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值皆為 **區分大小寫**. 為避免區分大小寫錯誤，請完全按照檔案中所示使用引數名稱和值。

## 開始使用對象範本API作業 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 建立對象範本 {#create}

您可以建立新的受眾範本，方法是建立 `POST` 向以下專案提出的請求： `/authoring/audience-templates` 端點。

**API格式**

```http
POST /authoring/audience-templates
```

+++请求

以下請求會建立新的受眾範本，由承載中提供的引數設定。 以下裝載包含 `/authoring/audience-templates` 端點。 請注意，您不需要在呼叫上新增所有引數，而且範本可以根據您的API需求自訂。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      }
   },
   "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| 属性 | 类型 | 描述 |
| -------- | ----------- | ----------- |
| `name` | 字符串 | 您目的地的對象中繼資料範本名稱。 此名稱將出現在Experience Platform使用者介面的任何合作夥伴特定錯誤訊息中，隨後是剖析的錯誤訊息 `metadataTemplate.create.errorSchemaMap`. |
| `url` | 字符串 | API的URL和端點，用於在您的平台上建立、更新、刪除或驗證對象/區段。 兩個產業範例為： `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` 和 `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | 字符串 | 在您的端點上使用的方法，以程式設計方式在您的目的地建立、更新、刪除或驗證區段/對象。 例如： `POST`， `PUT`， `DELETE` |
| `headers.header` | 字符串 | 指定應新增至API呼叫的任何HTTP標頭。 例如：`"Content-Type"` |
| `headers.value` | 字符串 | 指定應新增至API呼叫的HTTP標頭值。 例如：`"application/x-www-form-urlencoded"` |
| `requestBody` | 字符串 | 指定應傳送至API的訊息內文內容。 應新增至 `requestBody` 物件取決於API接受的欄位。 如需範例，請參閱 [第一個範本範例](../functionality/audience-metadata-management.md#example-1) （在對象中繼資料功能檔案中）。 |
| `responseFields.name` | 字符串 | 指定呼叫時API傳回的任何回應欄位。 如需範例，請參閱 [範本範例](../functionality/audience-metadata-management.md#examples) （在對象中繼資料功能檔案中）。 |
| `responseFields.value` | 字符串 | 指定API在呼叫時傳回之任何回應欄位的值。 |
| `responseErrorFields.name` | 字符串 | 指定呼叫時API傳回的任何回應欄位。 如需範例，請參閱 [ 範本範例](../functionality/audience-metadata-management.md#examples) （在對象中繼資料功能檔案中）。 |
| `responseErrorFields.value` | 字符串 | 剖析從您的目的地傳回API呼叫回應時的任何錯誤訊息。 這些錯誤訊息會在Experience Platform使用者介面中向使用者顯示。 |
| `validations.field` | 字符串 | 指示在對目的地進行API呼叫之前，是否應對任何欄位執行驗證。 例如，您可以使用 `{{validations.accountId}}` 驗證使用者的帳戶ID。 |
| `validations.regex` | 字符串 | 表示欄位應如何建構才能通過驗證。 |

{style="table-layout:auto"}

+++

+++响应

成功的回應會傳回HTTP狀態200以及您新建立的對象範本的詳細資訊。

+++

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤

閱讀本檔案後，您現在知道何時該使用對象範本，以及如何使用設定對象範本 `/authoring/audience-templates` api端點。 讀取 [如何使用Destination SDK設定您的目的地](../guides/configure-destination-instructions.md) 以瞭解此步驟在設定目的地的程式中的適用位置。
