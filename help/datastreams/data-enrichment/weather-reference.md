---
title: 天气数据字段映射
description: 有关可用的天气数据字段的参考页面，这些字段作为与天气渠道集成的一部分提供。
exl-id: bc0f158b-f9d0-424a-aa21-953e8380473f
source-git-commit: e2122008fcae1016db03d6b5f56e4fa25520f9d0
workflow-type: tm+mt
source-wordcount: '12238'
ht-degree: 0%

---

# 天气数据字段映射

Adobe已与 [!DNL [The Weather Company]](https://www.ibm.com/weather) 为通过数据流收集的数据引入美国天气的额外上下文。 您可以将此数据用于Experience Platform中的分析、定位和区段创建。

本页列出了可用于扩充受众数据的所有可用字段。

这些字段将划分为三个与字段组对齐的不同组。

* [**[!UICONTROL 当前天气]**](#current-weather)：用户的当前天气情况（基于其位置）。 这包括当前温度、沉降、云覆盖率等。
* [**[!UICONTROL 预测天气]**](#forecast)：该预测包括用户位置的1、2、3、5、7和10天预测。
* [**[!UICONTROL 触发器]**](#triggers)：触发器是映射到不同语义天气条件的特定组合。 有三种不同类型的天气触发器：

   * **[!UICONTROL 相对触发器]**：语义上有意义的情况，例如寒冷或雨天。 不同气候之间的定义可能有所不同。
   * **[!UICONTROL 产品触发器]**：导致购买不同类型产品的条件。 例如：寒冷的天气预报可能意味着购买雨衣的可能性更大。
   * **[!UICONTROL 恶劣天气触发程序]**：严重天气警告，例如冬季风暴或飓风警告。

## 当前天气 {#current-weather}

用户当前的天气情况（基于其位置）。

| 字段 | 描述 | XDM路径 |
| --- | ---- | --- |
| [!UICONTROL 温度露点（摄氏度）] | 空气必须恒压冷却达到饱和的温度。 露点也是间接测量空气湿度的方法。 露点永远不会超过温度。 当露点和温度相等时，通常会形成云或雾。 温度和露点值越接近，相对湿度越高。 范围 —80到100 (°F)或–62到37 (°C)。 以摄氏度表示的温度 | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL 华氏温度露点] | 空气必须恒压冷却达到饱和的温度。 露点也是间接测量空气湿度的方法。 露点永远不会超过温度。 当露点和温度相等时，通常会形成云或雾。 温度和露点值越接近，相对湿度越高。 范围 —80到100 (°F)或–62到37 (°C)。 以华氏度为单位的温度 | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL 过去一小时内的降水量] | 轧制小时液体沉淀量。 显示的金额是请求时间内的滚动时间（现在）。 降水量（英寸） | `weather.current.precip1Hour.inches` |
| [!UICONTROL 过去一小时的降水量] | 轧制小时液体沉淀量。 显示的金额是请求时间内的滚动时间（现在）。 降水（毫米） | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 轧制二十四小时液相沉淀量。 显示的金额是请求时间内的滚动时间（现在）。 降水量（英寸） | `weather.current.precip24Hour.inches` |
| [!UICONTROL 降雨量持续24小时] | 轧制二十四小时液相沉淀量。 显示的金额是请求时间内的滚动时间（现在）。 降水（毫米） | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL 降水持续6小时] | 轧制六小时液相沉淀量。 显示的金额是请求时间内的滚动时间（现在）。 降水量（英寸） | `weather.current.precip6Hour.inches` |
| [!UICONTROL 降雨量持续6小时] | 轧制六小时液相沉淀量。 显示的金额是请求时间内的滚动时间（现在）。 降水（毫米） | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL 压力变化] | 过去三小时压力变化，毫巴。 | `weather.current.pressureChange` |
| [!UICONTROL 压力平均海平面] | 平均海平面压力。  换句话说，就是海平面上的平均气压值。<br>范围 — 精确到1/10 mb的毫巴。 | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL 相对湿度] | 空气的相对湿度，定义为空气中的水蒸汽量与使空气在恒定温度下饱和所需的水蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.current.relativeHumidity` |
| [!UICONTROL 降雪时间为前一小时厘米] | 一小时的降雪量。  显示的金额是请求时间内的滚动时间（现在）。 降雪量（厘米） | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL 雪花最后一小时（英寸）] | 一小时的降雪量。  显示的金额是请求时间内的滚动时间（现在）。 降雪（以英寸为单位） | `weather.current.snow1Hour.inches` |
| [!UICONTROL 24小时厘米的雪] | 二十四小时的降雪量。  显示的金额是请求时间内的滚动时间（现在）。 降雪量（厘米） | `weather.current.snow24Hour.centimeters` |
| 雪24小时英寸 | 二十四小时的降雪量。  显示的金额是请求时间内的滚动时间（现在）。 降雪（以英寸为单位） | `weather.current.snow24Hour.inches` |
| [!UICONTROL 雪持续6小时厘米] | 一小时的降雪量。  显示的金额是请求时间内的滚动时间（现在）。 降雪量（厘米） | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL 雪持续6小时] | 一小时的降雪量。  显示的金额是请求时间内的滚动时间（现在）。 降雪（以英寸为单位） | `weather.current.snow6Hour.inches` |
| [!UICONTROL 日落时间] | UTC的日落时间。 | `weather.current.sunsetTime` |
| [!UICONTROL 摄氏温度] | 以定义的度量单位表示的温度。 范围–140到140。 以摄氏度表示的温度 | `weather.current.temperature.celsius` |
| [!UICONTROL 华氏温度] | 以定义的度量单位表示的温度。 范围–140到140。 以华氏度为单位的温度 | `weather.current.temperature.fahrenheit` |
| [!UICONTROL 温度变化24小时] | 与24小时前报告相比的温度变化。 以摄氏度表示的温度 | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL 24小时内的温度变化] | 与24小时前报告相比的温度变化。 以华氏度为单位的温度 | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL 温度感觉像摄氏度] | 一个明显的温度。 它表示由于风寒或热指数的综合影响，暴露在人体皮肤上的空气温度“感觉”。<br>当温度在65°F或更高时，Feel Like值表示计算的热指数。  当温度低于65°F时，感觉相似值表示计算出的风冷。<br>范围–140到140。 以摄氏度表示的温度 | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL 温度感觉像华氏度] | 一个明显的温度。 它表示由于风寒或热指数的综合影响，暴露在人体皮肤上的空气温度“感觉”。<br>当温度在65°F或更高时，Feel Like值表示计算的热指数。  当温度低于65°F时，感觉相似值表示计算出的风冷。<br>范围–140到140。 以华氏度为单位的温度 | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL 自上午7点以来的最高温度] | 当地时间清晨7点以来的最高温度。 以摄氏度表示的温度 | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL 自上午7点以来的最高温度（华氏）] | 当地时间清晨7点以来的最高温度。 以华氏度为单位的温度 | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL 最低温度过去24小时（摄氏）] | 过去24小时内的最低温度。  24小时是指请求时间（现在）。  以摄氏度表示的温度 | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL 最低温度持续24小时（华氏）] | 过去24小时内的最低温度。  24小时是指请求时间（现在）。  以华氏度为单位的温度 | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL 风向] | 风吹向的磁力风向以度表示。 磁方向从0度变化到359度，其中0°表示北方，90°表示东方，180°表示南方，270°表示西方，依此类推。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，以10度为间隔。 | `weather.current.windDirection` |
| [!UICONTROL 每小时阵风公里数] | 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速（以公里为单位/小时） | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL 每小时阵风里数] | 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速以英里/小时为单位 | `weather.current.windGust.`milesPerHour |
| [!UICONTROL 风速公里/小时] | 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL 风速英里/小时] | 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.current.windSpeed.milesPerHour` |

