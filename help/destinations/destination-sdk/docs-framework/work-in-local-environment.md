---
title: 在本機環境中使用文字編輯器來建立目的地檔案頁面
description: 本頁上的指示會示範如何使用文字編輯器在本機環境中運作，為Experience Platform目的地編寫檔案頁面並提交它以供檢閱。
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 2%

---

# 在本機環境中使用文字編輯器來建立目的地檔案頁面 {#local-authoring}

本頁上的指示會示範如何使用文字編輯器在本機環境中運作，以撰寫檔案並提交提取請求(PR)。 在依照此處指出的步驟進行之前，請務必閱讀 [在Adobe Experience Platform目的地中記錄您的目的地](./documentation-instructions.md).

>[!TIP]
>
>另請參閱Adobe投稿人指南中的支援檔案：
>* [安裝Git和Markdown編寫工具](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [在本地设置适用于文档的 Git 存储库](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [针对主要更改的 GitHub 参与工作流](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## 連線至GitHub並設定您的本機撰寫環境 {#set-up-environment}

1. 在您的瀏覽器中，導覽至 `https://github.com/AdobeDocs/experience-platform.en`
2. 至 [分支](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) 存放庫，按一下 **分支** 如下所示。 這會在您自己的GitHub帳戶中建立Experience Platform存放庫的復本。

   ![復本Adobe檔案存放庫](../assets/docs-framework/ssd-fork-repository.gif)

3. 将存储库克隆到您的本地计算机. 選取 **程式碼> HTTPS >使用GitHub Desktop開啟**，如下所示。 確定您擁有 [GitHub Desktop](https://desktop.github.com/) 已安裝。 如需進一步參考，請閱讀 [建立存放庫的本機複製](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) 在Adobe投稿人指南中。

   ![將Adobe檔案存放庫複製到本機環境](../assets/docs-framework/clone-local.png)

4. 在本機檔案結構中，導覽至 `experience-platform.en/help/destinations/catalog/[...]`，其中 `[...]` 是您目的地所需的類別。 例如，如果您要將個人化目的地新增至Experience Platform，請選取 `personalization` 資料夾。

## 為您的目的地撰寫檔案頁面 {#author-documentation}

1. 您的檔案頁面是根據 [自助服務目的地範本](../docs-framework/self-service-template.md). 下載 [目的地範本](../assets/docs-framework/yourdestination-template.zip). 解壓縮並解壓縮檔案 `yourdestination-template.md` 至上述步驟4中所述的目錄。  重新命名檔案 `YOURDESTINATION.md`，其中YOURDESTINATION是您在Adobe Experience Platform中的目的地名稱。 例如，如果您的公司名為Moviestar，您可以將您的檔案命名為 `moviestar.md`.
2. 在「 」中開啟您的新檔案 [選擇的文字編輯器](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). Adobe建議您使用 [Visual Studio Code](https://code.visualstudio.com/) 並安裝AdobeMarkdown Authoring擴充功能。 若要安裝擴充功能，請開啟Visual Studio Code，選取 **[!DNL Extensions]** 標籤進行搜尋 `adobe markdown authoring`. 選取擴充功能並按一下 **[!DNL Install]**.
   ![安裝Adobe Markdown Authoring擴充功能](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. 編輯包含目的地相關資訊的範本。 請依照範本中的指示操作。
4. 如需您打算新增至檔案的任何熒幕擷取畫面或影像，請前往 `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`，其中 `[...]` 是您目的地所需的類別。 例如，如果您要將個人化目的地新增至Experience Platform，請選取 `personalization` 資料夾。 為目的地建立新資料夾，並將影像儲存至此處。 您必須從正在編寫的頁面連結至這些專案。 另請參閱 [如何連結至影像的說明](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. 準備就緒後，儲存您正在處理的檔案。

## 提交您的檔案以供檢閱 {#submit-review}

>[!TIP]
>
>請注意，您無法在此處中斷任何內容。 依照本節的指示，您只是建議更新檔案。 您建議的更新將由Adobe Experience Platform檔案團隊核准或編輯。

1. 在GitHub Desktop中，為您的更新建立工作分支，然後選取 **發佈分支** 將分支發佈至GitHub。

![新增本地分支](../assets/docs-framework/new-branch-local.gif)

1. 在GitHub Desktop中， [認可](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) 您的工作，如下所示。

   ![提交本機](../assets/docs-framework/commit-local.png)

1. 在GitHub Desktop中， [推播](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) 將您的工作移至 [遠端](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) 分支，如下所示。

   ![推送您的認可](../assets/docs-framework/push-local-to-remote.png)

1. 在GitHub網頁介面中，開啟提取請求(PR)，將您的工作分支合併至Adobe檔案存放庫的主分支。 確定已選取並選取您處理的分支 **Contribute >開啟提取請求**.

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
