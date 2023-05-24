---
keywords: 啟用設定檔要求目的地；啟用資料；設定檔要求目的地
title: 將受眾資料啟用至設定檔請求目的地
type: Tutorial
description: 瞭解如何將區段對應至設定檔請求目的地，以啟用您在Adobe Experience Platform中的受眾資料。
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: f771cf0c9ea692ad02cf987608b3710772712d54
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 4%

---

# 將受眾資料啟用至設定檔請求目的地

>[!IMPORTANT]
> 
> * 若要啟用資料並啟用 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> * 若要在不透過 [對應步驟](#mapping) 的工作流程中，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用區段而不進行對應]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions).
> 
> 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

## 概述 {#overview}

本文說明在Adobe Experience Platform設定檔要求目的地啟用對象資料所需的工作流程。 搭配使用時 [邊緣細分](../../segmentation/ui/edge-segmentation.md)，這些目的地會在您的網頁和行動屬性上啟用相同頁面和下一頁個人化使用案例。 深入瞭解 [啟用相同頁面和下一頁個人化使用案例](/help/destinations/ui/configure-personalization-destinations.md).

設定檔請求目的地的範例包括 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化](../../destinations/catalog/personalization/custom-personalization.md) 連線。

## 先决条件 {#prerequisites}

若要啟用目的地的資料，您必須已成功 [已連線至目的地](./connect-destination.md). 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的個人化目的地，並設定您要使用的目的地。

### 區段合併原則 {#merge-policy}

目前，設定檔請求目的地僅支援啟用使用 [主動邊緣合併原則](../../segmentation/ui/segment-builder.md#merge-policies) 設定為預設值。

## 選取您的目的地 {#select-destination}

1. 前往 **[!UICONTROL 連線>目的地]**，然後選取 **[!UICONTROL 目錄]** 標籤。

   ![目的地目錄標籤](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 選取 **[!UICONTROL 啟用區段]** 對應至您要啟用區段之個人化目的地的卡片上，如下圖所示。

   ![啟動按鈕](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 選取您要用來啟用區段的目的地連線，然後選取 **[!UICONTROL 下一個]**.

   ![選取目的地](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 移至下一區段至 [選取您的區段](#select-segments).

## 選取您的區段 {#select-segments}

使用區段名稱左邊的核取方塊來選取您要啟用至目的地的區段，然後選取 **[!UICONTROL 下一個]**.

![選取區段](../assets/ui/activate-profile-request-destinations/select-segments.png)

## (Beta)對應屬性 {#map-attributes}

>[!IMPORTANT]
>
>對應步驟，可針對以下專案啟用以屬性為基礎的個人化： [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [通用個人化目的地](/help/destinations/catalog/personalization/custom-personalization.md)，目前為測試版，貴組織可能尚未提供存取權。 本檔案內容可能會有變動。

選取您想要根據為使用者啟用個人化使用案例的屬性。 這表示如果屬性的值變更或將屬性新增至設定檔，該設定檔將成為區段的成員，並將啟動至個人化目的地。

新增屬性為選用，您仍可繼續進行下一個步驟，並在不選取屬性的情況下啟用相同頁面和下一頁個人化。 如果您未在此步驟中新增任何屬性，仍會根據設定檔的區段會籍和身分對應資格進行個人化。

![顯示已選取屬性之對應步驟的影像](../assets/ui/activate-profile-request-destinations/mapping-step.png)

### 選取來源屬性 {#select-source-attributes}

若要新增來源屬性，請選取 **[!UICONTROL 新增欄位]** 控制 **[!UICONTROL 來源欄位]** 欄並搜尋或導覽至您所需的XDM屬性欄位，如下所示。

![顯示如何在對應步驟中選取目標屬性的熒幕錄製](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

### 選取目標屬性 {#select-target-attributes}

>[!NOTE]
>
>有些目的地會要求您僅選取來源屬性，而有些目的地則同時要求來源和目標屬性。
>
>目前， [Adobe Target V2](../catalog/personalization/adobe-target-connection.md) 目的地只需要來源屬性，而 [使用屬性自訂個人化](../catalog/personalization/custom-personalization.md) 需要來源和目標屬性。

若要新增目標屬性，請選取 **[!UICONTROL 新增欄位]** 控制 **[!UICONTROL 目標欄位]** 欄並輸入您要對應來源屬性的自訂屬性名稱。

![熒幕錄製，顯示如何在對應步驟中選取XDM屬性](../assets/ui/activate-profile-request-destinations/mapping-step-select-target-attribute.gif)

## 排程區段匯出 {#scheduling}

根據預設， [!UICONTROL 區段排程] 頁面僅顯示您在目前啟用流程中選擇的新選取區段。

![新區段](../assets/ui/activate-profile-request-destinations/new-segments.png)

若要檢視所有啟用至目的地的區段，請使用篩選選項並停用 **[!UICONTROL 僅顯示新區段]** 篩選。

![所有區段](../assets/ui/activate-profile-request-destinations/all-segments.png)

於 **[!UICONTROL 區段排程]** 頁面，選取每個區段，然後使用 **[!UICONTROL 開始日期]** 和 **[!UICONTROL 結束日期]** 選取器，設定傳送資料至目的地的時間間隔。

![區段排程](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

選取 **[!UICONTROL 下一個]** 前往 [!UICONTROL 檢閱] 頁面。

## 请查看 {#review}

於 **[!UICONTROL 檢閱]** 頁面中，您可以看到選取範圍的摘要。 選取 **[!UICONTROL 取消]** 若要分解流量， **[!UICONTROL 返回]** 修改您的設定，或 **[!UICONTROL 完成]** 以確認您的選擇並開始傳送資料至目的地。

![稽核步驟中的選取專案摘要。](../assets/ui/activate-profile-request-destinations/review.png)

### 同意原則評估 {#consent-policy-evaluation}

如果您的组织购买了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，请选择&#x200B;**[!UICONTROL 查看适用的同意策略]**&#x200B;以查看应用了哪些同意策略以及作为其结果包含在激活中的配置文件数量。閱讀關於 [同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 以取得詳細資訊。

### 資料使用原則檢查 {#data-usage-policy-checks}

在 **[!UICONTROL 檢閱]** 步驟，Experience Platform也會檢查是否有任何資料使用原則違規。 以下是違反原則的範例。 您必須先解決違規，才能完成區段啟用工作流程。 如需有關如何解決原則違規的資訊，請閱讀關於 [資料使用原則違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) （位於資料控管檔案區段）。

![資料原則違規](../assets/common/data-policy-violation.png)

### 过滤区段 {#filter-segments}

此外，在此步驟中，您可以使用頁面上的可用篩選器，只顯示其排程或對應已隨著此工作流程而更新的區段。 您也可以切換要檢視的表格欄。

![熒幕錄製，顯示稽核步驟中可用的區段篩選器。](/help/destinations/assets/ui/activate-profile-request-destinations/filter-segments-review-step.gif)

如果您對您的選擇感到滿意，並且未偵測到任何原則違規，請選取 **[!UICONTROL 完成]** 以確認您的選擇並開始傳送資料至目的地。

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->