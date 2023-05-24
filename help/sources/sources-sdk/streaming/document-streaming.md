---
title: 記錄您的來源（串流SDK）
description: 在Adobe Experience Platform中讓新來源上線之前的最後一步，是記錄您的新來源。
hide: true
hidefromtoc: true
exl-id: 65ca7a4d-3e02-4f54-bf07-ea2c92b8dbf1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 記錄您的來源（串流SDK）

在Adobe Experience Platform中即時設定新來源之前的最後一步，是記錄您的新來源。

本檔案指南包含：

* 您可以遵循的教學課程，為您的新來源建立檔案頁面；
* 說明檔案範本可供您填寫新來源；
* [有關如何使用Markdown撰寫技術檔案的指示](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en)；
* [瞭解AdobeMarkdown風格的相關說明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions).

## 先决条件

開始記錄新來源之前，需要下列專案：

* **有效的GitHub使用者帳戶**：如果您沒有現有的GitHub帳戶，則必須透過以下連結建立一個帳戶： [GitHub註冊頁面](https://github.com/)；
* **存取GitHub Desktop**：您必須使用 [GitHub案頭應用程式](https://desktop.github.com/) 以便在您的本機環境中建立您的來原始檔；
* 您與Adobe的整合必須處於測試階段，且您的來源已部署在Platform中的中繼環境中。

## 在Platform中建立來原始檔的高階指示

從高層面來看，若要為來源建立檔案，您需要建立Platform檔案存放庫復本，並在新分支中編輯提供的檔案範本。 使用Adobe提供的範本建立新的來源頁面，並在您準備就緒時開啟提取請求(PR)。 在建立新來源頁面的步驟中，進一步說明如何執行此操作。

## 檔案範本

您可以使用預填 [api檔案範本](streaming-template-api.md) 或 [UI檔案範本](streaming-template-ui.md) 以協助建立您來源的檔案。 進一步瞭解下列資訊，瞭解如何編輯範本及開啟提取請求。 針對您新來源提交的說明檔案將由Adobe說明檔案團隊稽核並發佈。

您也可以下載下列檔案範本：

* [api檔案範本](../assets/streaming/streaming-template-api.zip)
* [UI檔案範本](../assets/streaming/streaming-template-ui.zip)

## 建立您的新來源頁面

您可以使用GitHub網頁介面或本機環境，在Platform中建立新來源的檔案。 請前往下列連結，尋找這兩個選項的指示：

* [使用GitHub網頁介面建立來原始檔頁面](../documentation/github.md)
* [在本機環境中使用文字編輯器來建立來原始檔頁面](../documentation/text-editor.md)
