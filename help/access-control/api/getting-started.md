---
keywords: Experience Platform；首頁；熱門主題；存取控制；api；快速入門
solution: Experience Platform
title: Access Control API指南
description: Adobe Experience Platform中的存取控制可讓您使用Adobe Admin Console管理各種Platform功能的角色和許可權。 以下章節提供開發人員成功呼叫Schema Registry API所需的其他資訊。
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---

# [!DNL Access Control] API指南

[!DNL Access control] 的 [!DNL Experience Platform] 是透過 [Adobe Admin Console](https://adminconsole.adobe.com). 此功能運用Admin Console中的產品設定檔，將使用者與許可權和沙箱連結。 請參閱 [存取控制總覽](../home.md) 以取得詳細資訊。

本開發人員指南提供如何格式化您向以下網址提出的請求的資訊： [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)，並涵蓋下列作業：

- [許可權和資源型別的清單名稱](./permissions-and-resource-types.md)
- [檢視目前使用者的有效存取原則](./effective-policies.md)

## 快速入门

以下小節提供您需瞭解的其他資訊，才能成功對 [!DNL Access Control] API。

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

## 后续步骤

現在您已收集到所需的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供有關其端點的重要資訊，並示範用於執行CRUD操作的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式化的裝載的範例請求以及成功呼叫的範例回應。
