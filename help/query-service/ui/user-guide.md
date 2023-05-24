---
keywords: Experience Platform；首頁；熱門主題；查詢編輯器；查詢編輯器；查詢服務；查詢服務；
solution: Experience Platform
title: 查詢編輯器UI指南
description: 查詢編輯器是Adobe Experience Platform查詢服務提供的互動式工具，可讓您在Experience Platform使用者介面中撰寫、驗證和執行客戶體驗資料的查詢。 查詢編輯器支援開發查詢以進行分析和資料探索，並可讓您執行互動式查詢以進行開發，以及執行非互動式查詢來填入Experience Platform中的資料集。
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: 90829713e85e930e4fd6a32b0dbd38aeb837b84e
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---

# [!DNL Query Editor] UI指南

[!DNL Query Editor] 是Adobe Experience Platform提供的互動式工具 [!DNL Query Service]，可讓您針對內的客戶體驗資料寫入、驗證及執行查詢 [!DNL Experience Platform] 使用者介面。 [!DNL Query Editor] 支援開發查詢以進行分析和資料探索，並可讓您執行互動式查詢以進行開發，以及執行非互動式查詢來填入資料集 [!DNL Experience Platform].

如需有關概念和功能的詳細資訊， [!DNL Query Service]，請參閱 [查詢服務總覽](../home.md). 若要進一步瞭解如何導覽查詢服務使用者介面，請前往 [!DNL Platform]，請參閱 [查詢服務UI總覽](./overview.md).

## 快速入门 {#getting-started}

[!DNL Query Editor] 透過連線至，提供靈活的查詢執行 [!DNL Query Service]，而且只有在此連線作用中時，查詢才會執行。

### 正在連線到 [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] 需要幾秒鐘的時間來初始化並連線到 [!DNL Query Service] 開啟時。 主控台會告訴您何時連線，如下所示。 如果您嘗試在編輯器連線之前執行查詢，則會延遲執行，直到連線完成。

![初次連線時查詢編輯器的主控台輸出。](../images/ui/query-editor/connect.png)

### 查詢的執行方式 [!DNL Query Editor] {#run-a-query}

查詢執行自 [!DNL Query Editor] 以互動方式執行。 這表示如果您關閉瀏覽器或離開瀏覽器，查詢就會被取消。 這也適用於透過查詢輸出產生資料集的查詢。

## 查詢編寫，使用 [!DNL Query Editor] {#query-authoring}

使用 [!DNL Query Editor]，您可以編寫、執行和儲存客戶體驗資料的查詢。 所有執行或儲存的查詢 [!DNL Query Editor] 可供貴組織中的所有使用者使用，並有權存取 [!DNL Query Service].

### 访问 [!DNL Query Editor] {#accessing-query-editor}

在 [!DNL Experience Platform] UI，選取 **[!UICONTROL 查詢]** 在左側導覽選單中開啟 [!DNL Query Service] 工作區。 接下來，選取 **[!UICONTROL 建立查詢]** 以開始撰寫查詢。 此連結可從 [!DNL Query Service] 工作區。

![反白顯示「建立查詢」的查詢工作區概述索引標籤。](../images/ui/query-editor/create-query.png)

### 寫入查詢 {#writing-queries}

[!UICONTROL 查詢編輯器] 組織方式，讓撰寫查詢儘可能容易。 以下熒幕擷圖顯示編輯器在UI中的顯示方式，其中包含SQL輸入欄位和 **播放** 反白顯示。

![「查詢編輯器」中反白顯示SQL輸入欄位和播放。](../images/ui/query-editor/editor.png)

為了將開發時間縮到最短，建議您使用傳回列的限制來開發查詢。 例如：`SELECT fields FROM table WHERE conditions LIMIT number_of_rows`。在您確認查詢產生預期的輸出後，請移除限制並使用執行查詢 `CREATE TABLE tablename AS SELECT` 以使用輸出產生資料集。

### 寫入工具 [!DNL Query Editor] {#writing-tools}

- **自動語法反白顯示：** 使讀取及組織SQL更容易。

![查詢編輯器中的SQL陳述式，示範語法色彩醒目提示。](../images/ui/query-editor/syntax-highlight.png)

- **SQL關鍵字自動完成：** 開始輸入查詢，然後使用方向鍵導覽至所需辭彙，然後按下 **輸入**.

![自動完成下拉式功能表提供查詢編輯器中的選項，提供SQL的幾個字元。](../images/ui/query-editor/syntax-auto.png)

