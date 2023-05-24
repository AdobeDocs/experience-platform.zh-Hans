---
title: 事件轉送概觀
description: 了解 Adobe Experience Platform 中的事件转发，通过此功能，无需更改您的标记实施，即可使用 Platform Edge Network 执行任务。
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: eb9d2f9a233f4214057db5136f32fc1290ece63c
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 7%

---

# 事件轉送概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

Adobe Experience Platform中的事件轉送可讓您將收集的事件資料傳送至目的地，以進行伺服器端處理。 事件轉送使用Adobe Experience Platform Edge Network執行通常在使用者端上完成的工作，以降低網頁和應用程式的負載。 以與標籤類似的方式實作，事件轉送規則可以轉換資料並傳送至新目的地，但此資料不會從使用者端應用程式（如網頁瀏覽器）傳送，而是從Adobe的伺服器傳送。

本檔案提供Platform中事件轉送的整體概觀。

![資料收集生態系統中的事件轉送](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>如需事件轉送如何在Platform的資料收集生態系統中適應的詳細資訊，請參閱 [資料彙集概觀](../../../collection/home.md).

事件轉送與Adobe Experience Platform結合 [Web SDK](../../../edge/home.md) 和 [行動SDK](https://aep-sdks.gitbook.io/docs/) 提供下列優點：

**效能**：

* 從包含資料裝載的頁面發出單一呼叫，然後這些資料在伺服器端組成聯盟，以減少使用者端網路流量，並為客戶提供更快速的體驗。
* 減少載入網頁所需的時間以改善網站效能。
* 減少提供您的體驗並將資料傳送至許多目的地所需的使用者端技術數量。

**資料控管**：

* 增加透明度，並控制要在所有屬性中將哪些資料傳送至何處。

## 事件轉送與標籤之間的差異 {#differences-from-tags}

在設定方面，事件轉送使用許多與標籤相同的概念，例如 [規則](../managing-resources/rules.md)， [資料元素](../managing-resources/data-elements.md)、和 [擴充功能](../managing-resources/extensions/overview.md). 兩者之間的主要差異可概括如下：

* 標籤 **收集** 來自網站或原生行動應用程式的事件資料，並傳送至Platform Edge Network。
* 事件轉送 **傳送** 從Platform Edge Network傳入事件資料至端點，該端點代表最終目的地或端點，提供您要用來擴充原始裝載的資料。

雖然標籤會使用Platform Web和Mobile SDK直接從您的網站或原生行動應用程式收集事件資料，但事件轉送需先透過Platform Edge Network傳送事件資料，才能轉送至目的地。 換言之，您必須在數位屬性上實作Platform Web或Mobile SDK （透過標籤或使用原始程式碼），才能使用事件轉送。

### 属性 {#properties}

事件轉送會維護其自身與標籤分開的屬性儲存，您可以在Experience PlatformUI或資料收集UI中透過選取這些屬性來檢視 **[!UICONTROL 事件轉送]** 左側導覽列中。

![資料收集UI中的事件轉送屬性](../../images/ui/event-forwarding/overview/properties.png)

所有事件轉送屬性清單 **[!UICONTROL Edge]** 作為他們的平台。 它們不會區分Web或行動裝置，因為它們只會處理從Platform Edge Network收到的資料，而該網路本身可同時接收來自Web和行動平台的事件資料。

### 扩展 {#extensions}

事件轉送有其專屬的相容擴充功能目錄，例如 [核心](../../extensions/server/core/overview.md) 擴充功能和 [Adobe雲端聯結器](../../extensions/server/cloud-connector/overview.md) 副檔名。 您可以在UI中檢視事件轉送屬性的可用擴充功能，方法是選取 **[!UICONTROL 擴充功能]** 在左側導覽列中，後面接著 **[!UICONTROL 目錄]**.

![資料收集UI中的事件轉送擴充功能](../../images/ui/event-forwarding/overview/extensions.png)

### 数据元素 {#data-elements}

事件轉送中可用的資料元素型別僅限於相容的目錄 [擴充功能](#extensions) 會提供這些資訊。

雖然在事件轉送中，資料元素本身的建立與設定方式與標籤相同，但在如何參照Platform Edge Network的資料方面，有一些重要的語法差異。

#### 引用Platform Edge Network的資料 {#data-element-path}

若要參照來自Platform Edge Network的資料，您必須建立提供該資料的有效路徑的資料元素。 在UI中建立資料元素時，請選取 **[!UICONTROL 核心]** 擴充功能和 **[!UICONTROL 路徑]** 型別。

此 **[!UICONTROL 路徑]** 資料元素的值必須遵循此模式 `arc.event.{ELEMENT}` (例如： `arc.event.xdm.web.webPageDetails.URL`)。 必須正確指定此路徑，才能傳送資料。

![用於事件轉送的路徑型別資料元素範例](../../images/ui/event-forwarding/overview/data-reference.png)

### 规则 {#rules}

在事件轉送屬性中建立規則的運作方式與標籤類似，主要差異在於您無法選取事件作為規則元件。 事件轉送規則會處理所有從接收的事件。 [資料串流](../../../edge/datastreams/overview.md) 並在符合特定條件時將事件轉送至目的地。

此外，有一個30秒的逾時，會套用至單一事件，因為單一事件會在事件轉送屬性內的所有規則（以及因此產生的所有動作）中處理。 這表示單一事件的所有規則和所有動作都必須在此時間範圍內完成。

![資料收集UI中的事件轉送規則](../../images/ui/event-forwarding/overview/rules.png)

#### 数据元素标记化 {#tokenization}

在標籤規則中，資料元素會使用 `%` 位於資料元素名稱的開頭和結尾處(例如： `%viewportHeight%`)。 在事件轉送規則中，資料元素會改用代碼化 `{{` 開頭和 `}}` 位於資料元素名稱結尾(例如： `{{viewportHeight}}`)。

![用於事件轉送的路徑型別資料元素範例](../../images/ui/event-forwarding/overview/tokenization.png)

#### 规则的操作顺序 {#action-sequencing}

此 [!UICONTROL 動作] 事件轉送規則的區段一律依序執行。 例如，如果規則有兩個動作，則第二個動作要等到前一個動作完成時才會開始執行（而且如果預期端點會回應，則表示該端點已回應）。 您在保存规则时，应确保操作顺序正确。此執行序列無法像使用標籤規則時一樣以非同步方式執行。

## 秘密 {#secrets}

事件轉送可讓您建立、管理和儲存秘密，這些秘密可用於驗證您所傳送資料的伺服器。 請參閱指南： [秘密](./secrets.md) 不同型別的可用密碼型別，以及在UI中如何實作。

## 后续步骤

本檔案提供事件轉送的高層級簡介。 如需如何為貴組織設定此功能的詳細資訊，請參閱 [快速入門手冊](./getting-started.md).
