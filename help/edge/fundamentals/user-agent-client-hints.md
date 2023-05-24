---
title: 使用者代理使用者端提示
description: 瞭解使用者代理程式使用者端提示在Web SDK中的運作方式。 使用者端提示可讓網站擁有者存取使用者代理字串中提供的大部分相同資訊，但採用更能保護隱私的方式。
keywords: 使用者代理；使用者端提示；字串；使用者代理字串；低平均資訊量；高平均資訊量
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 29679e85943f16bcb02064cc60a249a3de61e022
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 7%

---

# 使用者代理使用者端提示

## 概述 {#overview}

每次網頁瀏覽器向網頁伺服器提出請求時，請求的標題都會包含有關瀏覽器和執行瀏覽器環境的資訊。 所有這些資料都會彙總為一個字串，稱為 [!DNL User-Agent] 字串。

以下範例說明 [!DNL User-Agent] 字串看起來像請求中的文字，該請求來自於在上執行的Chrome瀏覽器 [!DNL Mac OS] 裝置。

>[!NOTE]
>
>多年以來，中包含的瀏覽器和裝置資訊量 [!DNL User-Agent] 字串已成長和修改多次。 以下範例顯示一系列最常見的選項 [!DNL User-Agent] 資訊。

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| 字段 | 值 |
|---|---|
| 软件名称 | Chrome |
| 软件版本 | 105 |
| 完整软件版本 | 105.0.0.0 |
| 版面引擎名称 | AppleWebKit |
| 版面引擎版本 | 537.36 |
| Operating system | Mac OS X |
| 操作系统版本 | 10.15.7 |
| 设备 | Intel Mac OS X 10_15_7 |

## 用例 {#use-cases}

[!DNL User-Agent] 長期以來，字串一直被用來為行銷和開發團隊提供重要見解，以說明瀏覽器、作業系統和裝置如何顯示網站內容，以及使用者如何與網站互動。

[!DNL User-Agent] 字串也可用來封鎖垃圾郵件，以及篩選機器人，這些機器人會為各種其他目的對網站進行編目。

## [!DNL User-Agent] Adobe Experience Cloud中的字串 {#user-agent-in-adobe}

Adobe Experience Cloud解決方案利用 [!DNL User-Agent] 字串。

* Adobe Analytics利用 [!DNL User-Agent] 字串：用來增加和衍生與用來造訪網站的作業系統、瀏覽器和裝置相關的其他資訊。
* Adobe Audience Manager和Adobe Target根據 [!DNL User-Agent] 字串。

## 引入使用者代理使用者端提示 {#ua-ch}

近幾年，網站擁有者和行銷供應商已使用 [!DNL User-Agent] 字串以及請求標頭中包含的其他資訊一起建立數位指紋。 這些指紋可用作為在使用者不知情的情況下識別使用者的手段。

儘管此專案的重要目的 [!DNL User-Agent] 字串會為網站擁有者服務，瀏覽器開發人員已決定變更做法 [!DNL User-Agent] 字串會運作，以限制使用者的潛在隱私權問題。

他們開發的解決方案稱為 [使用者代理使用者端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 使用者端提示仍可讓網站收集必要的瀏覽器、作業系統和裝置資訊，同時針對秘密追蹤方法（例如指紋）提供更強大的保護。

使用者端提示可讓網站擁有者存取 [!DNL User-Agent] 字串，但採用更能保護隱私的方式。

當現代瀏覽器將使用者傳送至網頁伺服器時， [!DNL User-Agent] 字串；無論是否需要，都會在每次請求時傳送。 另一方面，使用者端提示會強制執行模型，其中伺服器必須要求瀏覽器提供它想要瞭解的使用者端的其他資訊。 在收到此請求後，瀏覽器可以套用自己的原則或使用者設定，以決定要傳回哪些資料。 不要公開整個 [!DNL User-Agent] 字串)，現在會以明確且可稽核的方式管理存取。

## 瀏覽器支援 {#browser-support}

[使用者代理使用者端提示](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) 推出於 [!DNL Google Chrome ]89版。

其他以Chromium為基礎的瀏覽器支援使用者端提示API，例如：

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## 类别 {#categories}

使用者代理程式使用者端提示分為兩類：

