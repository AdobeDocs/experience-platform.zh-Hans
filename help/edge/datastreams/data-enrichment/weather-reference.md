---
title: 天气数据字段映射
description: 可用天气数据字段的参考页面，这些字段在与天气渠道集成时可用。
source-git-commit: 3e5ca8fe67e5ad9ce0fe70d0c9f1e2fbc20cee17
workflow-type: tm+mt
source-wordcount: '12238'
ht-degree: 0%

---


# 天气数据字段映射

Adobe与 [!DNL [The Weather Company]](https://www.ibm.com/weather) 为通过数据流收集的数据带来美国天气的额外背景。 您可以将此数据用于分析、定位和区段创建中的Experience Platform。

本页列出了可用于扩充受众数据的所有可用字段。

这些字段将划分为三个与字段组对齐的不同组。

* [**[!UICONTROL 当前天气]**](#current-weather):用户的当前天气条件（基于其位置）。 这包括当前温度、枕头、云覆盖等。
* [**[!UICONTROL 预测天气]**](#forecast):预测包括用户地点的1、2、3、5、7和10天预测。
* [**[!UICONTROL 触发器]**](#triggers):触发器是映射到不同语义天气条件的特定组合。 天气触发器有三种类型：

   * **[!UICONTROL 相对触发器]**:语义上有意义的条件，如寒冷或雨天。 这些气候在不同气候中的定义可能不同。
   * **[!UICONTROL 产品触发器]**:导致购买不同类型产品的条件。 例如：天气预报可能意味着更有可能购买雨衣。
   * **[!UICONTROL 恶劣天气触发]**:严重的天气警告，如冬季风暴或飓风警告。

## 当前天气 {#current-weather}

用户的当前天气条件（基于其位置）。

| 字段 | 描述 | XDM路径 |
| --- | ---- | --- |
| [!UICONTROL 温度露点Clisu] | 必须在恒定压力下冷却空气以达到饱和的温度。 露点也是间接测量空气湿度的方法。 露点永远不会超过温度。 当Dewpoint和Tempure相等时，通常会形成云或雾。 温度和露点值越近，相对湿度就越高。 范围 —80到100(°F)或–62到37(°C)。 温度（摄氏度） | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL 温度露点华氏度] | 必须在恒定压力下冷却空气以达到饱和的温度。 露点也是间接测量空气湿度的方法。 露点永远不会超过温度。 当Dewpoint和Tempure相等时，通常会形成云或雾。 温度和露点值越近，相对湿度就越高。 范围 —80到100(°F)或–62到37(°C)。 华氏温度 | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL 降水最后一小时英寸] | 滚时液体沉淀量。 显示的金额是整个请求时间（现在）的滚动时间。 以英寸为单位的降水 | `weather.current.precip1Hour.inches` |
| [!UICONTROL 降水最后一小时毫米] | 滚时液体沉淀量。 显示的金额是整个请求时间（现在）的滚动时间。 以毫米计的降水量 | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 滚动二十四小时液态沉淀量。 显示的金额是整个请求时间（现在）的滚动时间。 以英寸为单位的降水 | `weather.current.precip24Hour.inches` |
| [!UICONTROL 持续24小时降雨量] | 滚动二十四小时液态沉淀量。 显示的金额是整个请求时间（现在）的滚动时间。 以毫米计的降水量 | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL 降水持续6小时] | 滚动六小时液体沉淀量。 显示的金额是整个请求时间（现在）的滚动时间。 以英寸为单位的降水 | `weather.current.precip6Hour.inches` |
| [!UICONTROL 持续6小时的降水量] | 滚动六小时液体沉淀量。 显示的金额是整个请求时间（现在）的滚动时间。 以毫米计的降水量 | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL 压力变化] | 在密里巴斯，最近三小时里压力的变化。 | `weather.current.pressureChange` |
| [!UICONTROL 压力平均海平面] | 海平面压力（毫巴）。  换句话说，海平面的平均气压。<br>范围 — 毫巴精确到1/10mb。 | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL 相对湿度] | 空气的相对湿度，定义为空气中水蒸气量与在恒定温度下使空气达到饱和所需蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.current.relativeHumidity` |
| [!UICONTROL 雪最后一小时厘米] | 一小时的降雪量。  显示的金额是整个请求时间（现在）的滚动时间。 降雪量厘米 | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL 最后一小时] | 一小时的降雪量。  显示的金额是整个请求时间（现在）的滚动时间。 降雪以英寸计 | `weather.current.snow1Hour.inches` |
| [!UICONTROL 雪24小时厘米] | 二十四小时的降雪量。  显示的金额是整个请求时间（现在）的滚动时间。 降雪量厘米 | `weather.current.snow24Hour.centimeters` |
| 雪24小时英寸 | 二十四小时的降雪量。  显示的金额是整个请求时间（现在）的滚动时间。 降雪以英寸计 | `weather.current.snow24Hour.inches` |
| [!UICONTROL 最近6小时的雪] | 一小时的降雪量。  显示的金额是整个请求时间（现在）的滚动时间。 降雪量厘米 | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL 最近6小时的雪] | 一小时的降雪量。  显示的金额是整个请求时间（现在）的滚动时间。 降雪以英寸计 | `weather.current.snow6Hour.inches` |
| [!UICONTROL 日落时间] | 日落时间(UTC)。 | `weather.current.sunsetTime` |
| [!UICONTROL 温度Celsius] | 以定义的度量单位表示的温度。 范围–140到140。 温度（摄氏度） | `weather.current.temperature.celsius` |
| [!UICONTROL 温度华氏度] | 以定义的度量单位表示的温度。 范围–140到140。 华氏温度 | `weather.current.temperature.fahrenheit` |
| [!UICONTROL 温度变化24小时C] | 与24小时前的报告相比，温度有所变化。 温度（摄氏度） | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL 温度变化24小时（华氏度）] | 与24小时前的报告相比，温度有所变化。 华氏温度 | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL 温度像摄氏度] | 明显的温度。 它代表由于风冷或热指数的共同作用而暴露的人皮肤上的空气温度“感觉”。<br>当温度为65°F或更高时，Feels Like值表示计算的热指数。  当温度低于65°F时，“感觉”值表示计算的风寒。<br>范围–140到140。 温度（摄氏度） | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL 温度像华氏] | 明显的温度。 它代表由于风冷或热指数的共同作用而暴露的人皮肤上的空气温度“感觉”。<br>当温度为65°F或更高时，Feels Like值表示计算的热指数。  当温度低于65°F时，“感觉”值表示计算的风寒。<br>范围–140到140。 华氏温度 | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL 自上午7点以来的最高温度] | 自当地时间早上7点以来的最高温度。 温度（摄氏度） | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL 自华氏早7点以来的最高温度] | 自当地时间早上7点以来的最高温度。 华氏温度 | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL 最低温度持续24小时] | 过去24小时内的最低温度。  24小时的时段引用请求时间（现在）。  温度（摄氏度） | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL 最低温度持续24小时（华氏度）] | 过去24小时内的最低温度。  24小时的时段引用请求时间（现在）。  华氏温度 | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL 风向] | 风从中吹出的磁风方向以度表示。 磁方向在0~359度之间变化，0°表示北、90°表示东、180°表示南、270°表示西等。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，间隔为10度。 | `weather.current.windDirection` |
| [!UICONTROL 阵风时速] | 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 每小时风速（千米） | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL 每小时阵风英里] | 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 风速（以英里/小时为单位） | `weather.current.windGust.`milesPerHour |
| [!UICONTROL 风速公里/小时] | 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL 风速英里/小时] | 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.current.windSpeed.milesPerHour` |

