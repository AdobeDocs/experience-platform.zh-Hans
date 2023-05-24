---
keywords: Experience Platform；首頁；熱門主題；細分；區段；區段服務；區段；區段；區段
solution: Experience Platform
title: Segmentation Service概述
description: 瞭解Adobe Experience Platform Segmentation Service及其在平台生態系統中所扮演的角色。
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 11%

---

# [!DNL Segmentation Service] 概述

Adobe Experience Platform [!DNL Segmentation Service] 提供使用者介面和RESTful API，可讓您建立區段並從 [!DNL Real-Time Customer Profile] 資料。 這些區段會集中設定並維護於 [!DNL Platform]和可供任何Adobe解決方案輕鬆存取。

本檔案提供下列專案的概觀： [!DNL Segmentation Service] 以及在Adobe Experience Platform中扮演的角色。

## 開始使用 [!DNL Segmentation Service]

請務必瞭解本檔案中使用的下列重要術語：

- **細分**：將大量個人（例如客戶、潛在客戶、使用者或組織）劃分為具有類似特徵且對行銷策略有類似回應的較小群組。
- **區段定義**：用來描述目標對象之關鍵特性或行為的規則集。 概念化後，區段定義中概述的規則可用於判斷區段的合格受眾成員。
- **對象**：符合區段定義條件的結果設定檔集。

## 區段的運作方式

區段是定義個人資料存放區中個人資料子集所共用的特定屬性或行為的程式，以區分可行銷人群和您的客戶群。 例如，在名為「您忘記買運動鞋了嗎？」的電子郵件行銷活動中，您可能想要一個受眾，其中包含過去30天內搜尋跑鞋但未完成購買的所有使用者。

在概念上定義區段後，即會在內建該區段 [!DNL Experience Platform]. 一般而言，區段是由行銷人員或對象專家建立，不過有些組織偏好由行銷部門與資料分析師合作建立。 檢閱傳送至的資料時 [!DNL Platform]時，資料分析人員會選取用來建立區段規則或條件的欄位和值，以撰寫區段定義。 這是使用UI或API來完成。

## 创建区段

無論是使用API建立，還是使用 [!DNL Segment Builder]，區段最終可透過以下方式定義： [!DNL Profile Query Language] (PQL)。 這是以建立用來擷取符合條件的設定檔的語言描述概念區段定義的地方。 如需詳細資訊，請參閱 [PQL概述](./pql/overview.md).

若要瞭解如何在中建立和使用區段 [!DNL Segment Builder] (的UI實作 [!DNL Segmentation Service])，請參閱 [區段產生器指南](./ui/overview.md).

如需使用API建立區段定義的詳細資訊，請參閱以下教學課程： [使用API建立受眾區段](./tutorials/create-a-segment.md).

>[!NOTE]
>
>如果擴充了結構描述，所有未來上傳都必須相應地更新新新增的欄位。 如需自訂的詳細資訊 [!DNL Experience Data Model] (XDM)，造訪 [結構描述編輯器教學課程](../xdm/tutorials/create-schema-ui.md).
>
>此外，如果資料集已啟用體驗事件到期值，這可能會影響已建立區段的成員資格。 請閱讀指南： [體驗事件有效期](../profile/event-expirations.md) 瞭解此功能如何影響區段的詳細資訊。

## 評估區段 {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="评估方法"
>abstract="Platform 目前支持三种区段评估方法：流式分段、批量分段和边缘分段。"

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="流式评估"
>abstract="流式分段是一个持续的数据选择过程，它会更新区段以响应用户活动。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=zh-Hans" text="通过流式分段近乎实时地评估事件"

Platform 目前支持三种区段评估方法：流式分段、批量分段和边缘分段。

### 串流區段 {#streaming}

流式分段是一个持续的数据选择过程，它会更新区段以响应用户活动。建立並儲存區段後，區段定義會套用至傳入的資料 [!DNL Real-Time Customer Profile]. 會定期處理區段新增和移除，以確保您的目標對象仍然相關。

若要進一步瞭解串流細分，請閱讀 [串流細分檔案](./api/streaming-segmentation.md).

### 批次細分 {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="批量评估"
>abstract="作为持续数据选择过程的替代方案，批量分段通过区段定义一次性移动所有配置文件数据以产生相应的受众。创建后，区段将保存，以便您能够将其导出以供使用。"

作为持续数据选择过程的替代方案，批量分段通过区段定义一次性移动所有配置文件数据以产生相应的受众。建立後，會儲存並儲存此區段，以便您匯出以供使用。

每24小時自動評估批次區段。 若要依需求評估批次節段，您可以使用節段工單。 若要進一步瞭解區段工作，請閱讀 [區段作業檔案](./api/segment-jobs.md).

### 邊緣細分 {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="边缘评估"
>abstract="边缘分段能够在 Experience Edge 上即时评估 Platform 中的区段，从而实现同一页和下一页个性化用例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=zh-Hans" text="边缘分段 UI 指南"

邊緣區段是即時評估Platform中區段的能力 [在Experience Edge上](../edge/home.md)，啟用相同頁面和下一頁個人化使用案例。

若要進一步瞭解邊緣細分，請閱讀 [API檔案](./api/edge-segmentation.md) 或 [UI檔案](./ui/edge-segmentation.md).

