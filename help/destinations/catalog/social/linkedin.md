---
keywords: linkedin連線；linkedin連線；linkedin目的地；linkedin；
title: Linkedin相符受眾連線
description: 根據雜湊電子郵件，為您的LinkedIn行銷活動啟用設定檔，以用於對象目標定位、個人化和抑制。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 2%

---

# [!DNL LinkedIn Matched Audiences] 連線

## 概述 {#overview}

為您的啟動設定檔 [!DNL LinkedIn] 根據雜湊電子郵件和行動ID針對對象鎖定目標、個人化和抑制的促銷活動。

![Adobe Experience Platform UI中的LinkedIn目的地](../../assets/catalog/social/linkedin/catalog.png)

## 用例

協助您更清楚瞭解使用的方法和時機 [!DNL LinkedIn Matched Audiences] 目的地，以下是Adobe Experience Platform客戶可使用此功能解決的使用案例。

軟體公司會組織會議並希望與參與者保持聯絡，並根據其會議出席狀態向他們顯示個人化優惠。 公司可從自己的電子郵件地址或行動裝置ID擷取 [!DNL CRM] 移入Adobe Experience Platform。 然後，他們可以使用自己的離線資料建立區段，並將這些區段傳送至 [!DNL LinkedIn] 社交平台，最佳化廣告支出。

## 支援的身分 {#supported-identities}

[!DNL LinkedIn Matched Audiences] 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| GAID | Google廣告ID | 當您的來源身分是GAID名稱空間時，選取此目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分識別是IDFA名稱空間時，請選取此目標身分。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊處理的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 請依照 [ID比對需求](#id-matching-requirements-id-matching-requirements) 區段並使用適當的名稱空間，分別用於純文字和雜湊電子郵件。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，而這些成員具有「 」中使用的識別碼（名稱、電話號碼及其他）。 [!DNL LinkedIn Matched Audiences] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## linkedIn帳戶必要條件 {#LinkedIn-account-prerequisites}

開始使用 [!UICONTROL linkedIn相符的受眾] 目的地，確認您的 [!DNL LinkedIn Campaign Manager] 帳戶具有 [!DNL Creative Manager] 許可權層級或以上。

若要瞭解如何編輯您的 [!DNL LinkedIn Campaign Manager] 使用者許可權，請參閱 [新增、編輯和移除Advertising帳戶的使用者許可權](https://www.linkedin.com/help/lms/answer/5753) (位於LinkedIn檔案中)。

## ID比對需求 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 要求不會明確傳送任何個人識別資訊(PII)。 因此，啟用的對象 [!DNL LinkedIn Matched Audiences] 可以關閉 *雜湊* 識別碼，例如電子郵件地址或行動裝置ID。

根據您擷取至Adobe Experience Platform的ID型別，您必須遵守其對應的要求。

## 電子郵件雜湊需求 {#email-hashing-requirements}

您可以將電子郵件地址雜湊後再擷取至Adobe Experience Platform，或使用Experience Platform中清楚的電子郵件地址，並擁有 [!DNL Platform] 在啟動時進行雜湊。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱 [批次擷取概觀](/help/ingestion/batch-ingestion/overview.md) 和 [串流擷取概觀](/help/ingestion/streaming-ingestion/overview.md).

如果您選擇自行雜湊電子郵件地址，請務必符合下列要求：

* 修剪電子郵件字串中的所有前導和尾端空格。 例如： `johndoe@example.com`，非 `<space>johndoe@example.com<space>`；
* 雜湊電子郵件字串時，請務必雜湊小寫字串；
   * 範例： `example@email.com`，非 `EXAMPLE@EMAIL.COM`；
* 確認雜湊字串全部為小寫
   * 範例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，非 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`；
* 請勿對字串加鹽。

>[!NOTE]
>
>來自未雜湊名稱空間的資料會自動透過雜湊處理 [!DNL Platform] 啟用時。
> 屬性來源資料不會自動雜湊。
> 
> 期間 [身分對應](../../ui/activate-segment-streaming-destinations.md#mapping) 步驟，當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。
> 
> 此 **[!UICONTROL 套用轉換]** 選項只有在您選取屬性作為來源欄位時才會顯示。 選擇名稱空間時不會顯示。

![身分對應轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

以下影片也會示範設定 [!DNL LinkedIn Matched Audiences] 目的地和啟用區段。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform使用者介面經常更新，自從錄製此影片後，可能有所變更。 如需最新資訊，請參閱 [目的地設定教學課程](../../ui/connect-destination.md).

### 驗證至目的地 {#authenticate}

1. 尋找 [!DNL LinkedIn Matched Audiences] 目的地目錄中的目的地，然後選取 **[!UICONTROL 設定]**.
2. 選取 **[!UICONTROL 連線到目的地]**.
   ![向LinkedIn進行驗證](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. 輸入您的LinkedIn認證，然後選取 **登入**.

### 填寫目的地詳細資料 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="帐户 ID"
>abstract="您的 LinkedIn Campaign 管理器帐户 ID。您可以在 LinkedIn Campaign 管理器帐户中找到此 ID。"

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：您的 [!DNL LinkedIn Campaign Manager Account ID]. 此ID可在以下網址找到： [!DNL LinkedIn Campaign Manager] 帳戶。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用串流區段匯出目的地的受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## 匯出的資料 {#exported-data}

成功啟用意味著 [!DNL LinkedIn] 自訂對象將以程式設計方式建立於 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). 由於使用者符合或不符合啟用的區段的資格，因此將會新增及移除對象中的區段會籍。

>[!TIP]
>
>Adobe Experience Platform與的整合 [!DNL LinkedIn Matched Audiences] 支援歷史受眾回填。 所有歷史區段資格都會傳送至 [!DNL LinkedIn] 當您對目的地啟用區段時。
