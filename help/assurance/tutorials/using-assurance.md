---
title: 使用Adobe Experience Platform Assurance
description: 本指南說明在安裝及實作後，如何使用Adobe Experience Platform Assurance。
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 使用Adobe Experience Platform Assurance

本教學課程說明如何使用Adobe Experience Platform保證。 如需如何安裝及實作Adobe Experience Platform Assurance擴充功能的說明，請閱讀以下教學課程： [實作Assurance擴充功能](./implement-assurance.md).

## 建立工作階段

登入之後 [保證UI](https://experience.adobe.com/assurance)，您可以選取 **[!UICONTROL 建立工作階段]** 以開始建立工作階段。

![建立工作階段按鈕會反白顯示，顯示您可以在何處建立工作階段。](./images/using-assurance/create-session.png)

此 **[!UICONTROL 建立新工作階段]** 對話方塊隨即顯示。 請檢閱指定的指示，然後繼續選取 **[!UICONTROL 開始]**.

![「建立新工作階段」對話方塊隨即顯示，其中顯示如何使用「保證」的說明。](./images/using-assurance/create-new-session.png)

您現在可以輸入名稱來識別工作階段，然後提供 **[!UICONTROL 基本URL]** （應用程式的深層連結URL）。 提供這些詳細資料後，請選取 **[!UICONTROL 下一個]**.

>[!INFO]
>
>基礎URL是用來從URL啟動應用程式的根定義。 產生工作階段URL，您可以透過它啟動Assurance工作階段。 範例值可能如下所示： `myapp://default` 在 **[!UICONTROL 基本URL]** 欄位中，輸入應用程式的基本深層連結定義。

![隨即顯示建立新工作階段的完整工作流程。](./images/using-assurance/create-session.gif)

## 連線至工作階段

建立工作階段後，請確定您看到 **[!UICONTROL 建立新工作階段]** 對話方塊現在會顯示連結、QR碼和PIN。

![會顯示一個對話方塊，顯示連線至您的保證工作階段的選項。](./images/using-assurance/create-new-session-pin.png)

如果出現此對話方塊，您可以使用裝置的相機應用程式來掃描二維碼並開啟應用程式，或複製連結並在應用程式中開啟。 應用程式啟動時，應該會看到PIN輸入畫面重疊。 輸入上一步驟的PIN並按下 **[!UICONTROL Connect]**.

當應用程式上顯示Adobe Experience Platform圖示(紅色Adobe「A」)時，您可驗證應用程式是否已連線至Assurance。

![顯示將應用程式連線至保證工作階段的完整工作流程。](./images/using-assurance/connect-session.gif)

## 匯出工作階段

若要匯出保證工作階段，請在應用程式的工作階段詳細資訊頁面上，選取 **[!UICONTROL 匯出至JSON]** 在工作階段中：

![匯出工作階段](./images/using-assurance/export-session.png)

匯出選項會遵從搜尋篩選結果，並只匯出事件檢視中顯示的事件。 例如，如果您搜尋&quot;track&quot;事件，然後選取 **[!UICONTROL 匯出至JSON]**，只會匯出「追蹤」事件結果。
