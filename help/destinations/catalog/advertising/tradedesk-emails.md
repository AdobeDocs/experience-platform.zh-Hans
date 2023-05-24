---
title: (Beta)交易平台 — CRM連線
description: 對您的交易台帳戶啟用設定檔，以根據CRM資料進行受眾目標定位和隱藏。
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---

# (Beta) [!DNL Trade Desk] - CRM連線

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] Platform中的目的地目前為測試版。 檔案和功能可能會有所變更。
>
>隨著EUID (European Unified ID)的推出，您現在可以看到兩個 [!DNL The Trade Desk - CRM] 中的目的地 [目的地目錄](/help/destinations/catalog/overview.md).
>* 若您的資料來源是歐盟，請使用 **[!DNL The Trade Desk - CRM (EU)]** 目的地。
>* 如果您在APAC或NAMER地區取得資料，請使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目的地。
>
>Experience Platform中的兩個目的地目前都處於測試階段。 此檔案頁面是由 *[!DNL Trade Desk]* 團隊。 如有任何查詢或更新請求，請聯絡您的 [!DNL Trade Desk] 代表，說明檔案和功能可能會有所變更。

## 概述 {#overview}

本檔案旨在協助您啟用設定檔至 [!DNL Trade Desk] 根據CRM資料進行對象鎖定和隱藏的帳戶。

[!DNL The Trade Desk(TTD)] 不會隨時直接處理電子郵件地址的上傳檔案，也不會 [!DNL The Trade Desk] 儲存您的原始（未雜湊）電子郵件。

>[!TIP]
>
>使用 [!DNL The Trade Desk] CRM資料對應的CRM目的地，例如電子郵件或雜湊電子郵件地址。 使用 [其他交易台目的地](/help/destinations/catalog/advertising/tradedesk.md) Adobe Experience Platform目錄中的Cookie和裝置ID對應。

## 先决条件 {#prerequisites}

在您可以啟用區段至 [!DNL The Trade Desk]，您必須聯絡 [!DNL The Trade Desk] 帳戶管理員以簽署CRM入門合約。 [!DNL The Trade Desk] 然後會授予許可權並共用您的廣告商ID以設定您的目的地。

## ID比對需求 {#id-matching-requirements}

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。 請閱讀 [身分名稱空間總覽](/help/identity-service/namespaces.md) 以取得詳細資訊。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk] 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 請依照ID比對需求一節中的指示，針對純文字和雜湊電子郵件地址分別使用適當的名稱空間。

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 電子郵件地址（純文字） | 輸入 `email` 當您的來源身分是電子郵件名稱空間或屬性時，作為目標身分。 |
| Email_LC_SHA256 | 電子郵件地址需要使用SHA256和小寫進行雜湊處理。 請務必遵循下列任一選項 [電子郵件標準化](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) 規則為必填。 您稍後將無法變更此設定。 | 輸入 `hashed_email` 當您的來源身分是Email_LC_SHA256名稱空間或屬性時，作為目標身分。 |

{style="table-layout:auto"}

## 電子郵件雜湊需求 {#hashing-requirements}

您可以在電子郵件地址擷取到Adobe Experience Platform前加以雜湊處理，或使用原始電子郵件地址。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請閱讀 [批次擷取概觀](/help/ingestion/batch-ingestion/overview.md).

如果您選擇自行雜湊電子郵件地址，請務必符合下列要求：