- **表格和欄位自動完成：** 開始輸入您想要的表格名稱 `SELECT` 從中，然後使用方向鍵導覽至您要尋找的表格，然後按下 **輸入**. 選取表格後，自動完成將可識別該表格中的欄位。

![顯示下拉式表格名稱建議的「查詢編輯器」輸入。](../images/ui/query-editor/tables-auto.png)

### 自動完成UI設定切換 {#auto-complete}

此 [!DNL Query Editor] 會在您撰寫查詢時，自動建議可能的SQL關鍵字以及表格或資料行詳細資訊。 自動完成功能預設為啟用，並可透過選取 [!UICONTROL 語法自動完成] 切換至「查詢編輯器」的右上方。

自動完成組態設定是每個使用者設定的，並會在該使用者連續登入時被記住。

![語法自動完成切換的查詢編輯器反白顯示。](../images/ui/query-editor/auto-complete-toggle.png)

停用此功能會停止處理數個中繼資料命令，並提供通常有利於作者編輯查詢之速度的建議。

當您使用切換來啟用自動完成功能時，在短暫的暫停後，即可使用建議的表格和資料行名稱以及SQL關鍵字。 控制檯中「查詢編輯器」下方的成功訊息表示功能處於活動狀態。

如果您停用自動完成功能，則需要重新整理頁面才能讓功能生效。 當您停用「 」時，會出現一個包含三個選項的確認對話方塊 [!UICONTROL 語法自動完成] 切換：

- [!UICONTROL 取消]
- [!UICONTROL 儲存變更並重新整理]
- [!UICONTROL 重新整理而不儲存變更]

>[!IMPORTANT]
>
>如果您在停用此功能時正在撰寫或編輯查詢，則必須在重新整理頁面之前儲存對查詢所做的任何變更，否則所有進度都將遺失。

![用於停用自動完成功能的確認對話方塊。](../images/ui/query-editor/confirmation-dialog.png)

選取適當的選項以停用自動完成功能。

### 錯誤偵測 {#error-detection}

[!DNL Query Editor] 會在您撰寫查詢時自動驗證查詢，提供一般SQL驗證和特定執行驗證。 如果查詢下方出現紅色底線（如下圖所示），表示查詢中的錯誤。

![查詢編輯器輸入顯示紅色底線的SQL表示錯誤。](../images/ui/query-editor/syntax-error-highlight.png)

偵測到錯誤時，您可以暫留在SQL程式碼上來檢視特定的錯誤訊息。

![含有錯誤訊息的對話方塊。](../images/ui/query-editor/linting-error.png)

### 查詢詳細資料 {#query-details}

從中選擇任何已儲存的範本 [!UICONTROL 範本] 索引標籤以在「查詢編輯器」中檢視。 查詢詳細資訊面板提供管理所選查詢的更多資訊和工具。

![反白顯示查詢詳細資訊面板的查詢編輯器。](../images/ui/query-editor/query-details.png)

此面板可讓您直接從UI產生輸出資料集、刪除或命名顯示的查詢，以及向查詢新增排程。

此面板也會顯示有用的中繼資料，例如上次修改查詢的時間及修改者（如適用）。 若要產生資料集，請選取 **[!UICONTROL 輸出資料集]**. 此 **[!UICONTROL 輸出資料集]** 對話方塊隨即顯示。 輸入名稱和說明，然後選取 **[!UICONTROL 執行查詢]**. 新資料集會顯示在 **[!UICONTROL 資料集]** 標籤上的 [!DNL Query Service] 使用者介面於 [!DNL Platform].

### 排定的查詢 {#scheduled-queries}

已儲存為範本的查詢可以從「查詢編輯器」排程。 這可讓您以自訂步調自動執行查詢。 您可以根據頻率、日期和時間排程查詢，並視需要選擇結果的輸出資料集。 您也可以透過UI停用或刪除查詢排程。

排程是從「查詢編輯器」設定的。 以下是使用「查詢編輯器」時排程查詢的限制清單。 它們不適用於 [!DNL Query Service] API：

- 您只能將排程新增至已建立、儲存和執行的查詢。
- 您 **無法** 將排程新增至引數化查詢。
- 排定的查詢 **無法** 包含匿名區塊。

請參閱查詢排程檔案，瞭解如何 [在UI中建立查詢排程](./query-schedules.md). 或者，若要瞭解如何使用API新增排程，請參閱 [排程查詢端點指南](../api/scheduled-queries.md).

