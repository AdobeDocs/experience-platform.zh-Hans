---
title: Medallia連線
description: 針對鎖定目標Medallia調查和意見回饋收集啟用設定檔，以更好地瞭解客戶需求和期望。
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# Medallia連線

## 概述 {#overview}

針對鎖定目標Medallia調查和意見回饋收集啟用設定檔，以更好地瞭解客戶需求和期望。

>[!IMPORTANT]
>
>此檔案頁面是由Medallia團隊建立。 如有任何查詢或更新要求，請直接透過adobe-integrations@medallia.com聯絡。

## 用例 {#use-cases}

為協助您更清楚瞭解如何使用Medallia目的地，以下是Adobe Experience Platform客戶可使用此目的地解決的範例使用案例。

### 使用案例#1

B2B品牌想要評估並簡化其上線計畫。 他們想要將個人化調查即時傳送給剛剛完成入門流程的客戶。

### 使用案例#2

零售商想要更瞭解客戶對訂單履行情況的偏好。 他們想要傳送簡短1題SMS問卷給過去一個月曾經線上上和店內購買過的客戶。

## 先决条件 {#prerequisites}

建立Medallia連線需要下列資訊：
* **OAuth權杖端點URL**
* **使用者端ID**
* **使用者端密碼**
* **API閘道URL**
* **匯入API名稱**

請與您的Medallia傳送團隊合作，以取得這些詳細資訊。

## 支援的身分 {#supported-identities}

Medallia支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 描述 | 注意事项 |
|---|---|---|
| 电子邮件 | 电子邮件地址 | 當您想要傳送電子郵件邀請調查時，請選取電子郵件目標身分。 當設定檔與多個電子郵件地址關聯時，Medallia只會觸發第一個電子郵件的邀請。 |
| phone | 以E.164格式雜湊的電話號碼 | 當您想要傳送以SMS為基礎的調查時，請選取電話目標身分。 電話號碼必須是E.164格式，其中包括加號(+)、國際國家/地區的電話代碼、當地區號和電話號碼。 例如：(+)（國家/地區代碼）（區號）（電話號碼）。 當設定檔與多個電話號碼相關聯時，Medallia只會觸發第一個電話號碼的邀請。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有新合格成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如&lt;客戶名稱>的「選取設定檔屬性」畫面中所選。 [目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

若要驗證目的地，請填入必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!UICONTROL OAuth權杖端點URL]**：通常採用https://instance.medallia.tld/oauth/tenant/token的形式。
* **[!UICONTROL 使用者端ID]**：從您的Medallia傳送團隊取得。
* **[!UICONTROL 使用者端密碼]**：從您的Medallia傳送團隊取得。

![顯示此目的地之驗證畫面的影像。](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：您日後用來辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL API閘道URL]**：從您的Medallia傳送團隊取得。 通常採用https://instance-tenant.apis.medallia.com的形式。
* **[!UICONTROL 匯入API名稱]**：從您的Medallia傳送團隊取得。 用於此連線的Medallia Import API （也稱為Web摘要）名稱。 您可以對不同的匯入API啟用不同的區段，以觸發不同的調查方案。

![顯示此目的地之目的地詳細資訊畫面的影像。](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

讀取 [對串流區段匯出目的地啟用設定檔和區段](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

### 對應屬性和身分 {#map}

下列目標身分名稱空間必須根據使用案例進行對應：
* 對於電子郵件調查， **電子郵件** 必須使用將對應為目標欄位 **目標欄位** > **選取身分名稱空間** > **電子郵件**
* 對於以簡訊為基礎的調查， **電話** 必須使用將對應為目標欄位 **目標欄位** > **選取身分名稱空間** > **電話**. 電話號碼必須是E.164格式，其中包括加號(+)、國際國家/地區的電話代碼、當地區號和電話號碼

強烈建議您也對應其他目標自訂屬性，以建立個人化調查，並將客戶的更多相關資訊附加至調查記錄：

* 個人化調查通常會依名稱為客戶提供服務
   * 將客戶的名字對應至 **目標欄位** > **選取自訂屬性** > **屬性名稱** > **firstname**
   * 將客戶的姓氏對應至 **目標欄位** > **選取自訂屬性** > **屬性名稱** > **姓氏**
* 視需要新增任何其他目標自訂屬性的對應

![顯示身分和屬性對應範例的影像。](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> 與您的Medallia傳送團隊分享確切的 **屬性名稱** 對於您使用的每個目標自訂屬性 **目標欄位** > **選取自訂屬性** > **屬性名稱**. 您可能希望直接分享對應頁面的熒幕擷圖。

## 匯出的資料 {#exported-data}

一旦您將區段啟動至目的地，請通知您的Medallia傳送團隊，該團隊將能夠驗證從Adobe Experience Platform匯出至Medallia的資料。 請注意，調查只能在資料驗證成功後於Medallia中啟動；在此之前，資料將匯出至Medallia，但不會向客戶觸發調查。

以下提供匯出資料的JSON範例，其使用上方熒幕擷圖的範例對應 **對應屬性和身分** 區段：

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
