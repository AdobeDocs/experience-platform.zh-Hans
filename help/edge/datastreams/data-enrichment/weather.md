---
title: 使用來自DNL天氣頻道的天氣資料
description: 使用來自DNL The Weather Channel的天氣資料來增強您透過資料串流收集的資料。
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---

# 使用來自的天氣資料 [!DNL The Weather Channel]

Adobe已與 [!DNL [The Weather Company]](https://www.ibm.com/weather) 透過資料串流收集的資料，以納入美國天氣的其他情境。 您可以在Experience Platform中使用此資料進行分析、鎖定目標和建立區段。

有3種資料型別可從取得 [!DNL The Weather Channel]：

* **[!UICONTROL 目前天氣]**：使用者目前的天氣狀況（根據其位置）。 這包括目前的溫度、偏好、雲端涵蓋範圍等。
* **[!UICONTROL 天氣預報]**：此預測包含使用者位置的1、2、3、5、7和10天預測。
* **[!UICONTROL 觸發器]**：觸發器是對應至不同語意天氣條件的特定組合。 天氣觸發程式有三種不同型別：

   * **[!UICONTROL 天氣觸發程式]**：語義上有意義的情況，例如冷或雨天。 不同氣候之間的定義可能有所不同。
   * **[!UICONTROL 產品觸發程式]**：導致購買不同型別產品的條件。 例如：寒冷天氣預報可能代表您更可能購買雨衣。
   * **[!UICONTROL 惡劣天氣觸發程式]**：嚴重天氣警告，例如冬季風暴或颶風警告。

## 先决条件 {#prerequisites}

在使用天氣資料之前，請確定您符合下列先決條件：

* 您必須授權您將使用的天氣資料，從 [!DNL The Weather Channel]. 接著，他們會在您的帳戶上啟用該功能。
* 天氣資料只能透過資料串流使用。 若要使用天氣資料，您必須使用 [!DNL Web SDK]， [!DNL Mobile Edge Extension] 或 [伺服器API](../../../server-api/overview.md) 以善用此資料。
* 您的資料流必須具有 [[!UICONTROL 地理位置]](../configure.md#advanced-options) 已啟用。
* 新增 [天氣欄位群組](#schema-configuration) 至您正在使用的結構描述。

## 配置中 {#provisioning}

在您授權資料後，資料來自 [!DNL The Weather Channel]，可讓您的帳戶存取資料。 接下來，您必須聯絡Adobe客戶服務，才能在資料流上啟用資料。 啟用後，資料將自動附加。

您可以透過使用偵錯工具執行邊緣追蹤，或使用Assurance追蹤點選，來驗證是否正在新增該量度。 [!DNL Edge Network].

### 結構描述設定 {#schema-configuration}

您必須將天氣欄位群組新增至與您在資料流中使用的事件資料集相對應的Experience Platform結構描述。 有五個可用的欄位群組：

* [!UICONTROL 天氣預報]
* [!UICONTROL 目前天氣]
* [!UICONTROL 產品觸發程式]
* [!UICONTROL 相對觸發程式]
* [!UICONTROL 惡劣天氣觸發程式]

## 存取天氣資料 {#access-weather-data}

您的資料獲得授權並可供使用後，您就可以透過Adobe服務以各種方式存取資料。

### Adobe Analytics {#analytics}

在 [!DNL Adobe Analytics]，您便能透過處理規則對應天氣資料，以及您其他的 [!DNL XDM] 結構描述。

您可以在以下位置找到可對應的欄位清單： [天氣參考](weather-reference.md) 頁面。 與所有專案一樣 [!DNL XDM] 結構描述，索引鍵會加上前置詞 `a.x`. 例如，欄位名為 `weather.current.temperature.farenheit` 將顯示在 [!DNL Analytics] 作為 `a.x.weather.current.temperature.farenheit`.

![處理規則介面](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### 了解 Adobe Customer Journey Analytics {#cja}

在 [!DNL Adobe Customer Journey Analytics]，則可在資料流中指定的資料集中取得天氣資料。 只要天氣屬性為 [已新增至您的結構描述](#prerequisites-prerequisites)，這些區段將可供 [新增至資料檢視](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html) 在 [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

天氣資料可在 [Real-time Customer Data Platform](../../../rtcdp/overview.md)，用於區段。 天氣資料會附加至事件。

![顯示天氣事件的區段產生器](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

由於天氣狀況經常變更，Adobe建議您為區段設定時間限制，如上例所示。 在最後一天或兩天寒冷一天比六個月前寒冷一天的影響更大。

請參閱 [天氣參考](weather-reference.md) 以取得可用欄位。

### Adobe Target {#target}

在 [!DNL Adobe Target]，您可使用天氣資料即時推動個人化。 天氣資料傳遞至 [!DNL Target] 作為 [!UICONTROL mBox] 引數，而且您可以透過自訂 [!UICONTROL mBox] 引數。

![Target對象產生器](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

引數為 [!DNL XDM] 特定欄位的路徑。 請參閱 [天氣參考](weather-reference.md) 可用欄位及其對應路徑。

## 后续步骤 {#next-steps}

閱讀本檔案後，您現在已更瞭解如何在各種Adobe解決方案中使用天氣資料。 若要進一步瞭解天氣資料欄位對應，請參閱 [欄位對應參考](weather-reference.md).