任何已排程的查詢都會新增至 [!UICONTROL 排定的查詢] 標籤。 您可以從該工作區透過UI監控所有已排程查詢工作的狀態。 於 [!UICONTROL 排定的查詢] 索引標籤可讓您找到有關查詢執行的重要資訊，並訂閱警示。 可用的資訊包括狀態、排程詳細資料，以及執行失敗時的錯誤訊息/代碼。 請參閱 [監視排定的查詢檔案](./monitor-queries.md) 以取得詳細資訊。

### 儲存查詢 {#saving-queries}

此 [!DNL Query Editor] 提供儲存功能，可讓您儲存查詢並稍後處理。 若要儲存查詢，請選取 **[!UICONTROL 儲存]** 在的右上角 [!DNL Query Editor]. 在儲存查詢之前，必須使用為查詢提供名稱 **[!UICONTROL 查詢詳細資料]** 面板。

>[!NOTE]
>
>使用查詢編輯器命名並儲存在中的查詢在查詢儀表板中作為範本提供 [!UICONTROL 範本] 標籤。 請參閱 [範本檔案](./query-templates.md) 以取得詳細資訊。

### 如何尋找先前的查詢 {#previous-queries}

所有查詢執行自 [!DNL Query Editor] 記錄檔表格中擷取。 您可以在以下位置使用搜尋功能： **[!UICONTROL 記錄]** 索引標籤以尋找查詢執行。 已儲存的查詢會列在 **[!UICONTROL 範本]** 標籤。

如果已排程查詢，則 [!UICONTROL 排定的查詢] 索引標籤透過UI改善這些查詢作業的可見度。 請參閱 [查詢監視檔案](./monitor-queries.md) 以取得詳細資訊。

>[!NOTE]
>
>記錄檔不會儲存未執行的查詢。 為了讓查詢可用於 [!DNL Query Service]，它必須執行或儲存在 [!DNL Query Editor].

## 使用查詢編輯器執行查詢 {#executing-queries}

若要在中執行查詢，請執行下列動作 [!DNL Query Editor]，您可在編輯器中輸入SQL，或從 **[!UICONTROL 記錄]** 或 **[!UICONTROL 範本]** 標籤，然後選取 **播放**. 查詢執行的狀態會顯示在 **[!UICONTROL 主控台]** 標籤，而輸出資料會顯示在 **[!UICONTROL 結果]** 標籤。

### 控制台 {#console}

主控台會提供有關下列專案的狀態和操作的資訊： [!DNL Query Service]. 主控台顯示連線至 [!DNL Query Service]、正在執行的查詢作業，以及因這些查詢而產生的任何錯誤訊息。

![查詢編輯器控制檯的控制檯索引標籤。](../images/ui/query-editor/console.png)

>[!NOTE]
>
>主控台只會顯示執行查詢所產生的錯誤。 它不會在執行查詢之前顯示查詢驗證錯誤。

### 查詢結果 {#query-results}

完成查詢後，結果會顯示在 **[!UICONTROL 結果]** 標籤，在 **[!UICONTROL 主控台]** 標籤。 此檢視顯示查詢的表格輸出，最多可顯示100列。 此檢視可讓您驗證查詢是否產生預期的輸出。 若要使用您的查詢產生資料集，請移除傳回列的限制，然後使用執行查詢 `CREATE TABLE tablename AS SELECT` 以使用輸出產生資料集。 請參閱 [產生資料集教學課程](./create-datasets.md) 以取得有關如何從中的查詢結果產生資料集的指示 [!DNL Query Editor].

![「查詢編輯器」控制檯的「結果」標籤會顯示查詢執行的結果。](../images/ui/query-editor/query-results.png)

## 執行查詢，使用 [!DNL Query Service] 教學課程影片 {#query-tutorial-video}

以下影片說明如何在Adobe Experience Platform介面和PSQL使用者端中執行查詢。 此外，示範如何在XDM物件中使用個別屬性、使用Adobe定義的函式，以及使用CREATE TABLE AS SELECT (CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## 后续步骤

現在您知道有哪些功能可用於 [!DNL Query Editor] 以及如何導覽應用程式，您可以直接在中開始編寫自己的查詢 [!DNL Platform]. 如需對中的資料集執行SQL查詢的詳細資訊 [!DNL Data Lake]，請參閱以下內容的相關指南： [正在執行查詢](../best-practices/writing-queries.md).
