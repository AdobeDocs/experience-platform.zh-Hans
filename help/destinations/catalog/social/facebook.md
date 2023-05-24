---
keywords: facebook連線；facebook連線；facebook目的地；facebook；instagram；messenger；facebook messenger
title: facebook連線
description: 為您的Facebook行銷活動啟用設定檔，以根據雜湊電子郵件進行對象目標定位、個人化和抑制。
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 70670f7aec2ab6a5594f5e69672236c7bcc3ce81
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 6%

---

# [!DNL Facebook] 連線

## 概述 {#overview}

為您的啟動設定檔 [!DNL Facebook] 根據雜湊電子郵件進行對象目標定位、個人化和抑制的行銷活動。

您可以使用此目的地來定位整個領域的對象 [!DNL Facebook’s] 支援的應用程式系列 [!DNL Custom Audiences]，包括 [!DNL Facebook]， [!DNL Instagram]， [!DNL Audience Network]、和 [!DNL Messenger]. [!DNL Facebook Ads Manager] 中的版面级别会显示您要针对其运行营销活动的所选应用程序。

![Adobe Experience Platform UI中的Facebook目的地](../../assets/catalog/social/facebook/catalog.png)

## 用例

協助您更清楚瞭解使用的方法和時機 [!DNL Facebook] 目的地，以下是Adobe Experience Platform客戶可以使用此功能解決的兩個範例使用案例。

### 使用案例#1

線上零售商想要透過社交平台觸及現有客戶，並根據他們先前的訂單向他們顯示個人化優惠。 線上零售商可以從其CRM擷取電子郵件地址至Adobe Experience Platform、從自己的離線資料建立區段，並將這些區段傳送至 [!DNL Facebook] 社交平台，最佳化廣告支出。

### 使用案例#2

航空公司有不同的客戶層級（銅級、銀級和金級），並希望透過社交平台為每個層級提供個人化優惠。 不過，並非所有客戶都使用航空公司的行動應用程式，其中有些客戶尚未登入公司網站。 公司對這些客戶擁有的唯一識別碼是會員ID和電子郵件地址。

若要在社群媒體上鎖定他們，他們可以使用電子郵件地址作為識別碼，將客戶資料從其CRM載入Adobe Experience Platform。

接著，他們可以使用離線資料（包括相關聯的會籍ID和客戶階層），建立新的受眾區段，並透過 [!DNL Facebook] 目的地。

## 支援的身分 {#supported-identities}

