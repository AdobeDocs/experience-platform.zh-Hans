---
title: pinterest客戶清單連線
description: 從您的客戶清單、造訪過您網站的人或已在Pinterest上與您的內容互動的人中建立對象。
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] 連線

## 概述 {#overview}

從您的客戶清單、造訪過您網站的人或已在Pinterest上與您的內容互動的人中建立對象。

>[!IMPORTANT]
>
>此目的地是由Pinterest團隊建立。 如有任何查詢或更新要求，請直接透過https://help.pinterest.com/en/contact聯絡。

## 先决条件 {#prerequisites}

* 使用者需要使用Pinterest帳戶進行驗證，該帳戶可存取他們想要新增受眾的廣告商帳戶。 有關共用廣告商帳戶的詳細資訊可找到 [此處](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). 具體來說，使用者需要「對象」存取層級。
* 有關客戶清單身分格式的詳細資料可找到 [此處](https://help.pinterest.com/en/business/article/audience-targeting).

## 支援的身分 {#supported-identities}

此 [!DNL Pinterest Customer List] 目的地支援下表所述的身分啟用。 進一步瞭解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

在 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 在目的地啟用工作流程中，將所需的身分對應至目標欄位 *pinterest_audience*. 身分識別會在資料擷取至Pinterest時加以辨別和解析。

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 對應 *GAID* 目標身分欄位的來源身分名稱空間 *pinterest_audience*. 身分識別會在資料擷取至Pinterest時加以辨別和解析。 |
| IDFA | [!DNL Apple ID for Advertisers] | 對應 *IDFA* 目標身分欄位的來源身分名稱空間 *pinterest_audience*. 身分識別會在資料擷取至Pinterest時加以辨別和解析。 |
| 電子郵件 | 電子郵件地址（純文字或使用SHA256演演算法雜湊） | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 <br> 對應 *電子郵件* 或 *Email_LC_SHA256* 目標身分欄位的來源身分名稱空間 *pinterest_audience*. |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，並使用Pinterest客戶清單目的地中使用的識別碼（名稱、電話號碼或其他）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 用例 {#use-cases}

為了協助您更清楚瞭解應該如何及何時使用 [!DNL Pinterest Customer List] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地來解決的範例使用案例。

### 使用案例#1

從您的客戶清單、造訪過您網站的人或已在Pinterest上與您的內容互動的人中建立對象。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊：

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 廣告商ID]**：您的Pinterest廣告商ID。

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

請參閱 [pinterest說明中心頁面](https://help.pinterest.com/en/business/article/audience-targeting) 以取得其他資訊。
