---
keywords: Experience Platform；首頁；熱門主題；串流；串流擷取；串流擷取驗證；驗證；串流擷取驗證；驗證；同步驗證；同步驗證；非同步驗證；非同步驗證；
solution: Experience Platform
title: 串流擷取驗證
type: Tutorial
description: 串流內嵌可讓您使用串流端點即時將資料上傳到Adobe Experience Platform。 串流獲取API支援兩種驗證模式 — 同步和非同步。
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 3%

---

# 串流擷取驗證

串流內嵌可讓您使用串流端點即時將資料上傳到Adobe Experience Platform。 串流獲取API支援兩種驗證模式 — 同步和非同步。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md)：資料可傳送至的其中一種方法 [!DNL Experience Platform].

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括屬於 [!DNL Schema Registry]，會隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

- Content-Type: `application/json`

### 驗證涵蓋範圍

[!DNL Streaming Validation Service] 涵蓋下列領域的驗證：
- Range
- 是否存在
- 列舉
- 图案
- 类型
- 格式

## 同步驗證

同步驗證是一種驗證方法，可針對擷取失敗的原因提供立即回饋。 但是，失敗時，會捨棄驗證失敗的記錄，並阻止將其傳送至下游。 因此，同步驗證只應在開發過程中使用。 執行同步驗證時，會向呼叫者通知XDM驗證的結果，以及失敗的原因（如果失敗）。

依預設，同步驗證不會開啟。 若要啟用，您必須傳入選用查詢引數 `syncValidation=true` 進行API呼叫時。 此外，目前只有在您的串流端點位於VA7資料中心時，才可使用同步驗證。

>[!NOTE]
>
>此 `syncValidation` 查詢引數僅適用於單一訊息端點，且不能用於批次端點。

如果訊息在同步驗證期間失敗，訊息將不會寫入輸出佇列，這會為使用者提供立即的回饋。

>[!NOTE]
>
>結構描述變更可能無法立即使用，因為已快取變更。 快取最多允許15分鐘重新整理。

**API格式**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `id` 先前建立的串流連線的值。 |

**请求**

提交下列請求，以透過同步驗證將資料擷取至您的資料匯入：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要內嵌之資料的JSON內文。 |

**响应**

啟用同步驗證後，成功的回應會在其裝載中包含任何遇到的驗證錯誤：

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

上述回應會列出找到多少綱要違規，以及違規是什麼。 例如，此回應會指出索引鍵 `workEmail` 和 `person` 結構描述中未定義，因此是不允許的。 它也會標示以下專案的值： `_id` 不正確，因為結構描述預期 `string`，但 `long` 已改為插入。 請注意，一旦發生5個錯誤，驗證服務將 **停止** 正在處理該訊息。 不過，其他訊息仍會繼續剖析。

## 非同步驗證

非同步驗證是一種不會立即提供回饋的驗證方法。 而是將資料傳送至中的失敗批次 [!DNL Data Lake] 以防止資料遺失。 此失敗的資料稍後可擷取，以供進一步分析和重播。 此方法應用於生產環境。 除非另有要求，否則串流擷取會以非同步驗證模式運作。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 此 `id` 先前建立的串流連線的值。 |

**请求**

提交下列請求，以使用非同步驗證將資料擷取至您的資料入口：

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | 您要內嵌之資料的JSON內文。 |

>[!NOTE]
>
>不需要額外的查詢引數，因為預設會啟用非同步驗證。

**响应**

啟用非同步驗證時，成功回應會傳回以下內容：

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "syncValidation": {
        "skipped": true
    }
}
```

請注意回應如何指出已略過同步驗證，因為並未明確要求同步驗證。

## 附录

本節包含各種狀態代碼對擷取資料的回應有何意義的資訊。

### 狀態代碼

| 狀態代碼 | 其含義 |
| ----------- | ------------- |
| 200 | 成功. 對於同步驗證，這表示它已通過驗證檢查。 對於非同步驗證，這表示它僅成功收到訊息。 使用者可透過觀察資料集來瞭解最終的訊息狀態。 |
| 400 | 错误. 您的請求發生問題。 從串流驗證服務收到包含進一步詳細資訊的錯誤訊息。 |
| 401 | 错误. 您的請求未獲授權 — 您需要使用持有人權杖請求。 如需有關如何請求存取權的進一步資訊，請檢視此 [教學課程](https://www.adobe.com/go/platform-api-authentication-en) 或這個 [部落格貼文](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | 错误. 發生內部系統錯誤。 |
| 501 | 错误. 這表示同步驗證是 **not** 支援此位置。 |
| 503 | 错误. 服務目前無法使用。 使用者端應使用指數回退策略至少重試三次。 |
