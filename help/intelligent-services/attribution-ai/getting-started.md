---
keywords: Experience Platform；快速入門；attribution ai；熱門主題
feature: Attribution AI
title: Attribution AI快速入門
description: 下列指南需要您瞭解使用Attribution AI時所需的各種Adobe Experience Platform服務。 開始教學課程之前，請先檢閱下列檔案。
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Attribution AI快速入門

以下指南需要瞭解各種 [!DNL Adobe Experience Platform] 與使用Attribution AI有關的服務。 開始教學課程前，請先檢閱下列檔案：

- [Experience Data Model (XDM)系統概覽](../../xdm/home.md)： XDM是基礎架構，可讓 [!DNL Adobe Experience Cloud]由Experience Platform提供技術支援，可在正確的時間透過正確的頻道將正確的訊息傳送給正確的人。 建立Experience Platform所根據的方法XDM系統可將Experience Data Model結構描述可操作化，以供Platform服務使用。
- [結構描述組合基本概念](../../xdm/schema/composition.md)：本檔案介紹Experience Data Model (XDM)結構描述，以及構成要用於下列專案之結構描述的組成要素、原則和最佳實務 [!DNL Adobe Experience Platform].
- [建立結構描述](../../xdm/tutorials/create-schema-ui.md)：本教學課程涵蓋在Experience Platform中使用「結構編輯器」建立結構的步驟。

Attribution AI需要資料集符合消費者體驗事件(CEE)結構描述，也就是 [體驗資料模型(XDM)](../../xdm/home.md) 結構描述欄位群組。 請透過attributionai-support@adobe.com聯絡Adobe支援，以實作或變更此資料。 如果存在媒體支出資料，您可以執行進一步分析，例如增量收入和ROI。 如果客戶設定檔資料可供使用，您就可以進一步將銷退折讓歸因於客戶設定檔層次。

## 术语

- **轉換事件：** 客戶為指示達成目標的里程碑而執行的任何數位事件或數位互動，例如會議註冊。 其他範例包括付費轉換、免費帳戶註冊或符合特徵資格。

- **接觸點：** 客戶在達成目標的過程中進行的任何數位活動或數位互動。 範例包括購買前相關的行銷工作、顯示的廣告曝光次數已檢視，以及付費搜尋點選。

## 下載Attribution AI分數

>[!NOTE]
>
>如果您不需要下載原始分數，您可以略過此步驟，繼續進行 [後續步驟](#next-steps).

下載Attribution AI分數是透過API呼叫的組合完成。 若要對Platform API發出呼叫，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

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

## 访问控制 {#access-control}

使用角色型存取控制時， **檢視Attribution AI** 和 **管理Attribution AI** 許可權可授予對Attribution AI不同功能的存取權。 此 **管理Attribution AI** 可讓您 **建立**， **原地複製**， **編輯**， **刪除**， **啟用**，或 **disable** 執行個體，但 **檢視Attribution AI** 可讓您 **讀取** 或 **檢視** it. 此 **建立**， **編輯** 和 **刪除** 動作由稽核記錄檔記錄。

請參閱檔案以瞭解 [指派存取控制的許可權](../../../help/access-control/home.md) 或如何 [使用稽核記錄來監視存取和活動](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## 后续步骤 {#next-steps}

準備好並準備好所有認證和結構描述後，請遵循以下步驟開始 [Attribution AI使用者介面指南](./user-guide.md). 本指南會逐步引導您建立執行個體，並提交它以進行訓練和評分。