* [低平均資訊量使用者端提示](#low-entropy)
* [高平均資訊量使用者端提示](#high-entropy)

### 低平均資訊量使用者端提示 {#low-entropy}

低平均資訊量使用者端提示包含無法用於指紋識別使用者的基本資訊。 瀏覽器品牌、平台，以及請求是否來自行動裝置等資訊。

Web SDK預設會啟用低平均資訊量使用者端提示，並在每個請求時傳遞。

| HTTP 标头 | JavaScript | 預設包含在使用者代理程式中 | 預設包含在使用者端提示中 |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | 是 | 是 |
| `Sec-CH-UA-Platform` | `platform` | 是 | 是 |
| `Sec-CH-UA-Mobile` | `mobile` | 是 | 是 |

### 高平均資訊量使用者端提示 {#high-entropy}

高平均資訊量使用者端提示是有關使用者端裝置的更詳細資訊，例如平台版本、架構、型號、位元（64位元或32位元平台）或完整作業系統版本。 此資訊可能用於指紋識別。

| HTTP 标头 | JavaScript | 預設包含在使用者代理程式中 | 預設包含在使用者端提示中 |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | 是 | 否 |
| `Sec-CH-UA-Arc` | `architecture` | 是 | 否 |
| `Sec-CH-UA-Model` | `model` | 是 | 否 |
| `Sec-CH-UA-Bitness` | `Bitness` | 是 | 否 |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | 是 | 否 |

Web SDK預設會停用高平均資訊量使用者端提示。 若要啟用這些功能，您必須手動設定Web SDK以請求高平均資訊量使用者端提示。

## 高平均資訊量使用者端提示對Experience Cloud解決方案的影響 {#impact-in-experience-cloud-solutions}

有些Adobe Experience Cloud解決方案在產生報表時，會仰賴高平均資訊量使用者端提示中包含的資訊。

如果您未在環境中啟用高平均資訊量使用者端提示，則以下說明的Adobe Analytics和Audience Manager報表和特徵將無法運作。

### 依賴高平均資訊量使用者端提示的Adobe Analytics報告 {#analytics}

此 [作業系統](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html?lang=zh-Hans) dimension包含儲存為高平均資訊量使用者端提示的作業系統版本。 如果未啟用高平均資訊量使用者端提示，從Chromium瀏覽器收集之點選的作業系統版本可能不準確。

### 依賴高平均資訊量使用者端提示的Audience Manager特徵 {#aam}

[!DNL Google] 已更新 [!DNL Chrome] 瀏覽器功能可將透過 `User-Agent` 標頭。 因此，Audience Manager客戶使用 [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en) 將不會再收到基於下列條件之特徵的可靠資訊： [平台層級索引鍵](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html?lang=zh-Hans).

使用平台層級索引鍵進行目標定位的Audience Manager客戶必須切換至 [Experience PlatformWeb SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=en) 而非 [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en)，並啟用 [高平均資訊量使用者端提示](#enabling-high-entropy-client-hints) 以繼續接收可靠的特徵資料。

## 啟用高平均資訊量使用者端提示 {#enabling-high-entropy-client-hints}

若要在Web SDK部署上啟用高平均資訊量使用者端提示，您必須包含其他 `highEntropyUserAgentHints` 內容選項，如 [設定檔案](configuring-the-sdk.md#context)，以及您現有的設定。

例如，若要從Web屬性擷取高平均資訊量使用者端提示，您的設定將如下所示：

`context: ["highEntropyUserAgentHints", "web"]`

## 示例 {#example}

瀏覽器向網頁伺服器發出的第一個請求標題中所包含的使用者端提示將包含瀏覽器品牌、瀏覽器的主要版本，以及使用者端是否為行動裝置的指標。 每段資料都有自己的標題值，而非分組到單一資料中 [!DNL User-Agent] 字串，如下所示：

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

同等專案 [!DNL User-Agent] 相同瀏覽器的標題看起來像這樣：

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

雖然資訊類似，但對伺服器的第一個請求包含使用者端提示。 這些僅包括 [!DNL User-Agent] 字串。 請求中沒有作業系統架構、完整作業系統版本、版面引擎名稱、版面引擎版本和完整瀏覽器版本。

但在後續請求中， [!DNL Client Hints API] 可讓網頁伺服器詢問關於裝置的其他詳細資訊。 當請求這些值時，根據瀏覽器原則或使用者設定，瀏覽器回應可能包含該資訊。

以下是由傳回的JSON物件範例 [!DNL Client Hints API] 當請求高平均資訊量值時：


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
