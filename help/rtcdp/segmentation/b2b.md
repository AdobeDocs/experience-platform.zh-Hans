---
title: Real-time Customer Data Platform B2B版本的分段使用案例
description: 各種可用Adobe Real-time Customer Data Platform B2B版本使用案例的概觀。
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: b436aeb8a8628d9b481041be518c1113fb54c342
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B版本的分段使用案例

本檔案提供Adobe Real-time Customer Data Platform B2B Edition中的區段定義範例，並說明如何針對常見B2B使用案例來合併不同型別的屬性。 若要瞭解目的地如何適合您的B2B工作流程，請參閱 [端到端教學課程](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>這些細分使用案例所需的屬性僅供Real-time Customer Data Platform B2B Edition客戶使用。 如果您沒有使用Real-time Customer Data Platform B2B版本，請參閱 [區段概述](./segmentation-overview.md) 而非。

## 先决条件 {#prerequisites}

您必須先完成下列步驟，才能對B2B類別使用分段屬性：

1. 建立使用B2B類別的結構描述。 B2B版本類別包括Account、Campaign、Opportunity、Marketing List等。 有關以下專案的資訊： [如何設定與B2B類別一起使用的結構描述](../schemas/b2b.md) 請參閱結構描述檔案。
1. 在您的Experience Data Model (XDM) B2B結構描述之間建立關係。 以B2B版本屬性為基礎的區段需要類別之間的關係，才能完全使用擴充的B2B區段功能。 請參閱以下說明檔案： [如何定義兩個B2B結構描述之間的關係](../../xdm/tutorials/relationship-b2b.md) 以取得詳細資訊。
1. 使用根據您的B2B結構描述的資料集來擷取資料。 請參閱來原始檔，瞭解 [有關如何內嵌資料的資訊](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. 閱讀 [區段產生器使用手冊](../../segmentation/ui/segment-builder.md) 以取得如何建立區段的詳細指引。

滿足這些需求後，您就可以針對常見的B2B使用案例來組合這些屬性。

## 快速入门 {#getting-started}

一旦B2B類別的聯合結構描述建立關係並用於擷取資料後，其屬性即可在區段產生器的左側邊欄中使用。

B2B類別及其屬性會附加 `B2B` 區段工作區中的標籤，以區隔Real-time Customer Data Platform中的標準區段。

為了有效建立B2B使用案例的區段，請務必熟悉結構並瞭解資料模型外觀。 瞭解資料從一個資料物件前往另一個資料物件的路徑也很有用。

下圖說明Real-Time CDP B2B版本中可用的B2B類別之間的關係。

![B2B類別ERD](../assets/segmentation/b2b-classes.png)

由於您的資料模型可能很複雜，因此您可以使用Platform UI來檢視資料模型的更詳細視覺化表示法，以協助尋找使用案例的相關屬性。 若要開始，請前往Platform UI，然後在左側導覽中選取結構描述。

從可用清單中選取適當的結構描述，然後從 [!UICONTROL 組合] 側邊欄。 在以下範例中，選取「Person」關係會顯示目前結構描述中哪個屬性會參考相關的「Person」結構描述（如果它是關係中的來源結構描述），或被「Person」結構描述參考（如果它是關係中的參考結構描述）。

![來源金鑰在結構描述工作區中使用人員關係的範例](../assets/segmentation/source-key-schema-relationship-example.png)

此關係會透過使用的反映在區段產生器中 `Key` 資料夾，如下圖所示。

![在區段工作區中使用區段產生器的來源索引鍵範例](../assets/segmentation/source-key-segmentation-example.png)

請參閱 [Real-time Customer Data Platform B2B版本檔案中的結構描述](../schemas/b2b.md) 以取得可用B2B類別的詳細資訊。

以下使用案例提供相關資訊，說明使用哪些類別在不同結構描述之間建立關係來達成這些結果。 這些範例可用來協助您建立自己的區段。

## 不同區段使用案例的範例 {#use-cases}

下列使用案例可用於B2B版本的分段。 每個範例都會提供區段用途的描述，以及用來建立區段的類別描述。 提供的影像會反白顯示 [!UICONTROL 屬性] 反映結構描述的側邊欄。 此 [!UICONTROL 區段屬性] 右側區段包含區段屬性的書面劃分。

### 範例1：尋找B2B機會的「決策者」 {#find-decision-maker}

尋找任何機會的「決策者」所有人員。 此區段需要 [!UICONTROL XDM個別設定檔] 類別與 [!UICONTROL XDM商業機會個人關係] 類別。

![顯示範例1設定的UI](../assets/segmentation/example-1.png)

### 範例2：搜尋指定給超過特定金額之商機的B2B設定檔 {#find-opportunities-amount}

尋找直接指派給任何商機金額超過指定金額（100萬美元）之商機的所有人員。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商業機會個人關係] 類別，以及 [!UICONTROL XDM商業機會] 類別。

![顯示範例2設定的UI](../assets/segmentation/example-2.png)

### 範例3：依地點搜尋指定給商機的B2B設定檔 {#find-opportunities-location}

尋找直接指派給客戶位於指定位置（加拿大）之任何商機的所有人員。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商業機會個人關係] 類別， [!UICONTROL XDM商業機會] 類別，以及 [!UICONTROL XDM商業帳戶] 類別。

