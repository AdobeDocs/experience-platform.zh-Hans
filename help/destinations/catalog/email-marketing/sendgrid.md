---
keywords: 電子郵件；電子郵件；電子郵件；電子郵件目的地；sendgrid；sendgrid目的地
title: SendGrid連線
description: SendGrid目的地可讓您匯出第一方資料，並根據您的業務需求在SendGrid中加以啟用。
exl-id: 6f22746f-2043-4a20-b8a6-097d721f2fe7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 2%

---

# [!DNL SendGrid] 連線

## 概述 {#overview}

[SendGrid](https://www.sendgrid.com) 是適用於交易和行銷電子郵件的熱門客戶溝通平台。

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 可運用 [[!DNL SendGrid Marketing Contacts API]](https://api.sendgrid.com/v3/marketing/contacts)，可讓您匯出第一方電子郵件設定檔，並在新的SendGrid區段中加以啟用，以滿足您的業務需求。

SendGrid使用API持有人權杖作為驗證機制，與SendGrid API通訊。

## 先决条件 {#prerequisites}

開始設定目的地之前，需要下列專案。

1. 您必須有SendGrid帳戶。
   * 移至SendGrid [註冊](https://signup.sendgrid.com/) 頁面來註冊及建立SendGrid帳戶（如果尚未建立）。
1. 登入SendGrid入口網站後，您還需要產生API權杖。
1. 導覽至SendGrid網站並存取 **[!DNL Settings]** > **[!DNL API Keys]** 頁面。 或者，請參閱 [SendGrid檔案](https://app.sendgrid.com/settings/api_keys) 以存取SendGrid應用程式中的適當區段。
1. 最後，選取 **[!DNL Create API Key]** 按鈕。
   * 請參閱 [SendGrid檔案](https://docs.sendgrid.com/ui/account-and-settings/api-keys#creating-an-api-key)，以瞭解您要執行的動作。
   * 如果您想要以程式設計方式產生API金鑰，請參閱 [SendGrid檔案](https://docs.sendgrid.com/api-reference/api-keys/create-api-keys).

![](../../assets/catalog/email-marketing/sendgrid/01-api-key.jpg)

啟用資料至SendGrid目的地之前，您必須擁有 [綱要](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=zh-Hans)， a [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)、和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立於 [!DNL Experience Platform]. 另請參閱 [限制](#limits) 區段下方。

>[!IMPORTANT]
>
>* 用於從電子郵件設定檔建立郵寄清單的SendGrid API要求在每個設定檔中提供唯一的電子郵件地址。 無論其是否作為下列專案的值使用 *電子郵件* 或 *備用電子郵件*. 由於SendGrid連線支援電子郵件和備用電子郵件值的對應，請確保使用的每個設定檔中的所有電子郵件地址都應該是唯一的 *資料集*. 否則，將電子郵件設定檔傳送至SendGrid時，將會導致錯誤，且該電子郵件設定檔不會出現在資料匯出中。
>
>* 目前，從Experience Platform的區段移除設定檔時，無法從SendGrid移除設定檔。


## 支援的身分 {#supported-identities}

SendGrid支援如下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 电子邮件地址 | 請注意，支援純文字和SHA256雜湊電子郵件地址 [!DNL Adobe Experience Platform]. 如果Experience Platform來源欄位包含未雜湊屬性，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。<br/><br/> 請注意 **SendGrid** 不支援雜湊電子郵件地址，因此只會將未轉換的純文字資料傳送至目的地。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如&lt;客戶名稱>的「選取設定檔屬性」畫面中所選。 [目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 用例 {#use-cases}

為協助您更清楚瞭解應如何及何時使用SendGrid目的地，以下提供下列範例使用案例 [!DNL Experience Platform] 客戶可以使用此目的地來解析。

### 為多個行銷活動建立行銷清單

使用SendGrid的行銷團隊可以在SendGrid中建立郵寄清單，並填入電子郵件地址。 現在於SendGrid內建立的郵寄清單隨後可用於多個行銷活動。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

1. 在內 [!DNL Adobe Experience Platform] 主控台，導覽至 **目的地**.

1. 選取 **目錄** 標籤並搜尋 *SendGrid*. 然後選取 **設定**. 建立與目的地的連線後，UI標籤會變更為 **啟用區段**.
   ![](../../assets/catalog/email-marketing/sendgrid/02-catalog.jpg)

1. 畫面會顯示協助您設定SendGrid目的地的精靈。 選取以下專案以建立新目的地 **設定新目的地**.
   ![](../../assets/catalog/email-marketing/sendgrid/03.jpg)

1. 選取 **新帳戶** 選項並填入 **持有人權杖** 值。 此值是SendGrid *API金鑰* 先前在 [必要條件區段](#prerequisites).
   ![](../../assets/catalog/email-marketing/sendgrid/04.jpg)

1. 選取 **連線到目的地**. 如果SendGrid *API金鑰* 您提供的有效，UI會顯示 **已連線** 狀態，並顯示綠色核取記號，然後您可以繼續進行下一步以填寫其他資訊欄位。

![](../../assets/catalog/email-marketing/sendgrid/05.jpg)

### 填寫目的地詳細資料 {#destination-details}

當 [設定](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 您必須提供下列資訊：

* **[!UICONTROL 名稱]**：日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：此說明選填，可協助您日後識別此目的地。

![](../../assets/catalog/email-marketing/sendgrid/06.jpg)

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

如需此目的地的特定詳細資訊，請參閱下列影像。

1. 選取一或多個要匯出至SendGrid的區段。
   ![](../../assets/catalog/email-marketing/sendgrid/11.jpg)

1. 在 **[!UICONTROL 對應]** 步驟，選取之後 **[!UICONTROL 新增對應]**，您會看到對應頁面，以將來源XDM欄位對應到SendGrid API目標欄位。 下圖示範如何在Experience Platform和SendGrid之間對應身分識別名稱空間。 請確保 **[!UICONTROL 來源欄位]** *電子郵件* 應該對應至 **[!UICONTROL 目標欄位]** *external_id* 如下所示。
   ![](../../assets/catalog/email-marketing/sendgrid/13.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/14.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/15.jpg)
   ![](../../assets/catalog/email-marketing/sendgrid/16.jpg)

1. 同樣地，對應所需的 [!DNL Adobe Experience Platform] 要匯出至SendGrid目的地的屬性。
   ![](../../assets/catalog/email-marketing/sendgrid/17.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/18.jpg)

1. 完成對應後，選取 **[!UICONTROL 下一個]** 以進入檢閱畫面。
   ![](../../assets/catalog/email-marketing/sendgrid/22.png)

1. 選取 **[!UICONTROL 完成]** 以完成設定。
   ![](../../assets/catalog/email-marketing/sendgrid/23.jpg)

完整的支援屬性對應清單，可針對下列專案設定： [SendGrid行銷聯絡人>新增或更新聯絡人API](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact) 在底下。

| 來源欄位 | 目標欄位 | 类型 | 描述 | 限制 |
|---|---|---|---|---|
| xdm：<br/> homeAddress.street1 | xdm：<br/> address_line_1 | 字符串 | 地址的第一行。 | 最大長度：<br/> 100個字元 |
| xdm：<br/> homeAddress.street2 | xdm：<br/> address_line_2 | 字符串 | 選用的第二行地址。 | 最大長度：<br/> 100個字元 |
| xdm：<br/> _extconndev.alternate_emails | xdm：<br/> 備用電子郵件 | 字符串数组 | 與聯絡人關聯的其他電子郵件。 | <ul><li>最多：5個專案</li><li>最小值：0個專案</li></ul> |
| xdm：<br/> homeAddress.city | xdm：<br/> city | 字符串 | 連絡人的城市。 | 最大長度：<br/> 60個字元 |
| xdm：<br/> homeAddress.country | xdm：<br/> 國家/地區 | 字符串 | 連絡人的國家/地區。 可以是全名或縮寫。 | 最大長度：<br/> 50個字元 |
| identityMap：<br/> 電子郵件 | 身分：<br/> external_id | 字符串 | 連絡人的主要電子郵件。 這必須是有效的電子郵件。 | 最大長度：<br/> 254個字元 |
| xdm：<br/> person.name.firstName | xdm：<br/> 名字 | 字符串 | 連絡人姓名 | 最大長度：<br/> 50個字元 |
| xdm：<br/> person.name.lastName | xdm：<br/> last_name | 字符串 | 連絡人的姓氏 | 最大長度：<br/> 50個字元 |
| xdm：<br/> homeAddress.postalCode | xdm：<br/> postal_code | 字符串 | 連絡人的郵遞區號或其他郵遞區號。 |  |
| xdm：<br/> homeAddress.stateProvince | xdm：<br/> state_province_region | 字符串 | 連絡人的州、省或地區。 | 最大長度：<br/> 50個字元 |

## 驗證SendGrid中的資料匯出 {#validate}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選取 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 以導覽至目的地清單。
   ![](../../assets/catalog/email-marketing/sendgrid/25.jpg)

1. 選取目的地並驗證狀態是否為 **[!UICONTROL 已啟用]**.
   ![](../../assets/catalog/email-marketing/sendgrid/26.jpg)

1. 切換至 **[!DNL Activation data]** 標籤，然後選取區段名稱。
   ![](../../assets/catalog/email-marketing/sendgrid/27.jpg)

1. 監視區段摘要，並檢查與資料集中建立的計數對應的設定檔計數。
   ![](../../assets/catalog/email-marketing/sendgrid/28.jpg)

1. 此 [SendGrid行銷清單>建立清單API](https://docs.sendgrid.com/api-reference/lists/create-list) 用於在SendGrid中建立唯一的連絡人清單，方法是聯結 *list_name* 屬性和資料匯出的時間戳記。 導覽至SendGrid網站，並檢查是否建立了符合名稱模式的新連絡人清單。
   ![](../../assets/catalog/email-marketing/sendgrid/29.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/30.jpg)

1. 選取新建立的連絡人清單，並檢查您建立之資料集中的新電子郵件記錄是否填入新連絡人清單中。

1. 此外，也請檢查一些電子郵件以驗證欄位對應是否正確。
   ![](../../assets/catalog/email-marketing/sendgrid/31.jpg)

   ![](../../assets/catalog/email-marketing/sendgrid/32.jpg)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 其他资源 {#additional-resources}

此SendGrid目的地會利用以下API：
* [SendGrid行銷清單>建立清單API](https://docs.sendgrid.com/api-reference/lists/create-list)
* [SendGrid行銷聯絡人>新增或更新聯絡人API](https://docs.sendgrid.com/api-reference/contacts/add-or-update-a-contact)

### 限制 {#limits}

* 此 [SendGrid行銷聯絡人>新增或更新聯絡人API](https://api.sendgrid.com/v3/marketing/contacts) 可接受30,000個連絡人，或6MB的資料（以較低者為準）。
