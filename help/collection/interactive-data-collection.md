---
title: 交互式数据收集
description: 了解Adobe Experience Platform Edge Network Server API如何执行交互式数据收集
seo-description: Learn how the Adobe Experience Platform Edge Network Server API performs interactive data collection
keywords: 数据收集；收集；experience platform边缘网络；API；交互式数据收集
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 6%

---


# 交互式数据收集

## 概述 {#overview}

交互式数据收集端点会收到一个事件，并在客户端期望Adobe Experience Platform边缘网络服务器返回响应时使用该事件。 执行数据收集时，这些端点还可以返回来自其他Experience Edge服务的内容。

服务器响应包括一个或多个 `Handle` 对象，如下所示。

## API调用示例

### API格式 {#format}

```http
POST /ee/v2/interact
```

### 请求 {#request}

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
            "Email_LC_SHA256": [
               {
                  "id": "0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary": true
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
   }
}'
```

| 参数 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | 可以。 | 数据流ID。 |
| `requestId` | `String` | 否 | 提供用于关联内部服务器请求的客户端随机ID。 如果未提供任何内容，边缘网络将生成一个，并在响应中返回。 |

### 响应 {#response}

成功响应会返回HTTP状态 `200 OK`、一个或多个 `Handle` 对象，具体取决于数据流配置中启用的实时边缘服务。

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