[!DNL Facebook Custom Audiences] 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google廣告ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分識別是IDFA名稱空間時，請選取IDFA目標身分。 |
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 請依照 [ID比對需求](#id-matching-requirements-id-matching-requirements) 區段並使用適當的名稱空間，分別用於純文字和雜湊電話號碼。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊處理的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 請依照 [ID比對需求](#id-matching-requirements-id-matching-requirements) 區段，並針對純文字和雜湊電子郵件地址分別使用適當的名稱空間。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| extern_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，選取此目標身分。 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，以及Facebook目的地中使用的識別碼（名稱、電話號碼或其他）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## facebook帳戶必要條件 {#facebook-account-prerequisites}

將受眾區段傳送至之前 [!DNL Facebook]，確認您符合下列需求：

* 您的 [!DNL Facebook] 使用者帳戶必須具備 **[!DNL Manage campaigns]** 已為您計畫使用的廣告帳戶啟用許可權。
* 此 **Adobe Experience Cloud** 必須將商業帳戶新增為中的廣告合作夥伴 [!DNL Facebook Ad Account]. 使用 `business ID=206617933627973`。另請參閱 [新增合作夥伴至您的業務經理](https://www.facebook.com/business/help/1717412048538897) 詳細資訊，請參閱Facebook檔案。
   >[!IMPORTANT]
   >
   > 設定Adobe Experience Cloud的許可權時，您必須啟用 **管理行銷活動** 許可權。 以下專案需要許可權： [!DNL Adobe Experience Platform] 整合。
* 閱讀並簽署 [!DNL Facebook Custom Audiences] 服務條款。 若要這麼做，請前往 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID].
   >[!IMPORTANT]
   >
   >簽署時 [!DNL Facebook Custom Audiences] 服務條款，請務必使用您在Facebook API中驗證時所用的相同使用者帳戶。

## ID比對需求 {#id-matching-requirements}

[!DNL Facebook] 要求不會明確傳送任何個人識別資訊(PII)。 因此，啟用的對象 [!DNL Facebook] 可以關閉 *雜湊* 識別碼，例如電子郵件地址或電話號碼。

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。

## 電話號碼雜湊需求 {#phone-number-hashing-requirements}

啟用電話號碼的方法有兩種 [!DNL Facebook]：

* **擷取原始電話號碼**：您可以將原始電話號碼擷取至 [!DNL E.164] 格式為 [!DNL Platform]. 它們會在啟動時自動執行雜湊處理。 如果選擇此選項，請務必將原始電話號碼擷取到 `Phone_E.164` 名稱空間。
* **擷取雜湊電話號碼**：您可以在擷取到之前預先雜湊您的電話號碼 [!DNL Platform]. 如果選擇此選項，請務必將雜湊電話號碼擷取至 `Phone_SHA256` 名稱空間。

>[!NOTE]
>
>內嵌到中的電話號碼 `Phone` 名稱空間無法在中啟動 [!DNL Facebook].

## 電子郵件雜湊需求 {#email-hashing-requirements}

您可以將電子郵件地址雜湊後再擷取至Adobe Experience Platform，或使用Experience Platform中清楚的電子郵件地址，並擁有 [!DNL Platform] 在啟動時進行雜湊。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱 [批次擷取概觀](/help/ingestion/batch-ingestion/overview.md) 和 [串流擷取概觀](/help/ingestion/streaming-ingestion/overview.md).

如果您選擇自行雜湊電子郵件地址，請務必符合下列要求：

* 修剪電子郵件字串中的所有前導和尾端空格；例如： `johndoe@example.com`，非 `<space>johndoe@example.com<space>`；
* 雜湊電子郵件字串時，請務必雜湊小寫字串；
   * 範例： `example@email.com`，非 `EXAMPLE@EMAIL.COM`；
* 確認雜湊字串全部為小寫
   * 範例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，非 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`；
* 請勿對字串加鹽。

>[!NOTE]
>
>來自未雜湊名稱空間的資料會自動透過雜湊處理 [!DNL Platform] 啟用時。
> 屬性來源資料不會自動雜湊。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。
> 此 **[!UICONTROL 套用轉換]** 選項只有在您選取屬性作為來源欄位時才會顯示。 選擇名稱空間時不會顯示。

![身分對應轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 使用自訂名稱空間 {#custom-namespaces}

開始使用 `Extern_ID` 要傳送資料的名稱空間 [!DNL Facebook]，確定您使用下列專案同步處理自己的識別碼： [!DNL Facebook Pixel]. 請參閱 [facebook正式檔案](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) 詳細資訊。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

以下影片也會示範設定 [!DNL Facebook] 目的地和啟用區段。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform使用者介面經常更新，自從錄製此影片後，可能有所變更。 如需最新資訊，請參閱 [目的地設定教學課程](../../ui/connect-destination.md).

### 驗證至目的地 {#authenticate}

1. 在目的地目錄中尋找Facebook目的地，然後選取 **[!UICONTROL 設定]**.
2. 選取 **[!UICONTROL 連線到目的地]**.
   ![向Facebook進行驗證](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. 輸入您的Facebook認證，然後選取 **登入**.

### 填寫目的地詳細資料 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="帐户 ID"
>abstract="您的 Facebook 广告帐户 ID。您可以在 Facebook 广告管理器帐户中找到此 ID。在输入此 ID 时，请始终为其添加前缀 `act_`。"

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：您的 [!DNL Facebook Ad Account ID]. 此ID可在以下網址找到： [!DNL Facebook Ads Manager] 帳戶。 在输入此 ID 时，请始终为其添加前缀 `act_`。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="受众来源"
>abstract="选择最初收集区段中的客户数据的方式。当用户被区段定位时，数据将显示在 Facebook 中"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="受众来源"
>abstract="广告商直接从客户那里收集数据。"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="受众来源"
>abstract="广告商直接从合作伙伴那里收集数据。"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="受众来源"
>abstract="广告商直接从客户和合作伙伴那里收集数据。"

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用串流區段匯出目的地的受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

在 **[!UICONTROL 區段排程]** 步驟，您必須提供 [!UICONTROL 對象來源] 將區段傳送至 [!DNL Facebook Custom Audiences].

![facebook對象來源](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### 對應範例：啟用對象資料於 [!DNL Facebook Custom Audience] {#example-facebook}

以下是在中啟用對象資料時的正確身分對應範例 [!DNL Facebook Custom Audience].

選取來源欄位：

* 選取 `Email` 如果您使用的電子郵件地址未進行雜湊處理，則名稱空間會作為來源身分。
* 選取 `Email_LC_SHA256` 名稱空間作為來源身分（如果您在資料擷取時已將客戶電子郵件地址雜湊到） [!DNL Platform]，根據 [!DNL Facebook] [電子郵件雜湊需求](#email-hashing-requirements).
* 選取 `PHONE_E.164` 名稱空間作為來源身分（如果您的資料包含非雜湊電話號碼）。 [!DNL Platform] 將雜湊電話號碼以符合 [!DNL Facebook] 需求。
* 選取 `Phone_SHA256` 名稱空間作為來源身分（如果您在資料擷取時已將電話號碼雜湊至） [!DNL Platform]，根據 [!DNL Facebook] [電話號碼雜湊需求](#phone-number-hashing-requirements).
* 選取 `IDFA` 名稱空間作為來源身分(如果您的資料包含 [!DNL Apple] 裝置ID。
* 選取 `GAID` 名稱空間作為來源身分(如果您的資料包含 [!DNL Android] 裝置ID。
* 選取 `Custom` 名稱空間作為來源身分（如果您的資料包含其他型別的識別碼）。

選取目標欄位：

* 選取 `Email_LC_SHA256` 當來源名稱空間為 `Email` 或 `Email_LC_SHA256`.
* 選取 `Phone_SHA256` 當來源名稱空間為 `PHONE_E.164` 或 `Phone_SHA256`.
* 選取 `IDFA` 或 `GAID` 當來源名稱空間為 `IDFA` 或 `GAID`.
* 選取 `Extern_ID` 當您的來源名稱空間是自訂名稱空間時，名稱空間會作為目標身分。

>[!IMPORTANT]
>
>來自未雜湊名稱空間的資料會自動透過雜湊處理 [!DNL Platform] 啟用時。
> 
>屬性來源資料不會自動雜湊。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。

![身分對應](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 匯出的資料 {#exported-data}

對象 [!DNL Facebook]，成功啟用意味著 [!DNL Facebook] 自訂對象將以程式設計方式建立於 [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). 由於使用者符合或不符合啟用的區段的資格，因此將會新增及移除對象中的區段會籍。

>[!TIP]
>
>Adobe Experience Platform與的整合 [!DNL Facebook] 支援歷史受眾回填。 所有歷史區段資格都會傳送至 [!DNL Facebook] 當您對目的地啟用區段時。

## 故障排除 {#troubleshooting}

### 400 Bad Request錯誤訊息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

當客戶使用新建立的帳戶時，以及 [!DNL Facebook] 許可權尚未啟用。

如果您收到 `400 Bad Request` 遵循中的步驟後的錯誤訊息 [facebook帳戶必要條件](#facebook-account-prerequisites)，請留出數天時間用於 [!DNL Facebook] 許可權將生效。
