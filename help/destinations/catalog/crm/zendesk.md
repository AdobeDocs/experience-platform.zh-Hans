---
title: Zendesk連線
description: Zendesk目的地可讓您匯出帳戶資料，並在Zendesk中加以啟用，以滿足您的業務需求。
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 55f1eafa68124b044d20f8f909f6238766076a7a
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 1%

---

# [!DNL Zendesk] 連線

[[!DNL Zendesk]](https://www.zendesk.com) 是客戶服務解決方案和銷售工具。

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 可運用 [[!DNL Zendesk] 連絡人API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/)，至 **建立和更新身分** 區段內的聯絡人 [!DNL Zendesk].

[!DNL Zendesk] 使用持有人權杖作為驗證機制，與 [!DNL Zendesk] 連絡人API。 向您的驗證身分的說明 [!DNL Zendesk] 執行個體的詳細資訊如下： [驗證至目的地](#authenticate) 區段。

## 用例 {#use-cases}

多管道B2C平台的客戶服務部門想要確保其客戶獲得順暢的個人化體驗。 部門可以根據自己的離線資料建立區段，以建立新的使用者設定檔，或更新不同互動（例如購買、退貨等）的現有設定檔資訊。 並從Adobe Experience Platform將這些區段傳送至 [!DNL Zendesk]. 將更新的資訊存放在中 [!DNL Zendesk] 確保客戶服務代理程式能立即取得客戶的最新資訊，以便更快回應和解決問題。

## 先决条件 {#prerequisites}

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在將資料啟用至 [!DNL Zendesk] 目的地，您必須擁有 [綱要](/help/xdm/schema/composition.md)， a [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立於 [!DNL Experience Platform].

請參閱Experience Platform檔案，瞭解 [區段會籍詳細資料結構描述欄位群組](/help/xdm/field-groups/profile/segmentation.md) 如果您需要區段狀態的指引。

### [!DNL Zendesk] 必備條件 {#prerequisites-destination}

為了將資料從Platform匯出至 [!DNL Zendesk] 您需要擁有 [!DNL Zendesk] 帳戶。

#### 收集 [!DNL Zendesk] 認證 {#gather-credentials}

在驗證之前，請記下以下專案 [!DNL Zendesk] 目的地：

| 認證 | 描述 | 示例 |
| --- | --- | --- |
| `Bearer token` | 您在中產生的存取Token [!DNL Zendesk] 帳戶。 <br> 請依照檔案說明進行 [產生 [!DNL Zendesk] 存取權杖](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) 如果您沒有。 | `a0b1c2d3e4...v20w21x22y23z` |

## 护栏 {#guardrails}

此 [訂價與費率限制](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) 頁面詳細資訊 [!DNL Zendesk] 與您的帳戶相關聯的API限制。 您需要確保您的資料和裝載在這些限制內。

## 支援的身分 {#supported-identities}

[!DNL Zendesk] 支援下表中描述的身分更新。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 示例 | 描述 | 強制 |
|---|---|---|---|
| `email` | `test@test.com` | 連絡人的電子郵件地址。 | 是 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | <ul><li>您正在匯出區段的所有成員，以及所需的結構描述欄位 *（例如：電子郵件地址、電話號碼、姓氏）*，根據您的欄位對應。</li><li> 中的每個區段狀態 [!DNL Zendesk] 會根據 **[!UICONTROL 對應ID]** 值期間提供 [區段排程](#schedule-segment-export-example) 步驟。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | <ul><li>串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

範圍 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL Zendesk]. 或者，您也可以在 **[!UICONTROL CRM]** 類別。

### 驗證至目的地 {#authenticate}

填寫以下必填欄位。 請參閱 [收集 [!DNL Zendesk] 認證](#gather-credentials) 區段以取得指引。
* **[!UICONTROL 持有人權杖]**：您在中產生的存取Token [!DNL Zendesk] 帳戶。

若要驗證目的地，請選取 **[!UICONTROL 連線到目的地]**.
![顯示如何驗證的平台UI熒幕擷圖。](../../assets/catalog/crm/zendesk/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連線]** 帶有綠色核取記號的狀態。 然後您可以繼續下一步驟。

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。
![顯示目的地詳細資訊的平台UI熒幕擷圖。](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要正確將對象資料從Adobe Experience Platform傳送至 [!DNL Zendesk] 目的地，您必須完成欄位對應步驟。 對應包括在Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應對應專案之間建立連結。

中指定的屬性 **[!UICONTROL 目標欄位]** 應與「屬性對應」表格中所述完全相同的名稱，因為這些屬性會形成請求內文。

中指定的屬性 **[!UICONTROL 來源欄位]** 請勿遵循任何此類限制。 您可以視需要加以對應，但如果推送至時的資料格式不正確 [!DNL Zendesk] 這會導致錯誤。

若要正確將XDM欄位對應至 [!DNL Zendesk] 目的地欄位，請依照下列步驟操作：

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 您會在畫面上看到新的對應列。
1. 在 **[!UICONTROL 選取來源欄位]** 視窗，選擇 **[!UICONTROL 選取屬性]** 類別並選取XDM屬性，或選擇 **[!UICONTROL 選取身分名稱空間]** 並選取身分。
1. 在 **[!UICONTROL 選取目標欄位]** 視窗，選擇 **[!UICONTROL 選取身分名稱空間]** 類別並選取目標身分，或選擇 **[!UICONTROL 選取屬性]** 類別並選取其中一個支援的結構描述屬性。
   * 重複這些步驟以新增以下強制對應，您也可以新增任何其他要在XDM設定檔結構描述和之間更新的屬性。 [!DNL Zendesk] 例項： |來源欄位|目標欄位|必要| |—|—|—| |`xdm: person.name.lastName`|`xdm: last_name`|是 | |`IdentityMap: Email`|`Identity: email`|是 | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * 使用這些對應的範例如下所示：
      ![具有屬性對應的平台UI熒幕擷圖範例。](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>此 `Attribute: last_name` 和 `Identity: email` 目標對應是此目的地的必要專案。 如果缺少這些對應，則會忽略任何其他對應，且不會傳送至 [!DNL Zendesk].

當您完成提供目的地連線的對應時，請選取 **[!UICONTROL 下一個]**.

### 排程區段匯出和範例 {#schedule-segment-export-example}

在 [[!UICONTROL 排程區段匯出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 啟動工作流程的步驟，您必須手動將Platform區段對應至中的自訂欄位屬性 [!DNL Zendesk].

若要這麼做，請選取每個區段，然後輸入對應的自訂欄位屬性 [!DNL Zendesk] 在 **[!UICONTROL 對應ID]** 欄位。

範例如下：
![顯示「排程區段匯出」的Platform UI熒幕擷圖範例。](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選取 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 並導覽至目的地清單。
1. 接下來，選取目的地並切換至 **[!UICONTROL 啟用資料]** 標籤，然後選取區段名稱。
   ![顯示目的地啟用資料的平台UI熒幕擷圖範例。](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. 監控區段摘要，並確保設定檔計數與區段內的計數相對應。
   ![顯示區段的平台UI熒幕擷圖範例。](../../assets/catalog/crm/zendesk/segment.png)

1. 登入 [!DNL Zendesk] 網站，然後導覽至 **[!UICONTROL 連絡人]** 頁面，以檢查是否已新增區段中的設定檔。 此清單可設定為顯示使用區段建立之其他欄位的欄 **[!UICONTROL 對應ID]** 和區段狀態。
   ![Zendesk UI熒幕擷圖顯示「連絡人」頁面，其中包含以區段名稱建立的其他欄位。](../../assets/catalog/crm/zendesk/contacts.png)

1. 或者，您也可以向下切入至個人 **[!UICONTROL 個人]** 頁面，並檢查 **[!UICONTROL 其他欄位]** 區段會顯示區段名稱和區段狀態。
   ![Zendesk UI熒幕擷圖顯示「人員」頁面，而其他欄位區段顯示區段名稱和區段狀態。](../../assets/catalog/crm/zendesk/contact.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

其他實用資訊來自 [!DNL Zendesk] 檔案如下：
* [進行您的第一次通話](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [自訂欄位](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

本節擷取此目的地聯結器的功能和重要檔案更新。

+++ 檢視變更記錄檔

| 發行月份 | 更新型別 | 描述 |
|---|---|---|
| 2023 年 4 月 | 檔案更新 | <ul><li>我們已更新 [使用案例](#use-cases) 區段，以更清楚的範例說明客戶何時可受益於使用此目的地。</li> <li>我們已更新 [對應](#mapping-considerations-example) 區段來反映正確的必要對應。 此 `Attribute: last_name` 和 `Identity: email` 目標對應是此目的地的必要專案。 如果缺少這些對應，則會忽略任何其他對應，且不會傳送至 [!DNL Zendesk].</li> <li>我們已更新 [對應](#mapping-considerations-example) 區段，其中包含強制和選擇性對應的明確範例。</li></ul> |
| 2023 年 3 月 | 初始版本 | 初始目的地版本和檔案發佈。 |

{style="table-layout:auto"}

+++