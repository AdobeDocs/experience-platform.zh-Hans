---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢
solution: Experience Platform
title: 查詢服務API指南
description: 查詢服務API可讓開發人員使用標準SQL查詢其Adobe Experience Platform資料。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# [!DNL Query Service] API指南

本開發人員指南提供在Adobe Experience Platform中執行各種操作的步驟 [!DNL Query Service] API。

## 快速入门

本指南需要您實際瞭解使用的各種Adobe Experience Platform服務 [!DNL Query Service].

- [[!DNL Query Service]](../home.md)：提供查詢資料集並將產生的查詢擷取為新資料集的能力 [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功使用所需的其他資訊 [!DNL Query Service] 使用API。

### 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需本檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Experience Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Platform] API呼叫，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，指定將執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在中使用沙箱的詳細資訊 [!DNL Experience Platform]，請參閱 [沙箱概觀檔案](../../sandboxes/home.md).

## API呼叫範例

現在您已瞭解要使用哪些標頭，可以開始對 [!DNL Query Service] API。 以下檔案會逐步說明您可以使用進行的各種API呼叫。 [!DNL Query Service] API。 每個呼叫範例都包含一般API格式、顯示必要標題的範例要求以及範例回應。

- [查询](queries.md)
- [連線引數](connection-parameters.md)
- [排定的查詢](scheduled-queries.md)
- [針對排定的查詢執行](runs-scheduled-queries.md)
- [查詢範本](query-templates.md)
- [加速的查詢](./accelerated-queries.md)
- [警報訂閱](./alert-subscriptions.md)

## 后续步骤

現在您已瞭解如何使用 [!DNL Query Service] API，您可以建立自己的非互動式查詢。 如需如何建立查詢的詳細資訊，請參閱 [SQL參考指南](../sql/overview.md).
