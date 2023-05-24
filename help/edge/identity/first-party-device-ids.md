---
title: Platform Web SDK中的第一方裝置ID
description: 瞭解如何為Adobe Experience Platform Web SDK設定第一方裝置ID (FPID)。
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 0%

---

# Platform Web SDK中的第一方裝置ID

Adobe Experience Platform Web SDK指派 [Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) 透過Cookie對網站訪客進行追蹤，以便追蹤使用者行為。 若要考慮Cookie有效期的瀏覽器限制，您可以選擇設定和管理自己的裝置識別碼。 这些被称为第一方设备 ID (FPID)。

>[!NOTE]
>
>只有透過Platform Web SDK將資料傳送至Platform Edge Network時，才支援第一方裝置ID。

本文介紹如何為您的Platform Web SDK實作設定第一方裝置ID。

## 先决条件

本指南假設您熟悉Platform Web SDK的身分識別資料運作方式，包括ECID和 `identityMap`. 請參閱以下文章的概觀： [Web SDK中的身分資料](./overview.md) 以取得詳細資訊。

## 使用FPID

FPID會透過使用第一方Cookie來追蹤訪客。 使用運用DNS的伺服器設定第一方Cookie時，成效最佳 [A記錄](https://datatracker.ietf.org/doc/html/rfc1035) （適用於IPv4）或 [AAAA記錄](https://datatracker.ietf.org/doc/html/rfc3596) （適用於IPv6），而非DNS CNAME或JavaScript程式碼。

>[!IMPORTANT]
>
>僅設定和追蹤Cookie支援記錄或AAAA記錄。 資料收集的主要方法是透過DNS CNAME。 換言之，FPID是使用A記錄或AAAA記錄設定，然後使用CNAME傳送至Adobe。
>
>此 [Adobe管理的憑證方案](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) 也仍支援第一方資料收集。

設定FPID Cookie後，便可在收集事件資料時擷取其值並傳送至Adobe。 收集的FPID會作為種子來產生ECID，這繼續是Adobe Experience Cloud應用程式中的主要識別碼。

若要將網站訪客的FPID傳送至Platform Edge Network，您必須將FPID加入至 `identityMap` 給該訪客的。 請參閱本檔案稍後章節於 [在中使用FPID `identityMap`](#identityMap) 以取得詳細資訊。

### ID格式需求

Platform Edge Network只接受符合 [UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122). 不採用UUIDv4格式的裝置ID將會遭到拒絕。

產生UUID幾乎都會產生不重複、隨機的ID，發生衝突的可能性極小。 無法使用IP位址或任何其他個人識別資訊(PII)內建的UUIDv4。 UUID隨處可見，而且幾乎可以找到每種程式設計語言的程式庫來產生它們。

## 使用您自己的伺服器設定Cookie

使用您擁有的伺服器設定Cookie時，可以使用各種方法防止Cookie因瀏覽器原則而受到限制：

* 使用伺服器端指令碼語言產生Cookie
* 設定Cookie以回應對子網域或網站上其他端點提出的API請求
* 使用CMS產生Cookie
* 使用CDN產生Cookie

>[!IMPORTANT]
>
>使用JavaScript的 `document.cookie` 方法幾乎永遠不會受到限制Cookie持續時間的瀏覽器原則的保護。

### 何時設定Cookie

最好在向Edge Network提出任何請求之前先設定FPID Cookie。 不過，在不可能的情況下，仍會使用現有方法產生ECID，並在Cookie存在時作為主要識別碼。

假設ECID最終受到瀏覽器刪除原則影響，但FPID未受到影響，則FPID會在下次造訪時成為主要識別碼，並用於在後續每次造訪時植入ECID。

### 設定Cookie的有效期

在實作FPID功能時，應謹慎設定Cookie的到期日。 做出此決定時，您應考量貴組織營運所在的國家或地區，以及每個地區的法律和政策。

在此決定中，您可能會想要採用公司範圍的Cookie設定原則，或根據您營運所在的每個地區設定中使用者的不同而採用的原則。

無論您為Cookie的初始過期時間選擇何種設定，都必須確保納入每次發生新造訪網站時延長Cookie過期時間的邏輯。

## Cookie標幟的影響

有各種Cookie標幟會影響Cookie在不同瀏覽器中的處理方式：

* [&#39;HTTPOnly&#39;](#http-only)
* [`安全`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

使用設定的Cookie `HTTPOnly` 無法使用使用者端指令碼存取標幟。 這表示如果您設定 `HTTPOnly` 標幟設定FPID時，您必須運用伺服器端指令碼語言來讀取要包含在 `identityMap`.

如果您選擇讓Platform Edge Network讀取FPID Cookie的值，請將 `HTTPOnly` 標幟將確保任何使用者端指令碼都無法存取值，但不會對Platform Edge Network讀取Cookie的能力產生任何負面影響。

>[!NOTE]
>
>使用 `HTTPOnly` 標幟對可能限制Cookie期限的Cookie原則沒有影響。 不過，在設定和讀取FPID的值時，您仍應考慮這個問題。

### `Secure` {#secure}

使用設定的Cookie `Secure` 屬性只會以加密的要求透過HTTPS通訊協定傳送至伺服器。 使用此標幟有助於確保中間人攻擊者無法輕鬆存取Cookie的值。 如果可能的話，最好設定 `Secure` 標幟。

### `SameSite` {#same-site}

此 `SameSite` attribute可讓伺服器判斷cookie是否隨跨網站要求傳送。 屬性可針對跨網站偽造攻擊提供某些保護。 有三種可能的值存在： `Strict`， `Lax` 和 `None`. 請洽詢您的內部團隊，判斷適合貴組織的設定。

若否 `SameSite` 屬性已指定，某些瀏覽器的預設設定現在為 `SameSite=Lax`.

## 在中使用FPID `identityMap` {#identityMap}

以下是如何在「 」中自行設定FPID的範例 `identityMap`：

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

如同其他身分型別，您可以將FPID與其他身分一起包含在 `identityMap`. 以下是已驗證身分的CRM ID所包含的FPID範例：

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

啟用第一方資料收集時，如果FPID包含在Edge Network讀取的Cookie中，則應僅擷取已驗證的CRM ID：

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

下列專案 `identityMap` 會導致Edge Network的錯誤回應，因為它遺失 `primary` FPID的指標。 最後出現其中一個ID `identityMap` 必須標示為 `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

在此情況下，Experience Edge傳回的錯誤回應將類似於以下內容：

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## ID階層

當ECID和FPID都存在時，ECID將在識別使用者時優先處理。 這將確保當瀏覽器Cookie存放區中存在現有ECID時，該ECID仍會是主要識別碼，且現有訪客計數不會受到影響。 對於現有使用者，在ECID過期或因瀏覽器原則或手動程式而被刪除之前，FPID不會成為主要身分。

身分會依下列順序排定優先順序：

1. ECID包含在 `identityMap`
1. ECID儲存在Cookie中
1. FPID包含在 `identityMap`
1. FPID儲存在Cookie中

## 移轉至第一方裝置ID

如果您要從先前的實作移轉至，可能很難在低層級看到轉換的樣子。

為協助說明此程式，請思考先前曾造訪過您網站的客戶的情況，以及FPID移轉對Adobe解決方案中識別該客戶的方式有何影響。

![圖表顯示客戶ID值在移轉至FPID後如何在兩次造訪之間更新](../assets/identity/tracking/visits.png)

| 访问 | 描述 |
| --- | --- |
| 首次造訪 | 假設您尚未開始設定FPID Cookie。 包含在 [AMCV Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) 將是用來識別訪客的識別碼。 |
| 第二次造訪 | 第一方裝置ID解決方案的推出已開始。 現有的ECID仍然存在，並繼續作為訪客身分識別的主要識別碼。 |
| 第三次造訪 | 在第二次和第三次造訪之間，已因瀏覽器原則而經過足夠的時間刪除ECID。 不過，由於FPID是使用DNS A記錄設定的，因此FPID會持續存在。 FPID現在會視為主要ID，並用來植入寫入一般使用者裝置的ECID。 在Adobe Experience Platform和Experience Cloud解決方案中，該使用者現在會被視為新訪客。 |
| 第四次瀏覽 | 在第三次和第四次瀏覽之間，由於瀏覽器原則而刪除ECID的間隔時間已足夠。 如同先前的造訪，FPID會因設定方式而異。 這次會產生與上次造訪相同的ECID。 在整個Experience Platform和Experience Cloud解決方案中，使用者會被視為與上次造訪相同的使用者。 |
| 第五次瀏覽 | 在第四次和第五次瀏覽之間，使用者已清除瀏覽器中的所有Cookie。 系統會產生新的FPID，並用來建立新ECID。 在Adobe Experience Platform和Experience Cloud解決方案中，該使用者現在會被視為新訪客。 |

{style="table-layout:auto"}

## 常见问题解答

以下是有關第一方裝置ID常見問題的回答清單。

### 植入ID和單純產生ID有何不同？

內建概念的獨特之處在於，傳遞至Adobe Experience Cloud的FPID會使用確定性演演算法轉換為ECID。 每次將相同的FPID傳送到Adobe Experience Platform Edge Network時，都會從FPID內建相同的ECID。

### 何時應該產生第一方裝置ID？

若要降低訪客的潛在膨脹率，應先產生FPID，再使用Platform Web SDK提出第一個請求。 不過，如果您無法這麼做，系統仍會為該使用者產生ECID，並將該ECID當作主要識別碼使用。 產生的FPID不會成為主要識別碼，直到ECID不再存在為止。

### 哪些資料收集方法支援第一方裝置ID？

目前只有Platform Web SDK支援FPID。

### FPID是否儲存在任何平台或Experience Cloud解決方案上？

使用FPID來設定ECID種子後，就會從 `identityMap` 和已取代為已產生的ECID。 FPID不會儲存在任何Adobe Experience Platform或Experience Cloud解決方案中。
