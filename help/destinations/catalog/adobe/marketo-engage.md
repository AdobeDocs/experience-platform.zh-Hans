---
title: Marketo Engage目的地
description: Marketo Engage是唯一適用於行銷、廣告、分析和商務的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化和管理活動，從CRM銷售機會管理和客戶參與，到以帳戶為基礎的行銷和收入歸因。
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: e68bbc07f7d2e4e05b725cbef37a1810a5825742
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 1%

---

# Marketo Engage目的地 {#beta-marketo-engage-destination}

## 目的地變更記錄檔 {#changelog}

>[!IMPORTANT]
>
>隨著版本的 [增強的Marketo V2目的地聯結器](/help/release-notes/2022/july-2022.md#destinations)，您現在會在目的地目錄中看到兩個Marketo卡片。
>* 如果您已將資料啟用至 **[!UICONTROL Marketo V1]** 目的地：請建立新的資料流至 **[!UICONTROL Marketo V2]** 目的地並刪除現有的資料流 **[!UICONTROL Marketo V1]** 2023年2月前抵達目的地。 截至該日期， **[!UICONTROL Marketo V1]** 目的地卡片將會移除。
>* 如果您尚未建立任何資料流至 **[!UICONTROL Marketo V1]** 目的地，請使用新的 **[!UICONTROL Marketo V2]** 卡片，用來連線及匯出資料至Marketo。


![並排檢視中的兩個Marketo目的地卡片影像。](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Marketo V2目的地的改良專案包括：

* 在 **[!UICONTROL 排程區段]** 啟動工作流程的步驟，在Marketo V1中，您需要手動新增 **對應ID** 以成功將資料匯出至Marketo。 Marketo V2不再需要此手動步驟。
* 在 **[!UICONTROL 對應]** 啟動工作流程的步驟，在Marketo V1中，您僅能將XDM欄位對應到Marketo中的三個目標欄位： `firstName`， `lastName`、和 `companyName`. 透過Marketo V2版本，您現在可以將XDM欄位對應到Marketo中的更多欄位。 如需詳細資訊，請閱讀 [支援的屬性](#supported-attributes) 區段下方。

## 概述 {#overview}

[!DNL Marketo Engage] 是唯一適用於行銷、廣告、分析和商務的端對端客戶體驗管理(CXM)解決方案。 它可讓您自動化和管理活動，從CRM銷售機會管理和客戶參與，到以帳戶為基礎的行銷和收入歸因。

目的地可讓行銷人員將在Adobe Experience Platform中建立的區段推送至Marketo，並在其中顯示為靜態清單。

## 支援的身分和屬性 {#supported-identities-attributes}

>[!NOTE]
>
>在 [對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) （在啟用目標工作流程中），它是 *強制* 對應身分和 *可選* 以對應屬性。 從「身分名稱空間」標籤對應電子郵件和/或ECID是最重要的事情，可確保人員在Marketo中相配。 對應電子郵件可確保最高的符合率。

### 支援的身分 {#supported-identities}

| 目標身分 | 描述 |
|---|---|
| ECID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請參閱以下檔案： [ECID](/help/identity-service/ecid.md) 以取得詳細資訊。 |
| 电子邮件 | 代表電子郵件地址的名稱空間。 這類名稱空間通常與單一人員相關聯，因此可用於跨不同管道識別該人員。 |

{style="table-layout:auto"}

### 支援的屬性 {#supported-attributes}

您可以將屬性從Experience Platform對應至貴組織在Marketo中可以存取的任何屬性。 在Marketo中，您可以使用 [說明API要求](https://developers.marketo.com/rest-api/lead-database/leads/#describe) 以擷取貴組織有權存取的屬性欄位。

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 项目 | 类型 | 注释 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 区段导出]** | 您正在匯出區段（受眾）的所有成員，而這些區段包含的識別碼（電子郵件、ECID）用於 [!DNL Marketo Engage] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦設定檔根據區段評估在Experience Platform中更新，聯結器就會將更新傳送至下游的目標平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 設定目的地並啟用區段 {#set-up}

>[!IMPORTANT]
> 
>* 若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions).
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。


如需如何設定目的地及啟用區段的詳細指示，請閱讀 [將Adobe Experience Platform區段推送至Marketo靜態清單](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) (位於Marketo檔案中)。

以下影片也會示範設定Marketo目的地和啟用區段的步驟。

>[!IMPORTANT]
>
>影片並未完全反映目前的功能。 如需最新資訊，請參閱上方連結的指南。 視訊的下列部分已過時：
> 
>* 您應在Experience PlatformUI中使用的目的地卡為 **[!UICONTROL Marketo V2]**.
>* 影片未顯示新的 **[!UICONTROL 個人建立]** 連線至目標工作流程中的選取器欄位。
>* 影片中叫用的兩個限制不再適用。 除了錄製影片時支援的區段會籍資訊外，您現在可以對應許多其他設定檔屬性欄位。 您也可以將尚未存在於Marketo靜態清單中的區段成員匯出至Marketo，這些成員將會新增至清單中。
>* 在 **[!UICONTROL 排程區段步驟]** 在Marketo V1中，您需要手動新增 **[!UICONTROL 對應ID]** 以成功將資料匯出至Marketo。 Marketo V2不再需要此手動步驟。


>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
