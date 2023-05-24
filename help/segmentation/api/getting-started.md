---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；API；
solution: Experience Platform
title: Segmentation Service API快速入門
description: 下列檔案提供成功使用分段API所需瞭解的其他資訊。
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 1%

---

# Segmentation Service API快速入門 {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] 可讓您在Adobe Experience Platform中建立區段，並從以下來源產生對象： [!DNL Real-Time Customer Profile] 資料。

開發人員指南需要深入瞭解各種 [!DNL Experience Platform] 使用時涉及的服務 [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md)：可讓您從以下專案建立受眾區段： [!DNL Real-Time Customer Profile] 資料。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。 為了充分利用「分段」，請確保您的資料已根據 [資料模型化的最佳實務](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需瞭解的其他資訊，才能成功使用 [!DNL Segmentation] API。

## 讀取範例API呼叫

此 [!DNL Segmentation Service] API檔案提供範例API呼叫，示範如何格式化請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 必要的標頭

API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫 [!DNL Platform] 端點。 完成驗證教學課程後，會提供中每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，指定將執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在中使用沙箱的詳細資訊 [!DNL Experience Platform]，請參閱 [沙箱概觀檔案](../../sandboxes/home.md).

## 后续步骤

使用進行呼叫 [!DNL Segmentation Service] API中，使用左側導覽或在 [開發人員指南概觀](./overview.md)
