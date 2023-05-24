---
title: (API) Oracle Eloqua連線
description: (API) Oracle Eloqua目的地可讓您匯出帳戶資料，並在Oracle Eloqua中根據您的業務需求加以啟用。
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: 3d54b89ab5f956710ad595a0e8d3567e1e773d0a
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 3%

---


# [!DNL (API) Oracle Eloqua] 連線

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 可讓行銷人員規劃及執行行銷活動，同時為其潛在客戶提供個人化的客戶體驗。 透過整合式銷售機會管理及輕鬆建立行銷活動，可協助行銷人員在買家歷程中的適當時間，與適當的對象互動，並可優雅地擴充，以觸及各管道（包括電子郵件、顯示搜尋、視訊和行動裝置）的對象。 銷售團隊能以更快的速度完成更多交易，透過即時深入分析提高行銷ROI。

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 可運用 [更新連絡人](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) 作業 [!DNL Oracle Eloqua] REST API，可讓您 **更新身分** 區段內至 [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] 使用 [基本驗證](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) 以與 [!DNL Oracle Eloqua] REST API。 向您的驗證身分的說明 [!DNL Oracle Eloqua] 執行個體的詳細資訊如下： [驗證至目的地](#authenticate) 區段。

## 用例 {#use-cases}

線上平台的行銷部門想要將電子郵件行銷活動廣播給已組織的潛在客戶受眾。 平台的行銷團隊可以透過Adobe Experience Platform更新現有潛在客戶資訊、從自己的離線資料建立區段，並將這些區段傳送至 [!DNL Oracle Eloqua]，然後可用於傳送行銷活動電子郵件。

## 先决条件 {#prerequisites}

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在將資料啟用至 [!DNL Oracle Eloqua] 目的地，您必須擁有 [綱要](/help/xdm/schema/composition.md)， a [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立於 [!DNL Experience Platform].

請參閱Experience Platform檔案以瞭解 [區段會籍詳細資料結構描述欄位群組](/help/xdm/field-groups/profile/segmentation.md) 如果您需要區段狀態的指引。

### [!DNL Oracle Eloqua] 必備條件 {#prerequisites-destination}

為了將資料從Platform匯出至 [!DNL Oracle Eloqua] 帳戶您必須擁有 [!DNL Oracle Eloqua] 帳戶。

此外，您至少需要 *「進階使用者 — 行銷許可權」* 您的 [!DNL Oracle Eloqua] 執行個體。 請參閱 *「安全性群組」* 區段於 [安全的使用者存取](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) 指引頁面。 目的地需要以程式設計方式存取許可權 [決定您的基本URL](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) 叫用 [!DNL Oracle Eloqua] API。

#### 收集 [!DNL Oracle Eloqua] 認證 {#gather-credentials}

在驗證之前，請記下以下專案 [!DNL Oracle Eloqua] 目的地：

| 認證 | 描述 |
| --- | --- |
| `Company Name` | 與您的關聯的公司名稱 [!DNL Oracle Eloqua] 帳戶。 <br>您稍後將使用 `Company Name` 和 [!DNL Oracle Eloqua] `Username` 作為要用作 **[!UICONTROL 使用者名稱]** 時間 [正在向目的地進行驗證](#authenticate). |
| `Username` | 您的使用者名稱 [!DNL Oracle Eloqua] 帳戶。 |
| `Password` | 您的密碼 [!DNL Oracle Eloqua] 帳戶。 |
| `Pod` | [!DNL Oracle Eloqua] 支援多個資料中心，每個資料中心都有獨特的網域名稱。 [!DNL Oracle Eloqua] 將這些稱為「pods」，目前總共有七種 — p01、p02、p03、p04、p06、p07和p08。 若要取得您目前所在的POD，請登入 [!DNL Oracle Eloqua] 並記下您成功登入後瀏覽器中的URL。 例如，如果您的瀏覽器URL為 `secure.p01.eloqua.com` 您的 `pod` 是 `p01`. 請參閱 [決定您的POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua) 頁面以取得其他指引。 |

請參閱 [登入 [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing) 以取得指引。

## 护栏 {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] 自訂連絡人欄位會使用於下列期間選取的區段名稱自動建立： **[!UICONTROL 選取區段]** 步驟。


* [!DNL Oracle Eloqua] 最多250個自訂聯絡人欄位。
* 在匯出新區段之前，請確定以下範圍中的Platform區段數和現有區段數 [!DNL Oracle Eloqua] 請勿超過此限制。
* 如果超過此限制，您將會在Experience Platform中遇到錯誤。 這是因為 [!DNL Oracle Eloqua] API無法驗證請求，並以 —  *400：發生驗證錯誤*  — 說明問題的錯誤訊息。
* 如果您已達到上述指定的限制，則需要從目的地移除現有的對應，並刪除中對應的自訂聯絡人欄位。 [!DNL Oracle Eloqua] 帳戶，然後才能匯出更多區段。

* 請參閱 [[!DNL Oracle Eloqua] 建立連絡人欄位](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) 頁面以取得其他限制的相關資訊。

## 支援的身分 {#supported-identities}

[!DNL Oracle Eloqua] 支援下表中描述的身分更新。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 | 強制 |
|---|---|---|
| `EloquaId` | 連絡人的唯一識別碼。 | 是 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | <ul><li>您正在匯出區段的所有成員，以及所需的結構描述欄位 *（例如：電子郵件地址、電話號碼、姓氏）*，根據您的欄位對應。</li><li> 針對Platform中選取的每個區段，將 [!DNL Oracle Eloqua] 區段狀態會從Platform更新其區段狀態。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | <ul><li>串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

範圍 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL (API) Oracle Eloqua]. 或者，您也可以在 **[!UICONTROL 電子郵件行銷]** 類別。

### 驗證至目的地 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="公司名称\用户名"
>abstract="在此字段中填写您的公司名称和来自 Oracle Eloqua 的用户名，格式为 `{COMPANY_NAME}\{USERNAME}`"

填寫以下必填欄位。 請參閱 [收集 [!DNL Oracle Eloqua] 認證](#gather-credentials) 區段以取得指引。
* **[!UICONTROL 密碼]**：您的密碼 [!DNL Oracle Eloqua] 帳戶。
* **[!UICONTROL 使用者名稱]**：由下列專案組成的串連字串： [!DNL Oracle Eloqua] 公司名稱和 [!DNL Oracle Eloqua] 使用者名稱。<br>串連值採用以下形式 `{COMPANY_NAME}\{USERNAME}`.<br> 注意，請勿使用任何大括弧或空格，並保留 `\`. <br>例如，如果您的 [!DNL Oracle Eloqua] 公司名稱是 `MyCompany` 和 [!DNL Oracle Eloqua] 使用者名稱為 `Username`，即您將在下列專案中使用的串連值： **[!UICONTROL 使用者名稱]** 欄位是 `MyCompany\Username`.

若要驗證目的地，請選取 **[!UICONTROL 連線到目的地]**.
![顯示如何驗證的平台UI熒幕擷圖。](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連線]** 帶有綠色核取記號的狀態。 然後您可以繼續下一步驟。

### 填寫目的地詳細資料 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="要查找您的 Pod 编号，请登录到 Oracle Eloqua。成功登录后，记下浏览器中的 URL。 "
>additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle 知识库 - 找出您的 Pod 编号"

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。
![顯示目的地詳細資訊的平台UI熒幕擷圖。](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Pod]**：若要取得哪一個 `pod` 您已開啟，登入 [!DNL Oracle Eloqua] 並記下您成功登入後瀏覽器中的URL。 例如，如果您的瀏覽器URL為 `secure.p01.eloqua.com` 此 `pod` 您需要選取的值為 `p01`. 請參閱 [收集 [!DNL Oracle Eloqua] 認證](#gather-credentials) 區段以取得其他指引。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要正確將對象資料從Adobe Experience Platform傳送至 [!DNL Oracle Eloqua] 目的地，您必須完成欄位對應步驟。 對應包括在Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應對應專案之間建立連結。

將XDM欄位對應至 [!DNL Oracle Eloqua] 目的地欄位，請依照下列步驟操作：

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 您會在畫面上看到新的對應列。
1. 在 **[!UICONTROL 選取來源欄位]** 視窗，選擇 **[!UICONTROL 選取屬性]** 類別並選取XDM屬性，或選擇 **[!UICONTROL 選取身分名稱空間]** 並選取身分。
1. 在 **[!UICONTROL 選取目標欄位]** 視窗，選擇 **[!UICONTROL 選取身分名稱空間]** 並選取身分，或選擇 **[!UICONTROL 選取自訂屬性]** 並在「 」中輸入所需的屬性名稱 **[!UICONTROL 屬性名稱]** 欄位。 您提供的屬性名稱應符合中現有的連絡人屬性 [!DNL Oracle Eloqua]. 另請參閱 [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 以取得您可在其中使用的確切屬性名稱 [!DNL Oracle Eloqua].
   * 重複這些步驟，在XDM設定檔結構描述和之間新增必要和任何需要的屬性對應。 [!DNL Oracle Eloqua]： |來源欄位 |目標欄位 |強制 | |—|—|—| |`IdentityMap: Eid`|`Identity: EloquaId`|是 | |`xdm: personalEmail.address`|`Attribute: emailAddress`|是 | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * 具有上述對應的範例如下所示：
      ![具有屬性對應的平台UI熒幕擷圖範例。](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* 中指定的屬性 **[!UICONTROL 目標欄位]** 應完全按照 [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 因為這些屬性會形成請求內文。
>* 中指定的屬性 **[!UICONTROL 來源欄位]** 請勿遵循任何此類限制。 您可以視需要加以對應，但如果推送至時的資料格式不正確 [!DNL Oracle Eloqua] 這會導致錯誤。 例如，您可以對應 **[!UICONTROL 來源欄位]** 身分名稱空間 `contact key`， `ABC ID` 等 至 **[!UICONTROL 目標欄位]** ： `EloquaId` 確認ID值符合以下格式之後： [!DNL Oracle Eloqua].
>* 此 `EloquaID` 對應是更新對應至身分識別的屬性的必要專案。
>* 此 `emailAddress` 需要對映。 若未包含API，API會擲回錯誤，如下所示：
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

當您完成提供目的地連線的對應時，請選取 **[!UICONTROL 下一個]**.

>[!NOTE]
>
>當傳送聯絡人欄位資訊到時，目的地會在每次執行時自動為所選區段名稱的唯一識別碼加上尾碼 [!DNL Oracle Eloqua]. 這可確保與區段名稱對應的聯絡人欄位名稱不會重疊。 請參閱 [驗證資料匯出](#exported-data) 區段熒幕擷圖範例 [!DNL Oracle Eloqua] 「連絡人詳細資料」頁面包含使用區段名稱建立的自訂連絡人欄位。

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選取 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 並導覽至目的地清單。
1. 接下來，選取目的地並切換至 **[!UICONTROL 啟用資料]** 標籤，然後選取區段名稱。
   ![顯示目的地啟用資料的平台UI熒幕擷圖範例。](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. 監控區段摘要，並確保設定檔計數與區段內的計數相對應。
   ![顯示區段的平台UI熒幕擷圖範例。](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. 登入 [!DNL Oracle Eloqua] 網站，然後導覽至 **[!UICONTROL 連絡人總覽]** 頁面，以檢查是否已新增區段中的設定檔。 若要檢視區段狀態，請向下展開至 **[!UICONTROL 連絡人詳細資料]** 頁面，並檢查是否已建立以所選區段名稱作為其首碼的聯絡人欄位。

![oracle Eloqua UI熒幕擷圖顯示「聯絡人詳細資料」頁面，其中包含以區段名稱建立的自訂聯絡人欄位。](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 錯誤與疑難排解 {#errors-and-troubleshooting}

建立目的地時，您可能會收到下列其中一個錯誤訊息： `400: There was a validation error` 或 `400 BAD_REQUEST`. 當您超過250個自訂聯絡人欄位限制時，就會發生此情況，如 [護欄](#guardrails) 區段。 若要修正此錯誤，請確定您未超過中的自訂聯絡人欄位限制 [!DNL Oracle Eloqua].
![平台UI熒幕擷圖顯示錯誤。](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

請參閱 [[!DNL Oracle Eloqua] HTTP狀態碼](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) 和 [[!DNL Oracle Eloqua] 驗證錯誤](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) 頁面，以取得狀態和錯誤碼的完整清單，並附上說明。

## 其他资源 {#additional-resources}

如需其他詳細資訊，請參閱 [!DNL Oracle Eloqua] 檔案：

* [oracle Eloqua行銷自動化](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [適用於OracleEloquaMarketing Cloud服務的REST API](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

本節擷取此目的地聯結器的功能和重要檔案更新。

+++ 檢視變更記錄檔

| 發行月份 | 更新型別 | 描述 |
|---|---|---|
| 2023 年 4 月 | 檔案更新 | <ul><li>我們已更新 [使用案例](#use-cases) 區段，以更清楚的範例說明客戶何時可受益於使用此目的地。</li> <li>我們已更新 [對應](#mapping-considerations-example) 區段，其中包含強制和選擇性對應的明確範例。</li> <li>我們已更新 [連線到目的地](#connect) 區段中有關如何為建構串連值的範例 **[!UICONTROL 使用者名稱]** 欄位使用 [!DNL Oracle Eloqua] 公司名稱和 [!DNL Oracle Eloqua] 使用者名稱。 (PLATIR-28343)</li><li>我們已更新 [收集 [!DNL Oracle Eloqua] 認證](#gather-credentials) 和 [填寫目的地詳細資料](#destination-details) 包含相關指引的區段 [!DNL Oracle Eloqua] **[!UICONTROL Pod]** 選取。 此 *&quot;Pod&quot;* 目的地會使用值來建構API呼叫的基本URL。 此 [[!DNL Oracle Eloqua] 必備條件](#prerequisites-destination) 區段亦已更新，其中包含指派的指引 *「進階使用者 — 行銷許可權」* 作為必要 *「安全性群組」* 您的 [!DNL Oracle Eloqua] 執行個體。</li></ul> |
| 2023 年 3 月 | 初始版本 | 初始目的地版本和檔案發佈。 |

{style="table-layout:auto"}

+++