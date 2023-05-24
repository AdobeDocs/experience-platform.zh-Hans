---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 開始使用資料擷取API
type: Documentation
description: Data Ingestion API快速入門手冊概述關鍵概念，以及開始使用API將資料擷取到Experience Platform之前需要瞭解的基本功能。
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 開始使用資料擷取API {#getting-started}

使用資料擷取API端點，您可以執行基本CRUD操作，以便在Adobe Experience Platform中擷取資料。

使用API指南需要實際瞭解與資料處理有關的多個Adobe Experience Platform服務。 在使用資料擷取API之前，請檢閱以下服務的檔案：

* [批次擷取](./overview.md)：可讓您將資料以批次檔案的形式內嵌至Adobe Experience Platform。
* [[!DNL Real-Time Customer Profile]](../home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：Platform組織客戶體驗資料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需瞭解的其他資訊，才能成功對進行呼叫 [!DNL Profile] API端點。

## 讀取範例API呼叫

資料擷取API檔案提供範例API呼叫，示範如何正確格式化請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 必要的標頭

API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程後，會提供中每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

要求內文中具有裝載的所有要求(例如POST、PUT和PATCH呼叫)必須包含 `Content-Type` 標頭。 呼叫引數中會提供每個呼叫專屬的接受值。

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 以下專案的請求： [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).
