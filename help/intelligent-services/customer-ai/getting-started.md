---
keywords: Experience Platform；快速入門；customer ai；熱門主題
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI快速入門
description: 本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Customer AI快速入門

Customer AI指南需要實際瞭解使用Customer AI的各種平台服務。 開始之前，請檢閱下列檔案：

- [Experience Data Model (XDM)系統概覽](../../xdm/home.md)： XDM是基礎架構，可讓 [!DNL Adobe Experience Cloud]由Experience Platform提供技術支援，可在正確的時間透過正確的頻道將正確的訊息傳送給正確的人。 建立Experience Platform所根據的方法XDM系統可將Experience Data Model結構描述可操作化，以供Platform服務使用。
- [結構描述組合基本概念](../../xdm/schema/composition.md)：本檔案介紹Experience Data Model (XDM)結構描述，以及構成要用於下列專案之結構描述的組成要素、原則和最佳實務 [!DNL Adobe Experience Platform].
- [建立結構描述](../../xdm/tutorials/create-schema-ui.md)：本教學課程涵蓋在Experience Platform中使用「結構編輯器」建立結構的步驟。
- [即時客戶個人檔案總覽](../../rtcdp/overview.md)：建置於 [!DNL Adobe Experience Platform]，Adobe Real-time Customer Data Platform (Real-Time CDP)可協助公司整合已知和未知的資料，透過客戶歷程中的智慧型決策來啟用客戶設定檔。 Real-Time CDP結合多個企業資料來源以即時建立統一的設定檔，其可用於跨所有管道和裝置提供一對一的個人化客戶體驗。
- [Segmentation Service概述](../../segmentation/home.md)：區段是定義個人資料存放區中個人資料子集所共用的特定屬性或行為的程式，以區分可行銷人群和您的客戶群。 例如，在名為「您忘記買運動鞋了嗎？」的電子郵件行銷活動中，您可能想要一個受眾，其中包含過去30天內搜尋跑鞋但未完成購買的所有使用者。 使用不同的區段，您可以專注於各種受眾，提供更自訂的行銷體驗。
- [區段產生器使用手冊](../../segmentation/tutorials/create-a-segment.md)：Platform可讓您輕鬆建立及存取區段，並使用不同的建置區塊來進一步表示區段特性。

## 下載Customer AI分數

>[!NOTE]
>
>如果您不需要下載原始分數，您可以略過此步驟，繼續進行 [設定指南](./user-guide/configure.md).

下載Customer AI分數是透過API呼叫的組合完成。 若要對Platform API發出呼叫，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Experience Platform中的所有資源都與特定的虛擬沙箱隔離。 對Platform API的所有請求都需要標頭，用於指定將在其中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需Platform中沙箱的詳細資訊，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

### 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md) 在Experience Platform疑難排解指南中。

## 后续步骤

完成上述檔案中概述的步驟後，請造訪 [輸入和輸出](./data-requirements.md) 說明檔案。 本檔案簡要概述在Customer AI中使用和產生的資料型別。
