---
keywords: Experience Platform；首頁；熱門主題；分段服務；分段；分段服務；使用手冊； ui指南；分段ui指南；區段產生器；區段產生器；已實現；現有；正在退出；
solution: Experience Platform
title: Segmentation Service UI指南
description: Adobe Experience Platform Segmentation Service提供使用者介面，用於建立和管理區段定義。
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '2650'
ht-degree: 3%

---

# Segmentation Service UI指南

[!DNL Adobe Experience Platform Segmentation Service] 提供使用者介面，用於建立和管理區段定義。

## 快速入门

使用區段定義需要瞭解各種 [!DNL Experience Platform] 與細分有關的服務。 閱讀本使用手冊前，請先檢閱下列服務的檔案：

- [[!DNL Segmentation Service]](../home.md)： [!DNL Segmentation Service] 可讓您分割儲存在 [!DNL Experience Platform] 和歸入較小群組的個人（例如客戶、潛在客戶、使用者或組織）相關的資訊。
- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md)：透過橋接從不同的資料來源擷取的身分來建立客戶設定檔 [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。 為了充分利用「分段」，請確保您的資料已根據 [資料模型化的最佳實務](../../xdm/schema/best-practices.md).

同時請務必瞭解此檔案所使用的兩個關鍵辭彙，並瞭解兩者之間的差異：
- **區段定義**：用來描述目標對象之關鍵特性或行為的規則集。
- **對象**：符合區段定義條件的結果設定檔集。 您可以透過Adobe Experience Platform （平台產生的對象）或從外部來源（外部產生的對象）建立此專案。

## 概述

在Experience PlatformUI中，選取 **[!UICONTROL 區段]** 在左側導覽以開啟 **[!UICONTROL 概觀]** 標籤顯示 [!UICONTROL 區段] 儀表板。

>[!NOTE]
>
>如果您的組織剛開始使用Platform，但尚未建立作用中的設定檔資料集或合併原則，請 [!UICONTROL 區段] 儀表板不可見。 取而代之的是 [!UICONTROL 概觀] 索引標籤會顯示連結和檔案，以幫助您開始使用區段。

### [!UICONTROL 區段] 儀表板 {#segments-dashboard}

此 **[!UICONTROL 區段]** 控制面板會概述與貴組織區段資料相關的關鍵量度。

若要進一步瞭解，請造訪 [區段控制面板指南](../../dashboards/guides/segments.md).

![隨即顯示區段控制面板。 它會顯示各種Widget，包括對象人數、依身分割槽分的設定檔、身分覆蓋圖，以及對象人數變更趨勢。](../../dashboards/images/segments/dashboard-overview.png)

## 浏览 {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="流失率"
>abstract="流失率表示与上次运行区段作业时相比，区段定义内正在更改的配置文件的百分比。"

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="评估方法"
>abstract="区段的评估方法包括批量评估、流式评估和边缘评估。"

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="将所有区段添加到计划"
>abstract="启用此项可在每日计划更新中包含所有批量评估区段。禁用此项可从计划更新中删除所有区段。"

選取 **[!UICONTROL 瀏覽]** 標籤來檢視貴組織的所有區段定義清單。

![隨即顯示區段瀏覽畫面。 此時會顯示屬於組織的所有區段清單。](../images/ui/overview/segment-browse-all.png)

此檢視表會列出區段定義的相關資訊，包括設定檔計數、建立日期和上次修改日期。

您可以透過選取「 」，將其他欄位新增到此顯示 ![篩選屬性圖示](../images/ui/overview/filter-attribute.png). 這些額外的欄位包括劃分、評估方法和工作ID。

如果選取劃分，畫面會顯示長條圖，概述屬於下列每個已計算設定檔狀態的設定檔百分比： [!UICONTROL 已實現] 和 [!UICONTROL 正在退出]. 此外，劃分會顯示在 [!UICONTROL 瀏覽] 索引標籤是區段狀態最準確的劃分。 如果此數字與 [!UICONTROL 概觀] 標籤上，您應該使用位於 [!UICONTROL 瀏覽] 標籤作為正確的資訊來源，因為 [!UICONTROL 概觀] 索引標籤編號每天僅更新一次。

| 状态 | 描述 |
| ------ | ----------- |
| 已實現 | 過去24小時內符合區段資格的設定檔計數。 因此，自上次執行批次區段作業以來，符合區段資格的設定檔數。 |
| 正在退出 | 過去24小時內退出區段的設定檔計數。 因此，自上次執行批次區段作業以來，不再符合區段資格的設定檔數。 |

評估方法可以是串流、批次或邊緣。 當資料進入系統時，會持續評估串流區段。 根據設定的排程評估批次區段。 會即時評估邊緣區段，以允許相同頁面和下一頁個人化使用案例。

![區段瀏覽頁面中的區段會反白顯示。](../images/ui/overview/segment-browse-segments.png)

頁面頂端有選項，可新增所有區段至排程和建立新區段。

切換 **[!UICONTROL 新增所有區段至排程]** 將啟用排程分段。 如需排程分段的詳細資訊，請參閱 [本使用手冊的已排程區段章節](#scheduled-segmentation).

選取 **[!UICONTROL 建立區段]** 將帶您前往區段產生器。 若要進一步瞭解如何建立區段，請閱讀以下章節： [在使用手冊中建立區段](#create-segment).

![區段瀏覽頁面上的頂端導覽列會反白顯示。 此列包含將所有區段新增至排程的切換按鈕，以及建立區段的按鈕。](../images/ui/overview/segment-browse-top.png)

右側邊欄包含組織內所有區段的相關資訊，其中會列出區段總數、上次評估日期、下次評估日期，以及依評估方法劃分的區段。

![區段瀏覽頁面上的右側邊欄會反白顯示。 隨即顯示組織中區段的相關資訊。 這包括區段總數、上次評估時間、下次評估時間，以及不同區段型別的劃分等資訊。](../images/ui/overview/segment-browse-segment-info.png)

選取區段定義列可提供區段定義的摘要，包括編輯或刪除區段、啟用區段至目的地、區段的合格對象、總對象人數以及區段名稱、說明、評估方法、建立日期和上次修改日期的選項。

>[!NOTE]
>
> 您會 **not** 能夠刪除用於目的地啟用的區段。

![有關所選區段的詳細資訊隨即顯示。 這包括合格設定檔數的詳細資訊、合格設定檔與總設定檔的百分比劃分、上次評估日期。](../images/ui/overview/segment-browse-details.png)

## 區段定義細節 {#segment-details}

若要檢視特定區段定義的詳細資訊，請在 **[!UICONTROL 瀏覽]** 標籤。

區段詳細資訊頁面隨即顯示。 上方提供區段定義的摘要、合格對象人數的相關資訊，以及區段啟用的目的地。

![此時會顯示區段定義詳細資訊頁面。 區段摘要、區段中的受眾總數以及啟用的目的地卡會醒目提示。](../images/ui/overview/segment-details-summary.png)

### 區段摘要 {#segment-summary}

此 **[!UICONTROL 區段摘要]** 區段提供屬性的ID、名稱、說明和詳細資訊等資訊。

此外，您可以選擇將區段啟動至目的地或編輯區段。 選取 **[!UICONTROL 啟用到目的地]** 可讓您啟用目的地的區段。 如需將區段啟用至目的地的詳細資訊，請參閱 [啟用概述](../../destinations/ui/activation-overview.md).

![「啟動至目的地」按鈕會反白顯示。](../images/ui/overview/segment-details-activate.png)

選取 **[!UICONTROL 編輯區段]** 將帶您前往 [!DNL Segment Builder]. 如需有關使用的詳細資訊，請參閱 [!DNL Segment Builder] 工作區，請閱讀 [[!DNL Segment Builder] 使用手冊](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### 區段中的對象總數

此 **[!UICONTROL 區段中的對象總數]** 區段會顯示符合區段資格的設定檔總數。

會使用當天樣本資料的樣本大小來產生預估。 如果您的個人資料存放區中的實體少於100萬個，則會使用完整的資料集；對於100萬到2,000萬個之間的實體，會使用100萬個實體；而對於2,000萬個以上的實體，則會使用全部實體的5%。 如需有關產生區段預估的詳細資訊，請參閱 [預估產生區段](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 區段建立教學課程的內容。

### 啟用的目的地

此 **[!UICONTROL 啟用的目的地]** 區段會顯示此區段啟用的目的地。

>[!NOTE]
>
> Destinations是提供的功能 [!DNL Adobe Real-Time Customer Data Platform]，並可讓您將資料匯出至外部平台。 如需有關目的地的詳細資訊，請閱讀 [目的地概觀](../../destinations/home.md). 若要瞭解如何對目的地啟用區段，請參閱 [啟用概述](../../destinations/ui/activation-overview.md).

### 設定檔範例

底下是符合區段資格的設定檔取樣，詳細說明包含 [!DNL Profile] ID、名字、姓氏和個人電子郵件。

資料取樣觸發的方式取決於擷取方法。

對於批次擷取，設定檔存放區會每十五分鐘自動掃描一次，以檢視自上次取樣工作執行以來，是否成功擷取新批次。 如果是這種情況，隨後會掃描設定檔存放區，以檢視記錄數量是否有至少5%的變更。 如果符合這些條件，則會觸發新的取樣工作。

對於串流擷取，每小時會自動掃描設定檔存放區，以檢視記錄數量是否有至少5%的變更。 如果符合此條件，則會觸發新的取樣工作。

掃描的樣本大小取決於設定檔存放區中的實體總數。 這些範例大小如下表所示：

| 設定檔存放區中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 少於100萬 | 完整資料集 |
| 1到2000萬 | 100萬 |
| 超過2,000萬 | 佔總數的5% |

關於每個專案的更多詳細資訊 [!DNL Profile] 可以透過選擇 [!DNL Profile] ID。 若要進一步瞭解設定檔的詳細資訊，請閱讀 [[!DNL Real-Time Customer Profile] 使用手冊](../../profile/ui/user-guide.md#profile-detail).

![區段定義的範例設定檔會反白顯示。 範例設定檔資訊包括設定檔ID、名字、姓氏和個人電子郵件。](../images/ui/overview/segment-details-profiles.png)

## 创建区段 {#create-segment}

選取 **[!UICONTROL 建立區段]** 在右上角開啟 [!DNL Segment Builder] 工作區，您可在其中開始建立區段定義。

![在「區段」瀏覽頁面上，「建立區段」按鈕會反白顯示。](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] 工作区

[!DNL Segment Builder] 提供豐富的工作區，讓您與互動 [!DNL Profile] 資料元素。 工作區提供直覺式控制項來建置和編輯規則，例如用來表示資料屬性的拖放圖磚。

如需有關使用的詳細資訊，請參閱 [!DNL Segment Builder] 工作區，請閱讀 [[!DNL Segment Builder] 使用手冊](./segment-builder.md).

![隨即顯示「區段產生器」工作區。](../images/ui/overview/segment-builder.png)

## 已排程分段 {#scheduled-segmentation}

建立區段定義後，您就可以透過隨選或排程（連續）評估來評估它們。 評估表示移動 [!DNL Real-Time Customer Profile] 資料區段定義，以產生對應的對象。 建立受眾後，系統會儲存並儲存受眾，以便使用將其匯出 [!DNL Experience Platform] API。

隨選評估涉及使用API來執行評估並視需要建立對象，而排程評估（也稱為「已排程分段」）可讓您建立週期性排程，以便在特定時間（最多，每天一次）評估區段定義。

### 啟用排程分段 {#enable-scheduled-segmentation}

使用UI或API啟用已排程評估的區段定義。 在UI中，返回 **[!UICONTROL 瀏覽]** 定位於 **[!UICONTROL 區段]** 並開啟 **[!UICONTROL 新增所有區段至排程]**. 這會導致根據貴組織設定的排程評估所有區段。

>[!NOTE]
>
>對於最多有五(5)個合併原則的沙箱，可啟用排程評估 [!DNL XDM Individual Profile]. 如果貴組織有五個以上的合併原則 [!DNL XDM Individual Profile] 在單一沙箱環境中，您將無法使用排程的評估。

排程目前只能使用API建立。 如需使用API建立、編輯及使用排程的詳細步驟，請依照評估及存取區段結果的教學課程，尤其是 [使用API排程的評估](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![「區段瀏覽」頁面會反白切換至「將所有區段新增至排程」。](../images/ui/overview/segment-browse-scheduled.png)

## 受众 {#audiences}

>[!IMPORTANT]
>
>受眾功能目前為有限測試版，並非所有使用者都可使用。 文档和功能可能会发生变化。

選取 **[!UICONTROL 受眾]** 索引標籤檢視貴組織的所有對象清單。

![貴組織的對象清單。](../images/ui/overview/list-audiences.png)

依預設，此檢視會列出對象的相關資訊，包括名稱、設定檔計數、來源、建立日期和上次修改日期。

您可以選取 ![自訂表格](../images/ui/overview/customize-table.png) 圖示來變更要顯示的欄位。

![自訂表格按鈕會反白顯示。 選取此按鈕可讓您自訂對象瀏覽頁面上顯示的欄位。](../images/ui/overview/select-customize-table.png)

此時會出現一個彈出視窗，其中列出可顯示在表格中的所有欄位。

![可針對「瀏覽對象」區段顯示的屬性。](../images/ui/overview/customize-table-attributes.png)

| 字段 | 描述 |
| ----- | ----------- | 
| [!UICONTROL 名称] | 受众的名称。 |
| [!UICONTROL 配置文件计数] | 符合對象資格的設定檔總數。 |
| [!UICONTROL Origin] | 對象的來源。 如果此對象是平台產生的，則其來源為Segmentation Service。 |
| [!UICONTROL 生命週期狀態] | 對象的狀態。 此欄位可能的值包括 `Draft`， `Published`、和 `Archived`. |
| [!UICONTROL 更新頻率] | 指出對象資料更新頻率的值。 此欄位可能的值包括 `On Demand`， `Scheduled`、和 `Continuous`. |
| [!UICONTROL 上次更新者] | 上次更新對象的人員名稱。 |
| [!UICONTROL 已建立] | 建立受眾的時間和日期。 |
| [!UICONTROL 上次更新时间] | 上次建立對象的時間和日期。 |
| [!UICONTROL 存取標籤] | 對象的存取權標籤。 存取標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 這些標籤可隨時套用，提供您選擇控管資料方式的靈活性。 如需存取標籤的詳細資訊，請參閱以下檔案： [管理標籤](../../access-control/abac/ui/labels.md). |

您可以選取 **[!UICONTROL 建立對象]** 以建立對象。

![建立受眾按鈕會醒目顯示，顯示建立受眾的選取位置。](../images/ui/overview/create-audience.png)

此時會出現彈出視窗，讓您在構成對象或建立規則之間做出選擇。

![顯示您可以建立的兩種對象型別的彈出視窗。](../images/ui/overview/create-audience-type.png)

選取 **[!UICONTROL 撰寫對象]** 帶您前往「對象產生器」。 若要進一步瞭解如何建立對象，請參閱 [Audience Builder指南](./audience-builder.md).

選取 **[!UICONTROL 建置規則]** 帶您前往區段產生器。 若要進一步瞭解如何建立區段，請參閱 [區段產生器指南](./segment-builder.md)

## 對象詳細資料 {#audience-details}

若要檢視特定對象的詳細資訊，請在 [!UICONTROL 受眾] 標籤。

對象詳細資訊頁面隨即顯示。 此頁面的詳細資訊有所不同，端視對象是透過Adobe Experience Platform產生，還是從Audience Orchestration等外部來源產生。

### 平台產生的對象

如需有關Platform產生的對象的詳細資訊，請參閱 [區段摘要區段](#segment-summary).

### 外部產生的對象

在對象詳細資訊頁面頂端，有對象摘要，以及儲存對象之資料集的詳細資訊。

![為外部產生的對象提供的詳細資料。](../images/ui/overview/externally-generated-audience.png)

此 **[!UICONTROL 對象摘要]** 區段提供屬性的ID、名稱、說明和詳細資訊等資訊。

此 **[!UICONTROL 資料集詳細資料]** 區段提供名稱、說明、表格名稱、來源和綱要等資訊。 您可以選取 **[!UICONTROL 檢視資料集]** 以檢視資料集的詳細資訊。

| 字段 | 描述 |
| ----- | ----------- |
| [!UICONTROL 名称] | 数据集的名称。 |
| [!UICONTROL 描述] | 資料集的說明。 |
| [!UICONTROL 表格名稱] | 資料集的表格名稱。 |
| [!UICONTROL 来源] | 資料集的來源。 對於外部產生的對象，此值將為 **結構描述**. |
| [!UICONTROL 架构] | 資料集對應的XDM結構描述型別。 |

若要進一步瞭解資料集，請閱讀 [資料集概述](../../catalog/datasets/overview.md).

## 串流區段 {#streaming-segmentation}

串流細分是執行細分的能力 [!DNL Platform] 近乎即時，同時專注於資料豐富度。 有了串流區段，現在當資料進入時，就會進行區段資格 [!DNL Platform]，減少排程和執行分段工作的需求。

如需串流區段的詳細資訊，請參閱 [串流細分使用手冊](./streaming-segmentation.md).

>[!NOTE]
>
>為了讓串流細分發揮作用，您需要為組織啟用排程分段。 如需啟用已排程分段的詳細資訊，請參閱 [本使用手冊中的串流細分割槽段](#scheduled-segmentation).

## 邊緣細分 {#edge-segmentation}

邊緣區段是即時在邊緣評估Platform中區段的能力，可啟用相同頁面和下一頁個人化使用案例。

有關邊緣細分的更多資訊可在以下網址找到： [edge segmentation UI指南](./edge-segmentation.md)

## 原則違規

>[!NOTE]
>
>只有在建立已指派給目的地的區段時，才適用原則違規。

建立完區段後，Adobe Experience Platform資料控管將會分析該區段，以確保區段內沒有違反原則的情況。 請參閱 [資料控管概觀](../../data-governance/home.md) 以取得詳細資訊。

![會顯示區段的原則違規。](../images/ui/overview/segment-dule-policy-violations.png)

## 後續步驟和其他資源 {#next-steps}

此 [!DNL Segmentation Service] UI提供豐富的工作流程，可讓您從以下專案隔離可行銷對象： [!DNL Real-Time Customer Profile] 資料。

若要深入瞭解 [!DNL Segmentation Service]，請繼續閱讀檔案。 若要瞭解如何使用 [!DNL Segmentation Service] API，請閱讀 [[!DNL Segmentation Service] 開發人員指南](../api/overview.md).
