---
title: 通过FPID进行访客识别
description: 了解如何使用FPID通过服务器API一致地识别访客
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: 边缘网络；网关；API；访客；标识；FPID
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# 通过FPID进行访客识别

[!DNL First-party IDs] (`FPIDs`)是由客户生成、管理和存储的设备ID。 这允许客户控制标识用户设备。 通过发送 `FPIDs`，Edge Network不会生成全新 `ECID` 用于不包含请求的请求。

此 `FPID` 可以包含在API请求正文中，作为 `identityMap` 也可以作为Cookie发送。

An `FPID` 可确定地转换为 `ECID` 由Edge Network提供，因此 `FPID` 标识与Experience Cloud解决方案完全兼容。 获取 `ECID` 来自特定 `FPID` 始终产生相同的结果，因此用户将获得一致的体验。

此 `ECID` 通过此方式获取，可通过 `identity.fetch` 查询：

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

对于同时包含 `FPID` 和 `ECID`，则 `ECID` 请求中已经存在的将优先于可能从生成的请求 `FPID`. 换言之，边缘网络使用 `ECID` 已提供，并且 `FPID` 将被忽略。 新 `ECID` 仅当 `FPID` 自行提供。

就设备ID而言， `server` 数据流应使用 `FPID` 作为设备ID。 其他身份(即 `EMAIL`)也可在请求正文中提供，但Edge Network要求显式提供主标识。 主要身份是将配置文件数据存储到的基本身份。

>[!NOTE]
>
>没有标识的请求（分别在请求正文中未显式设置主标识）将失败。

以下各项 `identityMap` 字段组的格式正确 `server` 数据流请求：

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

以下各项 `identityMap` 对字段组进行设置时，将导致错误响应 `server` 数据流请求：

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

## 使用进行访客识别 `FPID`

要通过标识用户，请执行以下操作 `FPID`，确保 `FPID` 在向Edge Network发出任何请求之前，已发送Cookie。 此 `FPID` 可以在Cookie中或作为 `identityMap` 在请求正文中。

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

## 请求方式 `FPID` 传递为 `identityMap` 字段

下面的示例传递 [!DNL FPID] 作为 `identityMap` 参数。

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
