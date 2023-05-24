---
keywords: 啟用區段串流目的地；啟用區段串流目的地；啟用資料
title: 啟用串流區段匯出目的地的受眾資料
type: Tutorial
description: 瞭解如何將區段對應至區段串流目的地，以啟用您在Adobe Experience Platform中的受眾資料。
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 8%

---

# 啟用串流區段匯出目的地的受眾資料

>[!IMPORTANT]
> 
> * 若要啟用資料並啟用 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> * 若要在不透過 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用區段而不進行對應]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> 
> 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

## 概述 {#overview}

本文說明在Adobe Experience Platform區段串流目的地啟用受眾資料所需的工作流程。

## 先决条件 {#prerequisites}

若要啟用目的地的資料，您必須已成功 [已連線至目的地](./connect-destination.md). 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地並設定您要使用的目的地。

## 選取您的目的地 {#select-destination}

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![目的地目錄標籤](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 選取 **[!UICONTROL 啟用區段]** 對應至您要啟用區段之目的地的卡片上，如下圖所示。

   ![啟動按鈕](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. 選取您要用來啟用區段的目的地連線，然後選取 **[!UICONTROL 下一個]**.

   ![選取目的地](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. 移至下一區段至 [選取您的區段](#select-segments).

## 選取您的區段 {#select-segments}

使用區段名稱左邊的核取方塊來選取您要啟用至目的地的區段，然後選取 **[!UICONTROL 下一個]**.

![選取區段](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## 對應屬性和身分 {#mapping}

>[!IMPORTANT]
>
>此步驟僅適用於某些區段串流目的地。 如果您的目的地沒有 **[!UICONTROL 對應]** 步驟，跳至 [排程區段匯出](#scheduling).

有些區段串流目的地會要求您選取來源屬性或身分名稱空間，以將目的地中的身分對應為目標身分。

1. 在 **[!UICONTROL 對應]** 頁面，選取 **[!UICONTROL 新增對應]**.

   ![新增對應](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. 選取右側的箭頭 **[!UICONTROL 來源欄位]** 登入點。

   ![選取來源欄位](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. 在 **[!UICONTROL 選取來源欄位]** 頁面，使用 **[!UICONTROL 選取屬性]** 或 **[!UICONTROL 選取身分名稱空間]** 可在兩種可用來源欄位類別之間切換的選項。 從可用的 [!DNL XDM] 設定檔屬性和身分名稱空間，選取您要對應至目的地的設定檔屬性，然後選擇 **[!UICONTROL 選取]**.

   ![選取來源欄位頁面](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. 選取「 」右側的按鈕 **[!UICONTROL 目標欄位]** 登入點。

   ![選取目標欄位](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. 在 **[!UICONTROL 選取目標欄位]** 頁面，選取您要對應來源欄位的目標身分名稱空間，然後選擇 **[!UICONTROL 選取]**.

   ![選取目標欄位頁面](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. 若要新增更多對應，請重複步驟1至5。

### 应用转换 {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="应用转换"
>abstract="使用未进行哈希处理的源字段时选中此选项，让 Adobe Experience Platform 在激活时自动对它们进行哈希处理。"

將未雜湊的來源屬性對應至目的地預期會雜湊的目標屬性時(例如： `email_lc_sha256` 或 `phone_sha256`)，檢查 **套用轉換** 讓Adobe Experience Platform在啟動時自動雜湊來源屬性的選項。

![身分對應](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 排程區段匯出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="结束日期"
>abstract="无法添加区段计划的结束日期。"

根據預設， [!UICONTROL 區段排程] 頁面僅顯示您在目前啟用流程中選擇的新選取區段。

![新區段](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

若要檢視所有啟用至目的地的區段，請使用篩選選項並停用 **[!UICONTROL 僅顯示新區段]** 篩選。

![所有區段](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. 於 **[!UICONTROL 區段排程]** 頁面，選取每個區段，然後使用 **[!UICONTROL 開始日期]** 和 **[!UICONTROL 結束日期]** 選取器，設定傳送資料至目的地的時間間隔。

   ![區段排程](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * 有些目的地會要求您選取 **[!UICONTROL 對象來源]** 對於每個區段，使用行事曆選擇器下方的下拉式選單。 如果您的目的地不包含此選擇器，請略過此步驟。

      ![映射 ID](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * 有些目的地需要您手動對應 [!DNL Platform] 區段與目標目的地中的對應區段。 若要這麼做，請選取每個區段，然後在中輸入目的地平台中對應的區段ID **[!UICONTROL 對應ID]** 欄位。 如果您的目的地不包含此欄位，請略過此步驟。

      ![映射 ID](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * 有些目的地會要求您輸入 **[!UICONTROL 應用程式ID]** 啟用時 [!DNL IDFA] 或 [!DNL GAID] 區段。 如果您的目的地不包含此欄位，請略過此步驟。

      ![应用程序 ID](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. 選取 **[!UICONTROL 下一個]** 前往 [!UICONTROL 檢閱] 頁面。

## 请查看 {#review}

於 **[!UICONTROL 檢閱]** 頁面中，您可以看到選取範圍的摘要。 選取 **[!UICONTROL 取消]** 若要分解流量， **[!UICONTROL 返回]** 修改您的設定，或 **[!UICONTROL 完成]** 以確認您的選擇並開始傳送資料至目的地。

![稽核步驟中的選取專案摘要。](/help/destinations/assets/ui/activate-segment-streaming-destinations/review.png)

### 同意原則評估 {#consent-policy-evaluation}

如果您的组织购买了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，请选择&#x200B;**[!UICONTROL 查看适用的同意策略]**&#x200B;以查看应用了哪些同意策略以及作为其结果包含在激活中的配置文件数量。閱讀關於 [同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 以取得詳細資訊。

### 資料使用原則檢查 {#data-usage-policy-checks}

在 **[!UICONTROL 檢閱]** 步驟，Experience Platform也會檢查是否有任何資料使用原則違規。 以下是違反原則的範例。 您必須先解決違規，才能完成區段啟用工作流程。 如需有關如何解決原則違規的資訊，請閱讀關於 [資料使用原則違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) （位於資料控管檔案區段）。

![資料原則違規](../assets/common/data-policy-violation.png)

### 过滤区段 {#filter-segments}

此外，在此步驟中，您可以使用頁面上的可用篩選器，只顯示其排程或對應已隨著此工作流程而更新的區段。 您也可以切換要檢視的表格欄。

![熒幕錄製，顯示稽核步驟中可用的區段篩選器。](/help/destinations/assets/ui/activate-segment-streaming-destinations/filter-segments-review-step.gif)

如果您對您的選擇感到滿意，並且未偵測到任何原則違規，請選取 **[!UICONTROL 完成]** 以確認您的選擇並開始傳送資料至目的地。

## 驗證區段啟用 {#verify}

檢查 [目的地監視檔案](../../dataflows/ui/monitor-destinations.md) 有關如何監控流向目的地的資料流的詳細資訊。

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
