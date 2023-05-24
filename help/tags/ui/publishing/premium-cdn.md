---
title: 標籤的Premium CDN支援
description: 瞭解標籤的頂級CDN功能，以及如何使用它來將您的內容傳送至多個地理區域。
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 標籤的Premium CDN支援（測試版）

>[!IMPORTANT]
>
>標籤的高階CDN功能目前為測試版，貴組織可能尚未存取該功能。 本檔案內容可能會有變動。

當您使用 [Adobe管理主機](./hosts/managed-by-adobe-host.md) 為了在您的網站上傳遞Adobe Experience Platform標籤資產，這些資產會散佈在世界各地各種內容傳遞網路(CDN)中，以提供最快的下載速度。 不過，某些地區要求將所有網站資產複製並託管於該地區的伺服器上。

為了說明此問題，Experience Platform中的標籤提供高級CDN功能，可讓您向這些特殊區域傳送內容。

Premium CDN支援是付費功能，貴組織必須購買才能啟用及使用它。 本指南說明購買此功能後，如何在Experience PlatformUI或資料收集UI中設定和使用它。

## 為您的組織啟用優質CDN

Premium CDN已在公司層級啟用。 貴組織購買進階CDN功能後，Adobe管理員會在貴公司的UI中啟用該功能。

## 使用更新的內嵌程式碼重建和安裝標籤程式庫

啟用Premium CDN後，並不表示您的標籤資產會立即復寫並準備在新的區域使用。 這僅表示您現在可以選擇何時加入此功能。

>[!IMPORTANT]
>
>在啟用優質CDN之前建立的程式庫將會繼續照常運作。 這也適用於不是由Adobe管理的程式庫，因為 [封存的環境](./environments.md#archive) 僅對其資產路徑使用相對URL。 請注意，啟用進階CDN後，您建置且非由Adobe管理的程式庫，其行為會與未啟用進階CDN功能相同。

啟用進階CDN並重新建置您要從新託管區域使用的任何程式庫後，您就可以擷取新的託管區域內嵌程式碼，以新增至您的網站。

>[!NOTE]
>
>列於「 」下方的程式庫內嵌程式碼 [!UICONTROL 標準] 託管區域將繼續照原樣運作，並且您的網站上已有任何Page Top或Page Bottom內嵌程式碼。

造訪 **[!UICONTROL 環境]** 從「程式庫」編輯畫面頁面或檢視環境安裝指示，以尋找新的內嵌程式碼。 每個新支援的託管區域都會顯示在 [!UICONTROL 標準] 託管區域（用於世界上沒有優質CDN支援的區域）。 以下熒幕擷圖顯示中國地區的內嵌程式碼，該程式碼使用 `.cn` 作為其頂層網域(TLD)。

![中國地區的內嵌程式碼](../../images/ui/publishing/premium-cdn/embed-codes.png)

為網頁選擇適當的內嵌程式碼，並將其貼到 `<head>` 標籤之前。 如需使用內嵌程式碼安裝標籤程式庫的詳細資訊，請參閱 [環境UI指南](./environments.md#installation).

## 后续步骤

本指南說明如何為您的標籤實作啟用和安裝進階CDN功能。 如需在Web和行動屬性上安裝及測試標籤程式庫的詳細資訊，請參閱 [發佈概觀](./overview.md).
