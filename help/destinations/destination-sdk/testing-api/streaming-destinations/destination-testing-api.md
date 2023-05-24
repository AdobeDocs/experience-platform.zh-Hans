---
description: 瞭解如何使用目的地測試API來測試您的串流目的地是否正確設定，以及驗證流向您設定之目的地的資料流的完整性。
title: 使用範例設定檔測試您的串流目的地
exl-id: 2b54250d-ec30-4ad7-a8be-b86b14e4f074
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---


# 使用範例設定檔測試您的串流目的地 {#template-api-operations}

>[!IMPORTANT]
>
>**API端點**： `https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/`

此頁面列出並描述您可以使用執行的所有API作業。 `/authoring/testing/destinationInstance/` API端點，用於測試您的目的地是否已正確設定，以及驗證流向您設定之目的地的資料流的完整性。 如需此端點支援的功能的說明，請閱讀 [測試您的目的地設定](streaming-destination-testing-overview.md).

無論您是否將設定檔新增至呼叫，您都可以向測試端點提出請求。 如果您未在請求上傳送任何設定檔，Adobe會在內部為您產生這些設定檔，並將其新增至請求。

您可以使用 [範例設定檔產生API](sample-profile-generation-api.md) 建立設定檔，以用於目的地測試API的請求中。

## 如何取得目的地執行個體ID {#get-destination-instance-id}

>[!IMPORTANT]
>
>* 若要使用此API，您在Experience PlatformUI中必須有與目的地的現有連線。 讀取 [連線到目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 和 [對目的地啟用設定檔和區段](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en) 以取得詳細資訊。
> * 建立與目的地的連線後，請在以下情況下取得您應用於此端點的API呼叫中的目的地執行個體ID： [瀏覽與目的地的連線](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=en).
   >![UI影像如何取得目的地執行個體ID](../../assets/testing-api/get-destination-instance-id.png)


## 目的地測試API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 如需成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 測試您的目的地設定，而不將設定檔新增至呼叫 {#test-without-adding-profiles}

您可以透過向以下發出POST請求來測試您的目的地設定： `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 端點，並提供您正在測試之目的地的目的地例項ID。

**API格式**


```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查詢引數 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您正在測試之目的地的目的地執行個體ID。 |

**请求**

以下請求會呼叫您目的地的REST API端點。 要求是由 `{DESTINATION_INSTANCE_ID}` 查詢引數。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的回應會傳回HTTP狀態200以及來自您目的地REST API端點的API回應。

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-vlnt6"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `aggregationKey` | 包含針對目的地設定的彙總原則相關資訊。 如需詳細資訊，請閱讀 [彙總原則](../../functionality/destination-configuration/aggregation-policy.md) 說明檔案。 |
| `traceId` | 作業的唯一識別碼。 遇到錯誤時，您可以與Adobe團隊共用此ID以進行疑難排解。 |
| `results.httpCalls.request` | 包含Adobe傳送至您的目的地的要求。 |
| `results.httpCalls.response` | 包含Adobe從目的地收到的回應。 |
| `inputProfiles` | 包含從呼叫匯出至目的地的設定檔。 設定檔符合您的來源結構描述。 |

{style="table-layout:auto"}

## 使用新增至呼叫的設定檔測試您的目的地設定 {#test-with-added-profiles}

您可以透過向以下發出POST請求來測試您的目的地設定： `authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}` 端點，並提供您正在測試之目的地的目的地例項ID。

**API格式**

```http
POST authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

| 查詢引數 | 描述 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 您正在測試之目的地的目的地執行個體ID。 |

**请求**

以下請求會呼叫您目的地的REST API端點。 要求是由裝載中提供的引數所設定，而且 `{DESTINATION_INSTANCE_ID}` 查詢引數。

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/49966037-32cd-4457-a105-2cbf9c01826a' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}'
```

**响应**

成功的回應會傳回HTTP狀態200以及來自您目的地REST API端點的API回應。

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "ECID":[
               {
                  "id":"ECID-Z3i2t"
               }
            ],
            "external_id":[
               {
                  "id":"external_id-h29Fq"
               }
            ]
         },
         "attributes":{
            "firstName":{
               "value":"John"
            }
         }
      }
   ]
}
```

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) （在平台疑難排解指南中）。

## 后续步骤

閱讀本檔案後，您現在知道如何測試目的地。 您現在可以使用Adobe [自助服務檔案程式](../../docs-framework/documentation-instructions.md) ，為您的目的地建立檔案頁面。
