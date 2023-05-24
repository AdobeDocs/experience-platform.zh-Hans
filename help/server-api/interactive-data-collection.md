---
title: 互動式資料彙集
description: 瞭解Adobe Experience Platform Edge Network Server API如何執行互動式資料收集。
exl-id: 1b06e755-b6a9-42dd-96c1-98ad67e7d222
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 6%

---

# 互動式資料彙集

## 概述 {#overview}

互動式資料收集端點會接收單一事件，並在使用者端預期Adobe Experience Platform Edge Network伺服器傳回回應時使用。 在執行資料收集時，這些端點也可以從其他Experience Edge服務傳回內容。

伺服器回應包含一或多個 `Handle` 物件，如下所示。

## API呼叫範例

### API格式 {#format}

```http
POST /ee/v2/interact
```

### 请求 {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
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
| `dataStreamId` | `String` | 可以。 | 資料串流ID。 |
| `requestId` | `String` | 否 | 提供用於關聯內部伺服器請求的使用者端隨機ID。 如果未提供，Edge Network將會產生一個，並在回應中傳回。 |

### 响应 {#response}

成功的回應會傳回HTTP狀態 `200 OK`，包含一或多個 `Handle` 物件，視資料流設定中啟用的即時邊緣服務而定。

```json
{
   "requestId": "c85402f5-83a1-4fb3-abdd-f4c17bf6dd49",
   "handle": []
}
```
