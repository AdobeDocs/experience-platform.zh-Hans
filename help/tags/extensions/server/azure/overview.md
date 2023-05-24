---
title: Microsoft Azure擴充功能概觀
description: 瞭解Adobe Experience Platform中用於事件轉送的Microsoft Azure擴充功能。
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 3%

---

# [!DNL Microsoft Azure] 擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

在 [!DNL Microsoft Azure]， [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) 是一種高度可擴充的即時資料匯入服務，可讓您處理和分析連線裝置和應用程式所產生的大量資料。 一旦資料收集到事件中樞中，就可以使用任何即時分析提供者或批次/儲存配接卡來轉換和儲存資料。

此 [!DNL Microsoft Azure] [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能運用 [!DNL Event Hubs] 將事件從Adobe Experience Platform Edge Network傳送至 [!DNL Azure] 以進一步處理。 本指南說明如何安裝擴充功能，以及在事件轉送規則中運用其功能。

## 先决条件

若要使用此擴充功能，您必須具備有效的 [!DNL Azure] 有權存取的帳戶 [!DNL Event Hubs]. 您也必須 [使用建立事件中樞 [!DNL Azure] 入口網站](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) 然後依照下列步驟進行。

## 安裝擴充功能

安裝Microsoft的方式 [!DNL Azure] 擴充功能，導覽至資料收集UI或Experience PlatformUI並選取 **[!UICONTROL 事件轉送]** 從左側導覽列中。 從這裡，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，選取 **[!UICONTROL 擴充功能]** 在左側導覽中，然後選取 **[!UICONTROL 目錄]** 標籤。 搜尋 [!UICONTROL Microsoft Azure] 卡片，然後選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL 安裝] 按鈕已選取 [!UICONTROL Microsoft Azure] 資料收集UI中的擴充功能。](../../../images/extensions/server/azure/install.png)

由於擴充功能沒有任何設定屬性，因此會立即將其新增至已安裝的擴充功能清單中。 您現在可以開始使用 [!DNL Event Hub] 設定事件轉送規則時的動作型別。

## 設定事件轉送規則 {#rule}

開始建立新的事件轉送規則，並視需要設定其條件。 選取規則的動作時，選取 **[!UICONTROL Microsoft Azure]** 針對擴充功能，然後選取「 」 **[!UICONTROL 傳送資料至事件中樞]** （動作型別）。

![此 [!UICONTROL 傳送資料至事件中樞] 為資料收集UI中的規則選取的動作型別。](../../../images/extensions/server/azure/select-action-type.png)

右側面板會更新，以顯示資料傳送方式的設定選項。 具體而言，您必須指派 [資料元素](../../../ui/managing-resources/data-elements.md) 至各種屬性，這些屬性代表 [!DNL Event Hub] 設定。

![的設定選項 [!UICONTROL 傳送資料至事件中樞] UI中顯示的動作型別。](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL 事件中心詳細資訊]**

| 輸入 | 描述 |
| --- | --- |
| [!UICONTROL 命名空间] | 的名稱 [!DNL Event Hubs] 您建立於 [設定事件中樞](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL 名称] | 事件中樞的名稱。 |
| [!UICONTROL SAS授權規則名稱] | 您整個專案的共用存取授權規則名稱 [!DNL Event Hubs] 名稱空間或您要傳送資料的特定事件中樞執行個體。 請參閱附錄中關於 [取得SAS授權值](#sas) 以取得詳細資訊。 |
| [!UICONTROL SAS存取金鑰] | 共用存取授權規則的主要金鑰，適用於您的整個系統 [!DNL Event Hubs] 名稱空間或您要傳送資料的特定事件中樞執行個體。 請參閱附錄中關於 [取得SAS授權值](#sas) 以取得詳細資訊。 |
| [!UICONTROL 資料分割ID] | [!DNL Event Hubs] 可讓您 [將事件直接傳送至特定分割區](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). 若要運用此功能，請提供您要接收事件的分割識別碼。 |

{style="table-layout:auto"}

**数据**

| 輸入 | 描述 |
| --- | --- |
| [!UICONTROL 裝載] | 此欄位包含將轉送至 [!DNL Event Hubs]. 資料可以是JSON物件、字串或資料元素。 |

{style="table-layout:auto"}

完成後，選取 **[!UICONTROL 保留變更]** 以將動作新增至規則設定。 如果您對規則滿意，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新的事件轉送 [建置](../../../ui/publishing/builds.md) 以啟用程式庫的變更。

## 后续步骤

本指南說明如何將資料傳送至 [!DNL Event Hubs] 使用 [!DNL Microsoft Azure] 事件轉送擴充功能。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).

## 附錄：取得SAS授權值 {#sas}

外部應用程式被授與存取權 [!DNL Event Hubs] 到 [共用存取權簽章(SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). 每個 [!DNL Event Hubs] 名稱空間和事件中心執行個體會在建立時自動指派預設SAS授權規則，但您也可以視需要為每個資源建立其他原則。

時間 [設定事件轉送規則](#rule) 使用 [!DNL Azure] 擴充功能上，您必須提供管理名稱空間或特定事件中樞的授權規則的名稱和主索引鍵，才能傳送資料。 有關如何從取得這些值的詳細資訊 [!DNL Azure] 入口網站，請參閱 [!DNL Azure] 檔案：

* [取得的SAS值 [!DNL Event Hubs] 名稱空間](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [取得名稱空間中特定事件中樞的SAS值](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

當您擁有必要的值後，授權規則名稱可以直接提供為設定輸入中的字串，或者您可以建立字串型別資料元素來參照它。 不過，主要金鑰必須先包含在事件轉送密碼中，才能在規則設定中提供該金鑰，以保護您的資料安全性。

在事件轉送UI中， [建立新密碼](../../../ui/event-forwarding/secrets.md) 並選取 **[!UICONTROL Token]** 作為秘密型別。 對於權杖值本身，請提供您先前複製的主金鑰。 建立密碼後，使用型別建立資料元素 **[!UICONTROL 密碼]** 並選取 [!DNL Event Hubs] 密碼來自清單。 設定機密資料元素後，您就可以在 **[!UICONTROL SAS存取金鑰]** 欄位。
