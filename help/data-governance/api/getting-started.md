---
keywords: Experience Platform；首頁；熱門主題；DULE；dule
solution: Experience Platform
title: 原則服務API快速入門
description: 原則服務API可讓您建立和管理與Adobe Experience Platform資料控管相關的各種資源。 本檔案會介紹您在嘗試呼叫原則服務API之前需要瞭解的核心概念。
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 開始使用 [!DNL Policy Service] API

此 [!DNL Policy Service] API可讓您建立和管理與Adobe Experience Platform資料控管相關的各種資源。 本檔案會介紹您在嘗試呼叫「 」之前需要瞭解的核心概念。 [!DNL Policy Service] API。

## 先决条件

使用開發人員指南需要實際瞭解各種 [!DNL Experience Platform] 與資料控管功能搭配使用的服務。 開始使用之前 [!DNL Policy Service API]，請檢閱以下服務的檔案：

* [資料控管](../home.md)：作為依據的框架 [!DNL Experience Platform] 強制資料使用規範。
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

## 讀取範例API呼叫

此 [!DNL Policy Service] API檔案提供範例API呼叫，示範如何格式化請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 必要的標頭

API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程後，會提供中每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括屬於資料控管的那些，會隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

* `Content-Type: application/json`

## 核心與自訂資源

在內 [!DNL Policy Service] API，所有原則和行銷動作稱為 `core` 或 `custom` 資源。

`core` 資源是由Adobe定義及維護的資源，而 `custom` 資源是由您的組織建立和維護的資源，因此是唯一的並且僅對您的組織可見。 因此，列出和查詢作業(`GET`)是唯一允許對執行的操作 `core` 資源，而列出、查詢及更新作業(`POST`， `PUT`， `PATCH`、和 `DELETE`)可用於 `custom` 資源。

## 后续步骤

若要開始使用原則服務API進行呼叫，請選取其中一個可用的端點指南。
