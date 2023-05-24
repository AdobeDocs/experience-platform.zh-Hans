---
title: Adobe Experience Platform Web SDK概觀
description: 瞭解如何使用Adobe Experience Platform Web SDK將Platform功能整合至您的網站。
keywords: Adobe Experience Platform Web SDK；Platform Web SDK；Web SDK；Edge；Visitor.js；AppMeasurement.js；AT.js；DIL.js；Web SDK；SDK；Web SDK；Launch；Launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK總覽 {#overview}

Adobe Experience Platform Web SDK是使用者端的JavaScript程式庫，可讓Adobe Experience Cloud的客戶與 [!DNL Experience Cloud] 透過Adobe Experience Platform Edge Network。 除了JavaScript程式庫，還有 [標籤延伸模組](./extension/web-sdk-extension-configuration.md) 以協助進行Web SDK設定。

如需使用標籤設定Web SDK並將資料傳送至解決方案的逐步指南，請參閱我們的 [使用Web SDK教學課程實作Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>本產品持續進化和成長，以支援越來越多的使用案例。 若要掌握最新資訊並檢視我們目前支援的內容，請參閱 [支援的使用案例頁面](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是構成 [!DNL Adobe Experience Edge]. [!DNL Experience Edge] 包含下列技術：

* **[[!DNL Adobe Experience Platform Web SDK]](#overview)：** JavaScript SDK和標籤擴充功能可大幅簡化部署作業 [!DNL Adobe] 技術。
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview)：** v5行動SDK的擴充功能，可讓客戶使用新的部署方法
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md)：** 全球性的分散式伺服器網路，提供全新的部署方法 [!DNL Adobe] 產品

此 [!DNL Adobe Experience Edge] 是全新架構，適用於所有可定址管道的低延遲資料收集、可插拔式運算和快速資料啟用。

[!DNL Adobe Experience Edge] 為每個管道（JavaScript、行動裝置、伺服器端）提供單一整合SDK，將資料傳送至通用Adobe網域(`adobedc.net`)並接收單一裝載，以傳回資料和體驗傳送。

在伺服器端，統一的邊緣閘道和通用平台服務架構可讓您輕鬆地在此即時運算環境中外掛程式及部署新功能。  此架构：

* 縮短客戶實現價值的時間
* 結束對「點」整合的需求
* 相較於舊程式庫，提升效能
* 降低成本
* 加快創新速度
* 為Adobe客戶創造持續的競爭優勢

單一整合的Edge系統可讓客戶管理其跨所有頻道的廣告、行銷或個人化行銷活動，作為整合式體驗。 它允許 [!DNL Adobe] 以較低的總體擁有成本為客戶提供服務。  此外，透過即時邊緣可插拔並允許 [!DNL Adobe] 以及客戶更快新增新功能和客戶定義的邏輯至該即時系統。

## 视频概述 {#video}

下列影片會概略介紹Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 以Web SDK取代的程式庫 {#sdks}

Web SDK不僅僅是現有程式庫的包裝函式。 這是一個全新的程式庫，從頭開始撰寫，以納入現有程式庫的功能。 其目的是為了結束標籤必須依正確順序引發的挑戰、與程式庫版本設定挑戰的不一致，以及更好的相依性管理。 這是實作 [!DNL Experience Cloud] 而且它是 [開放原始碼](https://github.com/adobe/alloy).

Web SDK會取代下列SDK：

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

除了新程式庫外，還有一個新端點，可簡化Adobe解決方案的HTTP請求。 之前，Visitor.js傳送封鎖呼叫給訪客ID服務，然後AT.js傳送呼叫給Adobe Target，DIL.js傳送呼叫給Adobe Audience Manager，最後AppMeasurement.js傳送呼叫給Adobe Analytics。 此新程式庫和端點可以擷取ID、擷取 [!DNL Target] 體驗，傳送資料至 [!DNL Audience Manager]，並透過單一呼叫將資料傳遞至Adobe Experience Platform。

下列影片示範Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network] 執行中。 影片範例使用單一呼叫來Adobe，將資料傳送至 [!DNL Experience Platform]， [!DNL Analytics]， [!DNL Audience Manager]、和 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 從現有程式庫移轉至Web SDK {#migrating-to-web-sdk}

若要簡化從任一 [現有程式庫](#sdks) Adobe為Web SDK提供簡化的升級途徑，讓您將網站的每個個別頁面移轉至Web SDK，而不需要一次移轉整個網站。

這表示您可以在頁面上使用Web SDK，並將現有程式庫保留在其他頁面上，直到您也可以移轉為止。

### at.js移轉至Web SDK的考量事項 {#considerations}

移轉使用下列專案的頁面之前： [!DNL at.js] 若要使用Web SDK，請務必啟用下列Web SDK設定選項。 這可確保從以下頁面導覽時保留訪客設定檔： [!DNL at.js ] 至使用Web SDK的頁面。

* [&#39;idMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [&#39;targetMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>從at.js移轉至Web SDK時不支援下列Target功能：
> * [重定向选件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [CNAME和跨網域支援](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


從at.js移轉至Web SDK後，您應移除 `targetMigrationEnabled` 選項。



