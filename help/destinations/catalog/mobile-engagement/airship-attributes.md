---
keywords: 飛艇屬性；飛艇目的地
title: 飛艇屬性連線
description: 無縫地將Adobe對象資料傳遞至Airship，作為Airship中用於鎖定目標的對象屬性。
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 0%

---

# [!DNL Airship Attributes] 連線 {#airship-attributes-destination}

## 概述 {#overview}

[!DNL Airship] 是領先的客戶參與平台，可在客戶生命週期的每個階段，協助您為使用者提供有意義、個人化的全通路訊息。

此整合會將Adobe設定檔資料傳遞至 [!DNL Airship] 作為 [屬性](https://docs.airship.com/guides/audience/attributes/) 目標定位或觸發時。

若要深入瞭解 [!DNL Airship]，請參閱 [飛艇檔案](https://docs.airship.com).

>[!TIP]
>
>此檔案頁面是由 [!DNL Airship] 團隊。 如有任何查詢或更新請求，請直接聯絡他們： [support.airship.com](https://support.airship.com/).

## 先决条件 {#prerequisites}

將受眾區段傳送至之前 [!DNL Airship]，您必須：

* 在中啟用屬性 [!DNL Airship] 專案。
* 產生持有人權杖以進行驗證。

>[!TIP]
>
>建立 [!DNL Airship] 帳戶透過 [此註冊連結](https://go.airship.eu/accounts/register/plan/starter/) 如果您尚未這樣做。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏）和/或身分（根據您的欄位對應）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 啟用屬性 {#enable-attributes}

Adobe Experience Platform設定檔屬性類似於 [!DNL Airship] 屬性，並可使用本頁面下方進一步說明的對應工具，在Platform中輕鬆相互對應。

[!DNL Airship] 專案具有數個預先定義的和預設屬性。 如果您有自訂屬性，則必須在下列位置定義它： [!DNL Airship] 首先。 另請參閱 [設定和管理屬性](https://docs.airship.com/tutorials/audience/attributes/) 以取得詳細資訊。

## 產生持有人權杖 {#bearer-token}

前往 **[!UICONTROL 設定]** &quot; **[!UICONTROL API和整合]** 在 [飛艇儀表板](https://go.airship.com) 並選取 **[!UICONTROL Token]** 在左側功能表中。

按一下 **[!UICONTROL 建立Token]**.

為您的Token提供好記的名稱，例如「Adobe屬性目的地」，然後為角色選取「所有存取」。

按一下 **[!UICONTROL 建立Token]** 並將詳細資料儲存為機密檔案。

## 用例 {#use-cases}

為了協助您更清楚瞭解應該如何及何時使用 [!DNL Airship Attributes] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地來解決的範例使用案例。

### 使用案例#1

運用Adobe Experience Platform中收集的設定檔資料，在任一項中個人化訊息和豐富的內容 [!DNL Airship]的頻道。 例如，善用 [!DNL Experience Platform] 設定檔資料，以設定位置屬性 [!DNL Airship]. 這可讓飯店品牌為每位使用者顯示最近飯店位置的影像。

### 使用案例#2

運用Adobe Experience Platform的屬性進一步豐富 [!DNL Airship] 設定檔並將其與SDK或 [!DNL Airship] 預測性資料。 例如，零售商可建立具有忠誠度狀態和位置資料（來自Platform的屬性）的區段，並 [!DNL Airship] 預測會流失資料，以傳送高針對性訊息給居住在內華達州拉斯維加斯且具有高流失機率的金級忠誠度使用者。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證至目的地 {#authenticate}

若要驗證目的地，請填入必填欄位並選取 **[!UICONTROL 連線到目的地]**.

* **[!UICONTROL 持有人權杖]**：您從產生的持有人權杖 [!DNL Airship] 儀表板。

### 填寫目的地詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下列必要和選用欄位。 UI中欄位旁的星號表示該欄位為必填。

* **[!UICONTROL 名稱]**：輸入有助於您識別此目的地的名稱。
* **[!UICONTROL 說明]**：輸入此目的地的說明。
* **[!UICONTROL 網域]**：選取美國或歐盟資料中心，視何者為何 [!DNL Airship] 資料中心適用於此目的地。

### 啟用警示 {#enable-alerts}

您可以啟用警報，以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警示](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊後，請選取 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

另請參閱 [啟用串流區段匯出目的地的受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地的受眾區段的指示。

## 對應考量事項 {#mapping-considerations}

[!DNL Airship] 屬性可在代表裝置例項(例如iPhone)的頻道上設定，或可將使用者的所有裝置對應到通用識別碼（例如客戶ID）的指定使用者上設定。 如果您的結構描述中以純文字（未雜湊）電子郵件地址作為主要身分，請選取 **[!UICONTROL 來源屬性]** 並將對應至 [!DNL Airship] 具名使用者在右欄中的 **[!UICONTROL 目標身分]**，如下所示。

![已命名的使用者對應](../../assets/catalog/mobile-engagement/airship/mapping.png)

對於應該對應至管道（即裝置）的識別碼，請根據來源對應至適當的管道。 下列影像顯示如何建立兩個對應：

* 將IDFA iOS Advertising ID設為 [!DNL Airship] iOS頻道
* Adobe `fullName` 屬性至 [!DNL Airship] 「全名」屬性

>[!NOTE]
>
>使用好記的名稱，該名稱會顯示在 [!DNL Airship] 儀表板來選取屬性對應的目標欄位。

**對應身分**

選取來源欄位：

![連線到飛艇屬性](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

選取目標欄位：

![連線到飛艇屬性](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**對應屬性**

選取來源屬性：

![選取來源欄位](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

選取目標屬性：

![選取目標欄位](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

驗證對應：

![管道對應](../../assets/catalog/mobile-engagement/airship/mapping.png)


## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](../../../data-governance/home.md).
