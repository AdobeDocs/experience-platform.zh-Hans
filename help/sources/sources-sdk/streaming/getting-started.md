---
title: 自助式來源快速入門（串流SDK）
description: 本檔案會介紹嘗試使用自助來源（串流SDK）建立新來源之前，需要知道的先決條件資訊。
hide: true
hidefromtoc: true
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# 自助式來源快速入門（串流SDK）

自助來源（串流SDK）可讓您整合自己的來源，以將串流資料帶到Adobe Experience Platform。 本檔案會介紹您在嘗試呼叫「 」之前需要瞭解的核心概念。 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 高階流程

以Experience Platform設定來源的逐步流程概述如下：

### 集成

* [建立適用於串流SDK的新連線規格](create.md).
* [使用新的連線規格ID更新串流流程規格](update-flow-specs.md).
* [測試並提交您的串流來源](submit.md).

### 文档

* 若要開始記錄您的來源，請閱讀 [建立自助式來原始檔概覽](../documentation/doc-overview.md).
* 閱讀指南： [使用GitHub網頁介面](../documentation/github.md) 有關如何使用GitHub建立檔案的步驟。
* 閱讀指南： [使用文字編輯器](../documentation/text-editor.md) 有關如何使用本機電腦建立檔案的步驟。
* [使用串流SDK API檔案範本在API中記錄您的來源](streaming-template-api.md).
* [使用串流SDK UI檔案範本在UI中記錄您的來源](streaming-template-ui.md).

您也可以下載下列檔案範本：

* [api檔案範本](../assets/streaming/streaming-template-api.zip)
* [UI檔案範本](../assets/streaming/streaming-template-ui.zip)

## 先决条件

>[!IMPORTANT]
>
>您與Experience Platform整合的來源必須能夠支援端點可訂閱的webhook，才能傳送更新。

若要使用自助式來源（串流SDK），您必須確保您有權存取已布建Adobe Experience Platform來源的沙箱組織。

本指南也需要深入瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 讀取範例API呼叫

自助服務來源（串流SDK）和 [!DNL Flow Service] API檔案提供範例API呼叫，示範如何格式化請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

## 收集必要標題的值

若要對Platform API發出呼叫，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Platform中的所有資源，包括屬於 [!DNL Flow Service]，會隔離至特定的虛擬沙箱。 對Platform API的所有請求都需要標頭，用於指定將在其中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需Platform中沙箱的詳細資訊，請參閱 [沙箱檔案](../../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

* `Content-Type: application/json`

## 后续步骤

若要開始使用自助來源（串流SDK）建立新來源，請參閱以下主題上的教學課程： [建立新來源](./create.md).
