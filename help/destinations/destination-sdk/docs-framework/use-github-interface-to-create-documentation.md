---
title: 使用GitHub網頁介面建立目的地檔案頁面
description: 本頁上的指示會示範如何使用GitHub網頁介面為您的Experience Platform目的地撰寫檔案頁面，並提交該頁面以供檢閱。
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 1%

---

# 使用GitHub網頁介面建立目的地檔案頁面 {#github-interface}

以下指示會示範如何使用GitHub網頁介面來撰寫檔案及提交提取請求(PR)。 在依照此處指出的步驟進行之前，請務必閱讀 [在Adobe Experience Platform目的地中記錄您的目的地](./documentation-instructions.md).

>[!TIP]
>
>另請參閱Adobe投稿人指南中的支援檔案：
>* [安裝Git和Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [在本地设置适用于文档的 Git 存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [针对主要更改的 GitHub 参与工作流](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## 設定您的GitHub製作環境 {#set-up-environment}

1. 在您的瀏覽器中，導覽至 `https://github.com/AdobeDocs/experience-platform.en`.
2. 至 [分支](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) 存放庫，按一下 **分支** 如下所示。 這會在您自己的GitHub帳戶中建立Experience Platform存放庫的復本。

   ![復本Adobe檔案存放庫](../assets/docs-framework/ssd-fork-repository.gif)

3. 在存放庫復本中，為您的專案建立新分支，如下所示。 將此新分支用於您的工作。

   ![建立新的GitHub分支](../assets/docs-framework/new-branch-github.gif)

4. 在分支存放庫的GitHub資料夾結構中，導覽至 `experience-platform.en/help/destinations/catalog/[...]`，其中 `[...]` 是您目的地所需的類別。 例如，如果您要將個人化目的地新增至Experience Platform，請選取 `personalization` 類別。 選取 **新增檔案>建立新檔案**.

   ![新增檔案](../assets/docs-framework/github-navigate-and-create-file.gif)

5. 為您的目的地命名 `YOURDESTINATION.md`，其中YOURDESTINATION是您在Adobe Experience Platform中的目的地名稱。 例如，如果您的公司名為Moviestar，您可以將您的檔案命名為 `moviestar.md`.

## 為您的目的地撰寫檔案頁面 {#author-documentation}

1. 您將根據以下專案建立目的地頁面的內容： [檔案自助服務範本](./self-service-template.md). **[下載](../assets/docs-framework/yourdestination-template.zip)** 並解壓縮範本以解壓縮 `.md` 檔案範本。
2. 線上上Markdown編輯器中，貼上並編輯範本內容以及目的地的相關資訊，例如 [dillinger.io](https://dillinger.io/). 請依照範本中的指示操作，以取得關於您應填寫的內容以及哪些段落可以移除的詳細資訊。

   >[!TIP]
   >
   >您可以隨時關閉瀏覽器視窗，稍後再重新開啟。 系統會自動儲存您的工作，當您重新開啟瀏覽器時，系統會在您面前等待您。
3. 將內容從Markdown編輯器複製到GitHub的新檔案中。
4. 對於您打算使用的任何熒幕擷取畫面或影像，請使用GitHub介面將檔案上傳至 `experience-platform.en/help/destinations/assets/catalog/[...]`，其中 `[...]` 是您目的地所需的類別。 例如，如果您要將個人化目的地新增至Experience Platform，請選取 `personalization` 類別。 您需要從正在編寫的頁面連結至影像。 另請參閱 [如何連結至影像的說明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![將影像上傳至GitHub](../assets/docs-framework/upload-image.gif)

5. 準備就緒後，將檔案儲存在分支中。

![確認檔案建立](../assets/docs-framework/ssd-confirm-file-creation.png)

## 提交您的檔案以供檢閱 {#submit-review}

>[!TIP]
>
>請注意，您無法在此處中斷任何內容。 依照本節的指示，您只是建議更新檔案。 您建議的更新將由Adobe Experience Platform檔案團隊核准或編輯。

1. 儲存檔案並上傳所需影像後，您可以開啟提取請求(PR)，將工作分支合併至Adobe檔案存放庫的主分支。 確定已選取並選取您處理的分支 **Contribute >開啟提取請求**.

![建立提取請求](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. 請確定基底和比較分支正確無誤。 在PR中新增附註，說明您的更新，然後選取 **建立提取請求**. 這會開啟PR，以將復本的工作分支合併到Adobe存放庫的主分支。

   >[!TIP]
   >
   >離開 **允許維護者編輯** 核取方塊已選取，以便Adobe檔案團隊可以編輯PR。

   ![建立提取請求以Adobe檔案存放庫](../assets/docs-framework/ssd-create-pull-request-2.png)

1. 此時，會出現通知，提示您簽署Adobe貢獻者授權合約(CLA)。 此為必要步驟。 在您簽署CLA後，請重新整理PR頁面並提交提取請求。

1. 您可以透過檢查 **提取請求** 定位於 `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR成功](../assets/docs-framework/ssd-pr-successful.png)

1. 谢谢！若需要編輯檔案，Adobe檔案團隊會與PR聯絡，告知您檔案將於何時發佈。

>[!TIP]
>
>若要新增影像和連結至您的檔案，以及有關Markdown的其他問題，請閱讀 [使用Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) 在Adobe的合作撰寫指南中。
