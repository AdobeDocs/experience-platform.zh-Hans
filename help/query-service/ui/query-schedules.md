---
title: 查詢排程
description: 瞭解如何自動執行排定的查詢、刪除或停用查詢排程，以及透過Adobe Experience Platform UI利用可用的排程選項。
exl-id: 984d5ddd-16e8-4a86-80e4-40f51f37a975
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# 查詢排程

您可以透過建立查詢排程來自動執行查詢。 排程的查詢會在自訂節奏上執行，以根據頻率、日期和時間管理您的資料。 您也可以視需要選擇結果的輸出資料集。 已儲存為範本的查詢可以從「查詢編輯器」排程。

>[!IMPORTANT]
>
>以下是使用「查詢編輯器」時排程查詢的限制清單。 它們不適用於 [!DNL Query Service] API：<br/>您只能將排程新增至已建立、儲存和執行的查詢。<br/>您 **無法** 將排程新增至引數化查詢。<br/>排定的查詢 **無法** 包含匿名區塊。

任何已排程的查詢都會新增至 [!UICONTROL 排定的查詢] 標籤。 您可以從該工作區透過UI監控所有已排程查詢工作的狀態。 於 [!UICONTROL 排定的查詢] 索引標籤可讓您找到有關查詢執行的重要資訊，並訂閱警示。 可用的資訊包括狀態、排程詳細資料，以及執行失敗時的錯誤訊息/代碼。 請參閱 [監視排定的查詢檔案](./monitor-queries.md) 以取得詳細資訊。

## 建立查詢排程 {#create-schedule}

若要將排程新增至查詢，請從 [!UICONTROL 範本] 標籤或 [!UICONTROL 排定的查詢] 索引標籤以導覽至「查詢編輯器」。

若要瞭解如何使用API新增排程，請參閱 [排程查詢端點指南](../api/scheduled-queries.md).

從「查詢編輯器」存取已儲存的查詢時， [!UICONTROL 時程表] 索引標籤會顯示在查詢名稱下方。 選取 **[!UICONTROL 時程表]**.

![反白顯示「排程」標籤的「查詢編輯器」。](../images/ui/query-schedules/schedules-tab.png)

排程工作區隨即顯示。 選取 **[!UICONTROL 新增排程]** 以建立排程。

![「查詢編輯器排程」工作區中反白了新增排程。](../images/ui/query-schedules/add-schedule.png)

便會顯示「排程詳細資訊」頁面。 您可以在此頁面選取排定查詢的頻率、開始和結束日期、排定查詢在一週中執行的日期，以及要將查詢匯出到的資料集。

![「排程詳細資料」面板會反白顯示。](../images/ui/query-schedules/schedule-details.png)

您可以選擇下列選項 **[!UICONTROL 頻率]**：

- **[!UICONTROL 每小時]**：排定的查詢將在您選取的日期範圍內每小時執行一次。
- **[!UICONTROL 每日]**：排定的查詢將在您選擇的時間和日期期間每X天執行一次。 請注意，選取的時間為 **UTC**，而不是您的當地時區。
- **[!UICONTROL 每週]**：選取的查詢將在您選取的一週、時間和日期時段執行。 請注意，選取的時間為 **UTC**，而不是您的當地時區。
- **[!UICONTROL 每月]**：選取的查詢會在您選取的日期、時間和日期期間每個月執行。 請注意，選取的時間為 **UTC**，而不是您的當地時區。
- **[!UICONTROL 每年]**：選取的查詢每年都會在您選取的日期、月、時間和日期期間執行。 請注意，選取的時間為 **UTC**，而不是您的當地時區。

對於輸出資料集，您可以選擇使用現有資料集或建立新資料集。

>[!IMPORTANT]
>
> 由於您使用現有資料集或建立新資料集，因此您會 **not** 需要包含 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 做為查詢的一部分，因為資料集已設定。 包括 `INSERT INTO` 或 `CREATE TABLE AS SELECT` 作為您排程查詢的一部分，將導致錯誤。

確認所有這些詳細資料後，請選取 **[!UICONTROL 儲存]** 以建立排程。 您會回到顯示新建立之排程詳細資訊的排程工作區，包括排程ID、排程本身以及排程的輸出資料集。 您可以使用排程ID來查閱排程查詢本身執行的詳細資訊。 若要進一步瞭解，請閱讀 [已排程查詢執行端點指南](../api/runs-scheduled-queries.md).

![已反白新建立排程的排程工作區。](../images/ui/query-schedules/schedules-workspace.png)

## 刪除或停用排程 {#delete-schedule}

您可以從排程工作區刪除或停用排程。 您必須從以下任一項中選取查詢範本： [!UICONTROL 範本] 標籤或 [!UICONTROL 排定的查詢] 索引標籤以導覽至「查詢編輯器」並選取 **[!UICONTROL 排程]** 以存取排程工作區。

從可用排程的列選取排程。 您可以使用切換來停用或啟用排定的查詢。

>[!IMPORTANT]
>
>您必須先停用排程，才能刪除查詢的排程。

選取 **[!UICONTROL 刪除排程]** 刪除已停用的排程。

![反白顯示「停用排程」和「刪除」排程的排程工作區。](../images/ui/query-schedules/delete-schedule.png)
