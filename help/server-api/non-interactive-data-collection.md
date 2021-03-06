---
title: 非交互式数据收集
description: 了解Adobe Experience Platform Edge Network Server API如何执行非交互式数据收集。
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 4%

---

# 非交互式数据收集

## 概述 {#overview}

非交互式事件数据收集端点用于发送多个事件以Experience Platform数据集或其他引擎。

如果最终用户事件在本地排队一段时间（例如，没有网络连接时），则建议批量发送事件。

批量事件不一定属于同一最终用户，这意味着事件可以在其中包含不同的标识 `identityMap` 对象。

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
| `requestId` | `String` | 否 | 提供外部请求跟踪ID。 如果未提供任何内容，边缘网络将为您生成一个，并将其返回到响应主体/标头中。 |
| `silent` | `Boolean` | 否 | 可选布尔参数，指示边缘网络是否应返回 `204 No Content` 具有空负载或不具有空负载的响应。 使用相应的HTTP状态代码和负载报告严重错误。 |


### 响应 {#response}

成功的响应会返回以下状态之一，并返回 `requestID` 如果请求中未提供任何内容。

* `202 Accepted` 请求成功处理时；
* `204 No Content` 成功处理请求和 `silent` 参数设置为 `true`;
* `400 Bad Request` 请求格式不正确时（例如，找不到强制主标识）。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
