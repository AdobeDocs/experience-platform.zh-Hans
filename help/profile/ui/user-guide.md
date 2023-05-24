---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一；設定檔；rtcp；啟用設定檔；啟用設定檔；聯合結構描述；聯合設定檔
title: Real-Time Customer Profile UI指南
description: 即時客戶設定檔可為個別客戶建立整體檢視，並結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 本檔案可作為在Adobe Experience Platform使用者介面中與Real-time Customer Profile互動的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] UI指南

[!DNL Real-Time Customer Profile] 為每個個別客戶建立整體檢視，結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 本檔案可作為與互動的指南 [!DNL Real-Time Customer Profile] Adobe Experience Platform使用者介面(UI)中的資料。

## 快速入门

本UI指南需要瞭解各種 [!DNL Experience Platform] 與管理相關的服務 [!DNL Real-Time Customer Profiles]. 在閱讀本指南或使用UI之前，請檢視以下服務的檔案：

* [[!DNL Real-Time Customer Profile] 概觀](../home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Identity Service]](../../identity-service/home.md)：啟用 [!DNL Real-Time Customer Profile] 在擷取身分時，透過橋接來自不同資料來源的身分 [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。

## [!UICONTROL 概述]

在Experience PlatformUI中，選取 **[!UICONTROL 設定檔]** 在左側導覽以開啟 **[!UICONTROL 概觀]** 標籤顯示設定檔控制面板。

>[!NOTE]
>
>如果您的組織剛開始使用Platform，但尚未建立作用中的設定檔資料集或合併原則，請 [!UICONTROL 設定檔] 儀表板不可見。 取而代之的是 [!UICONTROL 概觀] 索引標籤會顯示連結和檔案，以幫助您開始使用即時客戶個人檔案。

### 設定檔儀表板 {#profile-dashboard}

設定檔儀表板會概述與組織設定檔資料相關的關鍵量度。

若要進一步瞭解，請造訪 [設定檔儀表板指南](../../dashboards/guides/profiles.md).

![「設定檔」儀表板隨即顯示。](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL 瀏覽] 索引標籤量度

選取 **[!UICONTROL 瀏覽]** 標籤來顯示與您組織設定檔資料相關的數個量度。 您也可以使用此標籤來瀏覽使用合併原則或身分的設定檔存放區，如本指南下一節中所述。

在的右側 **[!UICONTROL 瀏覽]** 索引標籤是 [設定檔計數](#profile-count) 以及清單 [依名稱空間的設定檔](#profiles-by-namespace).

>[!NOTE]
>
>這些設定檔量度可能與 [設定檔儀表板](#profile-dashboard) 因為它們是使用貴組織的預設合併原則來評估。 如需有關使用合併原則的詳細資訊，包括如何定義預設合併原則，請參閱 [合併原則概觀](../merge-policies/overview.md).

除了這些量度外，本節還提供上次更新的日期和時間，顯示上次評估量度的時間。

![設定檔量度會顯示並反白顯示。](../images/user-guide/browse-metrics.png)

### 配置文件计数 {#profile-count}

在您組織的預設合併原則已與設定檔片段合併在一起，以為每個個別客戶形成單一設定檔後，設定檔計數會顯示貴組織在Experience Platform內的設定檔總數。 換言之，您的組織可能擁有多個與跨不同頻道與您的品牌互動的單一客戶相關的設定檔片段，但這些片段會合併在一起（根據預設合併原則）並傳回「1」設定檔計數，因為它們都與同一個人相關。

設定檔計數也包含具有屬性（記錄資料）的設定檔，以及僅包含時間序列（事件）資料(例如Adobe Analytics設定檔)的設定檔。 設定檔計數會定期更新，以提供Platform內最新的設定檔總數。

#### 更新設定檔計數量度

將記錄擷取至 [!DNL Profile] 存放區增加或減少計數超過5%，則會觸發工作以更新計數。 對於串流資料工作流程，會每小時進行一次檢查，以判斷是否符合增加或減少5%的臨界值。 如果有的話，系統會自動觸發工作以更新設定檔計數。 對於批次擷取，在成功將批次擷取到設定檔存放區後15分鐘內，如果符合5%增加或減少臨界值，則會執行工作以更新設定檔計數。

### [!UICONTROL 依名稱空間的設定檔] {#profiles-by-namespace}

此 **[!UICONTROL 依名稱空間的設定檔]** 量度會顯示您的個人資料存放區中所有合併的個人資料中的名稱空間總計數和劃分。 依名稱空間區分的設定檔總數（也就是將每個名稱空間顯示的值相加）一律會高於設定檔計數量度，因為一個設定檔可能會有多個相關聯的名稱空間。 例如，如果客戶在多個頻道上與您的品牌互動，則多個名稱空間會與該個別客戶相關聯。

#### 更新 [!UICONTROL 依名稱空間的設定檔] 量度

類似於 [設定檔計數](#profile-count) 量度，將記錄擷取至 [!DNL Profile] 存放區增加或減少計數超過5%，則會觸發工作以更新名稱空間量度。 對於串流資料工作流程，會每小時進行一次檢查，以判斷是否符合增加或減少5%的臨界值。 如果有的話，系統會自動觸發工作以更新設定檔計數。 針對批次擷取，請在成功將批次擷取到 [!DNL Profile] 如果符合5%增加或減少臨界值，則會執行工作以更新量度。

## 使用 [!UICONTROL 瀏覽] 標籤以檢視設定檔

於 **[!UICONTROL 瀏覽]** 索引標籤您可以使用合併原則檢視範例設定檔，或使用身分名稱空間和值查詢特定設定檔。

![此時會顯示屬於組織的設定檔。](../images/user-guide/none-selected.png)

### 瀏覽依據 [!UICONTROL 合併原則]

此 **[!UICONTROL 瀏覽]** tab依預設會設定為您的組織的預設合併原則。 若要選擇不同的合併原則，請選取 `X` ，然後使用選取器開啟 **[!UICONTROL 選取合併原則]** 對話方塊。

>[!NOTE]
>
>如果未選取合併原則，請使用「 」旁邊的「 」選擇器按鈕 **[!UICONTROL 合併原則]** 欄位以開啟選取範圍對話方塊。

![「合併原則」選擇器會反白顯示。](../images/user-guide/browse-by-merge-policy.png)

若要從以下專案選擇合併原則： **[!UICONTROL 選取合併原則]** 對話方塊中，選取原則名稱旁的單選按鈕，然後使用 **[!UICONTROL 選取]** 以返回 [!UICONTROL 瀏覽] 標籤。 然後，您可以選取 **[!UICONTROL 檢視]** 以重新整理範例設定檔，並檢視已套用新合併原則的設定檔取樣。

![會顯示一個對話方塊，您可在其中選取要作為篩選依據的合併原則。](../images/user-guide/select-merge-policy.png)

顯示的設定檔代表在套用選取的合併原則後，貴組織設定檔存放區中最多20個設定檔的範例。 將新資料新增到貴組織的設定檔存放區時，會重新整理所選合併原則的範例設定檔。

若要檢視其中一個範例設定檔的詳細資訊，請選取 **[!UICONTROL 設定檔ID]**. 如需詳細資訊，請參閱本指南後面關於 [檢視設定檔詳細資料](#profile-detail).

![將顯示符合合併原則的範例設定檔。](../images/user-guide/sample-profiles.png)

若要進一步瞭解合併原則及其在Platform中的角色，請參閱 [合併原則概觀](../merge-policies/overview.md).

### 瀏覽依據 [!UICONTROL 身分] {#browse-identity}

於 **[!UICONTROL 瀏覽]** 索引標籤中，您可以使用身分名稱空間，以便透過身分值查詢特定設定檔。 依身分瀏覽需要您提供合併原則、身分名稱空間和身分值。

![合併原則選擇器會反白顯示。](../images/user-guide/browse-by-merge-policy.png)

如有必要，請使用 **[!UICONTROL 合併原則]** 選擇器以開啟 **[!UICONTROL 選取合併原則]** 對話方塊，並選擇要使用的合併原則。

![會顯示一個對話方塊，您可在其中選取要作為篩選依據的合併原則。](../images/user-guide/select-merge-policy.png)

然後使用 **[!UICONTROL 身分名稱空間]** 選擇器以開啟 **[!UICONTROL 選取身分名稱空間]** 對話方塊，並選擇要搜尋的名稱空間。 如果您的組織有許多名稱空間，您可以使用對話方塊中的搜尋列，開始輸入名稱空間的名稱。

您可以選取名稱空間以檢視其他詳細資訊，或選取選項按鈕以選擇名稱空間。 然後，您可以使用 **[!UICONTROL 選取]** 以繼續。

![會顯示一個對話方塊，您可以在其中選取要作為篩選依據的身分名稱空間。](../images/user-guide/select-identity-namespace.png)

選取 [!UICONTROL 身分名稱空間] 並返回 [!UICONTROL 瀏覽] 索引標籤中，您可以輸入 **[!UICONTROL 身分值]** 和您選取的名稱空間相關。

>[!NOTE]
>
>此值專屬於個別客戶設定檔，且必須是所提供名稱空間的有效專案。 例如，選取身分名稱空間「電子郵件」需要有效電子郵件地址形式的身分值。

![您要篩選的身分值會反白顯示。](../images/user-guide/filter-identity-value.png)

輸入值後，選取 **[!UICONTROL 檢視]** 且會傳回符合值的單一設定檔。 選取 **[!UICONTROL 設定檔ID]** 以檢視設定檔詳細資料。

![符合身分值的設定檔會反白顯示。](../images/user-guide/filtered-identity-value.png)

## 檢視設定檔詳細資料 {#profile-detail}

選取 **[!UICONTROL 設定檔ID]**，則 **[!UICONTROL 詳細資訊]** 標籤開啟。 顯示在上的設定檔資訊 **[!UICONTROL 詳細資訊]** 索引標籤已從多個設定檔片段合併在一起，以形成個別客戶的單一檢視。 這包括基本屬性、連結的身分和管道偏好設定等客戶細節。

顯示的預設欄位也可以在組織層級變更以顯示偏好的設定檔屬性。 若要進一步瞭解如何自訂這些欄位，包括新增和移除屬性以及調整儀表板面板大小的逐步指示，請閱讀 [設定檔詳細資料自訂指南](profile-customization.md).

![詳細資訊標籤會反白顯示。 設定檔詳細資訊隨即顯示。](../images/user-guide/profile-detail.png)

您可以選取其他可用的標籤，以檢視與個別客戶設定檔相關的額外資訊。 這些標籤包括屬性、事件和區段成員資格標籤，顯示設定檔目前符合資格的區段。

### 屬性標籤

此 **[!UICONTROL 屬性]** tab標籤提供清單檢視，在套用指定的合併原則後，彙總與單一設定檔相關的所有屬性。

這些屬性也可以透過選取以下專案來檢視為JSON物件 **[!UICONTROL 檢視JSON]**. 對於想更瞭解如何將設定檔屬性擷取到Platform的使用者，這個用法很有幫助。

![「屬性」標籤會反白顯示。 設定檔屬性隨即顯示。](../images/user-guide/attributes.png)

### 事件標籤

此 **[!UICONTROL 事件]** 索引標籤包含來自與客戶相關聯的100個最新ExperienceEvents的資料。 此資料可能包括電子郵件開啟、購物車活動和頁面檢視。 選取 **[!UICONTROL 檢視全部]** 對於任何個別事件，都會提供額外的欄位和值擷取，作為事件的一部分。

您也可以選取「 」，將事件視為JSON物件 **[!UICONTROL 檢視JSON]**. 這有助於瞭解如何在Platform中擷取事件。

![「事件」標籤會反白顯示。 設定檔事件隨即顯示。](../images/user-guide/events.png)

### 區段會籍標籤

此 **[!UICONTROL 區段會籍]** 索引標籤會顯示清單，其中包含個別客戶設定檔目前所屬的區段的名稱和說明。 當設定檔符合區段的資格或過期時，此清單會自動更新。 設定檔目前符合資格的區段總數會顯示在標籤的右側。

如需Experience Platform分段的詳細資訊，請參閱 [AdobeExperience Platform細分服務檔案](../../segmentation/home.md).

![「區段會籍」標籤會反白顯示。 設定檔區段會籍詳細資訊隨即顯示。](../images/user-guide/segment-membership.png)

## 合併原則

從主要 **[!UICONTROL 設定檔]** 功能表，選取 **[!UICONTROL 合併原則]** 標籤來檢視屬於您組織的合併原則清單。 每個列出的原則都會顯示其名稱（無論是否為預設的合併原則）及其套用的結構描述類別。

如需合併原則的詳細資訊，請參閱 [合併原則概觀](../merge-policies/overview.md).

![「合併原則」標籤會反白顯示。 此時會顯示屬於組織的合併原則。](../images/user-guide/merge-policies.png)

## 聯合結構描述 {#union-schema}

從主要 **[!UICONTROL 設定檔]** 功能表，選取 **[!UICONTROL 聯合結構描述]** 標籤以檢視您擷取資料的可用聯合結構描述。 聯合結構描述是所有專案的合併 [!DNL Experience Data Model] (XDM)相同類別下的欄位，其結構描述已啟用以用於中 [!DNL Real-Time Customer Profile].

如需聯合結構描述的詳細資訊，請造訪 [聯合結構描述UI指南](union-schema.md).

![「聯合結構描述」標籤會反白顯示。 會顯示屬於組織的聯合結構描述。](../images/user-guide/union-schema.png)

## 后续步骤

閱讀本指南後，您就會知道如何使用Experience PlatformUI檢視和管理組織的設定檔資料。 有關如何使用Experience Platform API處理設定檔資料的資訊，請參閱 [Real-Time Customer Profile API指南](../api/overview.md).