* 移除開頭和結尾的空格。
* 將所有ASCII字元轉換為小寫。
* 在 `gmail.com` 電子郵件地址，從電子郵件地址的使用者名稱部分移除下列字元：
   * 句點(. （ASCII代碼46）。 例如，標準化 `jane.doe@gmail.com` 至 `janedoe@gmail.com`.
   * 加號(+ （ASCII代碼43）)和所有後續字元。 例如，標準化 `janedoe+home@gmail.com` 至 `janedoe@gmail.com`.

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，其中包含交易台目的地使用的識別碼（電子郵件或雜湊電子郵件）。 |
| 匯出頻率 | **[!UICONTROL 每日批次]** | 由於設定檔會根據區段評估在Experience Platform中更新，因此設定檔（身分）會每天更新一次，以流向目的地平台。 深入瞭解 [批次匯出](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

### 驗證至目的地 {#authenticate}

[!DNL The Trade Desk] CRM目的地是每日批次檔案上傳，不需要使用者驗證。

### 填寫目的地詳細資訊 {#fill-in-details}

您必須先設定與您自己的目的地平台的連線，才能將對象資料傳送或啟用至目的地。 當 [設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 您必須提供下列資訊：

* **[!UICONTROL 帳戶型別]**：請選擇 **[!UICONTROL 現有帳戶]** 選項。
* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 廣告商ID]**：您的 [!DNL Trade Desk Advertiser ID]，可由您的 [!DNL Trade Desk] 帳戶管理員或位於以下位置： [!DNL Advertiser Preferences] 在 [!DNL Trade Desk] UI。

![顯示如何填寫目的地詳細資料的Platform UI熒幕擷圖。](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

連線到目的地時，設定資料治理原則是完全選用的。 請檢閱Experience Platform [資料控管概觀](/help/data-governance/policies/overview.md) 以取得更多詳細資料。

## 啟用此目的地的區段 {#activate}

讀取 [啟用對象資料以批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md) 以取得啟用目的地受眾區段的指示。

在 **[!UICONTROL 排程]** 頁面上，您可以為要匯出的每個區段設定排程和檔案名稱。 必須設定排程，但可選擇是否設定檔案名稱。

![用於排程區段啟用的平台UI熒幕擷圖。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>所有已啟用的區段 [!DNL The Trade Desk] CRM目的地會自動設定為每日頻率和完整檔案匯出。

![用於排程區段啟用的平台UI熒幕擷圖。](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

在 **[!UICONTROL 對應]** 頁面，您必須從來源資料欄選取屬性或身分識別名稱空間，並對應至目標資料欄。

![對應區段啟用的平台UI熒幕擷圖。](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

以下是啟用區段至時的正確身分對應範例 [!DNL The Trade Desk] CRM目的地。

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM目的地不接受原始和雜湊電子郵件地址作為相同啟用流程中的身分。 為原始和雜湊電子郵件地址建立個別的啟用流程。

選取來源欄位：

* 選取 `Email` 如果資料擷取時使用原始電子郵件地址，則名稱空間或屬性會作為來源身分。
* 選取 `Email_LC_SHA256` 如果您在資料擷取至Platform時雜湊了客戶電子郵件地址，請使用名稱空間或屬性作為來源身分。

選取目標欄位：

* 輸入  `email` 當來源名稱空間或屬性為 `Email`.
* 輸入  `hashed_email` 當來源名稱空間或屬性為 `Email_LC_SHA256`.

## 驗證資料匯出 {#validate}

驗證資料是否已正確從Experience Platform匯出並匯入 [!DNL The Trade Desk]，請在Adobe1PD資料拼貼下方找到區段， [!DNL The Trade Desk] 資料管理平台(DMP)。 以下是在中找到對應ID的步驟 [!DNL Trade Desk] UI：

1. 首先，按一下 **[!UICONTROL 資料]** 索引標籤和檢閱 **[!UICONTROL 第一方]**.
2. 向下捲動頁面，在底下 **[!UICONTROL 匯入的資料]**，您會找到 **[!UICONTROL Adobe1PD圖磚]**.
3. 按一下**[!UICONTROL Adobe1PD]圖磚**會列出所有啟用至「 」的區段 [!DNL Trade Desk] 您的廣告商目的地。 您也可以使用搜尋功能。
4. 來自Experience Platform的區段ID #將顯示為 [!DNL Trade Desk] UI。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
