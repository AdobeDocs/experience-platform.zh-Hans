---
keywords: 廣告；必應；
title: Microsoft Bing連線
description: 透過Microsoft Bing連線目的地，您可以在Microsoft顯示廣告中執行重新定位以及以受眾為目標的數位行銷活動。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: aec9708680c2a4cb3c70af12f95c67ec37b2e129
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 8%

---

# [!DNL Microsoft Bing] 連線 {#bing-destination}

## 概述 {#overview}

此 [!DNL Microsoft Bing] 目的地可協助您將設定檔資料傳送至 [!DNL Microsoft Display Advertising].

若要將設定檔資料傳送至 [!DNL Microsoft Bing]，您必須先連線至目的地。

## 用例 {#use-cases}

身為行銷人員，我想能夠使用以下專案建立的區段： [!DNL Microsoft Advertising IDs] 透過顯示廣告定位使用者 [!DNL Microsoft Advertising] 管道。

## 支援的身分 {#supported-identities}

[!DNL Microsoft Bing] 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 |
|---|---|
| MAID | Microsoft廣告ID |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

**[!DNL Segment Export]**  — 您正在將區段（對象）的所有成員匯出至 [!DNL Microsoft Bing] 目的地。

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在將區段（受眾）的所有成員匯出至 [!DNL Microsoft Bing] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

>[!IMPORTANT]
>
>如果您想要使用建立您的第一個目的地 [!DNL Microsoft Bing] 且尚未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 若是過去的Experience CloudID服務(使用Adobe Audience Manager或其他應用程式)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已設定 [!DNL Microsoft Bing] Audience Manager中的整合，您所設定的ID同步會結轉到Platform。

設定目的地時，您必須提供下列資訊：

* [!UICONTROL 帳戶ID]：這是您的 [!DNL Bing Ads CID]，以整數格式顯示。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊：

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：您的 [!DNL Bing Ads Customer ID] (CID)。 您的CID是整數，在您登入時可在URL中找到 [!DNL Microsoft Advertising].

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="映射 ID"
>abstract="输入要将所选区段映射到的数字 Bing 区段 ID。如果提供的[!UICONTROL 映射 ID] 未与 Bing 目标中的区段 ID 相对应，您将不会在 Bing 帐户中看到预期受众数据。"

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用串流區段匯出目的地的受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

在 [區段排程](../../ui/activate-segment-streaming-destinations.md#scheduling) 步驟，您必須手動對應 [!UICONTROL 對應ID] 欄位。 這可確保區段中繼資料可正確傳遞至 [!DNL Bing].

![顯示區段排程畫面的UI影像，其中包含如何將區段名稱對應至Bing對應ID的範例。](../../assets/catalog/advertising/bing/mapping-id.png)

## 匯出的資料 {#exported-data}

驗證資料是否已成功匯出至 [!DNL Microsoft Bing] 目的地，檢查您的 [!DNL Microsoft Bing Ads] 帳戶。 如果成功啟用，系統會將對象填入您的帳戶。
