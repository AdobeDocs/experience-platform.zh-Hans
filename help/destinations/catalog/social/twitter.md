---
title: twitter自訂對象連線
description: 在Twitter中鎖定您現有的追隨者和客戶，並透過啟用Adobe Experience Platform中建立的對象來建立相關的再行銷活動
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 4%

---

# [!DNL Twitter Custom Audiences] 連線

## 概述 {#overview}

在Twitter中鎖定您現有的追隨者和客戶，並透過啟用Adobe Experience Platform中建立的對象來建立相關的再行銷活動。

## 先决条件 {#prerequisites}

設定前 [!DNL Twitter Custom Audiences] 目的地，請務必檢閱您需要符合的下列Twitter必要條件。

1. 您的 [!DNL Twitter Ads] 帳戶必須符合廣告資格。 新增 [!DNL Twitter Ads] 帳戶在建立後的前2週內不符合廣告資格。
2. 您在中授權存取的Twitter使用者帳戶 [!DNL Twitter Audience Manager] 必須具有 *[!DNL Partner Audience Manager]* 許可權已啟用。

## 支援的身分 {#supported-identities}

[!DNL Twitter Custom Audiences] 支援下表所述的身分啟用。 進一步瞭解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Adobe Experience Platform支援廣告商Google Advertising ID (GAID)和Apple ID (IDFA)。 請對應來源結構描述中的這些名稱空間和/或屬性，位於 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 目的地啟用工作流程的URL。 |
| 电子邮件 | 使用者的電子郵件地址 | 請將純文字電子郵件地址和SHA256雜湊電子郵件地址對應至此欄位。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 如果您將客戶電子郵件地址雜湊再上傳至Adobe Experience Platform，請注意，這些身分識別必須使用SHA256進行雜湊處理，不可使用。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正使用Twitter自訂對象目的地中使用的識別碼匯出區段（對象）的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 用例 {#use-cases}

為了協助您更清楚瞭解應該如何及何時使用 [!DNL Twitter Custom Audiences] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地來解決的範例使用案例。

### 使用案例#1

在Twitter中鎖定您現有的追隨者和客戶，並透過啟用您在Adobe Experience Platform中建立的對象來建立相關的再行銷活動，做為 [!DNL List Custom Audiences] 在Twitter中。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

1. 尋找 [!DNL Twitter Custom Audiences] 目的地目錄中的目的地，然後選取 **[!UICONTROL 設定]**.
2. 選取 **[!UICONTROL 連線到目的地]**.
   ![向LinkedIn進行驗證](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. 輸入您的Twitter認證，然後選取 **登入**.

### 填寫目的地詳細資料 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="帐户 ID"
>abstract="您的 Twitter 广告帐户 ID。可以在 Twitter 广告设置中找到它。"

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：您的 [!DNL Twitter Ads] 帳戶ID。 您可在以下網址找到此專案： [!DNL Twitter Ads] 設定。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

## 其他资源 {#additional-resources}

將受眾區段對應至Twitter時，請確定符合下列區段命名需求：

1. 提供人類看得懂的區段對應名稱。 建議您使用與Experience Platform區段相同的名稱。
2. 請勿使用特殊字元(+ &amp; ， % ： ； @ / = ？ $)在區段和區段對應名稱中。 如果您的Experience Platform區段名稱包含這些字元，請在將區段對應至Twitter目的地之前移除這些字元。

更多關於的資訊 [!DNL List Custom Audiences] 在Twitter中，您可以在下文中找到： [twitter檔案](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
