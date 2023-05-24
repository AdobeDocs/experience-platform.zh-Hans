---
title: Adobe Experience Platform保證概觀
description: Adobe Experience Platform Assurance 可帮助您检查、证明、模拟和验证您在移动应用程序中收集数据或提供体验的方式。
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 4%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance產品來自 [Adobe Experience Cloud](https://www.adobe.com/cn/experience-cloud.html) 協助您檢查、校樣、模擬及驗證如何在行動應用程式中收集資料或提供體驗。

>[!IMPORTANT]
>
> Project Griffon現在稱為 **保證**！
>
> Project Griffon現在通常可供 **全部** Adobe Experience Cloud客戶作為保證。 若要進一步瞭解此轉變，請閱讀 [使用者存取指南](./user-access.md).

>[!INFO]
>
>Assurance Public API可供使用！
>
>[保證API](https://developer.adobe.com/adobe-assurance-public-apis/) 是API的集合，當使用者裝備AdobeAssurance Mobile SDK時，這些API可讓使用者測試和偵錯其網頁和行動應用程式。

## 正式发布

自2022年10月15日起，所有Adobe Experience Cloud皆普遍提供保證功能。

### 有什麼改變？

10月15日 — 將透過Admin Console管理對Assurance的存取。 請閱讀 [使用者存取指南](./user-access.md) 以確保您能繼續不間斷地存取。

對於現有的保證整合、工作階段和事件，預計不會發生其他變更或中斷。 保證可繼續透過以下方式存取： [https://griffon.adobe.com](https://griffon.adobe.com) **或** 您可以使用（和書籤） [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Assurance可為您做什麼？

### 快速設定

使用幾行程式碼快速開始使用。 針對行動應用程式，Assurance會與Adobe Experience Platform Mobile SDK搭配使用，協助您檢查、模擬及驗證應用程式事件、位置訊號、設定引數、SDK記錄、裝置資訊等。

### 輕鬆連線

有了Assurance，將您的應用程式與Platform連線起來既簡單又可靠。 您不需要使用網路代理， [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack))和其他網路體操 — 將應用程式連線至Assurance就像掃描QR碼或點選按鈕一樣簡單。

![](./images/index/no-hassle-connection.png)

### 即時檢查、模擬和驗證

連線至Assurance後，您可以檢查即時串流應用程式事件和活動，並篩選和搜尋以排除雜訊。 事件包含有關驗證、偵錯和疑難排解行動應用程式實作的詳細資訊。 Assurance也可讓您即時擷取熒幕擷圖、模擬位置訊號等等。

![](./images/index/real-time-insepction.png)

### 與Adobe Experience Cloud整合

使用者端資料和體驗透過使用者在我們的以行銷人員為中心的使用者介面上設定報告規則、活動和行銷活動來提供。 為了協助您連結這兩者之間的點，我們整合了Adobe Experience Cloud解決方案，例如Adobe Experience Platform、Adobe Analytics、Adobe Target、Places Service等。

![](./images/index/integration.png)

## 功能

### Adobe Experience Platform Mobile SDK事件、記錄檔等

Assurance可協助您檢查Adobe Experience Platform Mobile SDK產生的原始SDK事件。 SDK收集的所有事件都可供檢查。 SDK事件會載入清單檢視中，依時間排序。 每個事件都有一個詳細檢視，提供更多詳細資訊。 此外，也提供瀏覽SDK設定、資料元素、共用狀態和SDK擴充功能版本的其他檢視。

### Adobe Analytics

Adobe Analytics > Analytics事件檢視是重點檢視，可顯示與您的Adobe Analytics行動實施相關的事件。 清單檢視會在特別格式化的檢視中顯示生命週期或動作/狀態事件、後處理的「狀態」，以及必要的事件詳細資訊。 「後處理」狀態會顯示Adobe Analytics在處理規則套用至事件後，如何處理該事件。

### 适用于流媒体的 Adobe Analytics

「Adobe Analytics > Media Analytics事件」檢視會顯示音訊與視訊分析實作的事件。 事件詳細資料檢視會顯示針對每個播放工作階段追蹤的標準與自訂中繼資料。 此外，您還可以檢視處理後狀態和後處理的媒體分析資料，例如媒體逗留時間或總緩衝時間。

### 地點（定位服務）

Location Services檢視是裝置上的檢視，可顯示使用者位置登入和退出事件，以方便驗證。 此方便使用的檢視提供便利的介面，可檢視使用者端的特定位置資料點，以供進行內容內偵錯。

## 保證安全嗎？

保證已採取下列安全措施：

* Assurance和Assurance Web UI都有安全的PIN型連線握手。 使用者必須明確建立交握，以防止一般使用者建立「意外」保證連線。
* 僅支援屬於相同Adobe Experience Cloud組織ID的Assurance和Assurance Web UI之間的連線。
* Adobe Experience Platform Mobile SDK事件會透過HTTPS傳輸。
* Assurance和Adobe Experience Platform Mobile SDK使用TLS 1.2
* 保證工作階段會在30天後刪除。
* 依照儲存最佳實務，保證工作階段資料會進行靜態加密。

## 快速入门

若要設定Assurance，您必須先在應用程式中安裝Assurance擴充功能。 若要瞭解如何執行此動作，請閱讀以下教學課程： [實作Assurance擴充功能](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

將Assurance新增至應用程式後，您可以建立可連線至裝置的保證工作階段。 若要瞭解如何使用Assurance，請參閱 [使用保證指南](./tutorials/using-assurance.md).
