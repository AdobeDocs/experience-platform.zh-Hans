---
description: 瞭解如何使用目的地測試API，在發佈之前測試您的串流目的地設定。
title: 串流目的地測試API概覽
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 0befd65b91e49cacab67c76fd9ed5d77bf790b9d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# 串流目的地測試API概覽

在Destination SDK過程中，Adobe會提供開發人員工具，協助您設定和測試目的地。 此頁面說明如何測試目的地組態。 如需如何建立訊息轉換範本的詳細資訊，請閱讀 [建立及測試訊息轉換範本](../../testing-api/streaming-destinations/create-template.md).

至 **測試您的目的地是否正確設定，並驗證流向您設定之目的地的資料流的完整性**，使用 *目的地測試工具*. 使用此工具，您可以傳送訊息至REST API端點以測試目的地設定。

以下說明測試您的目的地如何符合 [目的地設定工作流程](../../guides/configure-destination-instructions.md) Destination SDK：

![目的地測試步驟適用於目的地設定工作流程的圖形](../../assets/testing-api/test-destination-step.png)

## 目的地測試工具 — 用途和先決條件 {#destination-testing-tool}

使用目的地測試工具，透過傳送訊息至您在中提供的合作夥伴端點來測試您的目的地設定。 [伺服器設定](../../authoring-api/destination-server/create-destination-server.md).

在使用工具之前，請確定：
* 請依照以下說明的步驟設定您的目的地： [目的地設定工作流程](../../authoring-api/destination-configuration/create-destination-configuration.md) 和
* 建立與目的地的連線，如所述 [如何取得目的地執行個體ID](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id).

使用此工具，在設定目的地後，您可以：
* 測試您的目的地是否已正確設定；
* 驗證資料流至您設定之目的地的完整性。

### 使用方式 {#how-to-use}

>[!NOTE]
>
>如需完整的API參考檔案，請閱讀 [目的地測試API操作](../../testing-api/streaming-destinations/destination-testing-api.md).

您可以呼叫目的地測試API端點，並在請求中新增或不新增設定檔。

如果您未在請求中新增任何設定檔，Adobe會在內部為您產生這些設定檔，並將其新增至請求。 如果要產生設定檔以在此請求中使用，請參閱 [範例設定檔產生API參考](../../testing-api/streaming-destinations/sample-profile-generation-api.md). 您需要根據來源XDM結構描述產生設定檔，如 [API參考](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema). 請注意，來源結構描述是 [聯合結構描述](../../../../profile/ui/union-schema.md) 沙箱的使用者名稱。

回應包含目的地請求處理的結果。 請求包含三個主要區段：
* 由Adobe為目的地產生的請求。
* 從您的目的地收到的回應。
* 請求中傳送的設定檔清單，無論設定檔是 [由您在請求中新增](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles)，或由Adobe產生，如果 [目的地測試請求的主體是空的](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe可產生多個請求和回應配對。 例如，如果您傳送10個設定檔至某個目的地，而該目的地具有 `maxUsersPerRequest` 值為7，則會有一個具有7個設定檔的請求，以及另一個具有3個設定檔的請求。

**內文中具有設定檔引數的範例請求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**內文中沒有設定檔引數的範例請求**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**示例响应**

請注意， `results.httpCalls` 引數專屬於您的REST API。

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
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
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

有關請求和回應引數的說明，請參閱 [目的地測試API操作](../../testing-api/streaming-destinations/destination-testing-api.md).

## 后续步骤

測試目的地並確認已正確設定後，請使用 [目的地發佈API](../../publishing-api/create-publishing-request.md) 以將您的設定提交至Adobe以供檢閱。
