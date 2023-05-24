---
keywords: Experience Platform；首頁；熱門主題；屬性型存取控制；屬性型存取控制
title: 屬性式存取控制API快速入門
description: 屬性式存取控制API可讓您以程式設計方式管理Adobe Experience Platform中的角色和存取原則。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 54e15234d1b1050ea2cdb8b7d37c79a133a339f1
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 4%

---

# 屬性式存取控制API快速入門

本開發人員指南提供步驟，協助您使用屬性式存取控制API來管理Adobe Experience Platform中的角色、產品、許可權類別和許可權集，並包含執行各種作業的範例API呼叫。

## 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

## 收集必要標題的值

本指南會要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 才能成功呼叫平台API。 完成驗證教學課程後，會提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

除了驗證標頭之外，所有請求都需要標頭，用於指定將在其中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT和PATCH)的所有請求都需要額外的標頭：

* `Content-Type: application/json`

## 后续步骤

現在您已收集到所需的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供有關其端點的重要資訊，並示範用於執行CRUD操作的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式化的裝載的範例請求以及成功呼叫的範例回應。

請參閱下列API教學課程，以開始呼叫屬性型存取控制API：

* [角色端點](./roles.md)
* [產品端點](./products.md)
