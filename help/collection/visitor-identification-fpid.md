---
title: 透過FPID的訪客身分識別
description: 瞭解如何使用FPID，透過伺服器API一致地識別訪客
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: 邊緣網路；閘道；API；訪客；識別；fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 透過FPID的訪客身分識別

[!DNL First-party IDs] (`FPIDs`)是由客戶產生、管理和儲存的裝置ID。 這可讓客戶控制識別使用者裝置。 透過傳送 `FPIDs`，Edge Network不會產生全新的 `ECID` 針對不包含此值的請求。

此 `FPID` 可包含在API要求內文中，作為 `identityMap` 或可作為Cookie傳送。

一個 `FPID` 可決定性地轉譯為 `ECID` 由Edge Network提供，因此 `FPID` 身分與Experience Cloud解決方案完全相容。 取得 `ECID` 來自特定 `FPID` 一律會產生相同的結果，因此使用者將擁有一致的體驗。

此 `ECID` 以這種方式取得，可透過 `identity.fetch` 查詢：

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

對於同時包含 `FPID` 和 `ECID`，則 `ECID` 已存在於請求中的優先順序將高於可從產生的優先順序 `FPID`. 換言之，邊緣網路使用 `ECID` 已提供，而且 `FPID` 會忽略。 新 `ECID` 只有當 `FPID` 會自行提供。

就裝置ID而言， `server` 資料串流應使用 `FPID` 做為裝置ID。 其他身分(即 `EMAIL`)也可在要求內文中提供，但Edge Network需要明確提供主要身分。 主要身分是將設定檔資料儲存到的基本身分。

>[!NOTE]
>
>沒有身分的請求（分別在請求內文中未明確設定主要身分）將失敗。

下列專案 `identityMap` 欄位群組的格式正確 `server` 資料流請求：

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

下列專案 `identityMap` 在欄位群組上設定時，將導致錯誤回應 `server` 資料流請求：

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

在這種情況下，Edge Network傳回的錯誤回應類似於以下內容：

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## 訪客身分識別 `FPID`

若要透過以下方式識別使用者： `FPID`，請確定 `FPID` 在向Edge Network提出任何請求之前，已傳送Cookie。 此 `FPID` 可在Cookie中傳遞，或作為 `identityMap` 在要求內文中。

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
                    },
                    "webReferrer": {
                        "URL": ""
                    }
                },
                "device": {
                    "screenHeight": 1440,
                    "screenWidth": 3440,
                    "screenOrientation": "landscape"
                },
                "environment": {
                    "type": "browser",
                    "browserDetails": {
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## 以下列方式要求 `FPID` 傳遞為 `identityMap` 欄位

以下範例會傳遞 [!DNL FPID] as a `identityMap` 引數。

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
