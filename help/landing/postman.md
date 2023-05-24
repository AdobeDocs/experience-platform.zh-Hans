---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform；api指南；平台api指南；平台簡介；開發人員指南
solution: Experience Platform
title: Adobe Experience Platform中的Postman
description: 本檔案包含概述如何設定Postman環境、匯入Postman集合的步驟，以及每個Platform服務的可用集合清單。
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Adobe Experience Platform中的Postman

Postman是API開發的共同作業平台，可讓您使用預設變數設定環境、共用API集合、簡化CRUD請求等。 大部分的Platform API服務都有Postman集合，可用來協助進行API呼叫。

## 如何設定Postman環境以進行Experience Platform

以下影片指南會概述如何建立和設定您的Postman環境。 Postman環境包含您需要對下面提供的各種集合進行API呼叫的所有必要標頭。 設定後，值隨時過期(例如 `ACCESS_TOKEN`)您可以更新環境中的目前值，此新值會用於所有集合。

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman集合 {#collections}

若要找到包含所有可用Postman集合的資料夾，請造訪 [Experience PlatformPostman範例GitHub存放庫](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). 或者，您也可以在的每個個別swagger檔案中找到Postman集合連結： [API參考檔案](https://www.adobe.com/go/platform-api-reference-en) 在Adobe I/O上。

若要下載Postman集合，請選取「 」 **[!DNL Raw]** 從GitHub頁面，在新索引標籤中載入原始JSON檔案。 然後，按一下滑鼠右鍵並選取 **[!DNL Save as]** 以將檔案儲存至您選擇的本機目的地。

![原始JSON](./images/api-guide/raw-collection.PNG)

## 匯入Postman集合 {#import}

為了利用 [Postman集合](#collections)，您必須設定環境。 完成環境設定後，請選取 **[!DNL Manage Environments]** 右上角的選取器。

![管理環境選擇器](./images/api-guide/environment-selector.png)

彈出視窗隨即出現，並顯示您所有目前的環境。 若要匯入集合，請選取 **[!DNL import]** .

![匯入按鈕](./images/api-guide/import-collection.png)

系統會要求您選擇要匯入的檔案。 選取您要匯入的Postman集合檔案。 選取後，集合會填入左側邊欄中的「集合」標籤下。

![填入的集合](./images/api-guide/imported-collection.png)

每個集合都有不同的索引鍵/值組，這些索引鍵/值組可能需要用來執行成功的CRUD操作。 請檢閱服務的 [API開發人員指南](api-guide.md#api-guides) 以瞭解必要的值、秘訣並參閱範例。

若要進一步瞭解Postman UI及其可用功能，請造訪 [Postman檔案](https://learning.postman.com/docs/getting-started/navigating-postman/).

### 使用Postman產生存取權杖以用於非生產用途

>[!WARNING]
>
>如Identity Management Service (IMS) Postman集合中所述，所代表的產生方法適用於 **非生產使用**. 本機簽署會從協力廠商主機載入JavaScript程式庫，而遠端簽署會將私密金鑰傳送至Adobe所擁有和操作的Web服務。 雖然Adobe不會儲存此私密金鑰，但生產金鑰絕不可與任何人共用。

以下影片使用 [Identity Management服務(IMS) Postman集合](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) 可從公共GitHub存放庫下載。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## 后续步骤

本檔案介紹Postman環境、集合以及如何匯入集合。 Postman準備就緒後，請前往 [Platform快速入門手冊](api-guide.md) 以取得必要標題、範例和清單的相關資訊 [API指南](api-guide.md#api-guides) 適用於各平台服務。
