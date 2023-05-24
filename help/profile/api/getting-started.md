---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: Real-Time Customer Profile API快速入門
type: Documentation
description: 設定檔API快速入門手冊概述您使用即時客戶設定檔API端點對設定檔資料執行基本CRUD操作所需瞭解的關鍵概念和基本功能。
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 開始使用 [!DNL Real-Time Customer Profile] API {#getting-started}

使用即時客戶設定檔API端點，您可以對設定檔資料執行基本CRUD操作，例如設定計算屬性、存取實體、匯出設定檔資料，以及刪除不需要的資料集或批次。

使用開發人員指南需要實際瞭解使用時涉及的各種Adobe Experience Platform服務 [!DNL Profile] 資料。 開始使用之前 [!DNL Real-Time Customer Profile] API，請檢閱以下服務的檔案：

* [[!DNL Real-Time Customer Profile]](../home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶設定檔。
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md)：透過跨裝置和系統橋接身分，讓您更清楚瞭解客戶及其行為。
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md)：可讓您從即時客戶個人檔案資料建立受眾區段。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：Platform組織客戶體驗資料的標準化架構。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需瞭解的其他資訊，才能成功對進行呼叫 [!DNL Profile] API端點。

## 讀取範例API呼叫

此 [!DNL Real-Time Customer Profile] API檔案提供API呼叫範例，示範如何正確格式化請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 必要的標頭

API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程後，會提供中每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 以下專案的請求： [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

要求內文中具有裝載的所有要求(例如POST、PUT和PATCH呼叫)必須包含 `Content-Type` 標頭。 呼叫引數中會提供每個呼叫專屬的接受值。

## 后续步骤

若要開始使用進行呼叫 [!DNL Real-Time Customer Profile] API中，選取其中一個可用的端點參考線。
