---
title: AWS擴充功能概觀
description: 瞭解Adobe Experience Platform中用於事件轉送的AWS擴充功能。
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 3%

---

# [!DNL AWS] 擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) 是雲端運算平台，提供各種服務，例如分散式運算、資料庫儲存、內容傳遞，以及客戶關係管理(CRM)和企業資源規劃(ERP)的軟體即服務(SaaS)整合服務。

此 [!DNL AWS] [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能運用 [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) 將事件從Adobe Experience Platform Edge Network傳送至 [!DNL AWS] 以進一步處理。 本指南說明如何安裝擴充功能，以及在事件轉送規則中運用其功能。

## 先决条件

您必須擁有 [!DNL AWS] 具有現有帳戶的帳戶 [!DNL Kinesis] 資料串流，以便使用此擴充功能。 如果您沒有既有的資料流，請參閱 [!DNL AWS] 檔案： [使用建立新資料流 [!DNL AWS] 管理主控台](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## 安裝擴充功能 {#install}

若要安裝 [!DNL AWS] 擴充功能，導覽至資料收集UI或Experience PlatformUI並選取 **[!UICONTROL 事件轉送]** 從左側導覽列中。 從這裡，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，選取 **[!UICONTROL 擴充功能]** 在左側導覽中，然後選取 **[!UICONTROL 目錄]** 標籤。 搜尋 [!UICONTROL AWS] 卡片，然後選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL 安裝] 按鈕已選取 [!UICONTROL AWS] 資料收集UI中的擴充功能。](../../../images/extensions/server/aws/install.png)

在下一個畫面中，您必須提供您的連線認證 [!DNL AWS] 帳戶。 具體而言，您必須提供 [!DNL AWS] 存取金鑰ID和秘密存取金鑰。 如果您不知道這些值，請參閱 [!DNL AWS] 檔案： [如何取得您的存取金鑰ID和秘密存取金鑰](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![擴充功能組態檢視中新增的存取金鑰ID和機密存取金鑰。](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>存取原則需要附加至 [!DNL AWS] 用來產生存取認證的帳戶。 此原則必須設定為授與存取許可權，才能將資料傳送至 [!DNL Kinesis] 資料串流。 請參閱 **範例2** 在 [!DNL AWS] 檔案於 [的原則範例 [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) 以瞭解應如何定義原則。

完成後，選取 **[!UICONTROL 儲存]** 且已安裝擴充功能。

## 設定事件轉送規則 {#rule}

安裝擴充功能後，建立新的事件轉送 [規則](../../../ui/managing-resources/rules.md) 並視需要設定其條件。 設定規則的動作時，選取 **[!UICONTROL AWS]** 擴充功能，然後選取 **[!UICONTROL 傳送資料至Kinesis Data Stream]** （動作型別）。

![此 [!UICONTROL 傳送資料至Kinesis Data Stream] 為資料收集UI中的規則選取的動作型別。](../../../images/extensions/server/aws/select-action-type.png)

右側面板會更新，以顯示資料傳送方式的設定選項。 具體而言，您必須指派 [資料元素](../../../ui/managing-resources/data-elements.md) 至各種屬性，這些屬性代表 [!DNL Event Hub] 設定。

![的設定選項 [!UICONTROL 傳送資料至Kinesis Data Stream] UI中顯示的動作型別。](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis資料流詳細資料]**

| 輸入 | 描述 |
| --- | --- |
| [!UICONTROL 資料流名稱] | 此事件轉送規則將傳送資料記錄到的資料流名稱。 |
| [!UICONTROL AWS地區] | 此 [!DNL AWS] 區域 [!DNL Kinesis] 資料串流已建立。 |
| [!UICONTROL 分割區索引鍵] | 此 [分割區索引鍵](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) 將資料傳送至資料流時，擴充功能會使用的擴充功能。<br><br>[!DNL Kinesis Data Streams] 將屬於某個資料流的資料記錄分割成多個分片。 它會使用隨每個資料記錄傳送的分割區索引鍵，來判斷指定資料記錄屬於哪個分片。<br><br>分發客戶的正確分割索引鍵可能是客戶編號，因為每個客戶的編號不同。 錯誤的分割區金鑰可能是它們的郵遞區號，因為它們可能都住在附近的同一個區域。 一般而言，您應該選擇具有最高範圍之不同潛在值的分割區索引鍵。 請參閱 [!DNL AWS] 文章： [縮放您的 [!DNL Kinesis] 資料串流](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) 以取得管理磁碟分割索引鍵的最佳實務。 |

{style="table-layout:auto"}

**[!UICONTROL 数据]**

| 輸入 | 描述 |
| --- | --- |
| [!UICONTROL 裝載] | 此欄位包含將轉送至 [!DNL Kinesis] 資料流，JSON格式。<br><br>在 **[!UICONTROL 原始]** 選項，您可以將JSON物件直接貼到提供的文字欄位中，或選取資料元素圖示(![資料集圖示](../../../images/extensions/server/aws/data-element-icon.png))以從現有資料元素清單中選取來代表裝載。<br><br>您也可以使用 **[!UICONTROL JSON索引鍵值配對編輯器]** 用於透過UI編輯器手動新增每個索引鍵/值組的選項。 每個值都可表示為原始輸入，或是改為選取資料元素。 |

{style="table-layout:auto"}

完成後，選取 **[!UICONTROL 保留變更]** 以將動作新增至規則設定。 如果您對規則滿意，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新的事件轉送 [建置](../../../ui/publishing/builds.md) 以啟用程式庫的變更。

## 后续步骤

本指南說明如何將資料傳送至 [!DNL Kinesis Data Streams] 使用 [!DNL AWS] 事件轉送擴充功能。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
