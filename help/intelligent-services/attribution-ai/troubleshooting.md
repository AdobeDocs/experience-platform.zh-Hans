---
keywords: Experience Platform；快速入門；attribution ai；熱門主題；attribution ai輸入；attribution ai輸出；attribution ai疑難排解；attribution ai錯誤
solution: Experience Platform, Real-time Customer Data Platform
feature: Attribution AI
title: Attribution AI錯誤疑難排解
description: 尋找Attribution AI中常見錯誤的解答。
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Attribution AI錯誤疑難排解

本檔案提供有關Attribution AI常見問題的解答。

## 無法無痕存取Chrome中的Attribution AI

由於Google Chrome無痕模式安全性設定有所更新，導致Google Chrome無痕模式中發生載入錯誤。 這個問題正在積極與Chrome合作，使experience.adobe.com成為受信任的網域。

<img src="./images/faq/error.PNG" width="500" /><br />

### 建議的修正

若要解決此問題，您需要將experience.adobe.com新增為可隨時使用Cookie的網站。 首先，請瀏覽至 **chrome://settings/cookies**. 接下來，向下捲動至 **自訂行為** 區段，然後選取 **新增** 按鈕（在「可隨時使用Cookie的網站」旁）。 在出現的彈出視窗中，複製並貼上 `[*.]experience.adobe.com` 然後選取 **包含第三方Cookie** 「在此網站上」核取方塊。 完成後，選取 **新增** 和以無痕方式重新載入Attribution AI。

![建議的修正](./images/faq/cookies2.gif)
