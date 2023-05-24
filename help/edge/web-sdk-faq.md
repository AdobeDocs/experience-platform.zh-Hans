---
title: Adobe Experience Platform Web SDK常見問題集
description: 取得有關Adobe Experience Platform Web SDK常見問題的解答。
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: a8f6bb8c3e35f4c17812ef944440210b7fe3f87b
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 2%

---

# 常见问题解答

本指南提供有關Adobe Experience Platform Web SDK的常見問題解答。

## 什麼是Adobe Experience Platform Web SDK？

Adobe Experience Platform Web SDK是使用者端的JavaScript程式庫，可讓Adobe Experience Cloud的客戶與Experience Cloud中的各種服務互動。

它會以與解決方案無關的方式(XDM)傳送資料至Adobe Experience Platform Edge Network，接著將資料對應至解決方案特定的格式和目的地，並即時傳送。

**更多資訊**
[Adobe Summit簡報](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform Web SDK和先前的解決方案有何不同？

### Adobe Experience Platform SDK之前

目前，您必須根據各個解決方案來部署不同的JavaScript程式庫。

* 每個解決方案都有自己的JavaScript程式庫、結構描述和網域。
* 這些程式庫都不是為了彼此搭配使用而建置的。
* 跨解決方案和Adobe Experience Platform使用案例需要這些不同的程式庫相互依存，造成部署上的摩擦。

雖然Platform中的標籤可讓您儘可能輕鬆地部署和管理這些程式庫，但下列專案仍有問題：

* 程式庫大小(頁面上的Adobe程式碼過多)
* 效能（網站載入時間太長）
* 單一使用案例的多次呼叫
* 在個人化呼叫之前等候ECID傳回（導致延遲）
* 分離式資料收集（什麼是evar？）
* 解決方案(A4T)之間的結構描述混淆
* 許多其他不太理想的事物

此外，目前也沒有將資料直接傳送至Adobe Experience Platform的JavaScript程式庫。

### 使用Adobe Experience Platform Web SDK

新的Web SDK會將下列解決方案的資料傳送至單一目的地(Adobe Experience Platform Edge Network)，並解決上述最常見的解決方案使用案例。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 访客 ID
* Adobe Experience Platform

其他解決方案將在今年晚些時候推出。

Adobe Experience Platform Web SDK也可以直接將資料傳送至Adobe Experience Platform。 此資料採用XDM格式，並對應至伺服器端解決方案結構描述。

## 這個新Web SDK有何價值？

**效能：** Web SDK比使用所有目前Adobe程式庫更小，且頁面載入速度更快。

**簡易性：** XDM、Web SDK、標籤、Experience Edge、Adobe Experience Cloud解決方案和Adobe Experience Platform的組合可建立易懂且易於遵循的資料收集故事。

* **XDM：** 用來傳送資料給Adobe且不受解決方案限制的結構描述。 不再標籤evar或mbox。
* **Adobe Experience Platform Web SDK：** 讓您可以輕鬆傳送及接收資料至Adobe Experience Platform Edge Network。
* **標籤：** 簡化網站上Web SDK （以及任何其他JavaScript標籤）的部署和設定。
* **Experience Edge：** 以所需的格式輕鬆將資料路由至Adobe Experience Platform和解決方案。
* **Adobe Experience Platform和Adobe解決方案：** 啟用他們的價值主張。

**控制：** 由於所有資料都使用單一且連線的資料流，因此在邏輯上，您可以追蹤並控制資料在往返應用程式的每個毫秒歷程中的外觀。

**現代，為未來做好準備：** Web SDK及其與Experience Edge Network的連線讓Adobe得以大幅現代化Adobe處理資料收集、個人化、同意和未來第三方Cookie的方式。 (這會啟用第一方網域，由Adobe管理。)

**價值實現時間：** Adobe一直努力（並將繼續）讓您儘可能輕鬆地透過標籤部署Web SDK，並將使用者端資料對應至XDM。 完成此工作後，即可開啟或關閉伺服器端的所有其他Adobe解決方案和Adobe Experience Platform服務。 例如，如果您將此用於Adobe Analytics，並且想要開啟Target或Experience Platform，您只需在資料流設定上翻轉切換即可開啟這些使用案例。

## 什麼是Alloy？

Alloy是Adobe Experience Platform Web SDK的程式碼名稱。 它用於SDK的原始程式碼和檔案名稱，雖然Adobe Experience Platform Web SDK是正式名稱。

## 客戶是否需要購買Adobe Experience Platform才能使用 [!DNL Web SDK]？

不会。任何Adobe Digital Experience客戶都可以免費使用Adobe Experience Platform Web SDK。 希望使用 [!DNL Web SDK] 將需要在資料收集UI或Experience PlatformUI中設定正確的許可權，以建立結構描述、資料集、身分名稱空間和資料串流。

如需設定這些許可權的詳細資訊，請參閱以下說明檔案： [資料彙集許可權管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## 誰應使用Web SDK？

Adobe Experience Platform Web SDK專為下列人員開發：

* Adobe Experience Platform使用者
   * 如果您需要直接從裝置傳送資料至Adobe Experience Platform，這是正式建議的方式。
   * Adobe瞭解，如果客戶已有Adobe Analytics，使用Adobe Analytics聯結器會更快，但這並非資料收集的長期策略。

* Adobe Experience Cloud解決方案客戶
   * 新的Adobe Analytics、Adobe Audience Manager和Adobe Target客戶應該從新的Web SDK開始，而不是使用舊版程式庫。
   * 想要儘可能獲得最佳化實作的現有客戶，應使用新的Web SDK。


## 如何取得存取權以開始使用Adobe Experience Platform Web SDK？

Web SDK目前可供一般公眾使用，並可用來將資料傳送至Adobe Experience Cloud產品。 近期即將推出將資料傳送至協力廠商解決方案的功能。 SDK免費，並由Adobe免費託管。 如有需要，您可以免費下載並在您自己的伺服器上託管。 Platform Web SDK需要存取資料流設定和Adobe Experience Platform XDM結構描述產生器，以便Adobe的伺服器能夠正確處理來自SDK的傳入資料。 如果您想要取得存取權，請聯絡您的Adobe帳戶團隊以開始請求流程。

## Web SDK目前支援哪些使用案例？

Web SDK正在迅速發展。 正在處理更多使用案例。 您可以找到 [此處列出目前支援的使用案例。](https://github.com/adobe/alloy/projects/5)

## 目前客戶是否必須重新標籤其網站？

这依具体情况而定。Adobe Experience Platform Web SDK可以兩種不同的樣式部署。 未來的移轉檔案將提供其他詳細資訊。

* **只是另一個標籤：** 如果網站已標籤解決方案，且您無法重新標籤，但您想要將資料傳送至Adobe Experience Platform Edge Network以進行Experience Platform使用案例或即將推出的事件轉送功能（請參閱下文），您可以新增 `alloy.js` 標籤到網站，在那裡它就像是「另一個標籤」。

* **唯一標籤：** 如果您想要將Web SDK用於Experience Cloud解決方案，則必須將其用於 _全部_ 頁面上的解決方案。 例如，如果您的網站已針對Adobe Analytics進行標籤，而您想要將其用於Target，則您需要將其用於兩者，以及未來的任何其他網站。

換言之，如果您決定將Adobe Experience Platform Web SDK用於非解決方案使用案例，則可以在網站上使用 `alloy.js` 然後像新解決方案一樣繼續前進。 如果您想要將其用於Adobe Analytics、Target、Audience Manager或應用程式使用案例，您可能需要移除頁面上的任何舊版程式碼。

## 我可以在開始使用Alloy時移轉ECID，讓我的網站訪客不會開始顯示為新訪客嗎？

是，Adobe Experience Platform Web SDK提供身分移轉功能。 請依照「 」中的ID移轉指示操作 [Platform Web SDK身分檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) 以取得更多詳細資料。

## Web SDK與標籤有何不同？

* **Experience Platform中的標籤** 管理裝置代碼。 使用它們可更輕鬆地部署程式碼。 免費且功能強大。

* **Adobe Experience Platform Web SDK** 是標籤為Adobe使用案例部署的新程式碼的正式名稱。 它也是免費且功能強大的。

* **`alloy.js`** 是Adobe Experience Platform Web SDK程式碼的檔案名稱。

## 我是否必須使用標籤才能部署Web SDK？

不会。您可以下載 `alloy.js` 自行檔案。

但是:

* Adobe Experience Platform Web SDK需要資料流ID，讓Edge Network可以識別資料流，並決定如何處理資料。 此ID是在Experience Platform中建立。 這並不意味著您必須使用UI來建立屬性或部署JavaScript程式碼，但您確實需要使用標籤來建立設定ID。

* 標籤不僅是最佳可用標籤和SDK管理員，而且可讓您輕鬆部署 `alloy.js` 並將資料對應至XDM結構描述。 如果您決定不使用標籤，則必須管理部署 `alloy.js`，事件以及在傳送資料之前將資料對應至XDM。 這是 _很多_ 比使用標籤更難的流程。

* 建議您使用標籤進行部署 `alloy.js`，即使這是您使用它的唯一標籤。

## 什麼是事件轉送？

如果您使用我們的SDK並將XDM傳送至Experience Edge，這些新功能事件轉送可讓您安裝新的伺服器端擴充功能，並將資料對應至任何Edge網路上的任何專案，並將資料傳送至任何地方。 將其視為「資料收集即服務」。 這項服務不需支付相關費用，且會隨附於Adobe Experience Platform中。

## 什麼是CNAME或第一方網域？它為什麼重要？

有關CNAME的更多資訊，請參閱 [Adobe檔案](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK是否使用Cookie？ 若有，會使用哪些Cookie？

是，根據您的實作，目前Web SDK會使用一到七個Cookie。 以下是您在Web SDK中可能會看到的Cookie清單及其使用方式：

| **名称** | **maxAge** | **友善年齡** | **描述** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 天 | 身分Cookie會儲存ECID以及與ECID相關的其他資訊。 |
| **kndctr_orgid_consent_check** | 7200 | 2 小时 | 此Cookie會儲存使用者對網站的同意偏好設定。 |
| **kndctr_orgid_consent** | 15552000 | 180 天 | 此工作階段型Cookie會傳送訊號，讓伺服器查詢同意偏好設定伺服器端。 |
| **kndctr_orgid_cluster** | 1800 | 30 分钟 | 此Cookie會儲存為目前使用者請求提供服務的Experience Edge區域。 URL路徑會使用地區，這樣Experience Edge就可以將請求路由到正確的地區。 此Cookie的存留期為30分鐘，因此如果使用者以不同的IP位址連線，則請求可以路由至最近的區域。 |
| **mbox** | 63072000 | 2 年 | 當Target移轉設定設為true時，此Cookie便會出現。 這將允許Target [mbox Cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) 將由Web SDK設定。 |
| **mboxEdgeCluster** | 1800 | 30 分钟 | 當Target移轉設定設為true時，此Cookie便會出現。 此Cookie可讓Web SDK將正確的邊緣叢集通訊至at.js，以便在使用者導覽網站時，Target設定檔可以維持同步。 |
| **AMCV_###@AdobeOrg** | 34128000 | 395 天 | 只有在Adobe Experience Platform Web SDK上啟用ID移轉時，此Cookie才會出現。 在網站某些部分仍在使用visitor.js時，此Cookie有助於轉換至Web SDK。 請參閱 [idMigrationEnabled檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) 以進一步瞭解此設定。 |

使用Web SDK時，Edge Network會設定上方的一個或多個Cookie。 Edge Network會使用設定所有Cookie `secure` 和 `sameSite="none"` 屬性。

如果您的網站上目前同時有安全和不安全的區段，可能會干擾使用者識別。 當使用者從網站的安全區段導覽到非安全區段時，Edge Network會產生一個新的 `ECID` 透過要求。

## Adobe Experience Platform Web SDK支援哪些瀏覽器？

Adobe Experience Platform Web SDK的設計可在最新版Google Chrome、Safari、Firefox、Internet Explorer 11和Microsoft Edge Chromium中以最佳方式運作。 在舊版的瀏覽器上使用某些功能時可能會發生問題。

## 我可以在哪裡取得有關Adobe Experience Platform Web SDK的詳細資訊？

* [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hans)
* [源代码](https://github.com/adobe/alloy)
