---
title: Adobe Campaign Managed Cloud Services連線
description: Adobe Campaign Managed Cloud Services為跨頻道客戶體驗設計提供平台，並為視覺行銷活動的策劃、即時互動管理和跨頻道執行提供環境。
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: ef49bebb96afb9b25430fcc69f8ba91305ad6697
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 4%

---

# Adobe Campaign Managed Cloud Services連線 {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>此整合適用於 [Adobe Campaign 8.4或更高版本](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1).

## 概述 {#overview}

Adobe Campaign Managed Cloud Services為跨頻道客戶體驗設計提供平台，並為視覺行銷活動的策劃、即時互動管理和跨頻道執行提供環境。 [開始使用行銷活動](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

使用 Campaign 可以：
* 通过客户的单一可访问视图推动个性化和参与,
* 将电子邮件、移动、线上和线下渠道整合到客户历程中,
* 自动投放有意义、及时的消息和优惠.

>[!IMPORTANT]
>
>使用Adobe Campaign Managed Cloud Services連線時，請記得下列護欄：
>
>* 最多50個區段可以是 [已啟用](#activate) 對於目的地，
>* 對於每個區段，您最多可以新增20個欄位至 [對應](#map) 至Adobe Campaign，
>* Azure Blob儲存體資料登陸區域(DLZ)上的資料保留：7天，
>* 啟動頻率為最少3小時。


## 用例 {#use-cases}

為協助您更清楚瞭解您應如何使用Adobe Campaign管理服務目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

Adobe Experience Platform會建立客戶設定檔，其中納入身分圖表、來自analytics的行為資料、合併離線和線上資料等資訊。 透過這項整合，您可以使用Adobe Experience Platform支援的受眾來增強Adobe Campaign中已有的區段功能，從而在Campaign中啟用該資料。

例如，一家運動服裝公司想要運用Adobe Experience Platform支援的智慧型區段，並使用Adobe Campaign加以啟用，以便透過Adobe Campaign支援的不同管道聯絡其客戶群。

傳送訊息後，他們想要使用Adobe Campaign的體驗資料（例如傳送、開啟和點按）來增強Adobe Experience Platform中的客戶設定檔。

如此一來，跨管道的行銷活動在Adobe Experience Cloud生態系統中更為一致，而豐富的客戶個人資料能迅速適應和學習。

[進一步瞭解Adobe Campaign與Adobe Experience Platform的整合](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)

## 支援的身分 {#supported-identities}

*Adobe Campaign Managed Cloud Services* 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| external_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，選取此目標身分。 我們建議使用此身分，並將其對應至代表客戶的Campaign執行個體中的ID (loyalty_ID、account_ID、customer_ID...) |
| ECID | Experience Cloud ID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請參閱以下檔案： [ECID](/help/identity-service/ecid.md) 以取得詳細資訊。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊處理的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| GAID | Google廣告ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分識別是IDFA名稱空間時，請選取IDFA目標身分。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如&lt;客戶名稱>的「選取設定檔屬性」畫面中所選。 [目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 選取例項]**：您的 **[!DNL Campaign]** 行銷執行個體。
* **[!UICONTROL 目標對應]**：選取您在中使用的目標對應 **[!DNL Adobe Campaign]** 以傳送傳遞。 [了解详情](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html)。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

### 治理原則與執行動作 {#governance}

選取適用於您要匯出至目的地之資料的行銷動作。 若為Adobe Campaign，建議您選取 **[!UICONTROL 電子郵件目標定位]** 行銷動作。

如需行銷動作的詳細資訊，請參閱 [資料使用原則概觀](/help/data-governance/policies/overview.md) 頁面。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [啟用對象資料以批次設定檔匯出目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html) 以取得啟用此目的地的對象資料的相關指示。

### 對應屬性和身分 {#map}

選取要與設定檔一起匯出的XDM欄位，並將它們對應至對應的Adobe Campaign欄位。[深入瞭解電子郵件行銷目的地的身分和屬性選擇](overview.md)

1. 選取來源欄位：

   * 選取 **識別碼** （例如：電子郵件欄位）當作來源身分，可唯一識別Adobe Experience Platform和Adobe Campaign中的設定檔。

   * 選取所有其他 **xdm來源設定檔屬性** 需要匯出至Adobe Campaign的區段。
   >[!NOTE]
   >
   >「segmentMembershipStatus」欄位是反映segmentMembership狀態的必要對應。 此欄位預設為新增，無法修改或移除。

1. 在Adobe Campaign中將每個欄位與其目標欄位對應。 可用的目標欄位由以下情況時選取的目標對應決定： [建立目的地](#destination-details).

1. 識別必要屬性和重複資料刪除索引鍵。 請注意，標示為「必要」或「重複資料刪除索引鍵」的屬性中的值不得為Null。

   * [必要屬性](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 確定所有設定檔記錄都包含選取的屬性。 例如：所有匯出的設定檔都包含電子郵件地址。 建議將身分欄位和用作重複資料刪除索引鍵的欄位都設為強制性。
   * [重複資料刪除索引鍵](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 是主要索引鍵，可決定使用者希望為其設定檔進行重複資料刪除的身分識別。

      >[!IMPORTANT]
      >
      >請確定重複資料刪除索引鍵屬性的名稱符合所選目標對應的欄名稱。
   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. 執行對應後，您可以檢閱並完成目的地設定，以開始將資料傳送至 **[!DNL Campaign]**.
   [瞭解如何檢閱並完成目的地設定](/help/destinations/destination-types.md#review).

## 匯出的資料/驗證資料匯出 {#exported-data}

一旦啟用目的地後，您就可以在Campaign中存取對應的工作和匯出的資料。

### 監視資料匯出作業 {#jobs}

導覽至 **[!UICONTROL 管理]** > **[!UICONTROL 稽核]** > **[!UICONTROL 對象載入工作]** 功能表以監視從Adobe Experience Platform啟動的所有匯出作業。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### 存取匯出的資料 {#data}

導覽至 **[!UICONTROL 設定檔和目標]** > **[!UICONTROL 清單]** > **[!UICONTROL AEP對象]** 功能表，以存取在啟用目的地後建立的對象。

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請閱讀 [資料控管概觀](/help/data-governance/home.md).
