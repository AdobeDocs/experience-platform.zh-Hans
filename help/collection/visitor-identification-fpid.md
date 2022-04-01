---
title: 通过FPID识别访客
description: 了解如何通过使用FPID，通过服务器API始终如一地识别访客
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: 边缘网络；网关；API；访客；识别；FPID
source-git-commit: eaeab8fe96a9af399f8288b62b6ca9f31d949cfa
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# 通过FPID识别访客

## 概述

[!DNL First-party IDs] (`FPIDs`)是客户生成、管理和存储的设备ID。 这使客户能够控制识别用户设备。 通过发送 `FPIDs`，则边缘网络不会生成全新 `ECID` 请求中不包含一个。

的 `FPID` 可作为的一部分包含在API请求正文中 `identityMap` 或者可以作为Cookie发送。

安 `FPID` 可被确定地转换为 `ECID` 边缘网络，所以 `FPID` 身份与Experience Cloud解决方案完全兼容。 获取 `ECID` 特定 `FPID` 结果始终相同，因此用户将拥有一致的体验。

的 `ECID` 通过 `identity.fetch` 查询：

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

对于同时包含 `FPID` 和 `ECID`, `ECID` 请求中已存在的将优先于可从 `FPID`. 因此，边缘网络将使用 `ECID` 已提供，且不会从给定计算 `FPID`.

就设备ID而言， `server` 数据流应使用 `FPID` 作为设备ID。 其他身份(即 `EMAIL`)，但边缘网络要求明确提供主标识。 主标识是将配置文件数据存储到其中的基本标识。

>[!NOTE]
>
>请求正文中分别未明确设置任何主标识的没有标识的请求将失败。

以下 `identityMap` 为 `server` 数据流请求：

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

以下 `identityMap` 在 `server` 数据流请求：

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

在这种情况下，边缘网络返回的错误响应类似于以下内容：

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

## 访客识别 `FPID`

通过 `FPID`，请确保 `FPID` 在向边缘网络发出任何请求之前已发送cookie。 的 `FPID` 可以在Cookie中传递，或作为 `identityMap` 在请求正文中。

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/ee/v2/interact?dataStreamId={Data Stream ID}' \
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

## 请求 `FPID` 传递 `identityMap` 字段

以下示例将 [!DNL FPID] as `identityMap` 参数。

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {IMS_ORG_ID}"
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