![顯示範例3設定的UI](../assets/segmentation/example-3.png)

### 範例4：依產業和瀏覽行為尋找商機的「決策者」 {#find-industry-browsing-behavior}

尋找客戶屬於「金融」產業的任何機會的「決策者」所有人員，並在過去三天中造訪定價頁面。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商業機會個人關係] 類別， [!UICONTROL XDM商業機會] 類別，以及 [!UICONTROL XDM商業帳戶] 類別，以及 [!UICONTROL XDM ExperienceEvent] 類別。

![顯示範例4設定的UI](../assets/segmentation/example-4.png)

### 範例5：依部門名稱與商機金額搜尋商機的B2B設定檔 {#find-department-opportunity-amount}

尋找在人力資源(HR)部門工作的所有人員，以及擁有至少一個與指定金額（100萬美元）或以上價值相符的未結機會的任何帳戶。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商業帳戶] 類別，以及 [!UICONTROL XDM商業機會] 類別。

![顯示範例5設定的UI](../assets/segmentation/example-5.png)

### 範例6：依職稱和年度帳戶收入搜尋B2B設定檔 {#find-by-job-title-and-revenue}

尋找所有職銜為「副總裁」且帳戶年收入達到或超過指定金額（1億美元）的人，並在上個月至少造訪定價頁面3次的人。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商業帳戶] 類別，以及 [!UICONTROL XDM ExperienceEvent] 類別。

![顯示範例6設定的UI](../assets/segmentation/example-6.png)

### 範例7：依機會狀態和瀏覽行為尋找「決策者」 {#find-by-opportunity-status-and-browsing-behavior}

尋找任何已結束但失去的機會的「決策者」所有人員，並在上週造訪定價頁面。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商業機會個人關係] 類別， [!UICONTROL XDM商業機會] 類別，以及 [!UICONTROL XDM ExperienceEvent] 類別。

![顯示範例7設定的UI](../assets/segmentation/example-7.png)

### 範例8：使用相關帳戶來擴大細分範圍 {#related-accounts}

尋找在人力資源(HR)部門工作且與任何帳戶相關的所有人員 *或任何帳戶的相關帳戶* 至少有一個價值等於或大於指定金額（100萬美元）的未完成機會。 此區段需要 [!UICONTROL XDM個別設定檔] 類別， [!UICONTROL XDM商業帳戶] 類別，以及 [!UICONTROL XDM商業機會] 類別。

![顯示相關帳戶區段的UI](../assets/segmentation/example-8.png)

### 範例9：使用潛在客戶分數和/或帳戶分數來限定個人檔案 {#account-scoring}

尋找潛在客戶分數超過80的所有設定檔。

![顯示預測性銷售線索和帳戶評分分段的UI](../assets/segmentation/example-9.png)

### 範例10：搜尋與帳戶相關聯的B2B設定檔，其父組織的收入超過特定美元金額 {#find-parent-org-amount}

尋找與上層組織的收入超過指定金額($100,000,000)的帳戶相關聯的所有人員。

![顯示細分父級組織的UI](../assets/segmentation/example-10.png)

### 範例11：依職稱與帳戶名稱搜尋具有有效關係的B2B設定檔 {#find-by-job-title-and-account-name}

尋找帳戶「Acme」（帳戶關係為「作用中」）上所有身為「經理」的人。

![顯示細分父級組織的UI](../assets/segmentation/example-11.png)

### 範例12：尋找actualCost超過budgetedCost之行銷活動的目標B2B設定檔 {#find-actualcost-exceed-budgetcost}

尋找actualCost超過budgetedCost之行銷活動的所有目標人員。

![顯示細分父級組織的UI](../assets/segmentation/example-12.png)

### 範例13：尋找屬於Marketo靜態清單的B2B設定檔和isDeleted=false {#find-marketo-static-list}

尋找屬於Marketo靜態清單「週年紀念使用者」的所有人員，其中isDeleted=false。

![顯示細分父級組織的UI](../assets/segmentation/example-13.png)

## 后续步骤 {#next-steps}

閱讀本概述後，您現在瞭解了使用Real-Time CDP B2B版本時可用的分段可能性。 如需Segmentation Service的詳細資訊，請參閱 [區段檔案](../../segmentation/home.md).
