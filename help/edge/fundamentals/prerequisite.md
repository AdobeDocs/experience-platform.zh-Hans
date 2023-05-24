---
title: 使用Adobe Experience Platform Web SDK的必要條件
description: 瞭解使用Adobe Experience Platform Web SDK的先決條件。
keywords: 第一方網域；CNAME；結構；建立結構；啟動；aep web sdk擴充功能；擴充功能；設定ID；設定工具；資料元素；建立資料元素；XDM物件；sendEvent；傳送事件；
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 6a9882224cba08718c81a3aead237107b3e47726
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 使用Adobe Experience Platform Web SDK的必要條件

若要使用Adobe Experience Platform Web SDK，您必須先：

- 為您的組織中的使用者設定正確的許可權。 所有Experience Cloud客戶都能存取資料收集工具，而貴組織中的每位使用者只需要結構描述、身分和資料串流的許可權。 若要深入瞭解如何設定這些許可權，請參閱以下檔案： [資料彙集許可權管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
- 建議啟用第一方網域(CNAME)。 如果您已有Adobe Analytics的CNAME，應該使用該CNAME。 開發中的測試不需要使用CNAME即可運作，但Adobe建議您在進入生產階段前先使用一個。 雖然CNAME實作無法在Cookie存留期方面提供任何好處，但可防止某些廣告封鎖程式和較不常見的瀏覽器封鎖SDK請求。 在這些情況下，使用CNAME可防止這些工具使用者的資料收集中斷問題。

>[!IMPORTANT]
>
>**請注意，自2020年11月10日起，所有Safari瀏覽器和行動iOS裝置上的第一方CNAME實作都有7天的有效期。**

- 如果您的網站已使用 [Experience CloudID服務](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) 您的網站上(透過「訪客API」或Adobe Experience Platform Launch中的「Experience CloudID服務」擴充功能)，而您想要在移轉至Adobe Experience Platform Web SDK時繼續使用它，您必須使用最新版本的訪客API或Experience CloudID服務擴充功能。 另請參閱 [ID移轉](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) 以取得詳細資訊。
