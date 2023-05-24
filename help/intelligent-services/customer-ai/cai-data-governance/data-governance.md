---
keywords: Experience Platform；資料控管；customer ai；熱門主題
solution: Experience Platform
feature: Customer AI
title: Customer AI中的資料控管
description: Adobe Experience Platform提供數種服務和工具，可讓您自信地控制所收集的體驗資料，以符合您的業務實務、法律義務和開發程式。
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: 0fcdb358882fba7f7923e5d6fc1a947699276e18
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 9%

---

# Customer AI和資料控管

Customer AI中的任何資料控管相關設定都是從Adobe Experience Platform繼承而來。

## 数据治理 {#governance}

Customer AI與Adobe Experience Platform資料控管之間的整合可讓您在資料流經平台的整個過程中控制並理解您的資料。 這涉及維護資料品質、資料譜系、資料編目等。

在Platform使用的資料集上建立的資料使用標籤和原則，可以在Customer AI設定工作流程中顯示。 這些標籤會阻止或警告使用已標籤欄位的使用者。

此整合可讓您更有效率地管理合規性。 组织中的数据管理员可以设置策略以限制使用。 因此，您可以使用符合資料監管員所定義原則的資料。 請閱讀以下檔案： [標籤和原則](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html) 以深入瞭解。

## 同意原則 {#consent-policy}

Customer AI會遵循您的同意偏好設定。 一旦您擁有 [設定並啟用您的同意原則](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=zh-Hans#consent-policy)，Customer AI會尊重向您收集的同意資料。 在模型的後續執行中，僅會使用同意的資料來評分模型。 新分數將取代舊分數，並可用於分段。 此功能目前僅適用於HealthCare Shield客戶以及Privacy and Security shield客戶。

您可以在這裡進一步瞭解此功能：

[Customer AI快速入門](../../customer-ai/getting-started.md)
[Adobe Experience Platform與應用程式](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)
[Adobe Experience Cloud架構圖](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html)
