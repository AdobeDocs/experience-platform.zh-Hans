---
title: 使用者端狀態管理
description: 瞭解Adobe Experience Platform Edge Network如何管理使用者端狀態
seo-description: Learn how the Adobe Experience Platform Edge Network  manages client state
keywords: 使用者端；狀態；管理；邊緣；網路；閘道；api
exl-id: 798ecc52-1af1-4480-a2a3-3198a83538f8
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 2%

---

# 使用者端狀態管理

Edge Network本身是無狀態的（不會維護自己的工作階段）。 但是，某些使用案例需要使用者端狀態持續性，例如：

* 一致的裝置識別(請參閱 [訪客識別](visitor-identification.md))
* 收集並強制執行使用者同意
* 保留個人化工作階段ID

Edge Network使用狀態管理通訊協定，將儲存特性委派給其使用者端/SDK，並在其回應中包含狀態專案。 對於瀏覽器，專案會儲存為Cookie。

使用者端的責任是儲存這些檔案，並將其納入所有後續的請求。 使用者端也必須按照閘道的指示，注意專案的適當到期日。 當專案儲存為Cookie時，瀏覽器會自動完成所有這些工作。

雖然狀態專案永遠都會有明文 `String` 值（對呼叫者/SDK可見），您不應以任何方式使用或篡改值。 值結構/格式，甚至是名稱本身都可能隨時變更，這可能會導致在內部使用狀態的使用者端出現非預期的行為。 此狀態旨在讓閘道本身或其他邊緣服務一律使用。

## 將使用者端狀態作為中繼資料保留

由傳回的狀態 [!DNL Edge Network] 在回應內文中是 `Handle` 具有型別的物件 `state:store`.

```json
{
   "requestId":"421036b3-a7ff-480b-a9ab-30adba6eb4f0",
   "handle":[
      {
         "payload":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1",
               "maxAge":7200,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
               "value":"CiY1NDc1ODIxNzIzODk5MDY5MzQzMTIzNjQ1NTczNzExNjE4OTA1MFINCLGOvszNLhABGAEgBKABsY6-zM0uqAGHz-z2y82cul3wAbGOvszNLg==",
               "maxAge":34128000,
               "attrs":{
                  "SameSite":"None"
               }
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
               "value":"general=in",
               "maxAge":15552000,
               "attrs":{
                  "SameSite":"None"
               }
            }
         ],
         "type":"state:store"
      }
   ]
}
```

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| `key` | 字符串 | **必需**. 專案名稱。 |
| `value` | 字符串 | *可选*. 專案值。 |
| `maxAge` | 整数 | *可選* 專案到期前的時間（秒）。 遺失時，應該只為目前的工作階段儲存專案。 |
| `attrs` | `Map<String, String>` | *可选*. 專案屬性的選用清單。 對於所有具有安全參照HTTP標頭的安全連線， `SameSite` 屬性已設定為 `None`. |


為了支援多重標籤（亦即，同一屬性中有多個SDK執行個體，可能會參考不同的組織），所有狀態專案都會自動加上前置詞 `kndctr_` 和URL安全的組織ID。

使用者端SDK收到 `state:store` 在回應中處理，它必須執行下列動作：

* 在使用者端儲存專案，遵守閘道提供的到期時間。
* 從使用者端存放區載入這些專案，並在後續請求中包含所有未過期的專案。

以下是在使用者端儲存狀態中傳遞的請求範例：

```json
{
   "meta":{
      "state":{
         "entries":[
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent_check",
               "value":"1"
            },
            {
               "key":"kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_personalization_sessionId",
               "value":"0a88f43e-044b-41a6-a4f3-6c2848bbc672"
            }
         ]
      }
   }
}
```

## 在瀏覽器Cookie中保留使用者端狀態

使用瀏覽器使用者端時，Edge Network會自動將專案保留為瀏覽器Cookie。 這可提供透明狀態儲存支援，因為瀏覽器預設會遵循狀態管理通訊協定。

幾乎所有專案在啟用和支援時都會具體化為第一方Cookie （請參閱以下附註），但閘道也可以在第三方時儲存某些第三方Cookie `adobedc.demdex.net` 網域已使用。

由於專案總是依照其定義與特定範圍（裝置/應用程式）繫結，因此Edge Network只會寫入與目前要求內容相容的子集。 系統會將未寫入的專案傳回 `state:store` 控制代碼。

一般而言，應用程式範圍專案一律會寫入為第一方Cookie，而裝置範圍專案則會寫入為第三方Cookie。 此決定對於呼叫者完全透明，閘道會根據呼叫內容決定可以寫入哪些專案。

呼叫者必須明確啟用支援，透過 `meta.state.cookiesEnabled` 標幟：

```json
{
   "meta":{
      "state":{
         "cookiesEnabled":true,
         "domain":"foo.com"
      }
   }
}
```

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| `cookiesEnabled` | 布尔值 | 設定後，會啟用Cookie支援。 默认值为 `false`。 |
| `domain` | 字符串 | 下列情況需要： `cookiesEnabled: true`. 應在其上寫入Cookie的頂層網域。 Edge Network會使用此值來決定是否可將狀態持續當作Cookie。 |

即使Cookie支援是透過 `cookiesEnabled` 標幟，只有在要求最上層網域符合以下條件時，Adobe Experience Platform Edge Network才會寫入狀態專案： `domain` 由呼叫者指定。 當有不相符的專案時，會在 `state:store` 控制代碼。

在下列情況下，無法寫入第一方Cookie （即使啟用支援亦然）：

* 請求來自第三方 `adobedc.demdex.net` 網域。
* 請求來自第一方 `CNAME` 網域，與呼叫者指定的網域不同 `meta.state.domain`.

## Cookie安全性

所有Cookie都具有 [安全標幟](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies) 儘可能啟用。

所有安全Cookie都具有 [SameSite屬性](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie/SameSite) 設定為 `None`，這表示Cookie會在所有內容中傳送，包括第一方和跨來源。

* 針對第一方Cookie (`kndcrt_*`)， `Secure` 只有在要求內容安全(HTTPS)且反向連結([Referer HTTP標頭](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Referer))也是HTTPS。 如果反向連結不安全(HTTP)， `Secure` 省略此旗標，以允許Web SDK讀取它們。 無法從不安全的內容讀取安全Cookie。
* 對於第三方Cookie (demdex)， `Secure` 標幟一律會設定，因為所有要求都是HTTPS，所以要求內容是安全的，而且絕不會從JavaScript讀取此Cookie。

此 `Secure` 旗標不存在於 [Cookie的中繼資料表示](#state-as-metadata). 僅限 `SameSite` 包括屬性。 在此情況下，使用者端應負責正確設定 `Secure` 標幟每當 `SameSite` 屬性存在。 Cookie包含 `SameSite=None` 您也必須指定 `Secure` 屬性，因為它們需要安全內容(HTTPS)。
