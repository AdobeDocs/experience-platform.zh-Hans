---
title: （測試版）使用Experience PlatformUI隨選將檔案匯出至批次目的地
type: Tutorial
description: 瞭解如何使用Experience PlatformUI隨選將檔案匯出至批次目的地。
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 8%

---

# （測試版）使用Experience PlatformUI隨選將檔案匯出至批次目的地

>[!IMPORTANT]
>
>此 **[!UICONTROL 立即匯出檔案]** Adobe Experience Platform中的選專案前為Beta版。 檔案和功能可能會有所變更。
>請聯絡您的Adobe代表以取得此功能的存取權。

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

## **[!UICONTROL 立即匯出檔案]** 概觀 {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="立即导出文件"
>abstract="选择此控件可交付完整文件导出以及任何之前计划的导出。将立即触发文件导出，并获取 Experience Platform 分段运行的最新结果。"

本文說明如何使用Experience PlatformUI，隨選將檔案匯出至批次目的地，例如 [雲端儲存空間](/help/destinations/catalog/cloud-storage/overview.md) 和 [電子郵件行銷](/help/destinations/catalog/email-marketing/overview.md) 目的地。

此 **[!UICONTROL 立即匯出檔案]** 控制項可讓您匯出完整的檔案，而不會中斷先前排程區段的目前匯出排程。 此匯出除了先前排程的匯出之外還會進行，不會變更區段的匯出頻率。 将立即触发文件导出，并获取 Experience Platform 分段运行的最新结果。

您也可以將Experience Platform API用於此目的。 閱讀如何 [透過Ad Hoc Activation API依需求對批次目的地啟用對象區段](/help/destinations/api/ad-hoc-activation-api.md).

## 先决条件 {#prerequisites}

若要隨選將檔案匯出至批次目的地，您必須已成功完成 [已連線至目的地](./connect-destination.md). 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地並設定您要使用的目的地。

## 如何隨選匯出檔案 {#how-to-export-files-on-demand}

1. 前往 **[!UICONTROL 連線>目的地]**，選取 **[!UICONTROL 瀏覽]** 標籤和篩選符號來顯示與所需批次目的地的現有連線。

   ![反白顯示如何前往瀏覽標籤並篩選現有資料流的影像。](../assets/ui/activate-on-demand/browse-tab.png)

2. 選取您需要的目的地連線，以檢查到目的地的現有資料流。

   ![反白篩選資料流的影像。](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. 選取 **[!UICONTROL 啟用資料]** 標籤並選取您要隨選匯出檔案的區段，然後選取 **[!UICONTROL 立即匯出檔案]** 控制以觸發一次性匯出，將檔案傳送到批次目的地。

   >[!IMPORTANT]
   >
   >UI目前不支援選取多個區段來隨選大量匯出檔案。 使用 [臨機啟動API](/help/destinations/api/ad-hoc-activation-api.md) 為此目的。

   ![反白顯示「立即匯出檔案」按鈕的影像。](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. 選取 **[!UICONTROL 是]** 以確認並觸發檔案匯出。

   ![此影像顯示立即匯出檔案確認對話方塊。](../assets/ui/activate-on-demand/confirm-activation.png)

5. 確認訊息隨即顯示，讓您知道檔案匯出已開始。

   ![顯示成功隨選啟用的確認影像。](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. 您也可以切換至 **[!UICONTROL 資料流執行]** 索引標籤以確認檔案匯出已啟動。

## 注意事项 {#considerations}

使用時，請牢記以下注意事項 **[!UICONTROL 立即匯出檔案]** 控制：

* **[!UICONTROL 立即匯出檔案]** 僅適用於批次啟用資料流中的排程與目前日期重疊的區段。 這包括排程沒有結束日期(匯出頻率 **[!UICONTROL 一次]**)，或尚未超過結束日期時。
* 將區段新增至現有資料流時，請等候至少15分鐘，直到使用 **[!UICONTROL 立即匯出檔案]** 控制。
* 如果您變更區段的合併原則，或如果您建立的區段使用新的合併原則，請等待24小時，直到使用 **[!UICONTROL 立即匯出檔案]** 控制。

## UI錯誤訊息 {#ui-error-messages}

使用時 **[!UICONTROL 立即匯出檔案]** 控制，您可能會遇到下列任何錯誤訊息。 請檢閱表格以瞭解如何在它們出現時加以處理。

| 错误消息 | 解决方法 |
|---------|----------|
| 已為區段執行 `segment ID` 訂購 `dataflow ID` 具有執行id `flow run ID` | 此錯誤訊息指出區段的隨選啟用流程目前正在進行中。 再次觸發啟動工作之前，請等待工作完成。 |
| 區段 `<segment name>` 不是此資料流的一部分或超出排程範圍！ | 此錯誤訊息指出您選取要啟動的區段未對應至資料流，或是為區段設定的啟動排程已過期或尚未開始。 檢查區段是否確實對應至資料流，並確認區段啟用排程與目前日期重疊。 |

## 相關資訊 {#related-information}

* [使用Experience PlatformAPI依需求啟用批次目的地的受眾區段](/help/destinations/api/ad-hoc-activation-api.md)
* [啟用對象資料以批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md)
