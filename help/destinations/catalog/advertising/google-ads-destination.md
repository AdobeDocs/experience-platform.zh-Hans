---
keywords: Google ads；google ads；google adwords；Google AdWords；Google Adwords
title: Google Ads連線
description: Google Ads (舊稱為Google AdWords)是一項線上廣告服務，可讓企業在文字搜尋、圖形顯示、YouTube影片和應用程式內行動顯示等專案中，透過每次點按付費進行廣告。
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 7d32499bec8d7248472ae60b07893dbb5496d984
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 2%

---

# [!DNL Google Ads] 連線

## 概述 {#overview}

[!DNL Google Ads]，先前稱為 [!DNL Google AdWords]，是一項線上廣告服務，可讓企業在各種文字搜尋、圖形顯示 [!DNL YouTube] 視訊和應用程式內行動顯示。

## 目的地詳情 {#specifics}

請注意以下專屬於的詳細資訊 [!DNL Google Ads] 目的地：

* 啟用的對象是以程式設計方式建立於 [!DNL Google] 平台。
* [!DNL Platform] 目前不包含用於驗證成功啟用的測量量度。 請參考Google中的對象計數，以驗證整合併瞭解對象鎖定目標大小。

>[!IMPORTANT]
>
>如果您想要使用建立您的第一個目的地 [!DNL Google Ads] 且尚未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 若是過去的Experience CloudID服務(使用Audience Manager或其他應用程式)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前在Audience Manager中設定Google整合，則您設定的ID同步會結轉到Platform。

## 支援的身分 {#supported-identities}

[!DNL Google Ad Manager] 支援下表所述的身分啟用。

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當您的來源身分是GAID名稱空間時，選取此目標身分。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當您的來源身分識別是IDFA名稱空間時，請選取此目標身分。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也稱為 [!DNL Device ID]. 38位數的裝置ID，Audience Manager會與每個與其互動的裝置建立關聯。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hans) 目標鎖定加州的使用者，以及所有其他使用者的Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 使用此ID來鎖定加州以外的使用者。 |
| RIDA | 適用於廣告的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| MAID | Microsoft Advertising ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire電視。 |  |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在將區段（受眾）的所有成員匯出至Google目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先决条件 {#prerequisites}

### 現有 [!DNL Google Ads] 帳戶

>[!IMPORTANT]
>
> [!DNL Google] 已棄用新的 [!DNL Google Ads] Cookie與協力廠商的整合。 為了執行下一節中的允許清單步驟，您必須與現有的整合 [!DNL Google Ads]. 因此，建議使用 [!DNL Google Ads] 正在設定 [!DNL Google Customer Match] 整合。 有關建立詳細資訊 [!DNL Google Customer Match] 整合，請閱讀有關建立 [[!DNL Google Customer Match]](./google-customer-match.md) 連線。

### 允許清單 {#allow-listing}

>[!NOTE]
>
>必須先允許清單，才能設定您的第一個 [!DNL Google Ads] Platform中的目的地。 請確定以下說明的允許清單程式已由 [!DNL Google] 建立目的地之前。
>此規則的例外情況是 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 客戶。 如果您已在Audience Manager中建立與此Google目的地的連線，則不需要再次進行允許清單程式，您可以繼續後續步驟。

建立之前 [!DNL Google Ads] Platform中的目的地，您必須聯絡 [!DNL Google] ，以便將Adobe放入允許的資料提供者清單中，並將您的帳戶新增至允許清單中。 連絡人 [!DNL Google] 並提供下列資訊：

* **帳戶ID**：Adobe的帳戶ID與Google。 帳戶ID：87933855。
* **客戶ID**：Adobe的客戶帳戶ID與Google。 客戶ID：89690775。
* 您的帳戶型別： **AdWords**
* **Google AdWords ID**：這是您的ID，包含 [!DNL Google]. ID格式通常為123-456-7890。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊：

* **[!UICONTROL 名稱]**：填寫此目的地的偏好名稱。
* **[!UICONTROL 說明]**：選擇性。 例如，您可以提及要將此目的地用於哪個行銷活動。
* **[!UICONTROL 帳戶型別]**： AdWords是唯一可用的選項。
* **[!UICONTROL 帳戶ID]**：使用填入您的帳戶ID [!DNL Google Ads]. ID格式通常為123-456-7890。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用串流區段匯出目的地的受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## 匯出的資料

驗證資料是否已成功匯出至 [!DNL Google Ads] 目的地，檢查您的 [!DNL Google Ads] 帳戶。 如果成功啟用，系統會將對象填入您的帳戶。

## 故障排除 {#troubleshooting}

### 400 Bad Request錯誤訊息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合 [必備條件](#prerequisites) 或客戶嘗試設定沒有現有目的地時 [!DNL Google Ads] 帳戶。

[!DNL Google] 已棄用新的 [!DNL Google Ads] Cookie與協力廠商的整合。 若要執行 [允許清單](#allow-listing) 步驟，您必須與現有的整合 [!DNL Google Ads].

使用的建議方法 [!DNL Google Ads] 正在設定 [[!DNL Google Customer Match]](google-customer-match.md) 整合。
