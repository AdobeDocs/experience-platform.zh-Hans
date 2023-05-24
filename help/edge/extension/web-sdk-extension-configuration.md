---
title: 設定Adobe Experience Platform Web SDK擴充功能
description: 如何在UI中設定Adobe Experience Platform Web SDK標籤擴充功能。
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 6%

---

# 設定Adobe Experience Platform Web SDK擴充功能

Adobe Experience Platform Web SDK標籤擴充功能會透過Adobe Experience Cloud Edge Network，將資料從Web屬性傳送至Adobe Experience Platform。 擴充功能可讓您將資料串流至Platform、同步身分、處理客戶同意訊號，以及自動收集內容資料。

本文介紹如何在UI中設定擴充功能。

## 快速入门

如果已經為某個屬性安裝了Platform Web SDK擴充功能，請在UI中開啟該屬性，然後選取 **[!UICONTROL 擴充功能]** 標籤。 在Platform Web SDK底下，選取 **[!UICONTROL 設定]**.

![](../assets/extension/overview/configure.png)

如果您尚未安裝擴充功能，請選取 **[!UICONTROL 目錄]** 標籤。 從可用擴充功能清單中，找到Platform Web SDK擴充功能，然後選取「 」 **[!UICONTROL 安裝]**.

![](../assets/extension/overview/install.png)

在這兩種情況下，您都會進入Platform Web SDK的設定頁面。 以下各節說明擴充功能的設定選項。

![](../assets/extension/overview/config-screen.png)

## 一般設定選項

頁面頂端的設定選項可告知Adobe Experience Platform將資料路由到何處以及要在伺服器上使用哪些設定。

### [!UICONTROL 名称]

Adobe Experience Platform Web SDK擴充功能支援頁面上的多個執行個體。 此名稱可用來透過標籤設定將資料傳送至多個組織。

擴充功能的名稱預設為&quot;[!DNL alloy]「。 但是，您可以将实例名称更改为任何有效的 JavaScript 对象名称。

### **[!UICONTROL IMS 组织 ID]**

此 [!UICONTROL IMS組織ID] 是您想要在Adobe時傳送資料的組織。 大多數情況下，會使用自動填入的預設值。 頁面上有多個例項時，請使用此欄位填入您要傳送資料的第二個組織的值。

### **[!UICONTROL 边缘域]**

此 [!UICONTROL 邊緣網域] 是Adobe Experience Platform擴充功能傳送及接收資料的網域。 Adobe建議對此擴充功能使用第一方網域(CNAME)。 默认的第三方域适用于开发环境，但不适合生产环境。[此处](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hans)列出了有关如何设置第一方 CNAME 的说明。

## [!UICONTROL 数据流]

當請求傳送至Adobe Experience Platform Edge Network時，會使用資料串流ID來參考伺服器端設定。 您可以更新設定，而無須在您的網站上變更程式碼。

請參閱指南： [資料串流](../datastreams/overview.md) 以取得詳細資訊。


## [!UICONTROL Privacy]

![](../assets/extension/overview/privacy.png)

此 [!UICONTROL 隱私權] 區段可讓您設定SDK如何處理來自您網站的使用者同意訊號。 具體來說，它可讓您選取在未提供其他明確同意偏好設定時假設為使用者的預設同意層級。 預設同意層級不會儲存至使用者的設定檔。 下表會劃分每個選項的含意：

| [!UICONTROL 預設同意層級] | 描述 |
| --- | --- |
| [!UICONTROL 在] | 收集在使用者提供同意偏好設定之前發生的事件。 |
| [!UICONTROL 輸出] | 捨棄在使用者提供同意偏好設定之前發生的事件。 |
| [!UICONTROL 擱置中] | 在使用者提供同意偏好設定之前發生的佇列事件。 提供同意偏好設定時，會根據提供的偏好設定收集或捨棄事件。 |
| [!UICONTROL 資料元素提供] | 預設同意層級由您定義的個別資料元素決定。 使用此選項時，您必須使用提供的下拉式選單指定資料元素。 |

