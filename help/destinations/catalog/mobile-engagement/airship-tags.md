---
keywords: 飛艇標籤；飛艇目的地
title: 飛艇標籤連線
description: 無縫地將Adobe對象資料傳遞至Airship，作為Airship中用於鎖定目標的對象標籤。
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# [!DNL Airship Tags] 連線 {#airship-tags-destination}

## 概述

[!DNL Airship] 是領先的客戶參與平台，可在客戶生命週期的每個階段，協助您為使用者提供有意義、個人化的全通路訊息。

這項整合可將Adobe Experience Platform區段資料傳遞至 [!DNL Airship] 作為 [標籤](https://docs.airship.com/guides/audience/tags/) 目標定位或觸發時。

若要深入瞭解 [!DNL Airship]，請參閱 [飛艇檔案](https://docs.airship.com).


>[!TIP]
>
>此檔案頁面是由 [!DNL Airship] 團隊。 如有任何查詢或更新請求，請直接聯絡他們： [support.airship.com](https://support.airship.com/).

## 先决条件

將Adobe Experience Platform區段傳送至之前 [!DNL Airship]，您必須：

* 在您的中建立標籤群組 [!DNL Airship] 專案。
* 產生持有人權杖以進行驗證。

>[!TIP]
> 
>建立 [!DNL Airship] 帳戶透過 [此註冊連結](https://go.airship.eu/accounts/register/plan/starter/) 如果您尚未這樣做。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，其中包含在Airship標籤目的地中使用的識別碼。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 標籤群組

Adobe Experience Platform中的區段概念類似 [標籤](https://docs.airship.com/guides/audience/tags/) 在Airship中，實施上有細微差異。 此整合對映使用者的 [Experience Platform區段中的成員資格](../../../xdm/field-groups/profile/segmentation.md) 是否存在 [!DNL Airship] 標籤之間。 例如，在Platform區段中， `xdm:status` 變更為 `realized`，則標籤會新增至 [!DNL Airship] 此設定檔對應的頻道或具名使用者。 如果 `xdm:status` 變更為 `exited`，則會移除標籤。

若要啟用此整合，請建立 *標籤群組* 在 [!DNL Airship] 已命名 `adobe-segments`.

>[!IMPORTANT]
>
>建立新標籤群組時 **不要檢查** 顯示&quot;[!DNL Allow these tags to be set only from your server]「。 這麼做會導致Adobe標籤整合失敗。

另請參閱 [管理標籤群組](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) 以取得建立標籤群組的指示。

## 產生持有人權杖

前往 **[!UICONTROL 設定]** &quot; **[!UICONTROL API和整合]** 在 [飛艇儀表板](https://go.airship.com) 並選取 **[!UICONTROL Token]** 在左側功能表中。

按一下 **[!UICONTROL 建立Token]**.

為您的Token提供好記的名稱，例如「Adobe標籤目的地」，並為角色選取「所有存取」。

按一下 **[!UICONTROL 建立Token]** 並將詳細資料儲存為機密檔案。

## 用例

為了協助您更清楚瞭解應該如何及何時使用 [!DNL Airship Tags] 目的地，以下是Adobe Experience Platform客戶可以使用此目的地來解決的範例使用案例。

### 使用案例#1

零售商或娛樂平台可建立忠誠度客戶的使用者設定檔，並將這些區段傳遞至 [!DNL Airship] 適用於行動裝置行銷活動上的訊息目標定位。

### 使用案例#2

當使用者進入或退出Adobe Experience Platform中的特定區段時，即時觸發一對一訊息。

例如，零售商在Platform中設定牛仔褲品牌專屬區段。 當某人將其牛仔褲偏好設定為特定品牌時，該零售商現在可以立即觸發行動訊息。

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

[!DNL Airship] 標籤可在頻道上設定，以代表裝置例項(例如iPhone)，或可對映所有使用者裝置至共同識別碼（例如客戶ID）的指名使用者。 如果您的結構描述中以純文字（未雜湊）電子郵件地址作為主要身分，請選取 **[!UICONTROL 來源屬性]** 並將對應至 [!DNL Airship] 具名使用者在右欄中的 **[!UICONTROL 目標身分]**，如下所示。

![已命名的使用者對應](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

對於應該對應至管道（即裝置）的識別碼，請根據來源對應至適當的管道。 下列影像說明如何將Google Advertising ID對應至 [!DNL Airship] Android頻道。

![連線到飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![連線到飛艇標籤](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![管道對應](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](../../../data-governance/home.md).