## 预测天气 {#forecast}

根据特定时间点的位置为用户预测的天气。

| 字段 | 描述 | XDM路径 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 一天的天气预报。 指定日期的午夜至午夜每日最高温度。 温度（摄氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 一天的天气预报。 指定日期的午夜至午夜每日最高温度。 华氏温度 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 一天的天气预报。 指定日期的午夜至午夜每日最低温度。 温度（摄氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 一天的天气预报。 指定日期的午夜至午夜每日最低温度。 华氏温度 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 一天的天气预报。 白天的天气信息。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 一天的天气预报。 白天的天气信息。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 一天的天气预报。 白天的天气信息。 降水的概率（百分比）。 | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 一天的天气预报。 白天的天气信息。 降水的形式。 | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 一天的天气预报。 白天的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 一天的天气预报。 白天的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 一天的天气预报。 白天的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 一天的天气预报。 白天的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 一天的天气预报。 白天的天气信息。 空气的相对湿度，定义为空气中水蒸气量与在恒定温度下使空气达到饱和所需蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 一天的天气预报。 白天的天气信息。 潜在降雪量（1-3英寸、3-6英寸等）。 | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 一天的天气预报。 白天的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 温度（摄氏度） | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 一天的天气预报。 白天的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 华氏温度 | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 一天的天气预报。 白天的天气信息。 根据温度和湿度暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 一天的天气预报。 白天的天气信息。 根据温度和湿度暴露的人所感受的温度。 华氏温度 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 一天的天气预报。 白天的天气信息。 根据温度和风速暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 一天的天气预报。 白天的天气信息。 根据温度和风速暴露的人所感受的温度。 华氏温度 | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 一天的天气预报。 白天的天气信息。 雷暴对某个区域的影响概率指数。 0(无雷击5（严重雷电风险高）。 | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 一天的天气预报。 白天的天气信息。 12小时预测时段的最大UV指数。 | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 一天的天气预报。 白天的天气信息。 风从中吹出的磁风方向以度表示。 磁方向在0~359度之间变化，0°表示北、90°表示东、180°表示南、270°表示西等。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，间隔为10度。 | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 一天的天气预报。 白天的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 每小时风速（千米） | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 一天的天气预报。 白天的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 风速（以英里/小时为单位） | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 一天的天气预报。 白天的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 一天的天气预报。 白天的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour ` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 一天的天气预报。 夜间的天气信息。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 一天的天气预报。 夜间的天气信息。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第1天预报夜间降水机会] | 一天的天气预报。 夜间的天气信息。 降水的概率（百分比）。 | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 一天的天气预报。 夜间的天气信息。 降水的形式。 | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 一天的天气预报。 夜间的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 一天的天气预报。 夜间的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 一天的天气预报。 夜间的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 一天的天气预报。 夜间的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 一天的天气预报。 夜间的天气信息。 空气的相对湿度，定义为空气中水蒸气量与在恒定温度下使空气达到饱和所需蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 一天的天气预报。 夜间的天气信息。 潜在降雪量（1-3英寸、3-6英寸等）。 | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 一天的天气预报。 夜间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 温度（摄氏度） | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 一天的天气预报。 夜间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 华氏温度 | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 一天的天气预报。 夜间的天气信息。 根据温度和湿度暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 一天的天气预报。 夜间的天气信息。 根据温度和湿度暴露的人所感受的温度。 华氏温度 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 一天的天气预报。 夜间的天气信息。 根据温度和风速暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第1天预报夜间气温降温华氏度] | 一天的天气预报。 夜间的天气信息。 根据温度和风速暴露的人所感受的温度。 华氏温度 | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第1天预报夜雷指数] | 一天的天气预报。 夜间的天气信息。 雷暴对某个区域的影响概率指数。 0(无雷击5（严重雷电风险高）。 | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL 第1天预报夜间UV指数] | 一天的天气预报。 夜间的天气信息。 12小时预测时段的最大UV指数。 | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL 第1天预报夜间风向] | 一天的天气预报。 夜间的天气信息。 风从中吹出的磁风方向以度表示。 磁方向在0~359度之间变化，0°表示北、90°表示东、180°表示南、270°表示西等。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，间隔为10度。 | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL 第1天预报夜风公里/小时] | 一天的天气预报。 夜间的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 每小时风速（千米） | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第1天预报夜风阵风英里/小时] | 一天的天气预报。 夜间的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 风速（以英里/小时为单位） | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第1天预报夜间风速公里/小时] | 一天的天气预报。 夜间的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第1天预报夜间风速英里/小时] | 一天的天气预报。 夜间的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第1天预测QPF英寸] | 一天的天气预报。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL 第1天预测QPF毫米] | 一天的天气预报。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL 第1天预报QPF雪厘米] | 一天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第1天预测QPF雪英寸] | 一天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL 第2天预测日历日温度最高Celsius] | 两天的天气预报。 指定日期的午夜至午夜每日最高温度。 温度（摄氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第2天预测日历日温度最高华氏度] | 两天的天气预报。 指定日期的午夜至午夜每日最高温度。 华氏温度 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第2天预测日历日温度最低摄氏度] | 两天的天气预报。 指定日期的午夜至午夜每日最低温度。 温度（摄氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第2天预测日历日温度最低华氏度] | 两天的天气预报。 指定日期的午夜至午夜每日最低温度。 华氏温度 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第2天预测第1天云覆盖英里] | 两天的天气预报。 白天的天气信息。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL 第2天预测第1天云覆盖公里] | 两天的天气预报。 白天的天气信息。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第2天预报日降水机会] | 两天的天气预报。 白天的天气信息。 降水的概率（百分比）。 | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL 第2天预报日降水类型] | 两天的天气预报。 白天的天气信息。 降水的形式。 | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL 第2天预测第QPF英寸] | 两天的天气预报。 白天的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL 第2天预测第QPF毫米] | 两天的天气预报。 白天的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL 第2天预报第QPF雪厘米] | 两天的天气预报。 白天的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第2天预测第QPF雪英寸] | 两天的天气预报。 白天的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第2天预测第2天相对湿度] | 两天的天气预报。 白天的天气信息。 空气的相对湿度，定义为空气中水蒸气量与在恒定温度下使空气达到饱和所需蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL 第2天预测天雪范围] | 两天的天气预报。 白天的天气信息。 潜在降雪量（1-3英寸、3-6英寸等）。 | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL 第2天预测天温度Celsius] | 两天的天气预报。 白天的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 温度（摄氏度） | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL 第2天预测温度华氏度] | 两天的天气预报。 白天的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 华氏温度 | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第2天预测第2天温度热指数Celsiu] | 两天的天气预报。 白天的天气信息。 根据温度和湿度暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天预测第1天温度热指数（华氏）] | 两天的天气预报。 白天的天气信息。 根据温度和湿度暴露的人所感受的温度。 华氏温度 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天预报天气温风寒摄氏度] | 两天的天气预报。 白天的天气信息。 根据温度和风速暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第2天预报天气温风降温华氏] | 两天的天气预报。 白天的天气信息。 根据温度和风速暴露的人所感受的温度。 华氏温度 | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天预测第2天雷击指数] | 两天的天气预报。 白天的天气信息。 雷暴对某个区域的影响概率指数。 0(无雷击5（严重雷电风险高）。 | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL 第2天预测日UV指数] | 两天的天气预报。 白天的天气信息。 12小时预测时段的最大UV指数。 | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL 第2天预报第1天风向] | 两天的天气预报。 白天的天气信息。 风从中吹出的磁风方向以度表示。 磁方向在0~359度之间变化，0°表示北、90°表示东、180°表示南、270°表示西等。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，间隔为10度。 | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL 第2天预报每天阵风公里/小时] | 两天的天气预报。 白天的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 每小时风速（千米） | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第2天预报每天阵风英里/小时] | 两天的天气预报。 白天的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 风速（以英里/小时为单位） | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第2天预报日风速公里/小时] | 两天的天气预报。 白天的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天预报日风速英里/小时] | 两天的天气预报。 白天的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第2天预报夜间云覆盖英里] | 两天的天气预报。 夜间的天气信息。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL 第2天预报夜间云层覆盖公里] | 两天的天气预报。 夜间的天气信息。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第2天预报夜间降水机会] | 两天的天气预报。 夜间的天气信息。 降水的概率（百分比）。 | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL 第2天预报夜间降水类型] | 两天的天气预报。 夜间的天气信息。 降水的形式。 | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL 第2天预报夜QPF英寸] | 两天的天气预报。 夜间的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL 第2天预报夜QPF毫米] | 两天的天气预报。 夜间的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL 第2天预报夜QPF雪厘米] | 两天的天气预报。 夜间的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第2天预报夜QPF雪英寸] | 两天的天气预报。 夜间的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第2天预报夜间相对湿度] | 两天的天气预报。 夜间的天气信息。 空气的相对湿度，定义为空气中水蒸气量与在恒定温度下使空气达到饱和所需蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL 第2天预报夜间降雪范围] | 两天的天气预报。 夜间的天气信息。 潜在降雪量（1-3英寸、3-6英寸等）。 | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL 第2天预报夜间气温摄氏度] | 两天的天气预报。 夜间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 温度（摄氏度） | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL 第2天预报夜温华氏度] | 两天的天气预报。 夜间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 华氏温度 | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第2天预报夜间温度热指数Clisum] | 两天的天气预报。 夜间的天气信息。 根据温度和湿度暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天预报夜间温度热指数华氏] | 两天的天气预报。 夜间的天气信息。 根据温度和湿度暴露的人所感受的温度。 华氏温度 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天预报夜间气温风寒摄氏度] | 两天的天气预报。 夜间的天气信息。 根据温度和风速暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第2天预报夜间气温风降温华氏度] | 两天的天气预报。 夜间的天气信息。 根据温度和风速暴露的人所感受的温度。 华氏温度 | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天预报夜雷指数] | 两天的天气预报。 夜间的天气信息。 雷暴对某个区域的影响概率指数。 0(无雷击5（严重雷电风险高）。 | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL 第2天预报夜间UV指数] | 两天的天气预报。 夜间的天气信息。 12小时预测时段的最大UV指数。 | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL 第2天预报夜风方向] | 两天的天气预报。 夜间的天气信息。 风从中吹出的磁风方向以度表示。 磁方向在0~359度之间变化，0°表示北、90°表示东、180°表示南、270°表示西等。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，间隔为10度。 | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL 第2天预报每小时夜风公里] | 两天的天气预报。 夜间的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 每小时风速（千米） | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第2天预报夜风阵风英里/小时] | 两天的天气预报。 夜间的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 风速（以英里/小时为单位） | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第2天预报夜间风速公里/小时] | 两天的天气预报。 夜间的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天预报夜间风速英里/小时] | 两天的天气预报。 夜间的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第2天预测QPF英寸] | 两天的天气预报。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL 第2天预测QPF毫米] | 两天的天气预报。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL 第2天预报QPF雪厘米] | 两天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第2天预测QPF雪英寸] | 两天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL 第3天预测日历日温度最高Celsius] | 三天的天气预报。 指定日期的午夜至午夜每日最高温度。 温度（摄氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第3天预测日历日温度最高华氏度] | 三天的天气预报。 指定日期的午夜至午夜每日最高温度。 华氏温度 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第3天预测日历日温度最低摄氏度] | 三天的天气预报。 指定日期的午夜至午夜每日最低温度。 温度（摄氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第3天预测日历日温度最低华氏度] | 三天的天气预报。 指定日期的午夜至午夜每日最低温度。 华氏温度 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第3天预测第1天云覆盖英里] | 三天的天气预报。 白天的天气信息。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL 第3天预测第1天云覆盖公里] | 三天的天气预报。 白天的天气信息。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第3天预报日降水机会] | 三天的天气预报。 白天的天气信息。 降水的概率（百分比）。 | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL 第3天预报日降水类型] | 三天的天气预报。 白天的天气信息。 降水的形式。 | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL 第3天预测第QPF英寸] | 三天的天气预报。 白天的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL 第3天预测第QPF毫米] | 三天的天气预报。 白天的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL 第3天预报第QPF雪厘米] | 三天的天气预报。 白天的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第3天预测第QPF雪英寸] | 三天的天气预报。 白天的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第3天预测第3天相对湿度] | 三天的天气预报。 白天的天气信息。 空气的相对湿度，定义为空气中水蒸气量与在恒定温度下使空气达到饱和所需蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL 第3天预报天雪范围] | 三天的天气预报。 白天的天气信息。 潜在降雪量（1-3英寸、3-6英寸等）。 | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL 第3天预测天温度Celsius] | 三天的天气预报。 白天的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 温度（摄氏度） | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL 第3天预测温度华氏度] | 三天的天气预报。 白天的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 华氏温度 | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第3天预报第3天温度热指数Celsiu] | 三天的天气预报。 白天的天气信息。 根据温度和湿度暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天预报第3天温度热指数华氏] | 三天的天气预报。 白天的天气信息。 根据温度和湿度暴露的人所感受的温度。 华氏温度 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天预报天气温风寒摄氏度] | 三天的天气预报。 白天的天气信息。 根据温度和风速暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第3天预报天气温风降温华氏] | 三天的天气预报。 白天的天气信息。 根据温度和风速暴露的人所感受的温度。 华氏温度 | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天预测第3天雷击指数] | 三天的天气预报。 白天的天气信息。 雷暴对某个区域的影响概率指数。 0(无雷击5（严重雷电风险高）。 | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL 第3天预测第UV指数] | 三天的天气预报。 白天的天气信息。 12小时预测时段的最大UV指数。 | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL 第3天预报第1天风向] | 三天的天气预报。 白天的天气信息。 风从中吹出的磁风方向以度表示。 磁方向在0~359度之间变化，0°表示北、90°表示东、180°表示南、270°表示西等。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，间隔为10度。 | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL 第3天预报每天阵风公里/小时] | 三天的天气预报。 白天的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 每小时风速（千米） | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第3天预报每天阵风英里/小时] | 三天的天气预报。 白天的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 风速（以英里/小时为单位） | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第3天预报日风速公里/小时] | 三天的天气预报。 白天的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天预报第1天风速英里/小时] | 三天的天气预报。 白天的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第3天预报夜间云覆盖英里] | 三天的天气预报。 夜间的天气信息。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL 第3天预报夜间云层覆盖公里] | 三天的天气预报。 夜间的天气信息。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第3天预报夜间降水机会] | 三天的天气预报。 夜间的天气信息。 降水的概率（百分比）。 | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL 第3天预报夜间降水类型] | 三天的天气预报。 夜间的天气信息。 降水的形式。 | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL 第3天预报夜间QPF英寸] | 三天的天气预报。 夜间的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL 第3天预报夜QPF毫米] | 三天的天气预报。 夜间的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL 第3天预报夜QPF雪厘米] | 三天的天气预报。 夜间的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第3天预报夜QPF雪英寸] | 三天的天气预报。 夜间的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第3天预报夜间相对湿度] | 三天的天气预报。 夜间的天气信息。 空气的相对湿度，定义为空气中水蒸气量与在恒定温度下使空气达到饱和所需蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL 第3天预报夜间降雪范围] | 三天的天气预报。 夜间的天气信息。 潜在降雪量（1-3英寸、3-6英寸等）。 | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL 第3天预报夜间气温摄氏度] | 三天的天气预报。 夜间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 温度（摄氏度） | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL 第3天预报夜温华氏度] | 三天的天气预报。 夜间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 华氏温度 | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第3天预报夜间温度热指数Clisum] | 三天的天气预报。 夜间的天气信息。 根据温度和湿度暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天预报夜间温度热指数华氏] | 三天的天气预报。 夜间的天气信息。 根据温度和湿度暴露的人所感受的温度。 华氏温度 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天预报夜间气温风寒摄氏度] | 三天的天气预报。 夜间的天气信息。 根据温度和风速暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第3天预报夜间气温风降温华氏度] | 三天的天气预报。 夜间的天气信息。 根据温度和风速暴露的人所感受的温度。 华氏温度 | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天预报夜雷指数] | 三天的天气预报。 夜间的天气信息。 雷暴对某个区域的影响概率指数。 0(无雷击5（严重雷电风险高）。 | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL 第3天预报夜间UV指数] | 三天的天气预报。 夜间的天气信息。 12小时预测时段的最大UV指数。 | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL 第3天预报夜风方向] | 三天的天气预报。 夜间的天气信息。 风从中吹出的磁风方向以度表示。 磁方向在0~359度之间变化，0°表示北、90°表示东、180°表示南、270°表示西等。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，间隔为10度。 | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL 第3天预报每小时夜风公里] | 三天的天气预报。 夜间的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 每小时风速（千米） | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第3天预报每小时夜风阵风英里] | 三天的天气预报。 夜间的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 风速（以英里/小时为单位） | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第3天预报夜间风速公里/小时] | 三天的天气预报。 夜间的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天预报夜间风速英里/小时] | 三天的天气预报。 夜间的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第3天预测QPF英寸] | 三天的天气预报。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL 第3天预测QPF毫米] | 三天的天气预报。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL 第3天预报QPF雪厘米] | 三天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第3天预测QPF雪英寸] | 三天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL 第5天预测日历日温度最高Celsius] | 五天的天气预报。 指定日期的午夜至午夜每日最高温度。 温度（摄氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第5天预测日历日温度最高华氏度] | 五天的天气预报。 指定日期的午夜至午夜每日最高温度。 华氏温度 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第5天预测日历日温度最低摄氏度] | 五天的天气预报。 指定日期的午夜至午夜每日最低温度。 温度（摄氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第5天预测日历日温度最低华氏度] | 五天的天气预报。 指定日期的午夜至午夜每日最低温度。 华氏温度 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第5天预测第1天云覆盖英里] | 五天的天气预报。 白天的天气信息。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL 第5天预测日云覆盖公里] | 五天的天气预报。 白天的天气信息。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第5天预报日降水机会] | 五天的天气预报。 白天的天气信息。 降水的概率（百分比）。 | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL 第5天预报日降水类型] | 五天的天气预报。 白天的天气信息。 降水的形式。 | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL 第5天预测第QPF英寸] | 五天的天气预报。 白天的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL 第5天预测第QPF毫米] | 五天的天气预报。 白天的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL 第5天预报第QPF雪厘米] | 五天的天气预报。 白天的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第5天预测第QPF雪英寸] | 五天的天气预报。 白天的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第5天预测日相对湿度] | 五天的天气预报。 白天的天气信息。 空气的相对湿度，定义为空气中水蒸气量与在恒定温度下使空气达到饱和所需蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL 第5天预报日雪范围] | 五天的天气预报。 白天的天气信息。 潜在降雪量（1-3英寸、3-6英寸等）。 | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL 第5天预测天气温度Celsius] | 五天的天气预报。 白天的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 温度（摄氏度） | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL 第5天预测温度华氏度] | 五天的天气预报。 白天的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 华氏温度 | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第5天预报第5天温度热指数Celsiu] | 五天的天气预报。 白天的天气信息。 根据温度和湿度暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天预测天温度热指数华氏] | 五天的天气预报。 白天的天气信息。 根据温度和湿度暴露的人所感受的温度。 华氏温度 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天预报天气温风寒摄氏度] | 五天的天气预报。 白天的天气信息。 根据温度和风速暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第5天预报天气温风降温华氏度] | 五天的天气预报。 白天的天气信息。 根据温度和风速暴露的人所感受的温度。 华氏温度 | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天预测第1天雷击指数] | 五天的天气预报。 白天的天气信息。 雷暴对某个区域的影响概率指数。 0(无雷击5（严重雷电风险高）。 | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL 第5天预测日UV指数] | 五天的天气预报。 白天的天气信息。 12小时预测时段的最大UV指数。 | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL 第5天预报第1天风向] | 五天的天气预报。 白天的天气信息。 风从中吹出的磁风方向以度表示。 磁方向在0~359度之间变化，0°表示北、90°表示东、180°表示南、270°表示西等。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，间隔为10度。 | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL 第5天预报日阵风公里/小时] | 五天的天气预报。 白天的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 每小时风速（千米） | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第5天预报日阵风英里/小时] | 五天的天气预报。 白天的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 风速（以英里/小时为单位） | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第5天预报日风速公里/小时] | 五天的天气预报。 白天的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天预报日风速英里/小时] | 五天的天气预报。 白天的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第5天预报夜间云覆盖英里] | 五天的天气预报。 夜间的天气信息。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL 第5天预报夜间云层覆盖公里] | 五天的天气预报。 夜间的天气信息。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第5天预报夜间降水机会] | 五天的天气预报。 夜间的天气信息。 降水的概率（百分比）。 | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL 第5天预报夜间降水类型] | 五天的天气预报。 夜间的天气信息。 降水的形式。 | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL 第5天预报夜QPF英寸] | 五天的天气预报。 夜间的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL 第5天预报夜QPF毫米] | 五天的天气预报。 夜间的天气信息。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL 第5天预报夜QPF雪厘米] | 五天的天气预报。 夜间的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第5天预报夜QPF雪英寸] | 五天的天气预报。 夜间的天气信息。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第5天预报夜间相对湿度] | 五天的天气预报。 夜间的天气信息。 空气的相对湿度，定义为空气中水蒸气量与在恒定温度下使空气达到饱和所需蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL 第5天预报夜间降雪范围] | 五天的天气预报。 夜间的天气信息。 潜在降雪量（1-3英寸、3-6英寸等）。 | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL 第5天预报夜间气温摄氏度] | 五天的天气预报。 夜间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 温度（摄氏度） | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL 第5天预报夜温华氏度] | 五天的天气预报。 夜间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 华氏温度 | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第5天预报夜间温度热指数Clisum] | 五天的天气预报。 夜间的天气信息。 根据温度和湿度暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天预报夜间温度热指数华氏] | 五天的天气预报。 夜间的天气信息。 根据温度和湿度暴露的人所感受的温度。 华氏温度 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天预报夜间气温风寒摄氏度] | 五天的天气预报。 夜间的天气信息。 根据温度和风速暴露的人所感受的温度。 温度（摄氏度） | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第5天预报夜间气温降温华氏度] | 五天的天气预报。 夜间的天气信息。 根据温度和风速暴露的人所感受的温度。 华氏温度 | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天预报夜雷指数] | 五天的天气预报。 夜间的天气信息。 雷暴对某个区域的影响概率指数。 0(无雷击5（严重雷电风险高）。 | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL 第5天预报夜间UV指数] | 五天的天气预报。 夜间的天气信息。 12小时预测时段的最大UV指数。 | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL 第5天预报夜风方向] | 五天的天气预报。 夜间的天气信息。 风从中吹出的磁风方向以度表示。 磁方向在0~359度之间变化，0°表示北、90°表示东、180°表示南、270°表示西等。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，间隔为10度。 | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL 第5天预报每小时夜风公里] | 五天的天气预报。 夜间的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 每小时风速（千米） | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第5天预报每小时夜风阵风英里] | 五天的天气预报。 夜间的天气信息。 此数据字段包含有关平均风速的突然和临时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示“风速”，则它是必填的显示字段。 阵风的速度以每小时英里或每小时公里的速度表示。 风速（以英里/小时为单位） | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第5天预报夜间风速公里/小时] | 五天的天气预报。 夜间的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天预报夜间风速英里/小时] | 五天的天气预报。 夜间的天气信息。 风被当作矢量；因此，风必须具有方向和大小（速度）。 在当前条件下报告的风速信息，相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第5天预测QPF英寸] | 五天的天气预报。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以英寸为单位的降水 | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL 第5天预测QPF毫米] | 五天的天气预报。 12或24小时内的可测降水量（液体或液体当量）的预测。 以毫米计。 以毫米计的降水量 | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL 第5天预报QPF雪厘米] | 五天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第5天预测QPF雪英寸] | 五天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天预测日历日温度最高Celsius] | 七天的天气预报。 指定日期的午夜至午夜每日最高温度。 温度（摄氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第7天预测日历日温度最高华氏度] | 七天的天气预报。 指定日期的午夜至午夜每日最高温度。 华氏温度 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第7天预测日历日温度最低摄氏度] | 七天的天气预报。 指定日期的午夜至午夜每日最低温度。 温度（摄氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第7天预测日历日温度最低华氏度] | 七天的天气预报。 指定日期的午夜至午夜每日最低温度。 华氏温度 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第7天预报云覆盖英里] | 七天的天气预报。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL 第7天预报云覆盖公里] | 七天的天气预报。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL 第7天预测QPF英寸] | 七天的天气预报。 24小时内的可测降水量（液体或液体当量）。 以英寸为单位的降水 | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL 第7天预测QPF毫米] | 七天的天气预报。 24小时内的可测降水量（液体或液体当量）。 以毫米计的降水量 | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL 第7天预报QPF雪厘米] | 七天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第7天预测QPF雪英寸] | 七天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天预测UV指数] | 七天的天气预报。 12小时预测时段的最大UV指数。 | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL 第7天预报风向] | 七天的天气预报。 平均风向。 | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL 第7天预报风速公里/小时] | 七天的天气预报。 12小时预测期内最大持续风速的预测。<br>风被当作矢量；因此，风必须具有方向和大小（速度）。 预报中报告的风速信息相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第7天预报风速英里/小时] | 七天的天气预报。 12小时预测期内最大持续风速的预测。<br>风被当作矢量；因此，风必须具有方向和大小（速度）。 预报中报告的风速信息相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第10天预测日历日温度最高Celsius] | 十天的天气预报。 指定日期的午夜至午夜每日最高温度。 温度（摄氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第10天预测日历日温度最高华氏度] | 十天的天气预报。 指定日期的午夜至午夜每日最高温度。 华氏温度 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第10天预测日历日温度最低摄氏度] | 十天的天气预报。 指定日期的午夜至午夜每日最低温度。 温度（摄氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第10天预测日历日温度最低华氏度] | 十天的天气预报。 指定日期的午夜至午夜每日最低温度。 华氏温度 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第10天Forecast Cloud封面英里] | 十天的天气预报。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL 第10天预报云封面公里] | 十天的天气预报。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL 第10天预测QPF英寸] | 十天的天气预报。 24小时内的可测降水量（液体或液体当量）。 以英寸为单位的降水 | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL 第10天预测QPF毫米] | 十天的天气预报。 24小时内的可测降水量（液体或液体当量）。 以毫米计的降水量 | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL 第10天预报QPF雪公分] | 十天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第10天预测QPF雪英寸] | 十天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL 第10天预测UV指数] | 十天的天气预报。 12小时预测时段的最大UV指数。 | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL 第10天预报风向] | 十天的天气预报。 平均风向。 | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL 第10天预报风速公里/小时] | 十天的天气预报。 12小时预测期内最大持续风速的预测。<br>风被当作矢量；因此，风必须具有方向和大小（速度）。 预报中报告的风速信息相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第10天预报风速英里/小时] | 十天的天气预报。 12小时预测期内最大持续风速的预测。<br>风被当作矢量；因此，风必须具有方向和大小（速度）。 预报中报告的风速信息相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第14天预测日历日温度最高Celsius] | 14天的天气预报。 指定日期的午夜至午夜每日最高温度。 温度（摄氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第14天预测日历日温度最高华氏度] | 14天的天气预报。 指定日期的午夜至午夜每日最高温度。 华氏温度 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第14天预测日历日温度最低摄氏度] | 14天的天气预报。 指定日期的午夜至午夜每日最低温度。 温度（摄氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第14天预测日历日温度最低华氏度] | 14天的天气预报。 指定日期的午夜至午夜每日最低温度。 华氏温度 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第14天预报云覆盖英里] | 14天的天气预报。 白天平均云层覆盖以百分比表示。 距离（以英里为单位）。 | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL 第14天预报云覆盖公里] | 14天的天气预报。 白天平均云层覆盖以百分比表示。 距离（以公里为单位）。 | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 第14天预测QPF英寸 | 14天的天气预报。 24小时内的可测降水量（液体或液体当量）。 以英寸为单位的降水 | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL 第14天预测QPF毫米] | 14天的天气预报。 24小时内的可测降水量（液体或液体当量）。 以毫米计的降水量 | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL 第14天预报QPF雪公分] | 14天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪量厘米 | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第14天预测QPF雪英寸] | 14天的天气预报。 预测12或24小时预测期的可测降水量为雪。 以厘米计。 降雪以英寸计 | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL 第14天预测UV指数] | 14天的天气预报。 12小时预测时段的最大UV指数。 | `weather.forecast.day14Forecast.uvIndex` |
| 第14天预报风向 | 14天的天气预报。 平均风向。 | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL 第14天预报风速公里/小时] | 14天的天气预报。 12小时预测期内最大持续风速的预测。<br>风被当作矢量；因此，风必须具有方向和大小（速度）。 预报中报告的风速信息相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 每小时风速（千米） | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第14天预报风速英里/小时] | 14天的天气预报。 12小时预测期内最大持续风速的预测。<br>风被当作矢量；因此，风必须具有方向和大小（速度）。 预报中报告的风速信息相当于10分钟的平均风速，称为持续风速。 风速的突然或短暂变化被称为“风刮”，并在单独的数据场中报告。 风向总是表示为“从风吹来”，即北风从北向南吹来。 如果你在北风中面对北风，风就在你脸上。 朝南，北风在你后面。 风速（以英里/小时为单位） | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 触发器 {#triggers}

触发器根据各种输入定义语义天气条件。

| 字段 | 描述 | XDM路径 |
| --- | ---- | --- |
| [!UICONTROL 产品触发器] | 指示条件何时适合提高某些类别产品的销售。  它们映射到整数度。 可从IBM获取完整列表。 | `weather.productTriggers` |
| [!UICONTROL 相对触发器] | 基于人类感知的相对条件。 热或冷。 它们映射到整数度。 可从IBM获取完整列表。 | `weather.relativeTriggers` |
| [!UICONTROL 恶劣天气触发] | 表示各种恶劣的天气条件，如飓风或过度的降雨。 | `weather.severeTriggers` |