## 预测天气 {#forecast}

用户在特定时间点的预测天气（基于位置）。

| 字段 | 描述 | XDM路径 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 一天天气预报。 给定日期的午夜到午夜每日最高温度。 以摄氏度表示的温度 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 一天天气预报。 给定日期的午夜到午夜每日最高温度。 以华氏度为单位的温度 | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 一天天气预报。 给定日期的午夜到午夜每日最低温度。 以摄氏度表示的温度 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 一天天气预报。 给定日期的午夜到午夜每日最低温度。 以华氏度为单位的温度 | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 一天天气预报。 某个白天期间的天气信息。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 一天天气预报。 某个白天期间的天气信息。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 一天天气预报。 某个白天期间的天气信息。 有降水的概率（百分比）。 | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 一天天气预报。 某个白天期间的天气信息。 可能降水的形式（雨、雪、雨夹雪等）。 | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 一天天气预报。 某个白天期间的天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 一天天气预报。 某个白天期间的天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 一天天气预报。 某个白天期间的天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 一天天气预报。 某个白天期间的天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 一天天气预报。 某个白天期间的天气信息。 空气的相对湿度，定义为空气中的水蒸汽量与使空气在恒定温度下饱和所需的水蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 一天天气预报。 某个白天期间的天气信息。 潜在的降雪量（1-3&quot;、3-6&quot;等）。 | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 一天天气预报。 某个白天期间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以摄氏度表示的温度 | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 一天天气预报。 某个白天期间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以华氏度为单位的温度 | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 一天天气预报。 某个白天期间的天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 一天天气预报。 某个白天期间的天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 一天天气预报。 某个白天期间的天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 一天天气预报。 某个白天期间的天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 一天天气预报。 某个白天期间的天气信息。 雷暴影响一个区域的概率的指数。 0(无雷击至5（严重雷暴的高风险）。 | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 一天天气预报。 某个白天期间的天气信息。 12小时预测时段的最大UV索引。 | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 一天天气预报。 某个白天期间的天气信息。 风吹向的磁力风向以度表示。 磁方向从0度变化到359度，其中0°表示北方，90°表示东方，180°表示南方，270°表示西方，依此类推。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，以10度为间隔。 | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 一天天气预报。 某个白天期间的天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速（以公里为单位/小时） | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 一天天气预报。 某个白天期间的天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速以英里/小时为单位 | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 一天天气预报。 某个白天期间的天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 一天天气预报。 某个白天期间的天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour ` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 一天天气预报。 夜间天气信息。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 一天天气预报。 夜间天气信息。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第1天预报夜间降水机会] | 一天天气预报。 夜间天气信息。 有降水的概率（百分比）。 | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 一天天气预报。 夜间天气信息。 可能降水的形式（雨、雪、雨夹雪等）。 | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 一天天气预报。 夜间天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 一天天气预报。 夜间天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 一天天气预报。 夜间天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 一天天气预报。 夜间天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 一天天气预报。 夜间天气信息。 空气的相对湿度，定义为空气中的水蒸汽量与使空气在恒定温度下饱和所需的水蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 一天天气预报。 夜间天气信息。 潜在的降雪量（1-3&quot;、3-6&quot;等）。 | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 一天天气预报。 夜间天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以摄氏度表示的温度 | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 一天天气预报。 夜间天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以华氏度为单位的温度 | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 一天天气预报。 夜间天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 一天天气预报。 夜间天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 一天天气预报。 夜间天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第1天预报夜温寒风] | 一天天气预报。 夜间天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第1天预报夜雷指数] | 一天天气预报。 夜间天气信息。 雷暴影响一个区域的概率的指数。 0(无雷击至5（严重雷暴的高风险）。 | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL 第1天预测夜间UV指数] | 一天天气预报。 夜间天气信息。 12小时预测时段的最大UV索引。 | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL 第1天预报夜风向] | 一天天气预报。 夜间天气信息。 风吹向的磁力风向以度表示。 磁方向从0度变化到359度，其中0°表示北方，90°表示东方，180°表示南方，270°表示西方，依此类推。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，以10度为间隔。 | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL 第1天预报夜风阵风公里每小时] | 一天天气预报。 夜间天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速（以公里为单位/小时） | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第1天预报夜风阵风英里每小时] | 一天天气预报。 夜间天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速以英里/小时为单位 | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第1天预报夜间风速公里每小时] | 一天天气预报。 夜间天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第1天预测夜间风速英里/小时] | 一天天气预报。 夜间天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第1天预测QPF英寸] | 一天天气预报。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL 第1天预测QPF毫米] | 一天天气预报。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL 第1天预测QPF雪厘米] | 一天天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第1天预测QPF雪英寸] | 一天天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL 第2天预测日历天最高温度（摄氏）] | 两天的天气预报。 给定日期的午夜到午夜每日最高温度。 以摄氏度表示的温度 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第2天预测日历日温度最高华氏度] | 两天的天气预报。 给定日期的午夜到午夜每日最高温度。 以华氏度为单位的温度 | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第2天预测日历天温度最低摄氏度] | 两天的天气预报。 给定日期的午夜到午夜每日最低温度。 以摄氏度表示的温度 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第2天预测日历天温度最低华氏度] | 两天的天气预报。 给定日期的午夜到午夜每日最低温度。 以华氏度为单位的温度 | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第2天预测云覆盖英里] | 两天的天气预报。 某个白天期间的天气信息。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL 第2天预测云覆盖公里] | 两天的天气预报。 某个白天期间的天气信息。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第2天预测降水机会] | 两天的天气预报。 某个白天期间的天气信息。 有降水的概率（百分比）。 | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL 第2天预测降水类型] | 两天的天气预报。 某个白天期间的天气信息。 可能降水的形式（雨、雪、雨夹雪等）。 | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL 第2天预测日QPF英寸] | 两天的天气预报。 某个白天期间的天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL 第2天预测QPF毫米] | 两天的天气预报。 某个白天期间的天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL 第2天预测QPF雪厘米] | 两天的天气预报。 某个白天期间的天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第2天预测QPF雪英寸] | 两天的天气预报。 某个白天期间的天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第2天预测日期相对湿度] | 两天的天气预报。 某个白天期间的天气信息。 空气的相对湿度，定义为空气中的水蒸汽量与使空气在恒定温度下饱和所需的水蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL 第2天预测天雪范围] | 两天的天气预报。 某个白天期间的天气信息。 潜在的降雪量（1-3&quot;、3-6&quot;等）。 | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL 第2天预测天温度（摄氏）] | 两天的天气预报。 某个白天期间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以摄氏度表示的温度 | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL 第2天预测日温度华氏度] | 两天的天气预报。 某个白天期间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以华氏度为单位的温度 | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第2天预测天温度热指数摄氏度] | 两天的天气预报。 某个白天期间的天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天预测日温度热指数华氏度] | 两天的天气预报。 某个白天期间的天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天预测日气温寒冷摄氏度] | 两天的天气预报。 某个白天期间的天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第2天预测日气温寒风华氏度] | 两天的天气预报。 某个白天期间的天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天预测日雷鸣指数] | 两天的天气预报。 某个白天期间的天气信息。 雷暴影响一个区域的概率的指数。 0(无雷击至5（严重雷暴的高风险）。 | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL 第2天预测UV指数] | 两天的天气预报。 某个白天期间的天气信息。 12小时预测时段的最大UV索引。 | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL 第2天预报日风向] | 两天的天气预报。 某个白天期间的天气信息。 风吹向的磁力风向以度表示。 磁方向从0度变化到359度，其中0°表示北方，90°表示东方，180°表示南方，270°表示西方，依此类推。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，以10度为间隔。 | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL 第2天预报日阵风公里每小时] | 两天的天气预报。 某个白天期间的天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速（以公里为单位/小时） | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第2天预报日阵风英里每小时] | 两天的天气预报。 某个白天期间的天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速以英里/小时为单位 | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第2天预报日风速公里/小时] | 两天的天气预报。 某个白天期间的天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天预测日风速英里每小时] | 两天的天气预报。 某个白天期间的天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第2天预报夜云覆盖英里] | 两天的天气预报。 夜间天气信息。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL 第2天预报夜云覆盖公里] | 两天的天气预报。 夜间天气信息。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第2天预报夜降水机会] | 两天的天气预报。 夜间天气信息。 有降水的概率（百分比）。 | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL 第2天预报夜间降水类型] | 两天的天气预报。 夜间天气信息。 可能降水的形式（雨、雪、雨夹雪等）。 | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL 第2天预测夜间QPF英寸] | 两天的天气预报。 夜间天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL 第2天预测夜间QPF毫米] | 两天的天气预报。 夜间天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL 第2天预报夜QPF雪公分] | 两天的天气预报。 夜间天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第2天预测夜QPF雪英寸] | 两天的天气预报。 夜间天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第2天预测夜间相对湿度] | 两天的天气预报。 夜间天气信息。 空气的相对湿度，定义为空气中的水蒸汽量与使空气在恒定温度下饱和所需的水蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL 第2天预报夜降雪范围] | 两天的天气预报。 夜间天气信息。 潜在的降雪量（1-3&quot;、3-6&quot;等）。 | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL 第2天预测夜间温度摄氏] | 两天的天气预报。 夜间天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以摄氏度表示的温度 | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL 第2天预测夜间温度华氏度] | 两天的天气预报。 夜间天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以华氏度为单位的温度 | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第2天预测夜间温度热指数摄氏度] | 两天的天气预报。 夜间天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第2天预测夜间温度热指数华氏度] | 两天的天气预报。 夜间天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第2天预报夜温寒风] | 两天的天气预报。 夜间天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第2天预报夜温寒风] | 两天的天气预报。 夜间天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第2天预报夜雷指数] | 两天的天气预报。 夜间天气信息。 雷暴影响一个区域的概率的指数。 0(无雷击至5（严重雷暴的高风险）。 | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL 第2天预测夜间UV指数] | 两天的天气预报。 夜间天气信息。 12小时预测时段的最大UV索引。 | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL 第2天预报夜风向] | 两天的天气预报。 夜间天气信息。 风吹向的磁力风向以度表示。 磁方向从0度变化到359度，其中0°表示北方，90°表示东方，180°表示南方，270°表示西方，依此类推。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，以10度为间隔。 | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL 第2天预报夜风阵风公里每小时] | 两天的天气预报。 夜间天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速（以公里为单位/小时） | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第2天预报夜风阵风英里每小时] | 两天的天气预报。 夜间天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速以英里/小时为单位 | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第2天预报夜间风速公里每小时] | 两天的天气预报。 夜间天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第2天预报夜间风速英里/小时] | 两天的天气预报。 夜间天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第2天预测QPF英寸] | 两天的天气预报。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL 第2天预测QPF毫米] | 两天的天气预报。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL 第2天预测QPF雪厘米] | 两天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第2天预测QPF雪英寸] | 两天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL 第3天预测日历天最高温度（摄氏）] | 三天的天气预报。 给定日期的午夜到午夜每日最高温度。 以摄氏度表示的温度 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第3天预测日历日温度最高华氏度] | 三天的天气预报。 给定日期的午夜到午夜每日最高温度。 以华氏度为单位的温度 | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第3天预测日历天温度最低摄氏度] | 三天的天气预报。 给定日期的午夜到午夜每日最低温度。 以摄氏度表示的温度 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第3天预测日历天温度最低华氏度] | 三天的天气预报。 给定日期的午夜到午夜每日最低温度。 以华氏度为单位的温度 | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第3天预测云覆盖英里] | 三天的天气预报。 某个白天期间的天气信息。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL 第3天预测云覆盖公里] | 三天的天气预报。 某个白天期间的天气信息。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第3天预测降水机会] | 三天的天气预报。 某个白天期间的天气信息。 有降水的概率（百分比）。 | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL 第3天预测降水类型] | 三天的天气预报。 某个白天期间的天气信息。 可能降水的形式（雨、雪、雨夹雪等）。 | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL 第3天预测QPF英寸] | 三天的天气预报。 某个白天期间的天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL 第3天预测QPF毫米] | 三天的天气预报。 某个白天期间的天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL 第3天预测QPF雪厘米] | 三天的天气预报。 某个白天期间的天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第3天预测QPF雪英寸] | 三天的天气预报。 某个白天期间的天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第3天预测日期相对湿度] | 三天的天气预报。 某个白天期间的天气信息。 空气的相对湿度，定义为空气中的水蒸汽量与使空气在恒定温度下饱和所需的水蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL 第3天预测天雪范围] | 三天的天气预报。 某个白天期间的天气信息。 潜在的降雪量（1-3&quot;、3-6&quot;等）。 | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL 第3天预测天温度摄氏] | 三天的天气预报。 某个白天期间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以摄氏度表示的温度 | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL 第3天预测日温度华氏度] | 三天的天气预报。 某个白天期间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以华氏度为单位的温度 | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第3天预测天温度热指数摄氏度] | 三天的天气预报。 某个白天期间的天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天预测日温度热指数华氏度] | 三天的天气预报。 某个白天期间的天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天预测日气温寒冷摄氏度] | 三天的天气预报。 某个白天期间的天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第3天预报当天气温寒风华氏度] | 三天的天气预报。 某个白天期间的天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天预测日雷鸣指数] | 三天的天气预报。 某个白天期间的天气信息。 雷暴影响一个区域的概率的指数。 0(无雷击至5（严重雷暴的高风险）。 | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL 第3天预测UV指数] | 三天的天气预报。 某个白天期间的天气信息。 12小时预测时段的最大UV索引。 | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL 第3天预报日风向] | 三天的天气预报。 某个白天期间的天气信息。 风吹向的磁力风向以度表示。 磁方向从0度变化到359度，其中0°表示北方，90°表示东方，180°表示南方，270°表示西方，依此类推。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，以10度为间隔。 | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL 第3天预报日阵风公里每小时] | 三天的天气预报。 某个白天期间的天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速（以公里为单位/小时） | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第3天预测一天阵风英里每小时] | 三天的天气预报。 某个白天期间的天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速以英里/小时为单位 | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第3天预报日风速公里每小时] | 三天的天气预报。 某个白天期间的天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天预测日风速英里每小时] | 三天的天气预报。 某个白天期间的天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第3天预测夜云覆盖英里] | 三天的天气预报。 夜间天气信息。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL 第3天预报夜云覆盖公里] | 三天的天气预报。 夜间天气信息。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第3天预报夜间降水机会] | 三天的天气预报。 夜间天气信息。 有降水的概率（百分比）。 | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL 第3天预报夜间降水类型] | 三天的天气预报。 夜间天气信息。 可能降水的形式（雨、雪、雨夹雪等）。 | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL 第3天预测夜间QPF英寸] | 三天的天气预报。 夜间天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL 第3天预测夜间QPF毫米] | 三天的天气预报。 夜间天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL 第3天预报夜QPF雪公分] | 三天的天气预报。 夜间天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第3天预测夜QPF雪英寸] | 三天的天气预报。 夜间天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第3天预测夜间相对湿度] | 三天的天气预报。 夜间天气信息。 空气的相对湿度，定义为空气中的水蒸汽量与使空气在恒定温度下饱和所需的水蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL 第3天预报夜降雪范围] | 三天的天气预报。 夜间天气信息。 潜在的降雪量（1-3&quot;、3-6&quot;等）。 | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL 第3天预测夜间温度摄氏] | 三天的天气预报。 夜间天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以摄氏度表示的温度 | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL 第3天预测夜间气温华氏度] | 三天的天气预报。 夜间天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以华氏度为单位的温度 | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第3天预测夜间温度热指数摄氏度] | 三天的天气预报。 夜间天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第3天预测夜间温度热指数华氏度] | 三天的天气预报。 夜间天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第3天预报夜温寒风] | 三天的天气预报。 夜间天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第3天预报夜温寒风] | 三天的天气预报。 夜间天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第3天预报夜雷指数] | 三天的天气预报。 夜间天气信息。 雷暴影响一个区域的概率的指数。 0(无雷击至5（严重雷暴的高风险）。 | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL 第3天预测夜间UV指数] | 三天的天气预报。 夜间天气信息。 12小时预测时段的最大UV索引。 | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL 第3天预报夜风向] | 三天的天气预报。 夜间天气信息。 风吹向的磁力风向以度表示。 磁方向从0度变化到359度，其中0°表示北方，90°表示东方，180°表示南方，270°表示西方，依此类推。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，以10度为间隔。 | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL 第3天预报夜风阵风公里每小时] | 三天的天气预报。 夜间天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速（以公里为单位/小时） | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第3天预报夜风阵风英里每小时] | 三天的天气预报。 夜间天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速以英里/小时为单位 | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第3天预报夜间风速公里每小时] | 三天的天气预报。 夜间天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第3天预报夜间风速英里/小时] | 三天的天气预报。 夜间天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第3天预测QPF英寸] | 三天的天气预报。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL 第3天预测QPF毫米] | 三天的天气预报。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL 第3天预测QPF雪厘米] | 三天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第3天预测QPF雪英寸] | 三天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL 第5天预测日历天最高温度（摄氏）] | 五天的天气预报。 给定日期的午夜到午夜每日最高温度。 以摄氏度表示的温度 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第5天预测日历日温度最高华氏度] | 五天的天气预报。 给定日期的午夜到午夜每日最高温度。 以华氏度为单位的温度 | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第5天预测日历天温度最低摄氏度] | 五天的天气预报。 给定日期的午夜到午夜每日最低温度。 以摄氏度表示的温度 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第5天预测日历天温度最低华氏度] | 五天的天气预报。 给定日期的午夜到午夜每日最低温度。 以华氏度为单位的温度 | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第5天预测云覆盖英里] | 五天的天气预报。 某个白天期间的天气信息。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL 第5天预测云覆盖公里] | 五天的天气预报。 某个白天期间的天气信息。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL 第5天预测降水机会] | 五天的天气预报。 某个白天期间的天气信息。 有降水的概率（百分比）。 | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL 第5天预测降水类型] | 五天的天气预报。 某个白天期间的天气信息。 可能降水的形式（雨、雪、雨夹雪等）。 | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL 第5天预测QPF英寸] | 五天的天气预报。 某个白天期间的天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL 第5天预测QPF毫米] | 五天的天气预报。 某个白天期间的天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL 第5天预测QPF雪厘米] | 五天的天气预报。 某个白天期间的天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL 第5天预测QPF雪英寸] | 五天的天气预报。 某个白天期间的天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL 第5天预测日期相对湿度] | 五天的天气预报。 某个白天期间的天气信息。 空气的相对湿度，定义为空气中的水蒸汽量与使空气在恒定温度下饱和所需的水蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL 第5天预测天雪范围] | 五天的天气预报。 某个白天期间的天气信息。 潜在的降雪量（1-3&quot;、3-6&quot;等）。 | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL 第5天预测天温度摄氏] | 五天的天气预报。 某个白天期间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以摄氏度表示的温度 | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL 第5天预测日温度华氏度] | 五天的天气预报。 某个白天期间的天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以华氏度为单位的温度 | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL 第5天预测天温度热指数摄氏度] | 五天的天气预报。 某个白天期间的天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天预测日温度热指数华氏度] | 五天的天气预报。 某个白天期间的天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天预测日气温寒冷摄氏度] | 五天的天气预报。 某个白天期间的天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL 第5天预测当天气温寒风华氏度] | 五天的天气预报。 某个白天期间的天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天预测日雷鸣指数] | 五天的天气预报。 某个白天期间的天气信息。 雷暴影响一个区域的概率的指数。 0(无雷击至5（严重雷暴的高风险）。 | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL 第5天预测UV指数] | 五天的天气预报。 某个白天期间的天气信息。 12小时预测时段的最大UV索引。 | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL 第5天预报日风向] | 五天的天气预报。 某个白天期间的天气信息。 风吹向的磁力风向以度表示。 磁方向从0度变化到359度，其中0°表示北方，90°表示东方，180°表示南方，270°表示西方，依此类推。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，以10度为间隔。 | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL 第5天预报日阵风公里每小时] | 五天的天气预报。 某个白天期间的天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速（以公里为单位/小时） | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL 第5天预报日阵风英里每小时] | 五天的天气预报。 某个白天期间的天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速以英里/小时为单位 | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL 第5天预报日风速公里每小时] | 五天的天气预报。 某个白天期间的天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天预测日风速英里每小时] | 五天的天气预报。 某个白天期间的天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL 第5天预报夜云覆盖英里] | 五天的天气预报。 夜间天气信息。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL 第5天预报夜云覆盖公里] | 五天的天气预报。 夜间天气信息。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL 第5天预报夜降水机会] | 五天的天气预报。 夜间天气信息。 有降水的概率（百分比）。 | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL 第5天预报夜间降水类型] | 五天的天气预报。 夜间天气信息。 可能降水的形式（雨、雪、雨夹雪等）。 | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL 第5天预测夜QPF英寸] | 五天的天气预报。 夜间天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL 第5天预测夜QPF毫米] | 五天的天气预报。 夜间天气信息。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL 第5天预报夜QPF雪公分] | 五天的天气预报。 夜间天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL 第5天预测夜QPF雪英寸] | 五天的天气预报。 夜间天气信息。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL 第5天预测夜间相对湿度] | 五天的天气预报。 夜间天气信息。 空气的相对湿度，定义为空气中的水蒸汽量与使空气在恒定温度下饱和所需的水蒸汽量的比率。 相对湿度始终以百分比表示。<br>范围 — 0到100。 | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL 第5天预报夜降雪范围] | 五天的天气预报。 夜间天气信息。 潜在的降雪量（1-3&quot;、3-6&quot;等）。 | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL 第5天预测夜间温度摄氏] | 五天的天气预报。 夜间天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以摄氏度表示的温度 | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL 第5天预测夜间气温华氏度] | 五天的天气预报。 夜间天气信息。 以定义的度量单位表示的温度。 范围–140到140。 以华氏度为单位的温度 | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL 第5天预测夜间温度热指数摄氏度] | 五天的天气预报。 夜间天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL 第5天预测夜间温度热指数华氏度] | 五天的天气预报。 夜间天气信息。 根据温度和湿度，接触的人会感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL 第5天预报夜温寒风] | 五天的天气预报。 夜间天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以摄氏度表示的温度 | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL 第5天预报夜温寒风] | 五天的天气预报。 夜间天气信息。 根据温度和风速，暴露在外的人员感觉到的温度。 以华氏度为单位的温度 | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL 第5天预报夜雷指数] | 五天的天气预报。 夜间天气信息。 雷暴影响一个区域的概率的指数。 0(无雷击至5（严重雷暴的高风险）。 | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL 第5天预测夜间UV指数] | 五天的天气预报。 夜间天气信息。 12小时预测时段的最大UV索引。 | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL 第5天预报夜风向] | 五天的天气预报。 夜间天气信息。 风吹向的磁力风向以度表示。 磁方向从0度变化到359度，其中0°表示北方，90°表示东方，180°表示南方，270°表示西方，依此类推。<br>范围 — 0&lt;=wind_dire_deg&lt;=350，以10度为间隔。 | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL 第5天预报夜风阵风公里每小时] | 五天的天气预报。 夜间天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速（以公里为单位/小时） | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL 第5天预报夜风阵风英里每小时] | 五天的天气预报。 夜间天气信息。 此数据字段包含有关平均风速的突然和暂时变化的信息。 该报告始终显示观测期间记录的最大阵风速度。 如果显示了“风速”，则为必填显示字段。 阵风的速度可以用英里/小时或公里/小时表示。 风速以英里/小时为单位 | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL 第5天预报夜间风速公里每小时] | 五天的天气预报。 夜间天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL 第5天预报夜间风速英里/小时] | 五天的天气预报。 夜间天气信息。 风被视为矢量；因此，风必须有方向和大小（速度）。 在目前条件下所报告的风信息相当于一个叫做持续风速的10分钟的平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL 第5天预测QPF英寸] | 五天的天气预报。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水量（英寸） | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL 第5天预测QPF毫米] | 五天的天气预报。 12或24小时期间之预计可计量降水（液体或液体当量）。 以毫米为单位。 降水（毫米） | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL 第5天预测QPF雪厘米] | 五天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第5天预测QPF雪英寸] | 五天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天预测日历天最高温度（摄氏）] | 七天的天气预报。 给定日期的午夜到午夜每日最高温度。 以摄氏度表示的温度 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第7天预测日历日温度最高华氏度] | 七天的天气预报。 给定日期的午夜到午夜每日最高温度。 以华氏度为单位的温度 | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第7天预测日历天温度最低摄氏度] | 七天的天气预报。 给定日期的午夜到午夜每日最低温度。 以摄氏度表示的温度 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第7天预测日历天温度最低华氏度] | 七天的天气预报。 给定日期的午夜到午夜每日最低温度。 以华氏度为单位的温度 | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第7天预测云覆盖英里] | 七天的天气预报。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL 第7天预测云覆盖公里] | 七天的天气预报。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL 第7天预测QPF英寸] | 七天的天气预报。 24小时内之预计可计量降水（液体或液体当量）。 降水量（英寸） | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL 第7天预测QPF毫米] | 七天的天气预报。 24小时内之预计可计量降水（液体或液体当量）。 降水（毫米） | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL 第7天预报QPF雪厘米] | 七天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第7天预测QPF雪英寸] | 七天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL 第7天预测UV指数] | 七天的天气预报。 12小时预测时段的最大UV索引。 | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL 第7天预报风向] | 七天的天气预报。 磁标记法中的平均风向。 | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL 第7天预报风速公里/小时] | 七天的天气预报。 12小时预报期最大持续风速预报。<br>风被视为矢量；因此，风必须有方向和大小（速度）。 预报中报告的大风信息对应着称为持续风速的10分钟平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第7天预测风速英里每小时] | 七天的天气预报。 12小时预报期最大持续风速预报。<br>风被视为矢量；因此，风必须有方向和大小（速度）。 预报中报告的大风信息对应着称为持续风速的10分钟平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第10天预测日历天最高温度] | 十天的天气预报。 给定日期的午夜到午夜每日最高温度。 以摄氏度表示的温度 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第10天预测日历天温度最高华氏度] | 十天的天气预报。 给定日期的午夜到午夜每日最高温度。 以华氏度为单位的温度 | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第10天预测日历天温度最低摄氏度] | 十天的天气预报。 给定日期的午夜到午夜每日最低温度。 以摄氏度表示的温度 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第10天预测日历天温度最低华氏度] | 十天的天气预报。 给定日期的午夜到午夜每日最低温度。 以华氏度为单位的温度 | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第10天预测云覆盖英里] | 十天的天气预报。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL 第10天预测云覆盖公里] | 十天的天气预报。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL 第10天预测QPF英寸] | 十天的天气预报。 24小时内之预计可计量降水（液体或液体当量）。 降水量（英寸） | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL 第10天预测QPF毫米] | 十天的天气预报。 24小时内之预计可计量降水（液体或液体当量）。 降水（毫米） | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL 第10天预测QPF雪厘米] | 十天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第10天预测QPF雪英寸] | 十天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL 第10天预测UV指数] | 十天的天气预报。 12小时预测时段的最大UV索引。 | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL 第10天预报风向] | 十天的天气预报。 磁标记法中的平均风向。 | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL 第10天预报风速公里/小时] | 十天的天气预报。 12小时预报期最大持续风速预报。<br>风被视为矢量；因此，风必须有方向和大小（速度）。 预报中报告的大风信息对应着称为持续风速的10分钟平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第10天预测风速英里/小时] | 十天的天气预报。 12小时预报期最大持续风速预报。<br>风被视为矢量；因此，风必须有方向和大小（速度）。 预报中报告的大风信息对应着称为持续风速的10分钟平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL 第14天预测日历天最高温度（摄氏）] | 十四天的天气预报。 给定日期的午夜到午夜每日最高温度。 以摄氏度表示的温度 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL 第14天预测日历天温度最高华氏度] | 十四天的天气预报。 给定日期的午夜到午夜每日最高温度。 以华氏度为单位的温度 | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL 第14天预测日历天温度最低摄氏度] | 十四天的天气预报。 给定日期的午夜到午夜每日最低温度。 以摄氏度表示的温度 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL 第14天预测日历天温度最低华氏度] | 十四天的天气预报。 给定日期的午夜到午夜每日最低温度。 以华氏度为单位的温度 | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL 第14天预测云覆盖英里] | 十四天的天气预报。 白天平均云覆盖，以百分比表示。 以英里为单位的距离。 | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL 第14天预测云覆盖公里] | 十四天的天气预报。 白天平均云覆盖，以百分比表示。 以公里为单位的距离。 | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 第14天预测QPF英寸 | 十四天的天气预报。 24小时内之预计可计量降水（液体或液体当量）。 降水量（英寸） | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL 第14天预测QPF毫米] | 十四天的天气预报。 24小时内之预计可计量降水（液体或液体当量）。 降水（毫米） | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL 第14天预报QPF雪厘米] | 十四天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪量（厘米） | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL 第14天预测QPF雪英寸] | 十四天的天气预报。 在12小时或24小时的预报期内，降水量作为积雪进行预报。 以厘米衡量。 降雪（以英寸为单位） | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL 第14天预测UV指数] | 十四天的天气预报。 12小时预测时段的最大UV索引。 | `weather.forecast.day14Forecast.uvIndex` |
| 第14天预报风向 | 十四天的天气预报。 磁标记法中的平均风向。 | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL 第14天预报风速公里/小时] | 十四天的天气预报。 12小时预报期最大持续风速预报。<br>风被视为矢量；因此，风必须有方向和大小（速度）。 预报中报告的大风信息对应着称为持续风速的10分钟平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速（以公里为单位/小时） | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL 第14天预测风速英里每小时] | 十四天的天气预报。 12小时预报期最大持续风速预报。<br>风被视为矢量；因此，风必须有方向和大小（速度）。 预报中报告的大风信息对应着称为持续风速的10分钟平均值。 风速的突然或短暂变化被称为“阵风”，并在单独的数据字段中报告。 风向始终表示为“从风吹向何处”，即北风从北吹向南。 如果你面对的是北风，那风就在你的脸上。 朝南，北风在背后。 风速以英里/小时为单位 | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 触发器 {#triggers}

触发器根据各种输入定义语义天气条件。

| 字段 | 描述 | XDM路径 |
| --- | ---- | --- |
| [!UICONTROL 产品触发因素] | 指示条件何时适用于推动某些类别产品的销售。  它们被映射到整型标识符。 可从IBM获取完整列表。 | `weather.productTriggers` |
| [!UICONTROL 相对触发因素] | 基于人类知觉的相对状况。 冷热之类的。 它们被映射到整型标识符。 可从IBM获取完整列表。 | `weather.relativeTriggers` |
| [!UICONTROL 恶劣天气触发程序] | 表示各种恶劣天气条件，如飓风或暴雨。 | `weather.severeTriggers` |
