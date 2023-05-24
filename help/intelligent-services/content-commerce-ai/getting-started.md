---
keywords: Experience Platform；快速入門；內容；內容標籤
solution: Experience Platform
title: 內容標籤快速入門
description: 內容標籤會利用Adobe I/OAPI。 若要呼叫Adobe I/O API和I/O主控台整合，您必須先完成驗證教學課程。
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# 內容標籤快速入門

[!DNL Content tagging] 會利用Adobe I/O API。 若要呼叫Adobe I/O API和I/O主控台整合，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en).

不過，當您前往 **新增API** 步驟，API位於Creative Cloud下而非Adobe Experience Platform，如下列熒幕擷圖所示：

![新增內容標籤](./images/add-api-updated.png)

完成驗證教學課程後，會提供所有Adobe I/OAPI呼叫中每個必要標題的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## 建立Postman環境（選用）

在Adobe Developer主控台中設定專案和API後，您就可以選擇下載Postman的環境檔案。 下 **[!UICONTROL API]** 在專案的左側邊欄中，選取 **[!UICONTROL 內容標籤]**. 隨即開啟新標籤，內含標示為「[!DNL Try it out]「。 選取 **Postman專用下載** 以下載用來設定Postman環境的JSON檔案。

![郵遞員專用下載](./images/add-to-postman-updated.png)

下載檔案後，請開啟Postman並選取 **齒輪圖示** 以開啟 **管理環境** 對話方塊。

![齒輪圖示](./images/select-gear-icon.png)

接下來，選取 **匯入** 從 **管理環境** 對話方塊。

![匯入](./images/import-updated.png)

系統會將您重新導向，並要求您從電腦中選取環境檔案。 選取您先前下載的JSON檔案，然後選取 **開啟** 以載入環境。

![](./images/choose-your-file.png)

![](./images/click-open.png)

系統會將您重新導向回 *管理環境* 索引標籤中填入新環境名稱。 選取環境名稱，以檢視和編輯Postman中可用的變數。 您仍需手動填入 `JWT_TOKEN` 和 `ACCESS_TOKEN`. 這些值應在完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct-updated.png)

完成後，您的變數看起來應該類似下面的熒幕擷圖。 選取 **更新** 以完成環境設定。

![](./images/final-environment-updated.png)

您現在可以從右上角的下拉式選單中選取環境，並自動填入任何儲存的值。 您隨時只需重新編輯值，即可更新所有API呼叫。

![範例](./images/select-environment-updated.png)

如需使用Postman處理Adobe I/O API的詳細資訊，請參閱以下媒體文章： [在Adobe I/O上使用Postman進行JWT驗證](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md) 在Experience Platform疑難排解指南中。

## 后续步骤 {#next-steps}

取得所有認證後，您就可以為設定自訂背景工作 [!DNL Content tagging]. 下列檔案可協助您瞭解「擴充性架構」和環境設定。

若要進一步瞭解擴充性架構，請閱讀 [擴充性簡介](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) 檔案。 本檔案概述先決條件和布建需求。

若要進一步瞭解如何設定環境 [!DNL Content tagging]，請先閱讀以下專案的指南 [設定開發人員環境](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). 本檔案提供可讓您為Asset compute服務開發的設定指示。