如果您的業務操作需要明確的使用者同意，請使用「退出」或「擱置中」。

## [!UICONTROL 标识]

![](../assets/extension/overview/identity.png)

### [!UICONTROL 從VisitorAPI移轉ECID]

默认启用选项。啟用此功能後，SDK就能讀取AMCV和s_ecid Cookie，並設定Visitor.js使用的AMCV Cookie。 移轉至Adobe Experience Platform Web SDK時，此功能很重要，因為有些頁面可能仍在使用Visitor.js。 它可讓SDK繼續使用相同的ECID，因此不會將使用者識別為兩個不同的使用者。

### [!UICONTROL 使用第三方Cookie]

此選項可讓SDK嘗試將使用者識別碼儲存在第三方Cookie中。 如果成功，則會在使用者瀏覽多個網域時將其識別為單一使用者，而不是在每個網域上將其識別為單獨的使用者。 如果啟用此選項，如果瀏覽器不支援第三方Cookie或使用者已設定不允許第三方Cookie，SDK仍可能無法將使用者識別碼儲存在第三方Cookie中。 在此情況下，SDK只會將識別碼儲存在第一方網域中。

## [!UICONTROL 个性化]

![](../assets/extension/overview/personalization.png)

如果您想要在個人化內容載入時隱藏網站上的某些零件，您可以在預先隱藏樣式編輯器中指定要隱藏的元素。 然後您可以複製提供給您的預設預先隱藏程式碼片段，並將其貼到中 `<head>`HTML網站的元素。

## [!UICONTROL 数据收集]

![](../assets/extension/overview/data-collection.png)

### [!UICONTROL 回呼函式]

擴充功能中提供的回呼函式也稱為 [`onBeforeEventSend` 函式](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=zh-Hans) 在程式庫中。 此函式可讓您在事件傳送至Adobe Edge Network之前，先全域修改事件。 如需如何使用此函式的詳細資訊，請參閱 [此處](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL 按一下資料收集]

SDK可以自動收集您的連結點選資訊。 此功能預設為啟用，但可使用此選項加以停用。 如果連結包含「 」中列出的下載運算式之一，這些連結也會標示為下載連結。 [!UICONTROL 下載連結限定詞] 文字方塊。 Adobe會提供您一些預設的下載連結限定詞，但這些限定詞可隨時編輯。

### [!UICONTROL 自動收集的內容資料]

依預設，SDK會收集關於裝置、Web、環境和地標內容的特定內容資料。 如果您想檢視Adobe收集的資訊清單，可以找到 [此處](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). 如果您不想收集這些資料，或只想收集特定類別的資料，可以變更這些選項。

## [!UICONTROL 資料流設定覆寫]

資料串流覆寫可讓您為資料串流定義其他設定，這些設定會透過Web SDK傳遞到Edge Network。

這有助於您觸發與預設資料流行為不同的資料流行為，而不會建立新的資料流或修改現有的設定。

資料流設定覆寫是兩個步驟的程式：

1. 首先，您必須在以下位置定義資料流設定覆寫： [資料流設定頁面](../datastreams/configure.md).
2. 然後，您必須透過Web SDK命令或使用Web SDK標籤擴充功能，將覆寫傳送至Edge Network。

檢視資料流 [設定覆寫檔案](../datastreams/overrides.md) 以取得有關如何覆寫資料流設定的詳細說明。

除了透過Web SDK命令傳遞覆寫外，您也可以在下面顯示的標籤擴充功能畫面中設定覆寫。

![此影像顯示Web SDK標籤擴充功能頁面中的資料流設定覆寫。](../assets/extension/overview/datastream-overrides.png)

## [!UICONTROL 高级设置]

![](../assets/extension/overview/advanced-settings.png)

### [!UICONTROL 邊緣基底路徑]

如果您需要變更用來與Adobe Edge Network互動的基本路徑，請使用此欄位。 這應該不需要更新，但在您參與Beta或Alpha版的情況下，Adobe可能會要求您變更此欄位。
