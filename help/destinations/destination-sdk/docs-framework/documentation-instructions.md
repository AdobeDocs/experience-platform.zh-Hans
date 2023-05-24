---
title: 在Adobe Experience Platform中記錄您的目的地
description: 協助您在Adobe Experience Platform中建立目的地檔案頁面的逐步指示
exl-id: 6cc9c758-44bb-463b-941a-06b1a22ee8f3
source-git-commit: ffd87573b93d642202e51e5299250a05112b6058
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# 在Adobe Experience Platform中記錄您的目的地

>[!IMPORTANT]
>
>此處記錄的程式僅適用於提交生產（公用）目的地的合作夥伴。 如果您要建立私人目的地以供自己使用，則不需要為目的地建立和發佈檔案。

## 概述 {#overview}

歡迎使用Adobe Experience Platform，很高興在這裡見到您！
記錄您的目的地是可在Adobe Experience Platform中即時設定之前的最後一步。

本檔案區段包含：

* 逐步指示讓您為新目的地建立檔案頁面；
* 範本可供您填寫目的地；
* [使用Markdown的一般指示](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en)；
* [AdobeMarkdown風格的特定指示](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#custom-markdown-extensions) (AdobeMarkdown的風格與一般Markdown非常類似)。
* A [最佳實務頁面](./authoring-best-practices.md) 協助您為符合Experience Platform檔案品質標準的目的地頁面撰寫檔案頁面。

## 先决条件 {#prerequisites}

若要根據本文中的指示建立目的地的檔案，需要下列專案：

* **GitHub帳戶**. 註冊 [GitHub](https://github.com/) 如果您還沒有帳戶。
* **GitHub Desktop**. 如果您選取 [在本機環境中建立檔案](./work-in-local-environment.md)，您必須使用 [GitHub Desktop](https://desktop.github.com/).
* 您與Adobe的整合必須處於測試階段，且您的目的地部署在Adobe Experience Platform中的中繼環境中。

## 在Adobe Experience Platform中建立目的地檔案的高層級指示 {#high-level-instructions}

整體而言，若要建立目的地的檔案，您必須 [建立分支](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) Adobe Experience Platform存放庫的檔案並編輯 [提供的檔案範本](./self-service-template.md) 在新分支中。 使用Adobe提供的範本建立新的目的地頁面。 準備就緒後，開啟提取請求(PR)。 以下提供執行此動作的說明： [建立新目的地頁面的步驟](./documentation-instructions.md#steps-to-create-docs-page).

<!--

* In the table of contents (TOC.md) `/help/rtcdp/TOC.md`, add a link to your new destination page. Place it within the category where your destination resides in the Adobe Experience Platform user interface (for example: mobile, social, advertising). 
* In the overview page for the respective category, add a link to your new destination page. For example, for cloud storage destinations, you would add a link to [this page](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-cat/cloud-storage/cloud-storage-destinations.html). 

-->

## 檔案範本 {#documentation-template}

為協助您建立說明檔案頁面，Adobe已預先填入 [檔案範本](./self-service-template.md) 敬請參考使用。 進一步瞭解下列資訊，瞭解如何編輯範本及開啟提取請求。 Adobe檔案團隊將稽核並發佈您新目的地的檔案。

[在這裡下載範本](../assets/docs-framework/yourdestination-template.zip) 並解壓縮檔案以解壓縮 `yourdestination.md` 檔案。

使用範本建立檔案頁面的說明進一步列於下方。

## 建立新目的地頁面的步驟 {#steps-to-create-docs-page}

您可以使用GitHub網頁介面或本機環境，為Adobe Experience Platform中的新目的地建立檔案。 請前往下列連結，尋找這兩個選項的指示：

* [使用GitHub網頁介面建立目的地檔案頁面](./use-github-interface-to-create-documentation.md)
* [在本機環境中使用文字編輯器來建立目的地檔案頁面](./work-in-local-environment.md)

## 最佳实践 {#best-practices}

檢閱 [製作最佳實務](/help/destinations/destination-sdk/docs-framework/authoring-best-practices.md) 建立目的地檔案頁面之前和期間。 也請務必閱讀 [Adobe檔案撰寫指南](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) 以瞭解Adobe檔案團隊在撰寫檔案時所使用的更多撰寫提示。