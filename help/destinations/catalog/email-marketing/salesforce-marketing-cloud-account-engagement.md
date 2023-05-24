---
title: SalesforceMarketing Cloud帳戶參與度
description: 瞭解如何使用SalesforceMarketing Cloud帳戶參與（前身為Pardot）目的地匯出您的帳戶資料，並在SalesforceMarketing Cloud帳戶參與中加以啟用，以滿足您的業務需求。
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: 86feee5981aaa81d4c1f97ff8aaf303b2aacd977
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] 連線

使用 [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(先前稱為 [!DNL Pardot])* 擷取、追蹤、評分和評估潛在客戶的目的地。 您也可以透過電子郵件滴漏行銷活動，以及透過培養、評分和行銷活動細分的銷售機會管理，為目標市場細分和客戶群組設計管道所有階段的銷售機會追蹤。

比較對象 [!DNL Salesforce Marketing Cloud Engagement] 更傾向於 **B2C** 行銷， [!DNL Marketing Cloud Account Engagement] 非常適合 **B2B** 涉及多個部門與決策者的使用案例，這些使用案例需要較長的銷售和決策週期。 此外，您也可以與CRM維持更密切的鄰近關係及整合，以做出適當的銷售和行銷決策。 *請注意，Experience Platform也有以下專案的連線： [!DNL Salesforce Marketing Cloud Engagement]，您可在 [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 和 [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 頁面。*

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 可運用 [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) 端點，至 **新增或更新您的銷售機會** 在新的中啟用它們之後 [!DNL Marketing Cloud Account Engagement] 區段。

[!DNL Marketing Cloud Account Engagement] 使用具有授權代碼的OAuth 2通訊協定來驗證 [!DNL Account Engagement] API。 向您的驗證身分的說明 [!DNL Marketing Cloud Account Engagement] 執行個體的詳細資訊如下： [驗證至目的地](#authenticate) 區段。

## 用例 {#use-cases}

為了協助您更清楚瞭解應該如何及何時使用 [!DNL Marketing Cloud Account Engagement] 目的地，以下是Adobe Experience Platform客戶可使用此目的地解決的範例使用案例。

### 傳送電子郵件給行銷活動的聯絡人 {#use-case-send-emails}

線上平台的行銷部門想要將電子郵件行銷活動廣播給B2B潛在客戶的精選對象。 平台的行銷團隊可以透過Adobe Experience Platform新增潛在客戶或更新現有潛在客戶資訊、從自己的離線資料建立區段，並將這些區段傳送至 [!DNL Marketing Cloud Account Engagement]，然後可用於傳送行銷活動電子郵件。

## 先决条件 {#prerequisites}

如需在Experience Platform中設定所需的任何先決條件，請參閱以下章節，並 [!DNL Salesforce] 以及使用之前需要收集的資訊 [!DNL Marketing Cloud Account Engagement] 目的地。

### Experience Platform的必要條件 {#prerequisites-in-experience-platform}

在將資料啟用至 [!DNL Marketing Cloud Account Engagement] 目的地，您必須擁有 [綱要](/help/xdm/schema/composition.md)， a [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立於 [!DNL Experience Platform].

### 中的必要條件 [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

若要將資料從Platform匯出至您的 [!DNL Marketing Cloud Account Engagement] 帳戶：

#### 您需要擁有 [!DNL Marketing Cloud Account Engagement] 帳戶 {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] 訂閱「 」的帳戶 [Marketing Cloud帳戶參與度](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) 產品必須執行才能繼續。

您的 [!DNL Salesforce] 帳戶應具有 [!DNL Salesforce] `Account Engagement Administrator role`. 此為必要項 [建立自訂潛在客戶欄位](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

最後，您的帳戶應該也能夠存取 [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

請聯絡 [[!DNL Salesforce] 支援](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 或您的 [!DNL Salesforce] 帳戶管理員(如果您沒有帳戶，或帳戶遺失 [!DNL Marketing Cloud Account Engagement] 訂閱或 [!DNL Account Engagement Administrator role].

#### 收集 [!DNL Marketing Cloud Account Engagement] 認證 {#gather-credentials}

在驗證之前，請記下以下專案 [!DNL Marketing Cloud Account Engagement] 目的地。

| 認證 | 描述 |
| --- | --- |
| `Username` | 您的 [!DNL Marketing Cloud Account Engagement] 帳戶使用者名稱。 |
| `Password` | 您的 [!DNL Marketing Cloud Account Engagement] 帳戶密碼。 |
| `Account Engagement Business Unit ID` | 若要尋找Account Engagement Business Unit ID，請使用 [!DNL Salesforce]. 在設定中，輸入 *業務單位設定* 在「快速尋找」方塊中。 您的帳戶參與業務單位ID的開頭為 `0Uv` 和長度為18個字元。 如果您無法存取業務單位設定資訊，請詢問您的 [!DNL Salesforce] 帳戶管理員，為您提供 `Account Engagement Business Unit ID`. 如果您需要任何其他指引，請參閱 [[!DNL Salesforce] 驗證](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) 建議頁面。 |

{style="table-layout:auto"}

### 护栏 {#guardrails}

請參閱 [!DNL Marketing Cloud Account Engagement] [速率限制](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) 其中會詳細說明您的計畫所施加的限制，也適用於Experience Platform執行。

>[!IMPORTANT]
>
>若您的 [!DNL Salesforce] 帳戶管理員已限制受信任IP範圍的存取權，您需要聯絡他們以取得 [EXPERIENCE PLATFORMIP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 加入允許清單。 請參閱 [!DNL Salesforce] [限制連線應用程式可信任的IP範圍存取](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 說明檔案（若您需要其他指引）。

## 支援的身分 {#supported-identities}

[!DNL Marketing Cloud Account Engagement] 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 潛在客戶電子郵件地址 | 強制 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | <ul><li>您正在匯出區段的所有成員，以及所需的結構描述欄位 *（例如：電子郵件地址、電話號碼、姓氏）*，根據您的欄位對應。</li><li> 針對Platform中選取的每個區段，將 [!DNL Salesforce Marketing Cloud Account Engagement] 區段狀態會從Platform更新其區段狀態。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

範圍 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**，搜尋 [!DNL Salesforce Marketing Cloud Account Engagement]. 或者，您也可以在 **[!UICONTROL 電子郵件行銷]** 類別。

### 驗證至目的地 {#authenticate}

若要驗證目的地，請選取 **[!UICONTROL 連線到目的地]**. 您將會被導覽至 [!DNL Salesforce] 登入頁面。 輸入您的 [!DNL Marketing Cloud Account Engagement] 帳戶認證並選取 [!DNL Log In].

![顯示如何驗證Marketing Cloud帳戶參與度的平台UI熒幕擷圖。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

接下來，選取 [!UICONTROL 允許] 在後續視窗中授與 **Adobe Experience Platform** 應用程式以存取您的 [!DNL Salesforce Marketing Cloud Account Engagement] 帳戶。 *您只需執行此動作一次*.

![Salesforce應用程式熒幕擷圖確認快顯視窗，可授予Experience Platform應用程式存取Marketing Cloud帳戶參與度的許可權。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

如果提供的詳細資料有效，UI會顯示訊息： *您已成功連線到SalesforceMarketing Cloud帳戶參與帳戶* 訊息和 **[!UICONTROL 已連線]** 狀態，並顯示綠色核取記號，您就可以繼續進行下一個步驟。

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。 請參閱 [收集 [!DNL Marketing Cloud Account Engagement] 認證](#gather-credentials) 區段以取得指引。

![顯示目的地詳細資訊的平台UI熒幕擷圖。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| 字段 | 描述 |
| --- | --- |
| **[!UICONTROL 名称]** | 您日後用來辨識此目的地的名稱。 |
| **[!UICONTROL 描述]** | 可協助您日後識別此目的地的說明。 |
| **[!UICONTROL 帳戶參與業務單位ID]** | 您的 [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要正確將對象資料從Adobe Experience Platform傳送至 [!DNL Marketing Cloud Account Engagement] 目的地，您必須完成欄位對應步驟。 對應包括在Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應對應專案之間建立連結。

若要正確將XDM欄位對應至 [!DNL Marketing Cloud Account Engagement] 目的地欄位，請遵循下列步驟。

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 您會在畫面上看到新的對應列。
1. 在 **[!UICONTROL 選取來源欄位]** 視窗，選擇 **[!UICONTROL 選取屬性]** 類別並選取XDM屬性，或選擇 **[!UICONTROL 選取身分名稱空間]** 並選取身分。
1. 在 **[!UICONTROL 選取目標欄位]** 視窗，選擇 **[!UICONTROL 選取身分名稱空間]** 並選取身分或選擇 **[!UICONTROL 選取自訂屬性]** 類別並從清單中指定 [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) 從可用的結構描述。

   * 重複這些步驟以在XDM設定檔結構描述和之間新增任何對應 [!DNL Marketing Cloud Account Engagement]： |來源欄位 |目標欄位 |強制 | | — | — | — | |`IdentityMap: Email`|`Identity: email`|是 | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * 具有上述對應的範例如下所示：
      ![顯示Target對應的平台UI熒幕擷圖範例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

當您完成提供目的地連線的對應時，請選取 **[!UICONTROL 下一個]**.

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 導覽至您選取的其中一個區段。 选择 **[!DNL Activation data]** 选项卡。此 **[!UICONTROL 對應ID]** 欄顯示自訂欄位的名稱，該欄位是在 [!DNL Marketing Cloud Account Engagement Prospects] 頁面。
   ![顯示所選區段之對應ID的平台UI熒幕擷圖範例。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. 登入 [[!DNL Salesforce]](https://login.salesforce.com/) 網站。 然後導覽至 **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** 頁面，並檢查區段中的潛在客戶是否已新增/更新。 或者，您也可以存取 [[!DNL Salesforce Pardot]](https://pi.pardot.com/) 並存取 **[!DNL Prospects]** 頁面。
   ![顯示「潛在客戶」頁面的Salesforce UI熒幕擷圖。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. 若要檢查潛在客戶是否已更新，請選取潛在客戶並驗證自訂潛在客戶欄位是否已使用Experience Platform區段狀態更新。
   ![Salesforce UI熒幕擷圖顯示選取的潛在客戶頁面，自訂潛在客戶欄位會以區段狀態更新。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API檔案](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
