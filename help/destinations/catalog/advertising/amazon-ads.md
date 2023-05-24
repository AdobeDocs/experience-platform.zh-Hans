---
title: Amazon Ads
description: Amazon Ads提供一系列選項，協助您為註冊賣家、廠商、圖書廠商、Kindle Direct Publishing (KDP)作者、應用程式開發人員和/或代理商達成廣告目標。 Amazon Ads與Adobe Experience Platform的整合提供與Amazon Ads產品(包括Amazon DSP (ADSP))的全方位整合。 使用者可以在Adobe Experience Platform中使用Amazon Ads目的地，定義廣告商對象，以在Amazon DSP上鎖定和啟用。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---

# （測試版） Amazon Ads連線 {#amazon-ads}

## 概述 {#overview}

Amazon Ads提供一系列選項，協助您為註冊賣家、廠商、圖書廠商、Kindle Direct Publishing (KDP)作者、應用程式開發人員和/或代理商達成廣告目標。

Amazon Ads與Adobe Experience Platform的整合提供與Amazon Ads產品(包括Amazon DSP (ADSP))的全方位整合。 使用者可以在Adobe Experience Platform中使用Amazon Ads目的地，定義廣告商對象，以在Amazon DSP上鎖定和啟用。

此連線支援在以下Amazon Marketplaces中建立受眾： `US`， `CA`， `MX`， `BR`.

>[!IMPORTANT]
>
>此檔案頁面是由 *Amazon Ads* 團隊。 此產品目前為測試版，功能可能會有所變更。 如有任何查詢或更新請求，請直接聯絡他們： *`amc-support@amazon.com`.*

## 用例 {#use-cases}

為了協助您更清楚瞭解應該如何及何時使用 *Amazon Ads* 目的地，以下是Adobe Experience Platform客戶可以使用此目的地來解決的範例使用案例。

### 啟用與定位 {#activation-and-targeting}

此與Amazon DSP的整合可讓Amazon Ads廣告商將廣告商CDP區段從Adobe Experience Platform傳遞至Amazon的DSP，以針對廣告鎖定目標建立廣告商受眾。 可在Amazon DSP中選取正面目標定位和負面目標定位（隱藏）的對象。 此外，透過AmazonMarketing Cloud產生的訊號，廣告商可最佳化其廣告商對象，將對象變更與Amazon DSP同步。

## 先决条件 {#prerequisites}

若要將Amazon Ads連線與Adobe Experience Platform搭配使用，使用者必須先具有Amazon DSP廣告商帳戶的存取權。  若要布建這些例項，請造訪Amazon Ads網站上的下列頁面：

* [開始使用Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## 支援的身分 {#supported-identities}

此 *Amazon Ads* 連線支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md). 如需Amazon Ads支援的身分識別的詳細資訊，請造訪 [Amazon DSP支援中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊處理的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，而這些成員具有「 」中使用的識別碼（名稱、電話號碼或其他）。 *Amazon Ads* 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

若要驗證目的地，請填入必填欄位並選取 **[!UICONTROL 連線到目的地]**.

系統會將您帶至Amazon Ads連線介面，您可在此處先選取想要連線的廣告商帳戶。  連線後，系統會將您重新導向回Adobe Experience Platform，並顯示新連線，以及您選取的廣告商帳戶ID。 在目的地設定畫面上選取適當的廣告商帳戶以繼續。

* **[!UICONTROL 持有人權杖]**：填寫持有人權杖以對目的地進行驗證。

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Amazon Ads廣告商ID]**：選取用於目的地的目標Amazon Ads帳戶ID。

注意：選取此Amazon Ads廣告商ID後，您需要建立新目的地才能變更此專案。 如果您重新驗證OAuth憑證並選取新的廣告商ID，您的變更將不會套用。

![設定新目的地](../../assets/catalog/advertising/amazon_ads_image_1.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 對應屬性和身分 {#map}

Amazon Ads連線支援雜湊電子郵件地址和雜湊電話號碼，以進行身分比對。  以下熒幕擷圖提供與Amazon Ads連線相容的相符範例：

![Adobe至Amazon Ads對應](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 若要對應雜湊電子郵件地址，請選取 `Email_LC_SHA256` 身分名稱空間作為來源欄位。
* 若要對應雜湊電話號碼，請選取 `Phone_SHA256` 身分名稱空間作為來源欄位。
* 若要對應未雜湊的電子郵件地址或電話號碼，請選取對應的身分名稱空間作為來源欄位，並核取 `Apply Transformation` 啟用時讓Platform雜湊身分識別的選項。

強烈建議您儘量對應可用欄位。 如果只有一個來源屬性可用，您可以對應單一欄位。  Amazon Ads目的地會針對對應目的利用所有對應的欄位，如果提供更多欄位，可提供較高的匹配率。 如需所接受識別碼的詳細資訊，請造訪 [Amazon Ads雜湊對象說明頁面](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## 匯出的資料/驗證資料匯出 {#exported-data}

上傳對象後，您可以透過下列步驟驗證對象是否已正確建立及上傳：

**適用於Amazon DSP**

導覽至您的廣告商ID →受眾→廣告商受眾。 如果成功建立受眾且符合受眾成員的最低數量，您將會看到「狀態」 `Active`.  您可以在Amazon DSP使用者介面右側的預測觸及面板中找到有關您的對象人數和觸及率的更多詳細資料。

![Amazon DSP對象建立驗證](../../assets/catalog/advertising/amazon_ads_image_3.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請閱讀 [資料控管概觀](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

如需其他說明檔案，請瀏覽下列Amazon Ads說明資源：

* [Amazon DSP說明中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
