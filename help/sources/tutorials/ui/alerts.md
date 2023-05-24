---
keywords: Experience Platform；首頁；熱門主題；警報
description: 您可以在建立資料流時訂閱警示，以接收有關資料流執行狀態、成功或失敗的警示訊息。
title: 訂閱UI中的內容感知警報
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: 3f7f66c0d58d127299ad12027869ca0e9837f5cd
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 5%

---

# 訂閱UI中來源資料流的警報

>[!NOTE]
>
>非生產沙箱不支援警報。 若要訂閱警報，您必須確保使用生產沙箱。

Adobe Experience Platform可讓您訂閱有關Adobe Experience Platform活動的事件型警報。 警報可減少或免除輪詢 [[!DNL Observability Insights] API](../../../observability/api/overview.md) 以檢查工作是否已完成、是否已到達工作流程中的某個里程碑，或是否已發生任何錯誤。

建立資料流以接收有關資料流執行的狀態、成功或失敗的警報訊息時，您可以訂閱警報。

本檔案提供訂閱來源資料流接收警示訊息的步驟。

## 快速入门

本檔案需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [可觀察性](../../../observability/home.md)： [!DNL Observability Insights] 可讓您透過使用統計量度和事件通知來監控Platform活動。
   * [警報](../../../observability/alerts/overview.md)：當您的Platform作業達到特定條件集時（例如系統違反臨界值時會發生問題），Platform可以向您組織中訂閱警報訊息的任何使用者傳送警報訊息。

## 訂閱UI中的警示 {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="订阅源提醒"
>abstract="提醒可让您接收基于源数据流状态的通知。您可以设置提醒通知，以便在数据流已启动、成功、失败或未提取任何数据时获得更新。"
>text="Learn more in documentation"

>[!IMPORTANT]
>
>您必須啟用Platform帳戶的即時電子郵件通知，才能接收資料流的電子郵件警示通知。

您可以在以下期間為資料流啟用警報： [!UICONTROL 資料流詳細資料] 「來源」工作區中「來源」工作流程的步驟。

![資料流 — 詳細資料](../../images/tutorials/alerts/dataflow-detail.png)

來源資料流的可用警報包括：

| 警报 | 描述 |
| --- | --- |
| 來源資料流執行開始 | 此警報會在來源資料流啟動時傳送訊息給您。 |
| 來源資料流執行成功 | 當來源中的資料成功擷取到Platform時，此警報會傳送訊息給您。 |
| 來源資料流執行失敗 | 如果您的資料流發生錯誤，此警報會傳送訊息給您。 |
| ~~來源資料流缺乏擷取~~ | ~~如果內嵌延遲超過7小時且沒有資料內嵌到Platform，此警報會傳送訊息給您。~~ <br>**注意：** 您將不會再收到警示，因為此警示已過時。 |

選取您要訂閱的警示，然後選取 **[!UICONTROL 下一個]** 以檢閱並完成您的資料流。

![選取警示](../../images/tutorials/alerts/select-alerts.png)

如需在UI中建立來源資料流的詳細步驟，請參閱下列指南：

* [Advertising](./dataflow/advertising.md)
* [雲端儲存空間](./dataflow/batch/cloud-storage.md)
* [CRM](./dataflow/crm.md)
* [数据库](./dataflow/databases.md)
* [電子商務](./dataflow/ecommerce.md)
* [本機檔案](./create/local-system/local-file-upload.md)
* [行銷自動化](./dataflow/marketing-automation.md)
* [付款](./dataflow/payments.md)
* [通訊協定](./dataflow/protocols.md)

## 接收警示

資料流執行後，您可以透過UI或電子郵件接收警報。

### 在UI中

警報會在UI中以Platform UI頂端標題中的通知圖示表示。 選取通知圖示以檢視與資料流相關的特定警報訊息。

![通知](../../images/tutorials/alerts/notification.png)

此時會顯示通知面板，其中顯示您所建立之資料流上的狀態更新清單。

![警報視窗](../../images/tutorials/alerts/alert-window.png)

您可以將滑鼠指標暫留在警示訊息上，將其標示為已讀取，也可以選取時鐘圖示來設定資料流狀態的未來提醒。

![提醒](../../images/tutorials/alerts/remind-me.png)

選取警報訊息以檢視資料流的特定資訊。

![select-alert-message](../../images/tutorials/alerts/select-alert-message.png)

此 [!UICONTROL 資料流執行概觀] 頁面便會顯示。 畫面的上半部分會顯示資料流的概觀，包括其屬性、對應資料流執行ID和高級別錯誤摘要的相關資訊。

![資料流 — 概觀](../../images/tutorials/alerts/dataflow-overview.png)

頁面下半部會顯示任何 [!UICONTROL 資料流執行錯誤] 在資料流執行階段發生的錯誤。 從這裡，您可以預覽錯誤診斷或使用 [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) 以下載與您的資料流對應的錯誤診斷或檔案資訊清單。

![資料流 — 執行 — 錯誤](../../images/tutorials/alerts/dataflow-run-error.png)

如需處理資料流錯誤的詳細資訊，請參閱以下指南： [在UI中監控來源資料流](../../../dataflows/ui/monitor-sources.md).

### 透過電子郵件

資料流的警報也會透過電子郵件傳送給您。 選取電子郵件內文中的資料流名稱，以檢視資料流的詳細資訊。

![电子邮件](../../images/tutorials/alerts/email.png)

與UI警報類似， [!UICONTROL 資料流執行概觀] 頁面隨即顯示，提供您一個介面來調查與資料流關聯的任何錯誤。

![資料流 — 概觀](../../images/tutorials/alerts/dataflow-overview.png)

## 訂閱和取消訂閱警示

您可以訂閱更多警報，或取消訂閱中現有資料流的已建立警報。 [!UICONTROL 資料流] 頁面。 從清單中找出您建立的資料流，然後選取省略符號(`...`)，以檢視選項的下拉式功能表。 接下來，選取 **[!UICONTROL 訂閱警示]** 修改資料流的警示設定。

![選項](../../images/tutorials/alerts/options.png)

隨即出現快顯視窗，為您提供來源警示清單。 選取您要訂閱的警示，或取消選取您要取消訂閱的警示。 完成後，選取 **[!UICONTROL 儲存]**.

![保存](../../images/tutorials/alerts/save.png)

## 后续步骤

本檔案逐步說明如何訂閱來源資料流的內容感知警報。 如需詳細資訊，請參閱 [警報UI指南](../../../observability/alerts/ui.md).