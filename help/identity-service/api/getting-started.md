---
keywords: Experience Platform；首頁；熱門主題；identity service api；identity service開發人員指南；地區
solution: Experience Platform
title: Identity Service API指南
description: Identity Service API可讓開發人員使用Adobe Experience Platform中的身分圖表，管理跨裝置、跨頻道及幾乎即時的客戶身分識別。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# [!DNL Identity Service] API指南

Adobe Experience Platform [!DNL Identity Service] 在Adobe Experience Platform中透過稱為身分圖表的方式管理跨裝置、跨頻道及幾乎即時的客戶身分識別。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Identity Service]](../home.md)：解決客戶設定檔資料片段化帶來的基本挑戰。 其做法是跨客戶與您品牌互動的裝置和系統橋接身分。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的消費者設定檔。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。

以下小節提供您需瞭解或掌握的其他資訊，才能成功呼叫 [!DNL Identity Service] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

- Content-Type： application/json

### 以區域為基準的製程

此 [!DNL Identity Service] API採用特定於區域的端點，這些端點需要包含 `{REGION}` 作為請求路徑的一部分。 在布建您的組織期間，會確定一個區域並將其儲存在您的組織設定檔中。 對每個端點使用正確的區域，可確保使用 [!DNL Identity Service] API會路由至適當的區域。

目前有兩個區域受到支援 [!DNL Identity Service] API： VA7和NLD2。

下表顯示使用區域的範例路徑：

| 服务 | 地區： VA7 | 地區： NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>在未指定區域的情況下進行要求，可能會導致呼叫路由傳送到不正確的區域，或造成呼叫意外失敗。

如果您在組織設定檔中找不到該地區，請聯絡您的系統管理員以尋求支援。

## 使用 [!DNL Identity Service] API

這些服務中使用的身分引數可以用兩種方式之一表示：複合或XID。

複合身分是包含ID值和名稱空間的建構。 使用複合身分時，名稱空間可由任一名稱提供(`namespace.code`)或ID (`namespace.id`)。

當身分持續存在時， [!DNL Identity Service] 會產生一個ID並指派給該身分，稱為原生ID或XID。 Cluster和Mapping API的所有變數在其請求和回應中支援複合身分和XID。 需要其中一個引數 —  `xid` 或以下專案的組合 [`ns` 或 `nsid`] 和 `id` 以使用這些API。

為了限制回應中的裝載，API會調整其回應，以符合所使用的身分建構型別。 也就是說，如果您傳遞XID，您的回應將具有XID，如果您傳遞複合身分，回應將遵循請求中使用的結構。

本檔案中的範例不涵蓋 [!DNL Identity Service] API。 如需完整的API，請參閱 [Swagger API參考](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>當請求中使用原生XID時，所有傳回的身分都將採用原生XID格式。 建議使用ID/名稱空間表單。 如需詳細資訊，請參閱以下章節： [取得身分的XID](./create-custom-namespace.md).

## 后续步骤

現在您已收集到所需的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供有關其端點的重要資訊，並示範用於執行CRUD操作的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式化的裝載的範例請求以及成功呼叫的範例回應。
