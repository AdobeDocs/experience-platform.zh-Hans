---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
solution: Experience Platform
title: 使用GitHub網頁介面建立來原始檔頁面
description: 本檔案提供如何使用GitHub網頁介面來編寫檔案及提交提取請求(PR)的步驟。
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---

# 使用GitHub網頁介面建立來原始檔頁面

本檔案提供如何使用GitHub網頁介面來編寫檔案及提交提取請求(PR)的步驟。

>[!TIP]
>
>Adobe投稿指南中的下列檔案可用來進一步支援您的檔案流程： <ul><li>[安裝Git和Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[在本地设置适用于文档的 Git 存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[针对主要更改的 GitHub 参与工作流](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## 設定您的GitHub環境

設定GitHub環境的第一個步驟是導覽至 [Adobe Experience Platform GitHub存放庫](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

接下來，選取 **分支**.

![分支存储库](../assets/fork.png)

復本完成後，請選取 **主版** 並在出現的下拉式選單中輸入新分支的名稱。 請確定您為分支提供描述性名稱，因為這將用於包含您的工作，然後選取 **建立分支**.

![create-branch](../assets/create-branch.png)

在您取用的存放庫的GitHub資料夾結構中，導覽至 [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) 然後從清單中為您的來源選取適當的類別。 例如，如果您正在建立新CRM來源的檔案，請選取 **crm**.

>[!TIP]
>
>如果您要建立UI的檔案，請導覽至 [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) 並為您的來源選取適當的類別。 若要新增影像，請導覽至 [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) 然後將熒幕擷取畫面新增至 `sdk` 資料夾。

![crm](../assets/crm.png)

現有CRM來源的資料夾隨即顯示。 若要新增新來源的檔案，請選取「 」 **新增檔案** 然後選取 **建立新檔案** 從出現的下拉式功能表中。

![create-new-file](../assets/create-new-file.png)

為您的來源檔案命名 `YOURSOURCE.md` 其中YOURSOURCE是您在Platform中的來源名稱。 例如，如果您的公司是ACME CRM，則您的檔案名稱應該是 `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## 為您的來源編寫檔案頁面

若要開始製作新來源的檔案，請貼上 [來原始檔範本](./template.md) 移至GitHub網頁編輯器中。 您也可以下載範本 [此處](../assets/api-template.zip).

將範本複製到GitHub網頁編輯器介面後，請依照範本上概述的指示操作，並編輯包含來源相關資訊的值。

![貼上範本](../assets/paste-template.png)

完成後，在您的分支中提交檔案。

![認可](../assets/commit.png)

## 提交您的檔案以供檢閱

提交檔案後，您可以開啟提取請求(PR)，將工作分支合併到Adobe檔案存放庫的主分支。 確定已選取您正在處理的分支，然後選取 **比較和提取請求**.

![compare-pr](../assets/compare-pr.png)

請確認基底和比較分支正確無誤。 在PR中新增附註，說明您的更新，然後選取 **建立提取請求**. 這會開啟PR，以將您工作的工作分支合併到Adobe存放庫的主分支。

>[!TIP]
>
>離開 **允許維護者編輯** 核取方塊已選取，以確保Adobe檔案團隊可以編輯PR。

![create-pr](../assets/create-pr.png)

此時，會出現通知，提示您簽署Adobe貢獻者授權合約(CLA)。 此為必要步驟。 在您簽署CLA後，請重新整理PR頁面並提交提取請求。

您可以檢查https://github.com/AdobeDocs/experience-platform.en中的「提取請求」標籤，確認提取請求已提交。

![confirm-pr](../assets/confirm-pr.png)
