---
keywords: Experience Platform；首頁；熱門主題；沙箱開發人員指南
solution: Experience Platform
title: 開始使用Sandbox API
description: 沙箱API可讓開發人員以程式設計方式管理Adobe Experience Platform中的沙箱。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 5%

---

# 開始使用Sandbox API

Adobe Experience Platform中的沙箱提供獨立的開發環境，可讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產環境。

本開發人員指南提供步驟，協助您使用沙箱API管理Experience Platform中的沙箱，並包含執行各種操作的範例API呼叫。

## 先决条件

若要管理貴組織的沙箱，您必須擁有沙箱管理許可權。 沒有存取許可權的使用者只能使用 [可用的沙箱端點](./available.md) 以列出目前使用者的作用中沙箱。 請參閱 [存取控制總覽](../../access-control/home.md) 有關如何為Experience Platform指派沙箱許可權的詳細資訊。

### 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

### 收集必要標題的值

本指南會要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 才能成功呼叫平台API。 完成驗證教學課程後，會提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* 授權：持有人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

除了驗證標頭之外，所有請求都需要標頭，用於指定將在其中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

包含裝載(POST、PUT和PATCH)的所有請求都需要額外的標頭：

* Content-Type： application/json

## 后续步骤

現在您已收集到所需的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供有關其端點的重要資訊，並示範用於執行CRUD操作的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式化的裝載的範例請求以及成功呼叫的範例回應。
