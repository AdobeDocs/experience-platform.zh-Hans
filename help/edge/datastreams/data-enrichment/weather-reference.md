---
title: 天氣資料欄位對應
description: 可用天氣資料欄位的參考頁面，這些欄位屬於與天氣頻道整合的一部分。
exl-id: bc0f158b-f9d0-424a-aa21-953e8380473f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '12238'
ht-degree: 0%

---

# 天氣資料欄位對應

Adobe已與 [!DNL [The Weather Company]](https://www.ibm.com/weather) 透過資料串流收集的資料，以納入美國天氣的其他情境。 您可以在Experience Platform中使用此資料進行分析、鎖定目標和建立區段。

此頁面列出可用於擴充受眾資料的所有可用欄位。

欄位會分成三個與欄位群組對齊的不同群組。

* [**[!UICONTROL 目前天氣]**](#current-weather)：使用者目前的天氣狀況（根據其位置）。 這包括目前的溫度、偏好、雲端涵蓋範圍等。
* [**[!UICONTROL 天氣預報]**](#forecast)：此預測包含使用者位置的1、2、3、5、7和10天預測。
* [**[!UICONTROL 觸發器]**](#triggers)：觸發器是對應至不同語意天氣條件的特定組合。 天氣觸發程式有三種不同型別：

   * **[!UICONTROL 相對觸發程式]**：語義上有意義的情況，例如冷或雨天。 不同氣候之間的定義可能有所不同。
   * **[!UICONTROL 產品觸發程式]**：導致購買不同型別產品的條件。 例如：寒冷天氣預報可能代表您更可能購買雨衣。
   * **[!UICONTROL 惡劣天氣觸發程式]**：嚴重天氣警告，例如冬季風暴或颶風警告。

## 目前天氣 {#current-weather}

使用者目前的天氣狀況（根據其位置）。

| 字段 | 描述 | XDM路徑 |
| --- | ---- | --- |
| [!UICONTROL 露點溫度（攝氏）] | 空氣必須恆壓冷卻達到飽和的溫度。 露點也是空氣濕度的間接測量值。 露點絕不會超過溫度。 當露點和溫度相等時，通常會形成雲或霧。 溫度與露點值愈接近，相對濕度愈高。 範圍 —80到100 (°F)或–62到37 (°C)。 以攝氏度為單位的溫度 | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL 溫度露點華氏] | 空氣必須恆壓冷卻達到飽和的溫度。 露點也是空氣濕度的間接測量值。 露點絕不會超過溫度。 當露點和溫度相等時，通常會形成雲或霧。 溫度與露點值愈接近，相對濕度愈高。 範圍 —80到100 (°F)或–62到37 (°C)。 以華氏度表示的溫度 | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL 過去一小時的降水量（英吋）] | 滾動小時液體沈澱量。 顯示的金額是請求時間的滾動時間（現在）。 以英吋為單位的沈澱 | `weather.current.precip1Hour.inches` |
| [!UICONTROL 過去一小時的降雨量] | 滾動小時液體沈澱量。 顯示的金額是請求時間的滾動時間（現在）。 降水（以毫米為單位） | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 正在滾動24小時液體沈澱量。 顯示的金額是請求時間的滾動時間（現在）。 以英吋為單位的沈澱 | `weather.current.precip24Hour.inches` |
| [!UICONTROL 過去24小時的降雨量] | 正在滾動24小時液體沈澱量。 顯示的金額是請求時間的滾動時間（現在）。 降水（以毫米為單位） | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL 降水持續6小時（英吋）] | 滾動六小時液體沈澱量。 顯示的金額是請求時間的滾動時間（現在）。 以英吋為單位的沈澱 | `weather.current.precip6Hour.inches` |
| [!UICONTROL 過去6小時的降雨量] | 滾動六小時液體沈澱量。 顯示的金額是請求時間的滾動時間（現在）。 降水（以毫米為單位） | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL 壓力變化] | 過去三小時內的壓力變化（毫巴）。 | `weather.current.pressureChange` |
| [!UICONTROL 壓力平均海平面] | 平均海平面壓力（毫巴）。  換句話說，就是海平面上的平均氣壓值。<br>範圍 — 精確到1/10th mb的毫巴。 | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL 相對濕度] | 空氣的相對濕度，定義為空氣中的水蒸氣量，與在恆定溫度下使空氣飽和所需的水蒸氣量的比率。 相對濕度一律以百分比表示。<br>範圍 — 0到100。 | `weather.current.relativeHumidity` |
| [!UICONTROL 雪花過去一小時公分] | 一小時降雪量。  顯示的金額是請求時間的滾動時間（現在）。 降雪公分 | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL 雪花過去一小時英吋] | 一小時降雪量。  顯示的金額是請求時間的滾動時間（現在）。 降雪單位（英吋） | `weather.current.snow1Hour.inches` |
| [!UICONTROL 雪24小時公分] | 二十四小時降雪量。  顯示的金額是請求時間的滾動時間（現在）。 降雪公分 | `weather.current.snow24Hour.centimeters` |
| 雪24小時英吋 | 二十四小時降雪量。  顯示的金額是請求時間的滾動時間（現在）。 降雪單位（英吋） | `weather.current.snow24Hour.inches` |
| [!UICONTROL 雪持續6小時公分] | 一小時降雪量。  顯示的金額是請求時間的滾動時間（現在）。 降雪公分 | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL 雪花持續6小時（英吋）] | 一小時降雪量。  顯示的金額是請求時間的滾動時間（現在）。 降雪單位（英吋） | `weather.current.snow6Hour.inches` |
| [!UICONTROL 日落時間] | UTC的日落時間。 | `weather.current.sunsetTime` |
| [!UICONTROL 攝氏溫度] | 以定義的測量單位表示的溫度。 範圍–140到140。 以攝氏度為單位的溫度 | `weather.current.temperature.celsius` |
| [!UICONTROL 華氏溫度] | 以定義的測量單位表示的溫度。 範圍–140到140。 以華氏度表示的溫度 | `weather.current.temperature.fahrenheit` |
| [!UICONTROL 24小時溫度變化] | 相較於24小時前報告的溫度變更。 以攝氏度為單位的溫度 | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL 24小時溫度變化華氏] | 相較於24小時前報告的溫度變更。 以華氏度表示的溫度 | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL 溫度感覺像攝氏度] | 明顯的溫度。 它代表由於風寒或熱指數的綜合影響，外露的人類皮膚上的空氣溫度「感覺」。<br>當溫度是65°F或更高的時候，「感覺相似」值代表計算的「熱指數」。  當溫度低於65°F時，「感覺類似」值表示計算出的風冷。<br>範圍–140到140。 以攝氏度為單位的溫度 | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL 溫度感覺像華氏度] | 明顯的溫度。 它代表由於風寒或熱指數的綜合影響，外露的人類皮膚上的空氣溫度「感覺」。<br>當溫度是65°F或更高的時候，「感覺相似」值代表計算的「熱指數」。  當溫度低於65°F時，「感覺類似」值表示計算出的風冷。<br>範圍–140到140。 以華氏度表示的溫度 | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL 自上午7點以來的最高溫度] | 自當地時間上午7點以來的最高溫度。 以攝氏度為單位的溫度 | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL 自上午7點開始溫度最高] | 自當地時間上午7點以來的最高溫度。 以華氏度表示的溫度 | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL 最低溫度過去24小時（攝氏）] | 過去24小時的最低溫度。  24小時期間是指請求時間（現在）。  以攝氏度為單位的溫度 | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL 最低溫度過去24小時（華氏）] | 過去24小時的最低溫度。  24小時期間是指請求時間（現在）。  以華氏度表示的溫度 | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL 風向] | 風吹自的磁風方向，以度表示。 磁方向從0度到359度不等，其中0度表示北方、東方90度、南方180度、西方270度，依此類推。<br>範圍 — 0&lt;=wind_dream_deg&lt;=350，以10度為間隔。 | `weather.current.windDirection` |
| [!UICONTROL 每小時陣風公里數] | 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速（公里/小時） | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL 每小時陣風英里數] | 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速單位：英里/小時 | `weather.current.windGust.`milesPerHour |
| [!UICONTROL 風速公里/小時] | 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL 每小時風速英里] | 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.current.windSpeed.milesPerHour` |

## 天氣預報 {#forecast}

根據位置，在特定時間點的使用者預測天氣。

| 字段 | 描述 | XDM路徑 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 一天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以攝氏度為單位的溫度 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 一天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以華氏度表示的溫度 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 一天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以攝氏度為單位的溫度 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 一天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以華氏度表示的溫度 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 一天的天氣預報。 日時段天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 一天的天氣預報。 日時段天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 一天的天氣預報。 日時段天氣資訊。 有降水的機率（百分比）。 | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 一天的天氣預報。 日時段天氣資訊。 可能會下雨的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 一天的天氣預報。 日時段天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 一天的天氣預報。 日時段天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 一天的天氣預報。 日時段天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 一天的天氣預報。 日時段天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 一天的天氣預報。 日時段天氣資訊。 空氣的相對濕度，定義為空氣中的水蒸氣量，與在恆定溫度下使空氣飽和所需的水蒸氣量的比率。 相對濕度一律以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 一天的天氣預報。 日時段天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 一天的天氣預報。 日時段天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以攝氏度為單位的溫度 | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 一天的天氣預報。 日時段天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以華氏度表示的溫度 | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 一天的天氣預報。 日時段天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 一天的天氣預報。 日時段天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 一天的天氣預報。 日時段天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 一天的天氣預報。 日時段天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 一天的天氣預報。 日時段天氣資訊。 雷暴影響區域的機率索引。 0 (無雷擊至5 （有嚴重雷暴的高風險）。 | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 一天的天氣預報。 日時段天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 一天的天氣預報。 日時段天氣資訊。 風吹自的磁風方向，以度表示。 磁方向從0度到359度不等，其中0度表示北方、東方90度、南方180度、西方270度，依此類推。<br>範圍 — 0&lt;=wind_dream_deg&lt;=350，以10度為間隔。 | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 一天的天氣預報。 日時段天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速（公里/小時） | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 一天的天氣預報。 日時段天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速單位：英里/小時 | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 一天的天氣預報。 日時段天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 一天的天氣預報。 日時段天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour ` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 一天的天氣預報。 夜間天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 一天的天氣預報。 夜間天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第1天預測夜間降水機會] | 一天的天氣預報。 夜間天氣資訊。 有降水的機率（百分比）。 | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 一天的天氣預報。 夜間天氣資訊。 可能會下雨的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 一天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 一天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 一天的天氣預報。 夜間天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 一天的天氣預報。 夜間天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 一天的天氣預報。 夜間天氣資訊。 空氣的相對濕度，定義為空氣中的水蒸氣量，與在恆定溫度下使空氣飽和所需的水蒸氣量的比率。 相對濕度一律以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 一天的天氣預報。 夜間天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 一天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以攝氏度為單位的溫度 | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 一天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以華氏度表示的溫度 | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 一天的天氣預報。 夜間天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 一天的天氣預報。 夜間天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 一天的天氣預報。 夜間天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第1天預報夜溫寒風] | 一天的天氣預報。 夜間天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第1天預測夜雷指數] | 一天的天氣預報。 夜間天氣資訊。 雷暴影響區域的機率索引。 0 (無雷擊至5 （有嚴重雷暴的高風險）。 | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL 第1天預測夜間UV指數] | 一天的天氣預報。 夜間天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL 第1天預測夜間風向] | 一天的天氣預報。 夜間天氣資訊。 風吹自的磁風方向，以度表示。 磁方向從0度到359度不等，其中0度表示北方、東方90度、南方180度、西方270度，依此類推。<br>範圍 — 0&lt;=wind_dream_deg&lt;=350，以10度為間隔。 | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL 第1天預報夜風陣風公里/小時] | 一天的天氣預報。 夜間天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速（公里/小時） | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第1天預測夜間陣風英里每小時] | 一天的天氣預報。 夜間天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速單位：英里/小時 | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第1天預測夜間風速公里/小時] | 一天的天氣預報。 夜間天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第1天預測夜間風速英里/小時] | 一天的天氣預報。 夜間天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第1天預測QPF英吋] | 一天的天氣預報。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL 第1天預測QPF毫米] | 一天的天氣預報。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL 第1天預測QPF雪公分] | 一天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第1天預測QPF雪英吋] | 一天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL 第2天預測工作歷日期溫度最高攝氏度] | 兩天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以攝氏度為單位的溫度 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第2天預測工作歷日期溫度華氏最大值] | 兩天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以華氏度表示的溫度 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第2天預測工作歷日期溫度最低攝氏度] | 兩天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以攝氏度為單位的溫度 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第2天預測工作歷日期溫度最低華氏度] | 兩天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以華氏度表示的溫度 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第2天預測雲端涵蓋範圍英里] | 兩天的天氣預報。 日時段天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL 第2天預測雲端涵蓋公里] | 兩天的天氣預報。 日時段天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第2天預測日降水機會] | 兩天的天氣預報。 日時段天氣資訊。 有降水的機率（百分比）。 | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL 第2天預測日降水型態] | 兩天的天氣預報。 日時段天氣資訊。 可能會下雨的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL 第2天預測QPF英吋] | 兩天的天氣預報。 日時段天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL 第2天預測日QPF公厘] | 兩天的天氣預報。 日時段天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL 第2天預測日QPF雪公分] | 兩天的天氣預報。 日時段天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第2天預測QPF雪英吋] | 兩天的天氣預報。 日時段天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第2天預測日相對濕度] | 兩天的天氣預報。 日時段天氣資訊。 空氣的相對濕度，定義為空氣中的水蒸氣量，與在恆定溫度下使空氣飽和所需的水蒸氣量的比率。 相對濕度一律以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL 第2天預測天雪範圍] | 兩天的天氣預報。 日時段天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL 第2天預測天溫度攝氏] | 兩天的天氣預報。 日時段天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以攝氏度為單位的溫度 | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL 第2天預測日溫度華氏度] | 兩天的天氣預報。 日時段天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以華氏度表示的溫度 | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第2天預測日溫度熱指數攝氏度] | 兩天的天氣預報。 日時段天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天預測日溫度熱指數華氏度] | 兩天的天氣預報。 日時段天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天預測日溫度寒風攝氏度] | 兩天的天氣預報。 日時段天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第2天預測日溫度寒風華氏度] | 兩天的天氣預報。 日時段天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天預測日雷鳴指數] | 兩天的天氣預報。 日時段天氣資訊。 雷暴影響區域的機率索引。 0 (無雷擊至5 （有嚴重雷暴的高風險）。 | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL 第2天預測UV指數] | 兩天的天氣預報。 日時段天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL 第2天預測日風向] | 兩天的天氣預報。 日時段天氣資訊。 風吹自的磁風方向，以度表示。 磁方向從0度到359度不等，其中0度表示北方、東方90度、南方180度、西方270度，依此類推。<br>範圍 — 0&lt;=wind_dream_deg&lt;=350，以10度為間隔。 | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL 第2天預報日陣風公里/小時] | 兩天的天氣預報。 日時段天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速（公里/小時） | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第2天預測日陣風英里每小時] | 兩天的天氣預報。 日時段天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速單位：英里/小時 | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第2天預測日風速公里/小時] | 兩天的天氣預報。 日時段天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天預測日風速英里/小時] | 兩天的天氣預報。 日時段天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第2天預測夜雲封面英里] | 兩天的天氣預報。 夜間天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL 第2天預報雲端覆蓋公里] | 兩天的天氣預報。 夜間天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第2天預測夜間降水機會] | 兩天的天氣預報。 夜間天氣資訊。 有降水的機率（百分比）。 | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL 第2天預測夜間降水型態] | 兩天的天氣預報。 夜間天氣資訊。 可能會下雨的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL 第2天預測夜間QPF英吋] | 兩天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL 第2天預測夜間QPF公厘] | 兩天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL 第2天預測夜QPF雪公分] | 兩天的天氣預報。 夜間天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第2天預測夜QPF雪英吋] | 兩天的天氣預報。 夜間天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第2天預測夜間相對濕度] | 兩天的天氣預報。 夜間天氣資訊。 空氣的相對濕度，定義為空氣中的水蒸氣量，與在恆定溫度下使空氣飽和所需的水蒸氣量的比率。 相對濕度一律以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL 第2天預測夜間雪區] | 兩天的天氣預報。 夜間天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL 第2天預測夜間溫度攝氏] | 兩天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以攝氏度為單位的溫度 | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL 第2天預測夜間溫度華氏度] | 兩天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以華氏度表示的溫度 | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第2天預測夜間溫度熱指數（攝氏度）] | 兩天的天氣預報。 夜間天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天預測夜間溫度熱指數華氏度] | 兩天的天氣預報。 夜間天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天預報夜溫寒風] | 兩天的天氣預報。 夜間天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第2天預報夜溫寒風] | 兩天的天氣預報。 夜間天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天預測夜雷指數] | 兩天的天氣預報。 夜間天氣資訊。 雷暴影響區域的機率索引。 0 (無雷擊至5 （有嚴重雷暴的高風險）。 | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL 第2天預測夜間UV指數] | 兩天的天氣預報。 夜間天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL 第2天預測夜間風向] | 兩天的天氣預報。 夜間天氣資訊。 風吹自的磁風方向，以度表示。 磁方向從0度到359度不等，其中0度表示北方、東方90度、南方180度、西方270度，依此類推。<br>範圍 — 0&lt;=wind_dream_deg&lt;=350，以10度為間隔。 | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL 第2天預報夜風陣風公里/小時] | 兩天的天氣預報。 夜間天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速（公里/小時） | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第2天預測夜間陣風英里每小時] | 兩天的天氣預報。 夜間天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速單位：英里/小時 | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第2天預測夜間風速公里/小時] | 兩天的天氣預報。 夜間天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天預測夜間風速英里/小時] | 兩天的天氣預報。 夜間天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第2天預測QPF英吋] | 兩天的天氣預報。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL 第2天預測QPF毫米] | 兩天的天氣預報。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL 第2天預測QPF雪公分] | 兩天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第2天預測QPF雪英吋] | 兩天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL 第3天預測工作歷日期溫度最高攝氏度] | 三天天氣預報。 指定日期的午夜至午夜每日最高溫度。 以攝氏度為單位的溫度 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第3天預測工作歷日期溫度華氏最大值] | 三天天氣預報。 指定日期的午夜至午夜每日最高溫度。 以華氏度表示的溫度 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第3天預測工作歷日期溫度最低攝氏度] | 三天天氣預報。 指定日期的午夜至午夜每日最低溫度。 以攝氏度為單位的溫度 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第3天預測工作歷日期溫度最低華氏度] | 三天天氣預報。 指定日期的午夜至午夜每日最低溫度。 以華氏度表示的溫度 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第3天預測雲端涵蓋範圍英里] | 三天天氣預報。 日時段天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL 第3天預測雲端涵蓋公里] | 三天天氣預報。 日時段天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第3天預測日降水機會] | 三天天氣預報。 日時段天氣資訊。 有降水的機率（百分比）。 | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL 第3天預測天降水型態] | 三天天氣預報。 日時段天氣資訊。 可能會下雨的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL 第3天預測QPF英吋] | 三天天氣預報。 日時段天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL 第3天預測日QPF公厘] | 三天天氣預報。 日時段天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL 第3天預測日QPF雪公分] | 三天天氣預報。 日時段天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第3天預測QPF雪英吋] | 三天天氣預報。 日時段天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第3天預測日相對濕度] | 三天天氣預報。 日時段天氣資訊。 空氣的相對濕度，定義為空氣中的水蒸氣量，與在恆定溫度下使空氣飽和所需的水蒸氣量的比率。 相對濕度一律以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL 第3天預測天雪範圍] | 三天天氣預報。 日時段天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL 第3天預測天溫（攝氏）] | 三天天氣預報。 日時段天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以攝氏度為單位的溫度 | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL 第3天預測日溫度華氏度] | 三天天氣預報。 日時段天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以華氏度表示的溫度 | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第3天預測日溫度熱指數攝氏度] | 三天天氣預報。 日時段天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天預測日溫度熱指數華氏度] | 三天天氣預報。 日時段天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天預測日溫度寒風攝氏度] | 三天天氣預報。 日時段天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第3天預測日溫度寒風華氏度] | 三天天氣預報。 日時段天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天預測日雷鳴指數] | 三天天氣預報。 日時段天氣資訊。 雷暴影響區域的機率索引。 0 (無雷擊至5 （有嚴重雷暴的高風險）。 | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL 第3天預測UV指數] | 三天天氣預報。 日時段天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL 第3天預測日風向] | 三天天氣預報。 日時段天氣資訊。 風吹自的磁風方向，以度表示。 磁方向從0度到359度不等，其中0度表示北方、東方90度、南方180度、西方270度，依此類推。<br>範圍 — 0&lt;=wind_dream_deg&lt;=350，以10度為間隔。 | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL 第3天預報日陣風公里/小時] | 三天天氣預報。 日時段天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速（公里/小時） | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第3天預測日陣風英里每小時] | 三天天氣預報。 日時段天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速單位：英里/小時 | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第3天預測日風速公里/小時] | 三天天氣預報。 日時段天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天預測日風速英里/小時] | 三天天氣預報。 日時段天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第3天預測夜雲封面英里] | 三天天氣預報。 夜間天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL 第3天預報雲端覆蓋公里] | 三天天氣預報。 夜間天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第3天預測夜間降水機會] | 三天天氣預報。 夜間天氣資訊。 有降水的機率（百分比）。 | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL 第3天預測夜間降水型態] | 三天天氣預報。 夜間天氣資訊。 可能會下雨的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL 第3天預測夜間QPF英吋] | 三天天氣預報。 夜間天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL 第3天預測夜間QPF公厘] | 三天天氣預報。 夜間天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL 第3天預測夜間QPF雪公分] | 三天天氣預報。 夜間天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第3天預測夜QPF雪英吋] | 三天天氣預報。 夜間天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第3天預測夜間相對濕度] | 三天天氣預報。 夜間天氣資訊。 空氣的相對濕度，定義為空氣中的水蒸氣量，與在恆定溫度下使空氣飽和所需的水蒸氣量的比率。 相對濕度一律以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL 第3天預測夜間雪區] | 三天天氣預報。 夜間天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL 第3天預測夜間溫度攝氏] | 三天天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以攝氏度為單位的溫度 | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL 第3天預測夜間溫度華氏度] | 三天天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以華氏度表示的溫度 | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第3天預測夜間溫度熱指數（攝氏度）] | 三天天氣預報。 夜間天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天預測夜間溫度熱指數華氏度] | 三天天氣預報。 夜間天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天預報夜溫寒風] | 三天天氣預報。 夜間天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第3天預報夜溫寒風] | 三天天氣預報。 夜間天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天預測夜雷指數] | 三天天氣預報。 夜間天氣資訊。 雷暴影響區域的機率索引。 0 (無雷擊至5 （有嚴重雷暴的高風險）。 | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL 第3天預測夜間UV指數] | 三天天氣預報。 夜間天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL 第3天預測夜間風向] | 三天天氣預報。 夜間天氣資訊。 風吹自的磁風方向，以度表示。 磁方向從0度到359度不等，其中0度表示北方、東方90度、南方180度、西方270度，依此類推。<br>範圍 — 0&lt;=wind_dream_deg&lt;=350，以10度為間隔。 | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL 第3天預報夜風陣風公里/小時] | 三天天氣預報。 夜間天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速（公里/小時） | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第3天預測夜間陣風英里每小時] | 三天天氣預報。 夜間天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速單位：英里/小時 | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第3天預測夜間風速公里/小時] | 三天天氣預報。 夜間天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天預測夜間風速英里/小時] | 三天天氣預報。 夜間天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第3天預測QPF英吋] | 三天天氣預報。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL 第3天預測QPF毫米] | 三天天氣預報。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL 第3天預測QPF雪公分] | 三天天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第3天預測QPF雪英吋] | 三天天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL 第5天預測工作歷日期溫度最高攝氏度] | 五天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以攝氏度為單位的溫度 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第5天預測工作歷日溫度華氏最大值] | 五天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以華氏度表示的溫度 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第5天預測工作歷日期溫度最低攝氏度] | 五天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以攝氏度為單位的溫度 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第5天預測工作歷日期溫度最低華氏度] | 五天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以華氏度表示的溫度 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第5天預測雲端涵蓋範圍英里] | 五天的天氣預報。 日時段天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL 第5天預測雲端涵蓋公里] | 五天的天氣預報。 日時段天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第5天預測日降水機會] | 五天的天氣預報。 日時段天氣資訊。 有降水的機率（百分比）。 | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL 第5天預測天降水型態] | 五天的天氣預報。 日時段天氣資訊。 可能會下雨的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL 第5天預測QPF英吋] | 五天的天氣預報。 日時段天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL 第5天預測QPF公厘] | 五天的天氣預報。 日時段天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL 第5天預測日QPF雪公分] | 五天的天氣預報。 日時段天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第5天預測QPF雪英吋] | 五天的天氣預報。 日時段天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第5天預測日相對濕度] | 五天的天氣預報。 日時段天氣資訊。 空氣的相對濕度，定義為空氣中的水蒸氣量，與在恆定溫度下使空氣飽和所需的水蒸氣量的比率。 相對濕度一律以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL 第5天預測天雪範圍] | 五天的天氣預報。 日時段天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL 第5天預測天溫（攝氏）] | 五天的天氣預報。 日時段天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以攝氏度為單位的溫度 | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL 第5天預測日溫度華氏度] | 五天的天氣預報。 日時段天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以華氏度表示的溫度 | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第5天預測日溫度熱指數攝氏度] | 五天的天氣預報。 日時段天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天預測日溫度熱指數華氏度] | 五天的天氣預報。 日時段天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天預測日溫度寒風攝氏度] | 五天的天氣預報。 日時段天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第5天預測日溫度寒風華氏度] | 五天的天氣預報。 日時段天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天預測日雷鳴指數] | 五天的天氣預報。 日時段天氣資訊。 雷暴影響區域的機率索引。 0 (無雷擊至5 （有嚴重雷暴的高風險）。 | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL 第5天預測UV指數] | 五天的天氣預報。 日時段天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL 第5天預測日風向] | 五天的天氣預報。 日時段天氣資訊。 風吹自的磁風方向，以度表示。 磁方向從0度到359度不等，其中0度表示北方、東方90度、南方180度、西方270度，依此類推。<br>範圍 — 0&lt;=wind_dream_deg&lt;=350，以10度為間隔。 | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL 第5天預報日陣風公里/小時] | 五天的天氣預報。 日時段天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速（公里/小時） | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第5天預測日陣風英里每小時] | 五天的天氣預報。 日時段天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速單位：英里/小時 | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第5天預測日風速公里/小時] | 五天的天氣預報。 日時段天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天預測日風速英里/小時] | 五天的天氣預報。 日時段天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第5天預測夜雲封面英里] | 五天的天氣預報。 夜間天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL 第5天預報雲端覆蓋公里] | 五天的天氣預報。 夜間天氣資訊。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第5天預測夜間降水機會] | 五天的天氣預報。 夜間天氣資訊。 有降水的機率（百分比）。 | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL 第5天預測夜間降水型態] | 五天的天氣預報。 夜間天氣資訊。 可能會下雨的降水形式（雨、雪、雨夾雪等）。 | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL 第5天預測夜間QPF英吋] | 五天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL 第5天預測夜間QPF公厘] | 五天的天氣預報。 夜間天氣資訊。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL 第5天預測夜QPF雪公分] | 五天的天氣預報。 夜間天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第5天預測夜QPF雪英吋] | 五天的天氣預報。 夜間天氣資訊。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第5天預測夜間相對濕度] | 五天的天氣預報。 夜間天氣資訊。 空氣的相對濕度，定義為空氣中的水蒸氣量，與在恆定溫度下使空氣飽和所需的水蒸氣量的比率。 相對濕度一律以百分比表示。<br>範圍 — 0到100。 | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL 第5天預測夜間雪域] | 五天的天氣預報。 夜間天氣資訊。 潛在降雪量（1-3英吋、3-6英吋等）。 | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL 第5天預測夜間溫度攝氏] | 五天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以攝氏度為單位的溫度 | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL 第5天預測夜間溫度華氏度] | 五天的天氣預報。 夜間天氣資訊。 以定義的測量單位表示的溫度。 範圍–140到140。 以華氏度表示的溫度 | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第5天預測夜間溫度熱指數（攝氏度）] | 五天的天氣預報。 夜間天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天預測夜間溫度熱指數華氏度] | 五天的天氣預報。 夜間天氣資訊。 根據溫度和濕度，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天預報夜溫寒風] | 五天的天氣預報。 夜間天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以攝氏度為單位的溫度 | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第5天預報夜溫寒風] | 五天的天氣預報。 夜間天氣資訊。 根據溫度和風速，暴露在外的個人會感覺到的溫度。 以華氏度表示的溫度 | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天預測夜雷指數] | 五天的天氣預報。 夜間天氣資訊。 雷暴影響區域的機率索引。 0 (無雷擊至5 （有嚴重雷暴的高風險）。 | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL 第5天預測夜間UV指數] | 五天的天氣預報。 夜間天氣資訊。 12小時預測期間的最大UV索引。 | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL 第5天預測夜間風向] | 五天的天氣預報。 夜間天氣資訊。 風吹自的磁風方向，以度表示。 磁方向從0度到359度不等，其中0度表示北方、東方90度、南方180度、西方270度，依此類推。<br>範圍 — 0&lt;=wind_dream_deg&lt;=350，以10度為間隔。 | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL 第5天預報夜風陣風公里/小時] | 五天的天氣預報。 夜間天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速（公里/小時） | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第5天預測夜間陣風英里每小時] | 五天的天氣預報。 夜間天氣資訊。 此資料欄位包含平均風速突然和暫時變化的資訊。 報表一律會顯示觀測期間所記錄的最大陣風速度。 如果顯示「風速」，則是必填的顯示欄位。 陣風的速度可以用英里/小時或公里/小時表示。 風速單位：英里/小時 | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第5天預測夜間風速公里/小時] | 五天的天氣預報。 夜間天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天預測夜間風速英里/小時] | 五天的天氣預報。 夜間天氣資訊。 風被視為一個向量；因此，風必須有方向和大小（速度）。 在目前狀況中報告的風資訊對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第5天預測QPF英吋] | 五天的天氣預報。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 以英吋為單位的沈澱 | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL 第5天預測QPF毫米] | 五天的天氣預報。 12或24小時期間的可測量降水量（液體或液體當量）。 以毫米測量。 降水（以毫米為單位） | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL 第5天預測QPF雪公分] | 五天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第5天預測QPF雪英吋] | 五天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天預測工作歷日期溫度最高攝氏度] | 七天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以攝氏度為單位的溫度 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第7天預測日曆日溫度華氏最大值] | 七天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以華氏度表示的溫度 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第7天預測工作歷日期溫度最低攝氏度] | 七天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以攝氏度為單位的溫度 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第7天預測工作歷日期溫度最低華氏度] | 七天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以華氏度表示的溫度 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第7天預測雲端涵蓋範圍] | 七天的天氣預報。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL 第7天Forecast Cloud涵蓋公里] | 七天的天氣預報。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL 第7天預測QPF英吋] | 七天的天氣預報。 24小時期間的可測量降水量（液體或液體當量）。 以英吋為單位的沈澱 | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL 第7天預測QPF毫米] | 七天的天氣預報。 24小時期間的可測量降水量（液體或液體當量）。 降水（以毫米為單位） | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL 第7天預測QPF雪公分] | 七天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第7天預測QPF雪英吋] | 七天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天預測UV指數] | 七天的天氣預報。 12小時預測期間的最大UV索引。 | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL 第7天預報風向] | 七天的天氣預報。 以磁性標籤法表示的平均風向。 | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL 第7天預報風速公里/小時] | 七天的天氣預報。 12小時預測期間最大持續風速的預測。<br>風被視為一個向量；因此，風必須有方向和大小（速度）。 在預報中報告的風資料對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第7天預測風速英里/小時] | 七天的天氣預報。 12小時預測期間最大持續風速的預測。<br>風被視為一個向量；因此，風必須有方向和大小（速度）。 在預報中報告的風資料對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第10天預測工作歷天溫度最高攝氏度] | 十天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以攝氏度為單位的溫度 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第10天預測工作歷日溫度華氏最大值] | 十天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以華氏度表示的溫度 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第10天預測工作歷天溫度最低攝氏度] | 十天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以攝氏度為單位的溫度 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第10天預測工作歷日期溫度最低華氏度] | 十天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以華氏度表示的溫度 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第10天Forecast Cloud涵蓋英里] | 十天的天氣預報。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL 第10天Forecast Cloud涵蓋公里] | 十天的天氣預報。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL 第10天預測QPF英吋] | 十天的天氣預報。 24小時期間的可測量降水量（液體或液體當量）。 以英吋為單位的沈澱 | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL 第10天預測QPF公厘] | 十天的天氣預報。 24小時期間的可測量降水量（液體或液體當量）。 降水（以毫米為單位） | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL 第10天預測QPF雪公分] | 十天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第10天預測QPF雪英吋] | 十天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL 第10天預測UV指數] | 十天的天氣預報。 12小時預測期間的最大UV索引。 | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL 第10天預測風向] | 十天的天氣預報。 以磁性標籤法表示的平均風向。 | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL 第10天預報風速公里/小時] | 十天的天氣預報。 12小時預測期間最大持續風速的預測。<br>風被視為一個向量；因此，風必須有方向和大小（速度）。 在預報中報告的風資料對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第10天預測風速英里/小時] | 十天的天氣預報。 12小時預測期間最大持續風速的預測。<br>風被視為一個向量；因此，風必須有方向和大小（速度）。 在預報中報告的風資料對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第14天預測工作歷天溫度最高攝氏度] | 十四天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以攝氏度為單位的溫度 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第14天預測工作歷日溫度華氏最大值] | 十四天的天氣預報。 指定日期的午夜至午夜每日最高溫度。 以華氏度表示的溫度 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第14天預測工作歷天溫度最低攝氏度] | 十四天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以攝氏度為單位的溫度 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第14天預測工作歷日期溫度最低華氏度] | 十四天的天氣預報。 指定日期的午夜至午夜每日最低溫度。 以華氏度表示的溫度 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第14天Forecast Cloud涵蓋英里] | 十四天的天氣預報。 白天平均雲端涵蓋範圍，以百分比表示。 以英里為單位的距離。 | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL 第14天Forecast Cloud涵蓋公里] | 十四天的天氣預報。 白天平均雲端涵蓋範圍，以百分比表示。 以公里為單位的距離。 | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 第14天預測QPF英吋 | 十四天的天氣預報。 24小時期間的可測量降水量（液體或液體當量）。 以英吋為單位的沈澱 | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL 第14天預測QPF公厘] | 十四天的天氣預報。 24小時期間的可測量降水量（液體或液體當量）。 降水（以毫米為單位） | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL 第14天預測QPF雪公分] | 十四天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪公分 | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第14天預測QPF雪英吋] | 十四天的天氣預報。 在12或24小時預測期間作為雪的預估可測量降水。 以公分為單位。 降雪單位（英吋） | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL 第14天預測UV指數] | 十四天的天氣預報。 12小時預測期間的最大UV索引。 | `weather.forecast.day14Forecast.uvIndex` |
| 第14天預測風向 | 十四天的天氣預報。 以磁性標籤法表示的平均風向。 | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL 第14天預報風速公里/小時] | 十四天的天氣預報。 12小時預測期間最大持續風速的預測。<br>風被視為一個向量；因此，風必須有方向和大小（速度）。 在預報中報告的風資料對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速（公里/小時） | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第14天預測風速英里/小時] | 十四天的天氣預報。 12小時預測期間最大持續風速的預測。<br>風被視為一個向量；因此，風必須有方向和大小（速度）。 在預報中報告的風資料對應於稱為持續風速的10分鐘平均值。 風速的突然或短暫變化稱為「陣風」，並在單獨的資料欄位中報告。 風向一律表示為「從風吹過的地方」，表示北風從北吹到南。 如果您面對北風，風就在您的臉上。 朝南，北風在背後。 風速單位：英里/小時 | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 触发器 {#triggers}

觸發器根據各種輸入定義語意天氣條件。

| 字段 | 描述 | XDM路徑 |
| --- | ---- | --- |
| [!UICONTROL 產品觸發程式] | 表示條件何時適合推動特定類別產品的銷售。  它們會對應至整數個數。 您可以從IBM取得完整清單。 | `weather.productTriggers` |
| [!UICONTROL 相對觸發程式] | 基於人類知覺的相對條件。 熱或冷之類的。 它們會對應至整數個數。 您可以從IBM取得完整清單。 | `weather.relativeTriggers` |
| [!UICONTROL 惡劣天氣觸發程式] | 表示各種惡劣的天氣狀況，例如颶風或暴雨。 | `weather.severeTriggers` |
