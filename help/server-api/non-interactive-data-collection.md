---
title: 非交互式数据收集
description: 了解Adobe Experience PlatformEdge Network服务器API如何执行非交互式数据收集。
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 4%

---


# 非交互式数据收集

## 概述 {#overview}

非交互式事件数据收集端点用于将多个事件发送到Experience Platform数据集或其他插座。

当最终用户事件在本地排队较短时间（例如，当没有网络连接时）时，建议批量发送事件。

批次事件不一定属于同一最终用户，这意味着事件在其`identityMap`对象中可以包含不同的标识。

## 非交互式API调用示例 {#example}

### API格式 {#api-format}

```http
POST /ee/v2/collect
```

### 请求 {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
   "events": [
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "79bf8e83-f708-414b-b1ed-5789ff33bf0b",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webpagedetails.pageViews",
            "web": {
               "webPageDetails": {
                  "URL": "https://alloystore.dev/",
                  "name": "home-demo-Home Page"
               }
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         },
         "data": {
            "prop1": "custom value"
         }
      },
      {
         "xdm": {
            "identityMap": {
               "FPID": [
                  {
                     "id": "871e8460-a329-4e96-a5b6-ff359fb0afb9",
                     "primary": "true"
                  }
               ]
            },
            "eventType": "web.webinteraction.linkClicks",
            "web": {
               "webInteraction": {
                  "linkClicks": {
                     "value": 1
                  }
               },
               "name": "My Custom Link",
               "URL": "https://myurl.com"
            },
            "timestamp": "2021-08-09T14:09:20.859Z"
         }
      }
   ]
}'
```

| 参数 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 是 | 数据收集端点使用的数据流的ID。 |
| `requestId` | `String` | 否 | 提供外部请求跟踪ID。 如果未提供，则Edge Network将为您生成一个，并将其返回至响应正文/标头。 |
| `silent` | `Boolean` | 否 | 可选布尔参数，用于指示Edge Network是否应返回具有空负载的`204 No Content`响应。 使用相应的HTTP状态代码和有效负载报告严重错误。 |

### 响应 {#response}

成功的响应返回以下状态之一，如果请求中未提供任何状态，则返回`requestID`。

* 成功处理请求时的`202 Accepted`；
* 成功处理请求且`silent`参数设置为`true`时的`204 No Content`；
* `400 Bad Request`，因为请求格式不正确（例如，未找到必需的主标识）。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
