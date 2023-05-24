---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
solution: Experience Platform
title: 在本機環境中使用文字編輯器來建立來原始檔頁面
description: 本檔案提供相關步驟，說明如何使用本機環境編寫來原始檔，並提交提取請求(PR)。
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# 在本機環境中使用文字編輯器來建立來原始檔頁面

本檔案提供相關步驟，說明如何使用本機環境編寫來原始檔，並提交提取請求(PR)。

>[!TIP]
>
>Adobe投稿指南中的下列檔案可用來進一步支援您的檔案流程： <ul><li>[安裝Git和Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[在本地设置适用于文档的 Git 存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[针对主要更改的 GitHub 参与工作流](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## 先决条件

下列教學課程要求您在本機電腦上安裝GitHub Desktop。 如果您沒有GitHub Desktop，可以下載應用程式 [此處](https://desktop.github.com/).

## 連線至GitHub並設定您的本機撰寫環境

設定本機編寫環境的第一個步驟是導覽至 [Adobe Experience Platform GitHub存放庫](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

在Platform GitHub存放庫的首頁上，選取「 」 **分支**.

![分支存储库](../assets/fork.png)

若要將存放庫複製到本機電腦，請選取 **程式碼**. 從出現的下拉式功能表中，選取 **HTTPS** 然後，選取 **使用GitHub Desktop開啟**.

>[!TIP]
>
>如需詳細資訊，請參閱以下教學課程： [在本機設定適用於檔案的Git存放庫](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

接下來，請稍候片刻，讓GitHub Desktop複製 `experience-platform.en` 存放庫。

![複製](../assets/cloning.png)

復製程式完成後，請前往GitHub Desktop建立新分支。 選取 **主版** 從頂端導覽列中，然後選取 **新增分支**

![new-branch](../assets/new-branch.png)

在出現的彈出視窗面板中，輸入分支的描述性名稱，然後選取 **建立分支**.

![create-branch-vs](../assets/create-branch-vs.png)

接下來，選取 **發佈分支**.

![publish-branch](../assets/publish-branch.png)

## 為您的來源編寫檔案頁面

將存放庫複製到本機電腦，並建立新分支後，您現在可以開始透過為您的新來源編寫檔案頁面 [您選擇的文字編輯器](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors).

Adobe建議您使用 [Visual Studio Code](https://code.visualstudio.com/) 並安裝AdobeMarkdown Authoring擴充功能。 若要安裝擴充功能，請啟動Visual Studio Code，然後選取 **擴充功能** 標籤。

![扩展](../assets/extension.png)

接下來，輸入 `Adobe Markdown Authoring` 放入搜尋列，然後選取 **安裝** 從出現的頁面。

![安裝](../assets/install.png)

在本機電腦準備就緒後，下載 [來原始檔範本](../assets/api-template.zip) 並將檔案解壓縮至 `experience-platform.en/help/sources/tutorials/api/create/...` 替換為 [`...`] 代表您選擇的類別。 例如，如果您要建立資料庫來源，請選取資料庫資料夾。

最後，請遵循範本上概述的指示，使用與您的來源相關的資訊來編輯範本。

![edit-template](../assets/edit-template.png)

## 提交您的檔案以供檢閱

若要建立提取請求(PR)並提交檔案以供稽核，請先將您的工作儲存在 [!DNL Visual Studio Code] （或您選擇的文字編輯器）。 接下來，使用GitHub Desktop，輸入認可訊息並選取 **提交至create-source-documentation**.

![commit-vs](../assets/commit-vs.png)

接下來，選取 **推播來源** 將您的工作上傳至遠端分支。

![推播來源](../assets/push-origin.png)

若要建立提取請求，請選取 **建立提取請求**.

![create-pr-vs](../assets/create-pr-vs.png)

請確認基底和比較分支正確無誤。 在PR中新增附註，說明您的更新，然後選取 **建立提取請求**. 這會開啟PR，以將您工作的工作分支合併到Adobe存放庫的主分支。

>[!TIP]
>
>離開 **允許維護者編輯** 核取方塊已選取，以確保Adobe檔案團隊可以編輯PR。

![create-pr](../assets/create-pr.png)

您可以檢查https://github.com/AdobeDocs/experience-platform.en中的「提取請求」標籤，確認提取請求已提交。

![confirm-pr](../assets/confirm-pr.png)