## 存取區段結果

若要瞭解如何存取匯出的區段，請參閱 [區段評估教學課程](./tutorials/evaluate-a-segment.md).

## 區段中繼資料

區段中繼資料可在您的任何區段要重複使用和/或合併時協助建立索引。

構成區段(透過API或 [!DNL Segment Builder])需要您定義區段名稱和合併原則。

### 區段名稱

建立新區段時，您必須提供區段名稱。 區段名稱用於在建立的集合中識別特定區段 [!DNL Segmentation Service]. 因此，區段名稱應具描述性、簡潔且獨特。

>[!NOTE]
>
>規劃區段時，請記住，區段可從任何其他區段參照並與其結合。 選取名稱時，請考量您的區段可能包含可重複使用的部分。

### 合併原則

合併原則是以下人員使用的規則： [!DNL Profile] 以決定在特定條件下，如何將資料優先排序並合併到統一檢視中。
如果未定義合併原則，則預設值為 [!DNL Platform] 已使用合併原則。 若您想使用貴組織專屬的合併原則，您可以建立自己的原則，並將其標示為貴組織的預設值。

有關合併原則的更多資訊可在以下網址找到： [合併原則指南](../profile/api/merge-policies.md).

>[!NOTE]
>
>預估對象人數是根據組織的預設設定檔合併原則。

### 其他區段中繼資料

除了區段名稱和合併原則外， [!DNL Segment Builder] 為您提供額外的「區段說明」中繼資料欄位，您可以在其中摘要區段定義的用途。

## 進階分段功能

區段可設定為透過合併來持續產生對象 [串流資料擷取](../ingestion/streaming-ingestion/overview.md) 並具備下列任何進階分段功能：
- [循序分段](#sequential)
- [動態細分](#dynamic)
- [多實體分段](#multi-entity)

以下各節將更詳細地討論這些進階功能。

## 循序分段 {#sequential}

標準使用者歷程本質上為循序過程。 Adobe Experience Platform可讓您定義一系列有序的區段來反映此歷程，因此在事件發生時擷取事件順序。 您可以使用中的視覺事件時間軸，將事件依所需順序排列。 [!DNL Segment Builder].

需要循序細分的客戶歷程範例為產品檢視>產品新增>結帳>不購買。

## 動態細分 {#dynamic}

動態區段可解決行銷人員在建立行銷活動區段時，傳統上面臨的可擴充性問題。

靜態細分需要您明確且重複地擷取每個可能的使用案例，而動態細分則會使用變數來建立規則邏輯並動態地表示關係。

### 使用案例：尋找在本國以外地區進行購買的客戶

為了說明此進階細分功能的價值，請考慮讓資料架構師與行銷人員合作，識別在家庭狀態以外進行購買的客戶。

**問題**

靜態區段會要求您先以唯一的首頁狀態屬性定義個別區段，然後再篩選不等於首頁狀態的購買事件。 此型別的明確區段會顯示「我在尋找猶他州人，因為他們的購買狀態不是猶他州」。 使用此方法建立受眾時，需要您為美國各州定義一個區段，共50個區段。

隨著規模擴大，不可避免地會出現不同的區段組合，因此靜態區段所需的手動程式會變得更加耗時，進而降低您的整體效率。

**解決方案**

藉由將變數指派給購買狀態屬性，您的動態區段簡化為「尋找我的購買，其中該購買狀態不等於客戶的首頁狀態」。 如此一來，您就可以將50個靜態區段合併為單一動態區段。

## 多實體分段 {#multi-entity}

透過進階的多實體分段功能，您可以擴展 [!DNL Real-Time Customer Profile] 以產品、商店或其他非人員（也稱為「維度」實體）為依據而具備其他資料的資料。 因此， [!DNL Segmentation Service] 區段定義期間可以存取其他欄位，就好像這些欄位原本屬於 [!DNL Profile] 資料存放區。 根據與您獨特業務需求相關的資料，多實體細分在識別對象時可提供靈活性。 如需詳細資訊，包括使用案例和工作流程，請參閱 [多實體分段指南](multi-entity-segmentation.md).

## [!DNL Segmentation Service] 資料型別

[!DNL Segmentation Service] 支援各種基本和複雜的資料型別。 詳細資訊（包括支援的資料型別清單）可在以下網址找到： [支援的資料型別指南](./data-types.md).

## 后续步骤

[!DNL Segmentation Service] 提供整合的工作流程，以便從建立區段 [!DNL Real-Time Customer Profile] 資料。 摘要：

- [!DNL Segmentation] 是從您的設定檔存放區定義設定檔子集的程式，允許您表徵所需可銷售群組的行為或屬性。 [!DNL Segmentation Service] 讓此程式成為可能。
- 規劃區段時，請記住，可從任何其他區段參照區段並與之結合。
- 區段可從根據設定檔資料、相關時間序列資料或兩者的規則建立。
- 區段可依需求或持續評估。 依需求評估時，所有設定檔資料會一次透過區段定義傳遞。 持續評估時，資料會在進入時透過區段定義串流 [!DNL Platform].

若要瞭解如何在UI中定義區段，請參閱 [區段產生器指南](./ui/overview.md). 如需使用API建立區段定義的詳細資訊，請參閱以下教學課程： [使用API建立區段](./tutorials/create-a-segment.md).
