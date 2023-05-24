---
keywords: 事件轉送擴充功能；mixpanel；mixpanel事件轉送擴充功能
title: Mixpanel追蹤事件API事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能會將Adobe Experience Edge Network事件傳送至Mixpanel。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API事件轉送擴充功能

[[!DNL Mixpanel]](https://www.mixpanel.com) 是一款產品分析工具，可讓您擷取使用者與數位產品互動的相關資料。 您可以使用簡單的互動式報表來分析產品資料，只要按幾下即可查詢和視覺化資料。 [!DNL Mixpanel] 讓每個人都能即時分析使用者資料，找出趨勢、瞭解使用者行為，並做出產品決策，藉此讓團隊更有效率。

[!DNL Mixpanel] 採用以事件為基礎、以使用者為中心的模式，將每個互動都連結至單一使用者。 此 [!DNL Mixpanel] 資料模型是根據使用者、事件和屬性的概念所建立。

>[!NOTE]
>
>請參閱 [!DNL Mixpanel] 檔案： [身分管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) 以瞭解如何 [!DNL Mixpanel] 合併事件以建立身分叢集。 也建議您檢閱檔案： [相異ID](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) 以瞭解如何使用事件資料識別使用者。

## 用例

如果您想要使用來自Edge Network的資料，請使用此擴充功能 [!DNL Mixpanel] 以善用其產品分析功能。

例如，假設零售組織擁有多頻道實體（網站和行動裝置）。 組織從其平台擷取交易或對話輸入作為事件資料，並將其載入到 [!DNL Mixpanel] 使用事件轉送擴充功能。

之後，分析團隊就可以運用 [!DNL Mixpanel's] 處理資料集及取得業務深入分析的功能，這可用來產生圖表、儀表板或其他視覺效果，以告知業務利害關係人。

如需特定使用案例的詳細資訊，請參閱 [!DNL Mixpanel]，請參閱下列檔案：

* [新到 [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [什么是 [!DNL Mixpanel]？](https://developer.mixpanel.com/docs)
* [12次必須嘗試 [!DNL Mixpanel] 功能](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] 必備條件 {#prerequisites-mixpanel}

您必須具備有效的 [!DNL Mixpanel] 帳戶，以便使用此擴充功能。 前往 [[!DNL Mixpanel] 註冊頁面](https://mixpanel.com/register/) 註冊並建立帳戶。

確保 [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) 已為您的專案啟用設定。 導覽至 **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** 和切換設定。

### 瞭解中的身分叢集 [!DNL Mixpanel]

在 [!DNL Mixpanel]，身分叢集包含集合 `distinct_id` 連線至個別使用者的值。 [!DNL Mixpanel] 處理每個使用者的身分叢集，解析單一canonical `distinct_id` 報表中使用的每個叢集。 您也可以包含自己的識別碼(稱為本機 `distinct_id`)的訪客名稱，此為使用者識別事件之前發生的匿名事件。

[!DNL Mixpanel] 透過兩種方法解析身分叢集：

* **識別** ： [!DNL Mixpanel] 將您選擇的識別碼連線至匿名 `distinct_id`. 如果您的網站擁有 [!DNL Mixpanel] SDK已啟用，平台將使用 `distinct_id` 指派給目前登入的使用者。
* **別名**： [!DNL Mixpanel] 結合兩個非匿名 `distinct id`如果滿足其他合併條件，則為一起。

>[!NOTE]
>
>請參閱 [!DNL Mixpanel] 檔案於 [身分管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) 以取得這些方法的詳細資訊。
>
>確認您已啟用 [[!DNL Mixpanel] 身分合併功能](#prerequisites-mixpanel) 以確保身分叢集可正確解析。

### 收集必要的設定詳細資料 {#configuration-details}

為了將Experience Platform連線到 [!DNL Mixpanel] 您必須有以下輸入：

| 金鑰型別 | 描述 | 示例 |
| --- | --- | --- |
| 專案權杖 | 與您的關聯的專案代號 [!DNL Mixpanel] 帳戶。 請參閱 [!DNL Mixpanel] 檔案： [尋找您的專案代號](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) 以取得指引。 | `25470xxxxxxxxxxxxxxxxxxx1289` |

## 安裝並設定 [!DNL Mixpanel] 擴充功能 {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇現有屬性進行編輯。

選取 **[!UICONTROL 擴充功能]** 左側導覽列中。 在 **[!UICONTROL 目錄]** 索引標籤，選取 **[!UICONTROL 安裝]** 在的卡片上 [!DNL Mixpanel] 副檔名。

![安裝 [!DNL Mixpanel] 副檔名。](../../../images/extensions/server/mixpanel/install-extension.png)

## 建立 [!DNL Send Event] 規則

開始在事件轉送屬性中建立新規則。 下 **[!UICONTROL 動作]**，新增動作並將擴充功能設為 **[!UICONTROL Mixpanel]**. 接下來，將動作型別設定為 **[!UICONTROL 追蹤事件]** 傳送Adobe Experience Edge Network事件至 [!DNL Mixpanel].

| 輸入 | 描述 | 必需 |
| --- | --- | --- |
| [!UICONTROL 專案權杖] | 此欄位應對應至與您的關聯的專案代號 [!DNL Mixpanel] 帳戶。 | 是 |
| [!UICONTROL 事件类型] | 事件名稱。 | 是 |
| [!UICONTROL 事件時間] | 事件時間。 |  |
| [!UICONTROL Mixpanel相異ID] | 執行事件之使用者的唯一識別碼。 |  |
| [!UICONTROL 插入ID] | 事件的唯一識別碼，用於重複資料刪除。 |  |
| [!UICONTROL 事件屬性] | 包含事件的自訂屬性的JSON物件。 從提供原始JSON或使用一組簡化的鍵值輸入進行選取。 |  |

>[!NOTE]
>
>如需的詳細資訊，請參閱 [!DNL Mixpanel] 事件，請參閱 [正式檔案](https://developer.mixpanel.com/reference/import-events#event).

![新增事件轉送規則動作設定。](../../../images/extensions/server/mixpanel/track-event-action.png)

一旦 [!UICONTROL 追蹤事件] 動作已新增至規則，您可以設定規則的條件，使其僅針對特定事件觸發，或者將條件區段留空以使規則針對所有事件觸發。

>[!IMPORTANT]
>
>如果您的網站使用 [!DNL Mixpanel] SDK，您可以繼續的下一個步驟 [驗證您的資料於 [!DNL Mixpanel]](#validate). 如果您沒有使用 [!DNL Mixpanel] SDK，您必須 [建立獨立的身分追蹤規則](#create-an-identity-tracking-rule) 以確保適當的事件和 `distinct_id` 值會傳送至 [!DNL Mixpanel] 當發生使用者識別事件時。

## 驗證中的資料 [!DNL Mixpanel] {#validate}

如果您的實施成功且已收集事件，您將會在 [[!DNL Mixpanel] 主控台](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

檢查 [!DNL Mixpanel] 已合併填入電子郵件值的貼文登入事件和使用時建立的事件 **[!UICONTROL 傳送事件]**. 如果實作正確， [!DNL Mixpanel] 會將它們與單一檔案建立關聯 [使用者設定檔](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## 后续步骤

本指南說明如何將轉換事件傳送至 [!DNL Mixpanel] 使用事件轉送。 此事件轉送擴充功能會利用 [!DNL Mixpanel] SDK和JavaScript API。 如需這些基礎技術的詳細資訊，請參閱正式檔案：

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
