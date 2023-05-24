---
title: 在使用者介面中建立Adobe Analytics來源連線
description: 瞭解如何在UI中建立Adobe Analytics來源連線，以將消費者資料匯入Adobe Experience Platform。
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 1839e67d86a04762d93a5c35050e261fb1d1cf50
workflow-type: tm+mt
source-wordcount: '2406'
ht-degree: 5%

---

# 在使用者介面中建立Adobe Analytics來源連線

本教學課程提供在UI中建立Adobe Analytics來源連線的步驟，以便將Adobe Analytics報表套裝資料匯入Adobe Experience Platform。

## 快速入门

本教學課程需要您實際瞭解下列Experience Platform元件：

* [Experience Data Model (XDM)系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
* [即時客戶個人檔案](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 关键术语

請務必瞭解本檔案中使用的下列重要術語：

* **標準屬性**：標準屬性是Adobe預先定義的任何屬性。 它們對於所有客戶都包含相同涵義，並且可在 [!DNL Analytics] 來源資料和 [!DNL Analytics] 結構描述欄位群組。
* **自訂屬性**：自訂屬性是中自訂變數階層內的任何屬性 [!DNL Analytics]. 自訂屬性用於Adobe Analytics實作，將特定資訊擷取到報表套裝中，各報表套裝的屬性使用方式可能有所不同。 自訂屬性包括eVar、prop和清單。 請參閱下列內容 [[!DNL Analytics] 有關轉換變數的檔案](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 以取得有關eVar的詳細資訊。
* **自訂欄位群組中的任何屬性**：源自客戶建立的欄位群組的屬性都是使用者定義的，不屬於標準或自訂屬性。
* **易記名稱**：易記名稱是使用者為中的自訂變數提供的標籤。 [!DNL Analytics] 實作。 請參閱下列內容 [[!DNL Analytics] 有關轉換變數的檔案](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 以取得易記名稱的詳細資訊。

## 建立與Adobe Analytics的來源連線

>[!NOTE]
>
>在生產沙箱中建立Analytics來源資料流時，會建立兩個資料流：
>
>* 此資料流會將13個月的歷史報告套裝資料回填至Data Lake。 此資料流會在回填完成時結束。
>* 將即時資料傳送至資料湖和的資料流流程 [!DNL Real-Time Customer Profile]. 此資料流會持續執行。


在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 您也可以使用搜尋列來縮小顯示的來源。

在 **[!UICONTROL Adobe應用程式]** 類別，選取 **[!UICONTROL Adobe Analytics]** 然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/analytics/catalog.png)

### 选择数据

>[!IMPORTANT]
>
>畫面上列出的報表套裝可能來自不同區域。 您有責任瞭解您資料的限制與義務，以及如何跨地區在Adobe Experience Platform中使用該資料。 請確定貴公司允許這樣做。

此 **[!UICONTROL Analytics來源新增資料]** 步驟為您提供以下清單 [!DNL Analytics] 建立來源連線的報表套裝資料。

報表套裝是資料容器，可構成下列專案的基礎 [!DNL Analytics] 報告。 一個組織可以有許多報表套裝，每個報表套裝都包含不同的資料集。

您可以從任何區域擷取報表套裝（美國、英國或新加坡），前提是這些報表套裝對應到與建立來源連線的Experience Platform沙箱例項相同的組織。 報告套裝只能使用單一作用中資料流擷取。 已在您使用的沙箱或其他沙箱中擷取無法選取的報表套裝。

可以建立多個繫結連線，將多個報告套裝帶入同一個沙箱。 如果報表套裝中變數（例如eVar或事件）有不同的結構描述，則應將其對應至自訂欄位群組中的特定欄位，避免使用時發生資料衝突 [資料準備](../../../../../data-prep/ui/mapping.md). 報表套裝只能新增至單一沙箱。

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>只有在沒有資料衝突(例如兩個具有不同含義的自訂屬性（eVar、清單和prop）)時，才能為即時客戶設定檔啟用多個報表套裝的資料。

若要建立 [!DNL Analytics] 來源連線，選取報表套裝，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Analytics報表套裝一次可設定一個沙箱。 若要將相同的報表套裝匯入不同的沙箱，必須透過不同沙箱的設定刪除資料集流程並重新例項化。—>

### 映射

>[!IMPORTANT]
>
>「資料準備」轉換可能會增加整個資料流程的延遲。 新增的額外延遲因轉換邏輯的複雜度而異。

在您可以對應您的 [!DNL Analytics] 資料目標XDM結構描述時，您必須先選取您是使用預設結構描述還是自訂結構描述。

預設結構描述會代表您建立新的結構描述，包含 [!DNL Adobe Analytics ExperienceEvent Template] 欄位群組。 若要使用預設綱要，請選取 **[!UICONTROL 預設結構描述]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

透過自訂結構描述，您可以為您的選擇任何可用的結構描述 [!DNL Analytics] 資料，只要該結構描述具有 [!DNL Adobe Analytics ExperienceEvent Template] 欄位群組。 若要使用自訂結構描述，請選取 **[!UICONTROL 自訂結構描述]**.

![custom-schema](../../../../images/tutorials/create/analytics/custom-schema.png)

此 [!UICONTROL 對應] 頁面提供了一個介面，用於將來源欄位對應到它們適當的目標結構描述欄位。 從這裡，您可以將自訂變數對應到新的結構描述欄位群組，並套用資料準備支援的計算。 選取目標結構描述以開始對應程式。

>[!TIP]
>
>只有結構描述具有 [!DNL Adobe Analytics ExperienceEvent Template] 欄位群組會顯示在結構描述選取功能表中。 省略其他結構描述。 如果您的報表套裝資料沒有適用的結構描述，則必須建立新的結構描述。 如需建立結構描述的詳細步驟，請參閱以下指南： [在UI中建立和編輯方案](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

此 [!UICONTROL 對應標準欄位] 區段顯示面板 [!UICONTROL 已套用標準對應]， [!UICONTROL 不符合的標準對應] 和 [!UICONTROL 自訂對應]. 如需各個類別的特定資訊，請參閱下表：

| 對應標準欄位 | 描述 |
| --- | --- |
| [!UICONTROL 已套用標準對應] | 此 [!UICONTROL 已套用標準對應] 面板會顯示對應屬性的總數。 標準對應是指來源中所有屬性之間的對應集 [!DNL Analytics] 中的資料和對應屬性 [!DNL Analytics] 欄位群組。 這些專案已預先對應，無法編輯。 |
| [!UICONTROL 不符合的標準對應] | 此 [!UICONTROL 不符合的標準對應] panel是指包含易記名稱衝突的對應屬性數目。 當您重複使用已有來自不同報表套裝之欄位描述項填入集的結構描述時，這些衝突就會出現。 您可以繼續進行 [!DNL Analytics] 資料流，即使易記名稱有衝突。 |
| [!UICONTROL 自訂對應] | 此 [!UICONTROL 自訂對應] 面板會顯示對應自訂屬性的數量，包括eVar、prop和清單。 自訂對應是指來源中自訂屬性之間的對應集 [!DNL Analytics] 包含在所選結構描述中的自訂欄位群組中的資料和屬性。 |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

若要預覽 [!DNL Analytics] ExperienceEvent範本結構描述欄位群組，選取 **[!UICONTROL 檢視]** 在 [!UICONTROL 已套用標準對應] 面板。

![view](../../../../images/tutorials/create/analytics/view.png)

此 [!UICONTROL Adobe Analytics ExperienceEvent範本結構欄位群組] 頁面提供檢查結構描述結構時使用的介面。 完成後，選取 **[!UICONTROL 關閉]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform會自動偵測您的對應集是否有任何易記名稱衝突。 如果對應集沒有衝突，請選取 **[!UICONTROL 下一個]** 以繼續進行。

![對應](../../../../images/tutorials/create/analytics/mapping.png)

如果您的來源報告套裝和您選取的結構描述之間有易記名稱衝突，您仍可以繼續進行 [!DNL Analytics] 資料流，確認欄位描述項不會變更。 或者，您可以選擇使用一組空白的描述項建立新結構描述。

選取 **[!UICONTROL 下一個]** 以繼續進行。

![注意](../../../../images/tutorials/create/analytics/caution.png)

#### 自訂對應

若要使用「資料準備」函式並為自訂屬性新增對應或計算欄位，請選取 **[!UICONTROL 檢視自訂對應]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

接下來，選取 **[!UICONTROL 新增對應]**.

視您的需求而定，您可以選取 **[!UICONTROL 新增對應]** 或 **[!UICONTROL 新增計算欄位]** 從顯示的選項中。

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

出現空的對映集。 選取對應圖示以新增來源欄位。

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

您可以使用介面瀏覽來源結構描述結構，並識別您要使用的新來源欄位。 選取要對應的來源欄位後，請選取 **[!UICONTROL 選取]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

接下來，選取底下的對應圖示 [!UICONTROL 目標欄位] 以將您選取的來源欄位對應至其適當的目標欄位。

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

與來源結構描述類似，您可以使用介面導覽目標結構描述結構，並選取您要對應的目標欄位。 選取適當的目標欄位後，請選取 **[!UICONTROL 選取]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

完成自訂對應集後，選取 **[!UICONTROL 下一個]** 以繼續進行。

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

下列檔案提供進一步瞭解「資料準備」、計算欄位和對映函式的資源：

* [資料準備總覽](../../../../../data-prep/home.md)
* [資料準備對應函式](../../../../../data-prep/functions.md)
* [新增計算欄位](../../../../../data-prep/ui/mapping.md#calculated-fields)

### 篩選即時客戶設定檔 {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="创建筛选规则"
>abstract="在将数据发送到实时客户配置文件时定义行级和列级筛选规则。使用行级筛选来应用条件并指示要&#x200B;**为配置文件提取包含**&#x200B;的数据。使用列级筛选来选择要&#x200B;**为配置文件提取排除**&#x200B;的数据列。筛选规则不适用于发送到数据湖的数据。"

完成下列專案的對應後： [!DNL Analytics] 報表套裝資料時，您可以套用篩選規則和條件，選擇性地將資料納入或排除在內嵌至Real-Time Customer Profile中。 篩選支援僅適用於 [!DNL Analytics] 資料與資料僅在輸入前進行篩選 [!DNL Profile.] 所有資料都會內嵌至Data Lake。

#### 列層級篩選

>[!IMPORTANT]
>
>使用行级筛选来应用条件并指示要&#x200B;**为配置文件提取包含**&#x200B;的数据。使用列级筛选来选择要&#x200B;**为配置文件提取排除**&#x200B;的数据列。

您可以篩選資料 [!DNL Profile] 列層級和欄層級的擷取。 列層級篩選可讓您定義字串包含、等於、開頭或結尾等條件。 您也可以使用列層級篩選來聯結條件，使用 `AND` 以及 `OR`，並使用否定條件 `NOT`.

若要篩選您的 [!DNL Analytics] 資料列層級，選取 **[!UICONTROL 列篩選]**.

![row-filter](../../../../images/tutorials/create/analytics/row-filter.png)

使用左側邊欄瀏覽結構描述階層，並選取您選擇的結構描述屬性，以進一步向下鑽研特定結構描述。

![左側欄](../../../../images/tutorials/create/analytics/left-rail.png)

識別您要設定的屬性後，選取該屬性，並將其從左側邊欄拖曳至篩選面板。

![filtering-panel](../../../../images/tutorials/create/analytics/filtering-panel.png)

若要設定不同的條件，請選取 **[!UICONTROL 等於]** 然後從出現的下拉式視窗中選取條件。

可設定的條件清單包括：

* [!UICONTROL 等于]
* [!UICONTROL 不等于]
* [!UICONTROL 開頭為]
* [!UICONTROL 結尾為]
* [!UICONTROL 结尾不为]
* [!UICONTROL 包含]
* [!UICONTROL 不包含]
* [!UICONTROL 存在]
* [!UICONTROL 不存在]

![条件](../../../../images/tutorials/create/analytics/conditions.png)

接下來，根據您選取的屬性輸入您要包含的值。 在以下範例中， [!DNL Apple] 和 [!DNL Google] 被選取作為內嵌的一部分 **[!UICONTROL 製造商]** 屬性。

![include-manufacturer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

若要進一步指定篩選條件，請從結構描述新增另一個屬性，然後根據該屬性新增值。 在以下範例中， **[!UICONTROL 模型]** 屬性已新增，且模型如下 [!DNL iPhone 13] 和 [!DNL Google Pixel 6] 經過篩選以便擷取。

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

若要新增容器，請選取省略符號(`...`)，然後選取「 」 **[!UICONTROL 新增容器]**.

![add-container](../../../../images/tutorials/create/analytics/add-container.png)

新增容器後，選取 **[!UICONTROL 包含]** 然後選取 **[!UICONTROL 排除]** 從出現的下拉式視窗中。

![排除](../../../../images/tutorials/create/analytics/exclude.png)

接下來，拖曳結構描述屬性，並新增您要從篩選中排除的對應值，以完成相同的程式。 在以下範例中， [!DNL iPhone 12]， [!DNL iPhone 12 mini]、和 [!DNL Google Pixel 5] 都是從排除清單中篩選出來的 **[!UICONTROL 模型]** 屬性，橫向會從 **[!UICONTROL 熒幕方向]**，和型號 [!DNL A1633] 排除自 **[!UICONTROL 型號]**.

完成後，選取 **[!UICONTROL 下一個]**.

![exclude-examples](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### 欄層級篩選

選取 **[!UICONTROL 欄篩選器]** 以套用欄層級篩選。

![column-filter](../../../../images/tutorials/create/analytics/column-filter.png)

頁面會更新為互動式結構描述樹狀結構，在欄層級顯示結構描述屬性。 從這裡，您可以選取要從中排除的資料欄 [!DNL Profile] 內嵌。 或者，您可以展開欄並選取要排除的特定屬性。

依預設，全部 [!DNL Analytics] 前往 [!DNL Profile] 而且此程式允許排除XDM資料的分支 [!DNL Profile] 內嵌。

完成後，選取 **[!UICONTROL 下一個]**.

![columns-selected](../../../../images/tutorials/create/analytics/columns-selected.png)

### 提供資料流詳細資料

此 **[!UICONTROL 資料流詳細資料]** 步驟隨即顯示，您必須在此為資料流提供名稱和說明（選用）。 選取 **[!UICONTROL 下一個]** 完成後。

![資料流 — 詳細資料](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 请查看

此 [!UICONTROL 檢閱] 步驟隨即顯示，可讓您在建立新的Analytics資料流之前先檢閱該資料流。 連線的詳細資訊會依類別分組，包括：

* [!UICONTROL 連線]：顯示連線的來源平台。
* [!UICONTROL 資料型別]：顯示選取的報表套裝及其對應的報表套裝ID。

![檢閱](../../../../images/tutorials/create/analytics/review.png)

### 監視資料流

建立資料流後，您可以監視透過該資料流擷取的資料。 從 [!UICONTROL 目錄] 畫面，選取 **[!UICONTROL 資料流]** 以檢視與您的Analytics帳戶相關聯的已建立流程清單。

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

此 **資料流** 畫面隨即顯示。 在此頁面是一對資料集流程，包括有關其名稱、來源資料、建立時間和狀態的資訊。

聯結器會將兩個資料集流程例項化。 一個流程代表回填資料，另一個流程代表即時資料。 未針對設定檔設定回填資料，但會傳送至資料湖，以用於分析和資料科學的使用案例。

如需回填、即時資料及其各自延遲的詳細資訊，請參閱 [Analytics Data Connector概述](../../../../connectors/adobe-applications/analytics.md).

從清單中選取您要檢視的資料集流程。

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

此 **[!UICONTROL 資料集活動]** 頁面便會顯示。 此頁面會以圖表形式顯示使用訊息的速率。 選取 **[!UICONTROL 資料控管]** 以存取標籤欄位。

![資料集 — 活動](../../../../images/tutorials/create/analytics/dataset-activity.png)

您可以檢視資料集流程的繼承標籤，從 [!UICONTROL 資料控管] 畫面。 如需如何為來自Analytics的資料加上標籤的詳細資訊，請造訪 [資料使用標籤指南](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

若要刪除資料流，請前往 [!UICONTROL 資料流] 頁面，然後選取省略符號(`...`)，然後選取「 」 [!UICONTROL 刪除].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## 後續步驟和其他資源

建立連線後，系統會自動建立資料流以包含傳入的資料，並以您選取的結構描述填入資料集。 此外，还会进行数据回填，并摄取至多 13 个月的历史数据。初始內嵌完成時， [!DNL Analytics] 資料以及供下游平台服務使用的資訊，例如 [!DNL Real-Time Customer Profile] 和細分服務。 如需更多詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 概述](../../../../../query-service/home.md)

以下影片旨在協助您瞭解如何使用Adobe Analytics來源聯結器擷取資料：

>[!WARNING]
>
> 此 [!DNL Platform] 以下影片中顯示的UI已過期。 請參閱上述檔案，瞭解最新的UI熒幕擷取畫面及功能。

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
