---
title: 通过FPID进行访客识别
description: 了解如何使用FPID通过Edge Network API以一致的方式识别访客
seo-description: Learn how to consistently identify visitors via the Edge Network API, by using the FPID
keywords: 边缘网络；网关；API；访客；识别；FPID
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 通过FPID进行访客识别

[!DNL First-party IDs] (`FPIDs`)是客户生成、管理和存储的设备ID。 这允许客户控制标识用户设备。 通过发送`FPIDs`，Edge Network不会为不包含的全新`ECID`的请求生成全新。

`FPID`可以作为`identityMap`的一部分包含在API请求正文中，也可以作为Cookie发送。

`FPID`可以由Edge Network确定性地转换为`ECID`，因此`FPID`标识与Experience Cloud解决方案完全兼容。 从特定`FPID`获取`ECID`将始终产生相同的结果，因此用户将拥有一致的体验。

以这种方式获得的`ECID`可以通过`identity.fetch`查询进行检索：

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

对于同时包含`FPID`和`ECID`的请求，请求中已存在的`ECID`将优先于可从`FPID`生成的请求。 换言之，Edge Network使用已提供的`ECID`并忽略`FPID`。 仅在自行提供`FPID`时生成新的`ECID`。

在设备ID方面，`server`数据流应使用`FPID`作为设备ID。 其他标识（即`EMAIL`）也可以在请求正文中提供，但Edge Network要求显式提供主标识。 主标识是用户档案数据将存储到的基本标识。

>[!NOTE]
>
>没有标识的请求（分别在请求正文中未显式设置主标识）将失败。

`server`数据流请求的以下`identityMap`字段组的格式正确：

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

在`server`数据流请求上设置以下`identityMap`字段组将导致错误响应：

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

在这种情况下，Edge Network返回的错误响应类似于以下内容：

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

## 使用`FPID`进行访客识别

要通过`FPID`识别用户，请确保在向Edge Network发出任何请求之前已发送`FPID` Cookie。 `FPID`可以在Cookie中或作为请求正文中`identityMap`的一部分进行传递。

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

## 以`identityMap`字段形式传递了具有`FPID`的请求

以下示例将[!DNL FPID]作为`identityMap`参数传递。

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
