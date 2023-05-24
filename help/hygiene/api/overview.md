---
title: 資料衛生API指南
description: 瞭解如何以程式設計方式修正或刪除客戶在Adobe Experience Platform中儲存的個人資料。
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: da8b5d9fffdf8a176a4d70be5df5b3021cf0df7b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 資料衛生API指南

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料檢疫功能目前僅適用於已購買的組織 **AdobeHealthcare Shield** 或 **Adobe隱私權與安全性盾牌**.

資料衛生API可讓您以程式設計方式更正或刪除客戶在Adobe Experience Platform中儲存的個人資料，以及排程資料集的到期日。 本指南涵蓋使用API的先決條件步驟，並提供更多端點特定檔案的連結。

## 快速入门

您可以透過下列根路徑存取資料衛生API： `https://platform.adobe.io/data/core/hygiene/`

以下各節會概述您在嘗試呼叫API之前需要瞭解的核心概念。

### 收集必要標題的值

若要呼叫資料衛生API，您必須先收集驗證認證。 請遵循 [API驗證指南](../../landing/api-authentication.md) 為資料衛生API的每個必要標題產生值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

* `Content-Type: application/json`

### 讀取範例API呼叫

本檔案提供範例API呼叫，示範如何格式化您的請求。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/api-guide.md#sample-api) (位於Experience PlatformAPI快速入門手冊中)。

## 資料集有效期

資料集到期是時間延遲的「刪除資料集」動作。 透過建立資料集有效期，您就能指定該資料集的未來刪除時間。 請參閱 [資料集到期端點指南](./dataset-expiration.md) 以取得在API中排程資料集有效期的詳細資訊。

## 記錄刪除

>[!IMPORTANT]
>
>記錄刪除請求僅適用於已購買的組織 **AdobeHealthcare Shield**.
>
>
>記錄刪除旨在用於資料清理、匿名資料移除或資料最小化。 它們是 **not** 根據一般資料保護規範(GDPR)等隱私權法規用於資料主體權利請求（法規遵循）。 對於所有合規性使用案例，請使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 而非。

資料衛生API可讓您在一個或所有資料集中刪除與身分相關的所有記錄。 刪除身分的所有資料檢疫任務都會由稱為工單的建構表示。 請參閱 [工單端點指南](./workorder.md) 以取得在API中使用記錄刪除的詳細資訊。

## 配額

您的組織受限於每種資料衛生操作的預定每月工作配額，這可能因授權而異。 請參閱 [配額端點指南](./quota.md) 以取得檢視資料檢疫程式目前配額狀態的詳細資訊。

## 后续步骤

本指南說明如何使用API呼叫管理資料檢疫請求。 如需如何在Platform UI中執行這些動作的詳細資訊，請參閱 [資料衛生UI指南](../ui/overview.md).
