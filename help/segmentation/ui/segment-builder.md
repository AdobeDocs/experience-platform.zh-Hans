---
keywords: Experience Platform；首頁；熱門主題；分段服務；分段；分段服務；使用手冊；ui指南；分段ui指南；區段產生器；區段產生器；
solution: Experience Platform
title: 區段產生器UI指南
description: Adobe Experience Platform UI中的區段產生器提供豐富的工作區，可讓您與設定檔資料元素互動。 工作區提供直覺式控制項來建置和編輯規則，例如用來表示資料屬性的拖放圖磚。
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 28b9458d29ce69bcbfdff53c0cb6bd7f427e4a2e
workflow-type: tm+mt
source-wordcount: '3258'
ht-degree: 6%

---

# [!DNL Segment Builder] UI指南

[!DNL Segment Builder] 提供豐富的工作區，讓您與互動 [!DNL Profile] 資料元素。 工作區提供直覺式控制項來建置和編輯規則，例如用來表示資料屬性的拖放圖磚。

![隨即顯示區段產生器UI。](../images/ui/segment-builder/segment-builder.png)

## 區段定義建置區塊 {#building-blocks}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_fields"
>title="字段"
>abstract="构成区段的三种字段类型是属性、事件和受众。属性允许您使用属于 XDM 个人配置文件类的配置文件属性，事件允许您基于使用 XDM ExperienceEvent 数据元素发生的操作或事件创建受众，受众允许您使用从外部源导入的受众。"

區段定義的基本建置區塊是屬性和事件。 此外，現有對象中包含的屬性和事件可作為新定義的元件。

您可以在以下連結中看到這些組成要素： **[!UICONTROL 欄位]** 左側部分 [!DNL Segment Builder] 工作區。 **[!UICONTROL 欄位]** 包含每個主要建置區塊的標籤： 」[!UICONTROL 屬性]「， 」[!UICONTROL 事件]「和」[!UICONTROL 受眾]「。

![區段產生器的欄位區段會反白顯示。](../images/ui/segment-builder/segment-fields.png)

### 属性

