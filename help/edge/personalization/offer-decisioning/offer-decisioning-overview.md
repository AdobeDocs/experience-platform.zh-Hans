---
title: 搭配Platform Web SDK使用Offer Decisioning
description: Adobe Experience Platform Web SDK可以提供並轉譯Offer Decisioning管理的個人化優惠。 您可以使用Offer decisioningUI或API建立您的優惠方案與其他相關物件。
keywords: offer decisioning；決策；Web SDK；平台Web SDK；個人化優惠；提供優惠；優惠傳遞；優惠個人化；
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 5%

---

# 搭配Platform Web SDK使用Offer Decisioning

>[!NOTE]
>
>特定使用者可提早存取Adobe Experience Platform Web SDK中的Offer decisioning。 此功能並非適用於所有組織。

Adobe Experience Platform [!DNL Web SDK] 可以傳遞和轉譯受Offer Decisioning管理的個人化優惠。 您可以使用 Offer Decisioning 用户界面 (UI) 或 API 创建优惠和其他相关对象。

## 先决条件

* 組織已啟用邊緣決策
* 優惠、建立的活動
* 資料流已發佈

## 术语

使用Offer Decisioning時，請務必瞭解下列術語。 如需詳細資訊和檢視其他詞語，請造訪 [offer decisioning字彙表](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **容器：** 容器是一種隔離機制，可將不同的關注點分開。 容器ID是所有存放庫API的第一個路徑元素。 所有決策物件都位於容器內。

* **決定範圍：** 對於Offer decisioning，決定範圍是JSON的Base64編碼字串，包含您希望offer decisioning服務用來建議優惠的活動和位置ID。

   *決定範圍JSON：*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *決定範圍Base64編碼字串：*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >您可以從以下位置複製決定範圍值： **活動概覽** UI中的頁面。

   ![](assets/decision-scope-copy.png)

* **資料串流：** 如需詳細資訊，請閱讀 [資料串流](../../datastreams/overview.md) 說明檔案。

* **身分**：如需詳細資訊，請閱讀本檔案並概述如何 [Platform Web SDK使用Identity Service](../../identity/overview.md).

## 啟用Offer decisioning

若要啟用Offer Decisioning，請執行下列步驟：

1. 在您的中啟用Adobe Experience Platform [資料串流](../../datastreams/overview.md) 並勾選「Offer decisioning」方塊

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. 依照指示進行 [安裝SDK](../../fundamentals/installing-the-sdk.md) (SDK可獨立安裝或透過UI安裝。 請參閱 [標籤快速入門手冊](../../../tags/quick-start/quick-start.md))以取得詳細資訊。
1. [設定SDK](../../fundamentals/configuring-the-sdk.md) 用於Offer decisioning。 以下提供其他Offer decisioning特定步驟。

   * 安裝獨立SDK

      1. 使用設定&quot;sendEvent&quot;動作 `decisionScopes`

         ```javascript
          alloy("sendEvent", {
             ...
             "decisionScopes": [
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
             ]
          })
         ```
   * 透過標籤安裝SDK

      1. [建立標籤屬性](../../../tags/ui/administration/companies-and-properties.md)
      1. [新增內嵌程式碼](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. 從「資料流」下拉式清單中選取設定，使用您建立的資料流安裝並設定Platform Web SDK擴充功能。 請參閱以下說明檔案： [擴充功能](../../../tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. 建立必要的 [資料元素](../../../tags/ui/managing-resources/data-elements.md). 您至少必須建立Platform Web SDK身分對應和Platform Web SDK XDM物件資料元素。

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. 建立您的 [規則](../../../tags/ui/managing-resources/rules.md).

         * 新增Platform Web SDK傳送事件動作並新增相關的 `decisionScopes` 至該動作的設定

            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      1. [建立及發佈程式庫](../../../tags/ui/publishing/libraries.md) 包含所有已設定的相關規則、資料元素和擴充功能



## 範例請求和回應

### 一 `decisionScopes` 值

**请求**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| 属性 | 必需 | 描述 | 限制 | 示例 |
|---|---|---|---|---|
| `identityMap` | 是 | 請參閱此 [Identity Service檔案](../../identity/overview.md). | 每個請求一個身分。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`的问题。<br><br> 注意：使用者不需要包含 `ECID` API呼叫中的引數 如有需要，此引數會自動新增至呼叫。 |
| `decisionScopes` | 是 | 包含活動和位置ID的JSON的Base64編碼字串陣列。 | 最多30個 `decisionScopes` 每個請求。 | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**响应**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| 属性 | 描述 | 示例 |
|---|---|---|
| `scope` | 導致建議優惠方案的決定範圍。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 優惠活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | 優惠方案位置的唯一ID。 | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | 建議優惠方案的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | 與建議選件相關聯的內容結構描述。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | 建議優惠方案的ID。 | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | 與建議選件相關聯的內容格式。 | `"format": "text/html"` |
| `language` | 與建議選件內容相關的一系列語言。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議選件相關聯的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式呈現與建議選件相關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 與JSON物件格式的建議選件相關聯的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### 多個 `decisionScopes` 值

**请求**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| 属性 | 必需 | 描述 | 限制 | 示例 |
|---|---|---|---|---|
| `identityMap` | 是 | 請參閱此 [Identity Service檔案](../../identity/overview.md). | 每個請求一個身分。 | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`的问题。<br><br> 注意：使用者不需要包含 `ECID` API呼叫中的引數 如有需要，此引數會自動新增至呼叫。 |
| `decisionScopes` | 是 | 包含活動和位置ID的JSON的Base64編碼字串陣列。 | 最多30個 `decisionScopes` 每個請求。 | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**响应**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| 属性 | 描述 | 示例 |
|---|---|---|
| `scope` | 導致建議優惠方案的決定範圍。 | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | 優惠活動的唯一ID。 | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | 優惠方案位置的唯一ID。 | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | 建議優惠方案的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | 與建議選件相關聯的內容結構描述。 | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | 建議優惠方案的ID。 | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | 與建議選件相關聯的內容格式。 | `"format": "text/text"` |
| `language` | 與建議選件內容相關的一系列語言。 | `"language": [ "en-US" ]` |
| `content` | 以字串格式與建議選件相關聯的內容。 | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | 以URL格式呈現與建議選件相關聯的影像內容。 | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | 與JSON物件格式的建議選件相關聯的特性。 | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## 限制

行動Experience Edge工作流程目前不支援部分優惠方案限制，例如上限。 「上限」欄位值會指定某個優惠方案可向所有使用者顯示的次數。 如需詳細資訊，請參閱 [優惠方案適用性規則和限制檔案](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
