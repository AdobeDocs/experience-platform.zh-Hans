---
title: TikTok連線
description: 使用您的資料在TikTok上建立自訂對象，以使用您的廣告促銷活動進行目標定位。 這些對象可能是造訪過您的網站或與您的內容互動的人。 使用Adobe與TikTok Ads Manager的即時整合，快速且安全地從Adobe Experience Platform推送所需的區段至TikTok。
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---

# TikTok連線

## 概述 {#overview}

使用您的資料在TikTok上建立自訂對象，以使用您的廣告促銷活動進行目標定位。 這些對象可能是造訪過您的網站或與您的內容互動的人。 使用Adobe與TikTok Ads Manager的即時整合，快速且安全地從Adobe Experience Platform推送所需的區段至TikTok。 造訪 [TikTok的業務說明中心](https://ads.tiktok.com/help/article/audiences?lang=en) 以取得詳細資訊。

>[!IMPORTANT]
>
>此檔案頁面是由TikTok團隊建立。 如有任何查詢或更新請求，請直接聯絡他們： [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## 用例 {#use-cases}

為協助您更清楚瞭解應如何使用TikTok目的地以及何時使用，以下是Adobe Experience Platform客戶的範例使用案例。

### 用例 {#use-case-1}

運動服裝品牌想要透過其社群媒體帳戶觸及現有客戶。 服飾品牌可以從自己的CRM擷取電子郵件地址至Adobe Experience Platform、從自己的離線資料建立區段，並將這些區段傳送至TikTok，以便在客戶的社群媒體摘要中顯示廣告。

## 先决条件 {#prerequisites}

將資料傳送至您的之前 [!DNL TikTok Ads Manager] 帳戶，您需要授予Adobe Experience Platform許可權才能存取您的廣告帳戶 `Audience Management`. 您可以在Experience Platform中輸入您的廣告商ID，並依照重新導向以授予許可權，即可提供此許可權。 如需詳細指示，請參閱 [TikTok API檔案](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## 支援的身分 {#supported-identities}

TikTok支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google廣告ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分識別是IDFA名稱空間時，請選取IDFA目標身分。 |
| 电话号码 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼，且必須採用E.164格式。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| 电子邮件 | 使用SHA256演演算法雜湊處理的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，以及TikTok目的地中使用的識別碼（名稱、電話號碼或其他）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

若要驗證至目的地，系統會將您重新導向以登入 [!DNL TikTok Ads Manager] 帳戶並授權Adobe代表您管理對象。

![TikTok許可權選擇](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "用於選取許可權的TikTok UI影像")

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

![目的地連線詳細資料](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Platform UI的影像，顯示要填寫的目的地連線詳細資訊")

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL TikTok Ads管理員ID]**：您的 [!DNL TikTok Ads Manager ID]. 您可以在以下位置找到此專案： [!DNL TikTok Ads manager] 帳戶。

![TikTok Ads管理員ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok Ads Manager UI的影像，顯示如何取得TikTok Ads Manager ID")

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 映射身份 {#map}

以下是將區段匯出至TikTok Ads Manager時的正確身分對應範例。

選取來源欄位：

* 選取識別碼(例如：` Email_LC_SHA256`)作為來源身分，可在Adobe Experience Platform中唯一識別設定檔，以及 [!DNL TikTok Ads Manager].

選取目標欄位：

* 選取電子郵件名稱空間作為目標身分。

![身分對應](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Platform UI影像，身分對應")

## 匯出的資料 {#exported-data}

檢查您的 [!DNL TikTok Ads Manager] 帳戶(在 **「資產」>「對象」**)，驗證您的Experience Platform區段是否已成功匯出。 對象將會填入為對象型別： `Partner Audience`.

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請閱讀 [資料控管概觀](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

請參閱 [TikTok說明中心頁面](https://ads.tiktok.com/help/article/audiences?lang=en) 以取得其他資訊。
