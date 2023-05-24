---
keywords: Experience Platform；首頁；熱門主題；分段；分段；區段服務；區段；多實體；多實體分段；多實體區段；
solution: Experience Platform
title: 多實體區段概觀
description: 多實體區段能根據產品、商店或其他非設定檔類別，以其他資料擴充設定檔資料。 連線後，其他類別的資料將變得可用，就好像它們是設定檔結構描述的原生資料。
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 多實體區段概觀

多實體區段是Adobe Experience Platform提供的進階功能 [!DNL Segmentation Service]. 此功能可讓您擴充 [!DNL Real-Time Customer Profile] 包含貴組織可定義的其他「非人物」資料（也稱為「維度實體」）的資料，例如與產品或商店相關的資料。 根據與您獨特業務需求相關的資料來定義受眾區段時，多實體細分可提供靈活性，並且無需具備查詢資料庫的專業知識即可執行。 透過多實體分段，您可以將關鍵資料新增至區段，而無需對資料串流進行成本高昂的變更，或等待後端資料合併。

## 快速入门

多實體區段需要深入瞭解區段所涉及的各種Adobe Experience Platform服務。 在繼續使用本指南之前，請先檢閱下列檔案：

* [[!DNL Real-Time Customer Profile]](../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的消費者設定檔。
   * [輪廓護欄](../profile/guardrails.md)：建立受支援之資料模型的最佳實務 [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md)：可讓您從建立區段 [!DNL Real-Time Customer Profile] 資料。
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../xdm/schema/composition.md#union)：瞭解撰寫要在Experience Platform中使用的結構描述的最佳實務。 為了充分利用「分段」，請確保您的資料已根據 [資料模型化的最佳實務](../xdm/schema/best-practices.md).

## 用例

為了說明多實體分段的價值，請考慮三個標準行銷使用案例，說明大多數行銷應用程式中存在的挑戰：

### 結合線上和離線購買資料

建立電子郵件行銷活動的行銷人員可能曾嘗試使用最近三個月內客戶商店的購買次數，為目標對象建立區段。 理想情況下，此區段會同時要求專案名稱和進行購買的商店名稱。 以前，難題是從購買事件中擷取商店識別碼，並將其指派給個別客戶設定檔。

### 針對購物車放棄重新定位電子郵件

建立使用者，並將其授與使用者以放棄為目標之區段的資格，通常較為複雜。 若要瞭解個人化重新鎖定目標行銷活動中要包含哪些產品，需要關於每個個人已放棄哪些產品的資料。 此資料與商業事件相連結，而這類事件過去在監控和擷取資料方面富有挑戰性。

## 建立多實體區段

建立多實體區段必須先定義結構描述之間的關係，才能使用 [!DNL Segmentation] API或區段產生器UI來建立區段定義。

### 定義關係

在體驗資料模型(XDM)結構描述的結構中定義關係，是建立多實體區段不可或缺的一部分。 對於關係，目的地中的欄位需要標示為該結構描述的主要身分。 身分只能標示在字串上，而不能標示在陣列上。 此外，關係不一定需要一對一，因為您可以將設定檔和體驗事件連線到多個目的地。

定義關係可以使用結構描述登入API或結構描述編輯器完成。 如需說明如何定義兩個結構描述之間關係的詳細步驟，請從下列教學課程中選擇：

* [使用API定義兩個結構描述之間的關係](../xdm/tutorials/relationship-api.md)
* [使用結構描述編輯器UI定義兩個結構描述之間的關係](../xdm/tutorials/relationship-ui.md)

### 建立多實體區段

定義必要的XDM關係後，您就可以開始建立多實體區段。 您可以使用分段API或區段產生器UI完成此操作。 如需詳細資訊，請從下列指南中選擇：

* [使用分段API建立區段](./tutorials/create-a-segment.md)
* [使用區段產生器UI建立區段](./ui/overview.md)

## 評估及存取多實體區段

建立區段後，您可以使用分段API來評估及存取區段結果。 評估多實體區段與評估標準區段非常類似。 此程式只能使用分段API完成。 如需有關如何使用API來評估和存取區段的詳細指南，請參閱 [評估及存取區段](./tutorials/evaluate-a-segment.md) 教學課程。
