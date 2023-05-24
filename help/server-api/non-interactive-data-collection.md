---
title: 非互動式資料彙集
description: 瞭解Adobe Experience Platform Edge Network Server API如何執行非互動式資料收集。
exl-id: 1a704e8f-8900-4f56-a843-9550007088fe
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 4%

---

# 非互動式資料彙集

## 概述 {#overview}

非互動式事件資料收集端點可用來傳送多個事件至Experience Platform資料集或其他插座。

當一般使用者事件在本機佇列較短時間（例如，沒有網路連線時）時，建議批次傳送事件。

批次事件不一定要屬於相同的一般使用者，這表示事件可以在其內包含不同的身分 `identityMap` 物件。

## 非互動式API呼叫範例 {#example}

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
| `dataStreamId` | `String` | 是 | 資料收集端點使用的資料串流的ID。 |
| `requestId` | `String` | 否 | 提供外部要求追蹤ID。 如果未提供，Edge Network會為您產生回應，並將其傳回至回應內文/標頭。 |
| `silent` | `Boolean` | 否 | 選用的布林值引數，指出Edge Network是否應該傳回 `204 No Content` 是否以空白承載回應。 系統會使用對應的HTTP狀態代碼和裝載來報告嚴重錯誤。 |


### 响应 {#response}

成功回應會傳回下列其中一種狀態，以及 `requestID` 請求中未提供任何請求時。

* `202 Accepted` 成功處理要求時；
* `204 No Content` 成功處理要求時，且 `silent` 引數已設為 `true`；
* `400 Bad Request` 要求格式不正確時（例如，找不到必要的主要身分）。

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