此 **[!UICONTROL 屬性]** 索引標籤可讓您瀏覽 [!DNL Profile] 屬於以下的屬性 [!DNL XDM Individual Profile] 類別。 每個資料夾都可以展開以顯示其他屬性，其中每個屬性都是一個圖磚，可將其拖曳至工作區中央的規則產生器畫布上。 此 [規則產生器畫布](#rule-builder-canvas) 本指南的稍後章節將更詳細地討論。

![區段產生器欄位的屬性區段會反白顯示。](../images/ui/segment-builder/attributes.png)

### 事件

此 **[!UICONTROL 事件]** 索引標籤可讓您根據使用發生的事件或動作建立對象 [!DNL XDM ExperienceEvent] 資料元素。 您也可以在以下網址找到事件型別： **[!UICONTROL 事件]** 索引標籤，這是常用事件的集合，可讓您更快速地建立區段。

除了能夠瀏覽 [!DNL ExperienceEvent] 元素，您也可以搜尋事件型別。 事件型別使用的編碼邏輯與相同 [!DNL ExperienceEvents]，不需您透過以下網址搜尋： [!DNL XDM ExperienceEvent] 尋找正確事件的類別。 例如，使用搜尋列搜尋「cart」會傳回事件型別[!UICONTROL AddCart]「和」[!UICONTROL RemoveCart]「」，這是建立區段定義時最常用的兩個購物車動作。

任何型別的元件都可在搜尋列中鍵入其名稱來搜尋，該名稱會使用 [Lucene的搜尋語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 輸入整個字詞時，搜尋結果會開始填入。 例如，根據XDM欄位建立規則的方式 `ExperienceEvent.commerce.productViews`，開始在搜尋欄位中輸入「產品檢視」。 輸入單字「product」後，搜尋結果就會開始出現。 每個結果都包含其所屬的物件階層。

>[!NOTE]
>
>貴組織定義的自訂結構描述欄位最多可能需要24小時才會顯示，並且可在建置規則中使用。

然後您就可以輕鬆拖放 [!DNL ExperienceEvents] 和&quot;[!UICONTROL 事件型別]」放入您的區段定義中。

![區段產生器UI的事件區段會強調顯示。](../images/ui/segment-builder/events.png)

依預設，只會顯示資料存放區中填入的結構描述欄位。 其中包括&quot;[!UICONTROL 事件型別]「。 若為「[!UICONTROL 事件型別]「清單不可見，或您只能選擇」[!UICONTROL 任何]&quot;作為&quot;[!UICONTROL 事件型別]&quot;，選取 **齒輪圖示** 旁邊 **[!UICONTROL 欄位]**，然後選取 **[!UICONTROL 顯示完整的XDM結構描述]** 在 **[!UICONTROL 可用欄位]**. 選取 **齒輪圖示** 再次返回至 **[!UICONTROL 欄位]** 標籤，您現在應該能夠檢視多個&quot;[!UICONTROL 事件型別]」和結構描述欄位，無論它們是否包含資料。

![選項按鈕可讓您選擇是隻顯示含有資料的欄位，還是顯示所有XDM欄位，反白顯示。](../images/ui/segment-builder/show-populated.png)

#### Adobe Analytics報表套裝資料集

您可以將單一或多個Adobe Analytics報表套裝的資料當成區段內的事件使用。

使用單一Analytics報告套裝中的資料時，Platform會自動新增描述項和易記名稱至eVar，以便更輕鬆地在中尋找這些欄位 [!DNL Segment Builder].

![此影像顯示一般變數(eVar)如何以使用者易記名稱對應。](../images/ui/segment-builder/single-report-suite.png)

使用來自多個Analytics報表套裝的資料時，平台 **無法** 自動將描述元或易記名稱新增至eVar。 因此，您必須先對應至XDM欄位，才能使用Analytics報表套裝的資料。 有關將Analytics變數對應至XDM的更多資訊，請參閱 [Adobe Analytics來源連線指南](../../sources/tutorials/ui/create/adobe-applications/analytics.md#mapping).

例如，假設您有兩個報表套裝包含以下變數：

| 字段 | 報表套裝結構描述A | 報表套裝結構描述B |
| ----- | --------------------- | --------------------- |
| eVar1 | 反向链接域 | 已登入Y/N |
| eVar2 | 页面名称 | 會員忠誠度ID |
| eVar3 | URL | 页面名称 |
| eVar4 | 搜尋字詞 | 產品名稱 |
| event1 | 单击次数 | Page Views |
| event2 | Page Views | 购物车加货 |
| event3 | 购物车加货 | 结账 |
| event4 | 购买 | 购买 |

在此情況下，您可以使用以下結構描述對應這兩個報表套裝：

![顯示如何將兩個報表套裝對應至一個聯合結構描述的影像。](../images/ui/segment-builder/union-schema.png)

>[!NOTE]
>
>雖然仍會填入一般eVar值，但您應 **not** 在區段定義中使用這些值（如有可能），因為這些值的意義可能和值原本在報表中的意義不同。

在對應報表套裝後，您可以在設定檔相關工作流程和區段中使用這些新對應的欄位。

| 场景 | 聯合結構描述體驗 | 分段通用變數 | 區段對應變數 |
| -------- | ----------------------- | ----------------------------- | ---------------------------- |
| 單一報告套裝 | 泛型變數中包含易記名稱描述項。 <br><br>**範例：** 頁面名稱(eVar2) | <ul><li>泛型變數中包含的易記名稱描述項</li><li>查詢會使用來自特定資料集的資料，因為這是唯一使用資料</li></ul> | 查詢可以使用Adobe Analytics資料，也可能使用其他來源。 |
| 多个报告包 | 泛型變數未包含任何易記名稱描述元。 <br><br>**範例：** EVAR2 | <ul><li>任何具有多個描述元的欄位都會顯示為一般。 這表示UI中未出現任何好記的名稱。</li><li>查詢可以使用任何包含eVar的資料集中的資料，這可能會導致混合或不正確的結果。</li></ul> | 查詢會使用來自多個資料集的正確組合結果。 |

### 受众

此 **[!UICONTROL 受眾]** 索引標籤會列出從外部來源(例如Adobe Audience Manager)匯入的所有對象，以及在中建立的對象 [!DNL Experience Platform].

於 **[!UICONTROL 受眾]** 索引標籤中，您可以將所有可用的來源視為一組資料夾。 當您選取資料夾時，可以看到可用的子資料夾和對象。 此外，您可以選取資料夾圖示（如最右側的影像中所示）來檢視資料夾結構（核取記號代表您目前所在的資料夾），並藉由選取樹狀結構中的資料夾名稱來輕鬆導覽至資料夾。

您可以將滑鼠移至對象旁的ⓘ結上，以檢視對象的相關資訊，包括其ID、說明，以及用來尋找對象的資料夾階層。

![此影像會示範資料夾階層如何為對象運作。](../images/ui/segment-builder/audience-folder-structure.png)

您也可以使用搜尋列來搜尋對象，此搜尋列會利用 [Lucene的搜尋語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 於 **[!UICONTROL 受眾]** 標籤，選取頂層資料夾會出現搜尋列，讓您在該資料夾中搜尋。 搜尋結果只會在輸入完整字詞後開始填入。 例如，若要尋找對象，請將 `Online Shoppers`，開始在搜尋列中輸入「線上」。 輸入「線上」一詞後，包含「線上」一詞的搜尋結果就會出現。

## 規則產生器畫布 {#rule-builder-canvas}

區段定義是用來描述目標對象之關鍵特性或行為的規則集合。 這些規則是使用規則產生器畫布建立的，位於的中心 [!DNL Segment Builder].

若要將新規則新增至區段定義，請從下列位置拖曳圖磚： **[!UICONTROL 欄位]** 定位並拖曳至規則產生器畫布上。 然後，會根據要新增的資料型別，為您顯示內容特定的選項。 可用的資料型別包括：字串、日期、 [!DNL ExperienceEvents]， &quot;[!UICONTROL 事件型別]「」和對象。

![空白規則產生器畫布。](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Adobe Experience Platform的最新變更已更新的 `OR` 和 `AND` 事件之間的邏輯運運算元。 這些更新不會影響現有區段。 不過，這些變更會影響現有區段及新區段建立的所有後續更新。 請閱讀 [時間常數更新](./segment-refactoring.md) 以取得詳細資訊。

選取屬性的值時，您會看到屬性可以成為的列舉值清單。

![顯示屬性可以成為的列舉值清單的影像。](../images/ui/segment-builder/enum-list.png)

如果從此列舉清單中選取一個值，該值將以實線框線列出。 但是，對於使用的欄位 `meta:enum` （柔性）列舉，也可以選取一個值 **not** 從列舉清單中。 如果您建立自己的值，則會以虛線邊框勾勒出它的輪廓，並附上警告，指出此值不在列舉清單中。

![如果插入的值不是列舉清單的一部分，則會顯示警告。](../images/ui/segment-builder/enum-warning.png)

如果您要建立多個值，可以使用大量上傳一次新增所有值。 選取 ![加號圖示](../images/ui/segment-builder/plus-icon.png) 以顯示 **[!UICONTROL 大量新增值]** 彈出視窗。

![加號圖示會反白顯示，顯示您可以選取以存取大量上傳彈出視窗的按鈕。](../images/ui/segment-builder/add-bulk-values.png)

於 **[!UICONTROL 大量新增值]** 彈出視窗，您可以上傳CSV或TSV檔案。

![此時會顯示「大量新增值」彈出視窗。 您可以選取來上傳CSV或TSV檔案的對話方塊會反白顯示。](../images/ui/segment-builder/bulk-values-popover.png)

或者，您也可以手動新增逗號分隔的值。

![此時會顯示「大量新增值」彈出視窗。 可用來插入值和新增值的對話方塊都會反白顯示。](../images/ui/segment-builder/bulk-values-comma-separated.png)

請注意，最多允許250個值。 如果超過此數量，則必須先移除一些值，才能新增更多值。

![系統會顯示警告，指出您已達到值的數量上限。](../images/ui/segment-builder/maximum-values.png)

### 新增對象

您可以從「 」拖放對象 **[!UICONTROL 對象]** 定位至規則產生器畫布，以參照新區段定義中的對象成員資格。 這可讓您在新的區段規則中，以屬性的形式包含或排除對象成員資格。

對象 [!DNL Platform] 使用建立的對象 [!DNL Segment Builder]，您可以選擇將受眾轉換為該受眾的區段定義中所使用的規則集。 此轉換會複製規則邏輯，然後修改而不會影響原始區段定義。 在將區段定義轉換為規則邏輯之前，請確定您已儲存對區段定義所做的任何最近變更。

>[!NOTE]
>
>從外部來源新增對象時，只會參考對象成員資格。 您無法將對象轉換為規則，因此用於建立原始對象的規則無法在新的區段定義中修改。

![此影像說明如何將對象屬性轉換為規則。](../images/ui/segment-builder/add-audience-to-segment.png)

如果將對象轉換為規則時發生任何衝突， [!DNL Segment Builder] 會儘量保留現有選項。

### 程式碼檢視

或者，您也可以檢視在中建立的規則之程式碼型版本。 [!DNL Segment Builder]. 在規則產生器畫布中建立規則後，您可以選取 **[!UICONTROL 程式碼檢視]** 以PQL形式檢視您的區段。

![程式碼檢視按鈕會反白顯示，讓您以PQL檢視區段。](../images/ui/segment-builder/code-view.png)

程式碼檢視提供了一個按鈕，可讓您複製要用於API呼叫中的區段值。 若要取得最新版本的區段，請確定您已儲存對區段進行的最新變更。

![系統會醒目提示「複製代碼」按鈕，讓您可以 ](../images/ui/segment-builder/copy-code.png)

### 聚合函数

中的彙總 [!DNL Segment Builder] 是一組XDM屬性的計算，其資料型別是數字（雙精度或整數）。 區段產生器中支援的四個彙總函式為SUM、AVERAGE、MIN和MAX。

若要建立彙總函式，請從左側邊欄選取事件，然後將其插入 [!UICONTROL 事件] 容器。

![事件區段會反白顯示。](../images/ui/segment-builder/events.png)

將事件放入「事件」容器內後，選取省略符號圖示(...)，然後選取 **[!UICONTROL 彙總]**.

![彙總文字會反白顯示。 選取此項可讓您選取彙總函式。](../images/ui/segment-builder/add-aggregation.png)

現在已新增彙總。 您現在可以選取彙總函式、選擇要彙總的屬性、相等函式以及值。 在以下範例中，即使每次購買少於$100，此區段仍會限定購買值總和大於$100的任何設定檔。

![事件規則，顯示彙總函式。](../images/ui/segment-builder/filled-aggregation.png)

### 計數函式 {#count-functions}

區段產生器中的計數函式可用來尋找指定的事件，並計算完成事件的次數。 區段產生器支援的計數函式為「最少」、「最多」、「完全符合」、「介於」和「全部」。

若要建立計數函式，請從左側邊欄選取事件，然後將其插入至 [!UICONTROL 事件] 容器。

![事件欄位會反白顯示。](../images/ui/segment-builder/events.png)

將事件放入事件容器內後，選取 [!UICONTROL 至少1] 按鈕。

![「至少」會反白顯示，顯示要選取的區域以檢視計數函式的完整清單。](../images/ui/segment-builder/add-count.png)

現在已新增count函式。 您現在可以選取count函式及函式值。 以下範例將包含具有至少一次點按的任何事件。

![計數函式的清單隨即顯示並反白顯示。](../images/ui/segment-builder/select-count.png)

## 容器

區段規則會依照其列出順序進行評估。 容器可讓您透過使用巢狀查詢來控制執行順序。

將至少一個圖磚新增至規則產生器畫布後，您就可以開始新增容器。 若要建立新容器，請選取圖磚右上角的省略符號(...)，然後選取 **[!UICONTROL 新增容器]**.

![「新增容器」按鈕會反白顯示，讓您新增容器作為第一個容器的子系。](../images/ui/segment-builder/add-container.png)

新容器會顯示為第一個容器的子系，但您可以拖曳和移動容器來調整階層。 容器的預設行為是&quot;[!UICONTROL 包含]」屬性、事件或提供的對象。 您可以將規則設為&quot;[!UICONTROL 排除]「 」設定檔只要選取「 」，就能符合容器條件 **[!UICONTROL 包含]** 並選取「[!UICONTROL 排除]「。

您也可以擷取子容器，並在內嵌新增至父容器，方法是在子容器上選取「解除容器包裝」。 選取子容器右上角的省略符號(...)以存取此選項。

![可讓您取消包裝或刪除容器的選項會反白顯示。](../images/ui/segment-builder/include-exclude.png)

一旦您選取 **[!UICONTROL 解除容器包裝]** 子容器隨即移除，條件隨即內嵌顯示。

>[!NOTE]
>
>展開容器時，請留意邏輯是否持續符合所需的區段定義。

![容器在展開後顯示。](../images/ui/segment-builder/unwrapped-container.png)

## 合併原則

[!DNL Experience Platform] 可讓您彙集來自多個來源的資料並將其合併，以便檢視每個個別客戶的完整檢視。 彙總此資料時，合併原則是指 [!DNL Platform] 使用來決定資料的優先順序以及將合併哪些資料以建立設定檔。

您可以為此對象選取符合您行銷目的的合併原則，或使用提供的預設合併原則 [!DNL Platform]. 您可以建立組織專屬的多個合併原則，包括建立自己的預設合併原則。 如需為貴組織建立合併原則的逐步指示，請先閱讀 [合併原則概觀](../../profile/merge-policies/overview.md).

若要為您的區段定義選取合併原則，請選取 **[!UICONTROL 欄位]** 標籤，然後使用 **[!UICONTROL 合併原則]** 下拉式選單，以選取您要使用的合併原則。

![合併原則選擇器會反白顯示。 這可讓您選擇要為區段定義選取的合併原則。](../images/ui/segment-builder/merge-policy-selector.png)

## 区段属性 {#segment-properties}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_segmentproperties"
>title="区段属性"
>abstract="区段属性部分显示生成的区段的大小估计值，并显示合格配置文件的数量与配置文件总数的比较情况。这允许您在构建受众本身之前根据需要调整区段定义。"

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_refreshestimate"
>title="刷新估计值"
>abstract="您可以刷新区段的估计值，以立即预览符合建议区段的资格的配置文件数目。受众估计值是通过使用当天的示例数据的示例大小生成的。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/tutorials/create-a-segment.html?lang=zh-Hans#estimate-and-preview-an-audience" text="估计和预览受众"

建立區段定義時， **[!UICONTROL 區段屬性]** 工作區右側的區段會顯示結果區段大小的預估值，可讓您在建立受眾本身之前根據需要調整區段定義。

此 **[!UICONTROL 區段屬性]** 區段也是您可以指定有關區段定義的重要資訊的地方，包括其名稱、說明和評估型別。 區段定義名稱是用來在組織所定義的區段中識別您的區段，因此應該是描述性、簡潔且唯一的。

在繼續建立區段定義時，您可以選取「 」，檢視分頁的對象預覽 **[!UICONTROL 檢視設定檔]**.

![區段定義屬性區段會反白顯示。 區段屬性包括但不限於區段名稱、說明和評估方法。](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>受众估计值是通过使用当天的示例数据的示例大小生成的。如果您的個人資料存放區中的實體少於100萬個，則會使用完整的資料集；對於100萬到2,000萬個之間的實體，會使用100萬個實體；而對於2,000萬個以上的實體，則會使用全部實體的5%。 如需有關產生區段預估的詳細資訊，請參閱 [預估產生區段](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 區段建立教學課程的內容。

您也可以選取評估方法。 如果您知道要使用的評估方法，可以使用下拉式清單選取所需的評估方法。 如果您想知道此區段符合哪些評估型別，可以選取瀏覽圖示 ![放大鏡的資料夾圖示](../images/ui/segment-builder/segment-evaluation-select-icon.png) 檢視可用區段評估方法的清單。

此 [!UICONTROL 評估方法資格] 彈出視窗隨即顯示。 此彈出視窗會顯示可用的評估方法，包括批次、串流和邊緣。 彈出視窗會顯示符合資格和不符合資格的評估方法。 根據您在區段定義中使用的引數，它可能不符合某些評估方法的資格。 如需每種評估方法需求的詳細資訊，請參閱 [串流細分](./streaming-segmentation.md#query-types) 或 [邊緣細分](./edge-segmentation.md#query-types) 概述。

![評估方法適用性快顯視窗會出現。 這會顯示哪些區段評估方法適用於該區段，哪些方法不適用。](../images/ui/segment-builder/select-evaluation-method.png)

如果您選取無效的評估方法，系統會提示您變更區段定義規則或變更評估方法。

![評估方法隨即出現。 如果選取了不符合資格的區段評估方法，彈出式視窗會說明它不符合資格的原因。](../images/ui/segment-builder/ineligible-evaluation-method.png)

如需不同區段定義評估方法的詳細資訊，請參閱 [區段概述](../home.md#evaluate-segments).

## 后续步骤 {#next-steps}

區段產生器提供豐富的工作流程，讓您能從以下專案隔離適銷對象： [!DNL Real-Time Customer Profile] 資料。 閱讀本指南後，您現在應該能夠：

- 使用屬性、事件和現有對象的組合作為建置組塊，以建立區段定義。
- 使用規則產生器畫布和容器可控制區段規則的執行順序。
- 檢視潛在對象的預估值，讓您視需要調整區段定義。
- 啟用已排程區段的所有區段定義。
- 啟用串流區段的指定區段定義。

若要深入瞭解 [!DNL Segmentation Service]，請繼續閱讀檔案，並觀看相關影片以補充您的學習。 若要進一步瞭解 [!DNL Segmentation Service] UI，請閱讀 [[!DNL Segmentation Service] 使用手冊](./overview.md)
