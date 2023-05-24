---
title: Adobe Advertising Cloud DSP連線
description: Adobe Advertising Cloud DSP是Adobe Real-time Customer Data Platform的整合式目的地，可讓您與核准的廣告商和使用者共用已驗證的第一方區段，以啟用行銷活動。
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---

# Adobe Advertising Cloud DSP連線

## 概述 {#overview}

Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP)目的地可讓您與核准的廣告商和使用者共用已驗證的第一方區段，以便透過DSP啟用行銷活動。 若要進一步瞭解Real-Time CDP與DSP的整合，請參閱 [關於從受眾來源啟用已驗證的區段](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>此頁面由DSP團隊建立。 如有任何查詢或更新請求，請直接聯絡Advertising Cloud支援： `adcloud_support@adobe.com`.

## 用例 {#use-cases}

為協助您更清楚瞭解如何使用Advertising Cloud DSP目的地，以下是Adobe Experience Platform客戶可使用此目的地解決的範例使用案例。

### 品牌廣告使用案例

一家線上零售商想要透過展示行銷活動重新鎖定其高價值客戶，而不使用Cookie進行目標定位。 零售商會共用一個區段，該區段包含其高價值客戶從其Adobe Real-time Customer Data Platform (Real-Time CDP)帳戶至其DSP帳戶的雜湊電子郵件ID。 然後DSP會將雜湊電子郵件ID轉換為已驗證 [!DNL RampIDs] 透過DSP與LiveRamp之間的合作關係。 產生的結果 [!DNL RampIDs] 可用於顯示行銷活動，以鎖定對象。

### 機構使用案例

擁有DSP帳戶的媒體代理商正代表其客戶（旅館業中的頂級品牌）執行重新目標定位行銷活動。 該品牌想要以新的促銷優惠重新鎖定去年所有訪客。 品牌代管所有來賓資訊 [!DNL Real-Time CDP]. 品牌可共用區段，該區段包含其來賓來自的雜湊電子郵件ID [!DNL Real-Time CDP] 帳號至媒體代理程式的DSP帳戶，以透過媒體促銷活動重新鎖定來賓。

## 先决条件 {#prerequisites}

* 啟用區段共用的DSP帳戶層級和促銷活動層級設定 [!DNL LiveRamp RampID]，可將客戶資料轉譯為 [!DNL RampIDs] 以建立可定位的區段。 您的DSP帳戶團隊將執行此設定。 [!DNL RampID] 可透過DSP與之間的合作夥伴關係取得 [!DNL LiveRamp]，而且您不需要自己的 [!DNL LiveRamp] 使用它的成員資格。
* Experience Platform帳戶的Experience Cloud組織ID。 您可以在以下網址找到您的ID： [!DNL Real-Time CDP] 使用者設定檔頁面。
* A [[!DNL Real-Time CDP] DSP中的來源](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) 以接收促銷活動啟用的區段。 您的DSP帳戶團隊將使用您的Experience Cloud組織ID建立來源。
* DSP帳戶或廣告商的來源金鑰，產生條件為 [[!DNL Real-Time CDP] 來源是在DSP中建立](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). 您的DSP帳戶團隊將會與您共用此金鑰。 在Experience Platform中，您將使用此外掛程式來建立與Advertising Cloud DSP目的地的目的地連線，如下所示 [說明如下](#authenticate).
* 由電子郵件或雜湊電子郵件組成的客戶資料。

## 支援的身分 {#supported-identities}

Adobe Advertising Cloud DSP目的地支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| email_lc_sha256 | 使用SHA256演演算法雜湊處理的電子郵件地址 | Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 讓Experience Platform在啟動時自動雜湊資料的選項。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，而這些區段具有Advertising Cloud DSP目的地使用的識別碼（電子郵件或雜湊電子郵件）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 當根據區段評估在Experience Platform中更新設定檔時，聯結器會將更新向下傳送至目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions) 用於Experience Platform。 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線到目的地，請依照指示執行 [建立目的地連線](/help/destinations/ui/connect-destination.md) 使用Experience Platform使用者介面。 在目標設定工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

若要連線到目的地，請在 [!UICONTROL 連線型別] 區段，然後選取 **[!UICONTROL 連線到目的地]**.：

* **[!UICONTROL 帳戶或廣告商金鑰]**：這個 [!UICONTROL 來源金鑰] 產生於 [[!DNL Real-Time CDP] 來源是在DSP使用者介面中建立](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). 您的DSP帳戶團隊會在建立來源後，與您共用此金鑰。

![連線型別欄位](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。

![目的地詳細資料欄位](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## 驗證資料匯出 {#exported-data}

若要確認資料區段已與Advertising Cloud共用，請檢查下列專案：

* 資料在您的 [!DNL Real-Time CDP] 目的地成功。

* 在DSP中，當您從建立或編輯對象時，可使用區段 [!UICONTROL 受眾] > [!UICONTROL 所有對象] 或從 [!UICONTROL 對象目標定位] 位置設定的區段。 區段應會顯示在 [!UICONTROL Adobe區段] 標籤下的 [!UICONTROL Real-Time CDP] 資料夾。

![DSP對象設定中的Real-Time CDP區段](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
