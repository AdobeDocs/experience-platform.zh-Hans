---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
solution: Experience Platform
title: 自助來源快速入門(Batch SDK)
description: 本檔案會介紹在嘗試使用自助式來源（批次SDK）建立新來源之前，需要知道的先決條件資訊。
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 2a5d545db18a5dd33c5ff2ac5c543ec35db4ca00
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# 自助來源快速入門(Batch SDK)

自助來源（批次SDK）可讓您整合自己的REST型來源，以將批次資料帶入Adobe Experience Platform。 本檔案會介紹您在嘗試呼叫「 」之前需要瞭解的核心概念。 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## 先决条件

若要使用自助式來源（批次SDK），您必須確保您有權存取以Adobe Experience Platform來源布建的組織沙箱。

本指南也需要深入瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 讀取範例API呼叫

自助來源（批次SDK）和 [!DNL Flow Service] API檔案提供範例API呼叫，示範如何格式化請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

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

若要開始使用自助來源（批次SDK）建立新來源，請參閱以下主題上的教學課程： [建立新來源](./create.md).
