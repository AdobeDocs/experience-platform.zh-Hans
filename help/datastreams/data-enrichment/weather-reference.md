---
title: 天气数据字段映射
description: 可用天气数据字段的参考页面，这些字段作为与 The Weather Channel 的集成的一部分提供。
exl-id: bc0f158b-f9d0-424a-aa21-953e8380473f
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '11147'
ht-degree: 99%

---

# 天气数据字段映射

Adobe 已与 [!DNL [The Weather Company]](https://www.ibm.com/weather) 合作，将美国天气的其他上下文引入通过数据流收集的数据中。您可以将此数据用于 Experience Platform 中的分析、定位和区段创建操作。

此页面列出了可用于扩充受众数据的所有可用字段。

这些字段分为与字段组一致的三个不同的组。

* [**[!UICONTROL Current Weather]**](#current-weather)：用户的当前天气情况（基于其位置）。 这包括当前温度、降水量、云量等。
* [**[!UICONTROL Forecasted Weather]**](#forecast)：预测包括用户位置的1、2、3、5、7和10天预测。
* [**[!UICONTROL Triggers]**](#triggers)：触发器是映射到不同语义天气条件的特定组合。 有三种不同类型的天气触发因素：

   * **[!UICONTROL Relative Triggers]**：语义上有意义的情况，例如冷天气。 在不同的气候条件下，它们的定义会有所不同。
   * **[!UICONTROL Product Triggers]**：导致购买不同类型产品的条件。 例如：寒冷天气预测可能意味着购买雨衣的可能性更大。
   * **[!UICONTROL Severe Weather Triggers]**：严重天气警告，如冬季风暴或飓风警告。

## 当前天气 {#current-weather}

用户的当前天气条件（基于其位置）。

| 字段 | 描述 | XDM 路径 |
| --- | ---- | --- |
| [!UICONTROL Temperature Dew Point Celsius] | 空气必须在恒定压力下冷却以达到饱和度的温度。露点也是对空气湿度的间接测量。露点绝不会超过温度。当露点和温度相等时，通常会形成云或雾。温度值和露点值越接近，相对湿度就越高。范围 - -80 至 100 (°F) 或 -62 至 37 (°C)。温度（摄氏度） | `weather.current.temperatureDewPoint.celsius` |
| [!UICONTROL Temperature Dew Point Fahrenheit] | 空气必须在恒定压力下冷却以达到饱和度的温度。露点也是对空气湿度的间接测量。露点绝不会超过温度。当露点和温度相等时，通常会形成云或雾。温度值和露点值越接近，相对湿度就越高。范围 - -80 至 100 (°F) 或 -62 至 37 (°C)。温度（华氏度） | `weather.current.temperatureDewPoint.fahrenheit` |
| [!UICONTROL Precipitation Last Hour Inches] | 滚动小时降水量。显示的数量是到请求时间（现在）的滚动时间。降水量（英寸） | `weather.current.precip1Hour.inches` |
| [!UICONTROL Precipitation Last Hour Millimeters] | 滚动小时降水量。显示的数量是到请求时间（现在）的滚动时间。降水量（毫米） | `weather.current.precip1Hour.millimeters` |
| [!DNL Precipitation Last 24 Hours Inches] | 滚动二十四小时降水量。显示的数量是到请求时间（现在）的滚动时间。降水量（英寸） | `weather.current.precip24Hour.inches` |
| [!UICONTROL Precipitation Last 24 Hours Millimeters] | 滚动二十四小时降水量。显示的数量是到请求时间（现在）的滚动时间。降水量（毫米） | `weather.current.precip24Hour.millimeters` |
| [!UICONTROL Precipitation Last 6 Hours Inches] | 滚动六小时降水量。显示的数量是到请求时间（现在）的滚动时间。降水量（英寸） | `weather.current.precip6Hour.inches` |
| [!UICONTROL Precipitation Last 6 Hours Millimeters] | 滚动六小时降水量。显示的数量是到请求时间（现在）的滚动时间。降水量（毫米） | `weather.current.precip6Hour.millimeters` |
| [!UICONTROL Pressure Change] | 过去三个小时的压力变化（毫巴）。 | `weather.current.pressureChange` |
| [!UICONTROL Pressure Mean Sea Level] | 平均海面压力（毫巴）。换句话说，海平面的平均气压。<br>范围 - 毫巴，精确到 1/10 mb。 | `weather.current.pressureMeanSeaLevel` |
| [!UICONTROL Relative Humidity] | 空气的相对湿度，定义为空气中的水蒸气量与在恒定温度下使空气达到饱和度所需的水蒸气量之比。相对湿度始终以百分比表示。<br>范围 - 0 到 100。 | `weather.current.relativeHumidity` |
| [!UICONTROL Snow Last Hour Centimeters] | 一小时降雪量。显示的数量是到请求时间（现在）的滚动时间。降雪量（厘米） | `weather.current.snow1Hour.centimeters` |
| [!UICONTROL Snow Last Hour Inches] | 一小时降雪量。显示的数量是到请求时间（现在）的滚动时间。降雪量（英寸） | `weather.current.snow1Hour.inches` |
| [!UICONTROL Snow 24 Hour Centimeters] | 二十四小时降雪量。显示的数量是到请求时间（现在）的滚动时间。降雪量（厘米） | `weather.current.snow24Hour.centimeters` |
| 24 小时降雪量（英寸） | 二十四小时降雪量。显示的数量是到请求时间（现在）的滚动时间。降雪量（英寸） | `weather.current.snow24Hour.inches` |
| [!UICONTROL Snow Last 6 Hours Centimeters] | 一小时降雪量。显示的数量是到请求时间（现在）的滚动时间。降雪量（厘米） | `weather.current.snow6Hour.centimeters` |
| [!UICONTROL Snow Last 6 Hours Inches] | 一小时降雪量。显示的数量是到请求时间（现在）的滚动时间。降雪量（英寸） | `weather.current.snow6Hour.inches` |
| [!UICONTROL Sunset Time] | 日落时间 (UTC)。 | `weather.current.sunsetTime` |
| [!UICONTROL Temperature Celsius] | 以定义的测量单位表示的温度。范围 -140 到 140。温度（摄氏度） | `weather.current.temperature.celsius` |
| [!UICONTROL Temperature Fahrenheit] | 以定义的测量单位表示的温度。范围 -140 到 140。温度（华氏度） | `weather.current.temperature.fahrenheit` |
| [!UICONTROL Temperature Change 24 hour Celsius] | 与 24 小时前报告的温度相比的温度变化。温度（摄氏度） | `weather.current.temperatureChange24Hour.celsius` |
| [!UICONTROL Temperature Change 24 hour Fahrenheit] | 与 24 小时前报告的温度相比的温度变化。温度（华氏度） | `weather.current.temperatureChange24Hour.fahrenheit` |
| [!UICONTROL Temperature Feels Like Celsius] | 体感温度。它标识由于风冷指数或热指数的综合影响，暴露的人体皮肤的“体感”气温。<br>当温度为 65°F 或更高时，体感温度值表示计算出的热指数。当温度低于 65°F 时，体感温度值表示计算出的风冷指数。<br>范围 -140 到 140。温度（摄氏度） | `weather.current.temperatureFeelsLike.celsius` |
| [!UICONTROL Temperature Feels Like Fahrenheit] | 体感温度。它标识由于风冷指数或热指数的综合影响，暴露的人体皮肤的“体感”气温。<br>当温度为 65°F 或更高时，体感温度值表示计算出的热指数。当温度低于 65°F 时，体感温度值表示计算出的风冷指数。<br>范围 -140 到 140。温度（华氏度） | `weather.current.temperatureFeelsLike.fahrenheit` |
| [!UICONTROL Temperature Max Since 7 AM Celsius] | 当地时间上午 7 点以后的最高温度。温度（摄氏度） | `weather.current.temperatureMaxSince7Am.celsius` |
| [!UICONTROL Temperature Max Since 7 AM Fahrenheit] | 当地时间上午 7 点以后的最高温度。温度（华氏度） | `weather.current.temperatureMaxSince7Am.fahrenheit` |
| [!UICONTROL Temperature Min Last 24 Hours Celsius] | 过去 24 小时的最低温度。24 小时期间相对于请求时间（现在）。温度（摄氏度） | `weather.current.temperatureMin24Hour.celsius` |
| [!UICONTROL Temperature Min Last 24 Hours Fahrenheit] | 过去 24 小时的最低温度。24 小时期间相对于请求时间（现在）。温度（华氏度） | `weather.current.temperatureMin24Hour.fahrenheit` |
| [!UICONTROL Wind Direction] | 风吹来的磁极风向（以度表示）。磁极方向在 0 度到 359 度之间变化，其中 0° 表示北，90° 表示东，180° 表示南，270° 表示西，依此类推。<br>范围 - 0&lt;=wind_dire_deg&lt;=350，以 10 度为间隔。 | `weather.current.windDirection` |
| [!UICONTROL Wind Gust Kilometers per Hour] | 此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（公里/小时） | `weather.current.windGust.kilometersPerHour` |
| [!UICONTROL Wind Gust Miles per Hour] | 此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（英里/小时） | `weather.current.windGust.`milesPerHour |
| [!UICONTROL Wind Speed Kilometers per Hour] | 风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.current.windSpeed.kilometersPerHour` |
| [!UICONTROL Wind Speed Miles per Hour] | 风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.current.windSpeed.milesPerHour` |

## 预测的天气 {#forecast}

根据位置，为用户预测的特定时间点的天气。

| 字段 | 描述 | XDM 路径 |
| --- | ---- | --- |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Celsius] | 一天的天气预测。给定天的午夜至午夜每日最高温度。温度（摄氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMax.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Max Fahrenheit] | 一天的天气预测。给定天的午夜至午夜每日最高温度。温度（华氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Celsius] | 一天的天气预测。给定天的午夜至午夜日最低温度。温度（摄氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMin.celsius` |
| [!DNL Day 1 Forecast Calendar Day Temperature Min Fahrenheit] | 一天的天气预测。给定天的午夜至午夜日最低温度。温度（华氏度） | `weather.forecast.day01Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!DNL Day 1 Forecast Day Cloud Cover Miles] | 一天的天气预测。白间的天气信息。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day01Forecast.day.cloudCover.inches` |
| [!DNL Day 1 Forecast Day Cloud Cover Kilometers] | 一天的天气预测。白间的天气信息。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day01Forecast.day.cloudCover.kilometers` |
| [!DNL Day 1 Forecast Day Precipitation Chance] | 一天的天气预测。白间的天气信息。降水概率（百分比）。 | `weather.forecast.day01Forecast.day.precipChance` |
| [!DNL Day 1 Forecast Day Precipitation Type] | 一天的天气预测。白间的天气信息。降水形式（雨、雪、雨夹雪等）。 | `weather.forecast.day01Forecast.day.precipType` |
| [!DNL Day 1 Forecast Day QPF Inches] | 一天的天气预测。白间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day01Forecast.day.qpf.inches` |
| [!DNL Day 1 Forecast Day QPF Millimeters] | 一天的天气预测。白间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day01Forecast.day.qpf.millimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Centimeters] | 一天的天气预测。白间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day01Forecast.day.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Day QPF Snow Inches] | 一天的天气预测。白间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day01Forecast.day.qpfSnow.inches` |
| [!DNL Day 1 Forecast Day Relative Humidity] | 一天的天气预测。白间的天气信息。空气的相对湿度，定义为空气中的水蒸气量与在恒定温度下使空气达到饱和度所需的水蒸气量之比。相对湿度始终以百分比表示。<br>范围 - 0 到 100。 | `weather.forecast.day01Forecast.day.relativeHumidity` |
| [!DNL Day 1 Forecast Day Snow Range] | 一天的天气预测。白间的天气信息。可能的降雪量（1-3&quot;、3-6&quot; 等）。 | `weather.forecast.day01Forecast.day.snowRange` |
| [!DNL Day 1 Forecast Day Temperature Celsius] | 一天的天气预测。白间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（摄氏度） | `weather.forecast.day01Forecast.day.temperature.celsius` |
| [!DNL Day 1 Forecast Day Temperature Fahrenheit] | 一天的天气预测。白间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（华氏度） | `weather.forecast.day01Forecast.day.temperature.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Celsius] | 一天的天气预测。白间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day01Forecast.day.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Day Temperature Heat Index Fahrenheit] | 一天的天气预测。白间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day01Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Celsius] | 一天的天气预测。白间的天气信息。根据温度和风速，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day01Forecast.day.temperatureWindChill.celsius` |
| [!DNL Day 1 Forecast Day Temperature Wind Chill Fahrenheit] | 一天的天气预测。白间的天气信息。根据温度和风速，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day01Forecast.day.temperatureWindChill.fahrenheit` |
| [!DNL Day 1 Forecast Day Thunder Index] | 一天的天气预测。白间的天气信息。雷暴影响某个地区的概率指数。0（无雷）到 5（严重雷暴的高风险）。 | `weather.forecast.day01Forecast.day.thunderIndex` |
| [!DNL Day 1 Forecast Day UV Index] | 一天的天气预测。白间的天气信息。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day01Forecast.day.uvIndex` |
| [!DNL Day 1 Forecast Day Wind Direction] | 一天的天气预测。白间的天气信息。风吹来的磁极风向（以度表示）。磁极方向在 0 度到 359 度之间变化，其中 0° 表示北，90° 表示东，180° 表示南，270° 表示西，依此类推。<br>范围 - 0&lt;=wind_dire_deg&lt;=350，以 10 度为间隔。 | `weather.forecast.day01Forecast.day.windDirection` |
| [!DNL Day 1 Forecast Day Wind Gust Kilometers per Hour] | 一天的天气预测。白间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（公里/小时） | `weather.forecast.day01Forecast.day.windGust.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Gust Miles per Hour] | 一天的天气预测。白间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（英里/小时） | `weather.forecast.day01Forecast.day.windGust.milesPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Kilometers per Hour] | 一天的天气预测。白间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day01Forecast.day.windSpeed.kilometersPerHour` |
| [!DNL Day 1 Forecast Day Wind Speed Miles per Hour] | 一天的天气预测。白间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day01Forecast.day.windSpeed.milesPerHour` |
| [!DNL Day 1 Forecast Night Cloud Cover Miles] | 一天的天气预测。夜间的天气信息。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day01Forecast.night.cloudCover.inches` |
| [!DNL Day 1 Forecast Night Cloud Cover Kilometers] | 一天的天气预测。夜间的天气信息。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day01Forecast.night.cloudCover.kilometers` |
| [!UICONTROL Day 1 Forecast Night Precipitation Chance] | 一天的天气预测。夜间的天气信息。降水概率（百分比）。 | `weather.forecast.day01Forecast.night.precipChance` |
| [!DNL Day 1 Forecast Night Precipitation Type] | 一天的天气预测。夜间的天气信息。降水形式（雨、雪、雨夹雪等）。 | `weather.forecast.day01Forecast.night.precipType` |
| [!DNL Day 1 Forecast Night QPF Inches] | 一天的天气预测。夜间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day01Forecast.night.qpf.inches` |
| [!DNL Day 1 Forecast Night QPF Millimeters] | 一天的天气预测。夜间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day01Forecast.night.qpf.millimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Centimeters] | 一天的天气预测。夜间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day01Forecast.night.qpfSnow.centimeters` |
| [!DNL Day 1 Forecast Night QPF Snow Inches] | 一天的天气预测。夜间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day01Forecast.night.qpfSnow.inches` |
| [!DNL Day 1 Forecast Night Relative Humidity] | 一天的天气预测。夜间的天气信息。空气的相对湿度，定义为空气中的水蒸气量与在恒定温度下使空气达到饱和度所需的水蒸气量之比。相对湿度始终以百分比表示。<br>范围 - 0 到 100。 | `weather.forecast.day01Forecast.night.relativeHumidity` |
| [!DNL Day 1 Forecast Night Snow Range] | 一天的天气预测。夜间的天气信息。可能的降雪量（1-3&quot;、3-6&quot; 等）。 | `weather.forecast.day01Forecast.night.snowRange` |
| [!DNL Day 1 Forecast Night Temperature Celsius] | 一天的天气预测。夜间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（摄氏度） | `weather.forecast.day01Forecast.night.temperature.celsius` |
| [!DNL Day 1 Forecast Night Temperature Fahrenheit] | 一天的天气预测。夜间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（华氏度） | `weather.forecast.day01Forecast.night.temperature.fahrenheit` |
| [!DNL  Day 1 Forecast Night Temperature Heat Index Celsius] | 一天的天气预测。夜间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day01Forecast.night.temperatureHeatIndex.celsius` |
| [!DNL Day 1 Forecast Night Temperature Heat Index Fahrenheit] | 一天的天气预测。夜间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day01Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!DNL Day 1 Forecast Night Temperature Wind Chill Celsius] | 一天的天气预测。夜间的天气信息。根据温度和风速，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day01Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL Day 1 Forecast Night Temperature Wind Chill Fahrenheit] | 一天的天气预测。夜间的天气信息。根据温度和风速，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day01Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 1 Forecast Night Thunder Index] | 一天的天气预测。夜间的天气信息。雷暴影响某个地区的概率指数。0（无雷）到 5（严重雷暴的高风险）。 | `weather.forecast.day01Forecast.night.thunderIndex` |
| [!UICONTROL Day 1 Forecast Night UV Index] | 一天的天气预测。夜间的天气信息。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day01Forecast.night.uvIndex` |
| [!UICONTROL Day 1 Forecast Night Wind Direction] | 一天的天气预测。夜间的天气信息。风吹来的磁极风向（以度表示）。磁极方向在 0 度到 359 度之间变化，其中 0° 表示北，90° 表示东，180° 表示南，270° 表示西，依此类推。<br>范围 - 0&lt;=wind_dire_deg&lt;=350，以 10 度为间隔。 | `weather.forecast.day01Forecast.night.windDirection` |
| [!UICONTROL Day 1 Forecast Night Wind Gust Kilometers per Hour] | 一天的天气预测。夜间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（公里/小时） | `weather.forecast.day01Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL Day 1 Forecast Night Wind Gust Miles per Hour] | 一天的天气预测。夜间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（英里/小时） | `weather.forecast.day01Forecast.night.windGust.milesPerHour` |
| [!UICONTROL Day 1 Forecast Night Wind Speed Kilometers per Hour] | 一天的天气预测。夜间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day01Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 1 Forecast Night Wind Speed Miles per Hour] | 一天的天气预测。夜间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day01Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL Day 1 Forecast QPF Inches] | 一天的天气预测。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day01Forecast.qpf.inches` |
| [!UICONTROL Day 1 Forecast QPF Millimeters] | 一天的天气预测。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day01Forecast.qpf.millimeters` |
| [!UICONTROL Day 1 Forecast QPF Snow Centimeters] | 一天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day01Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 1 Forecast QPF Snow Inches] | 一天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day01Forecast.qpfSnow.inches` |
| [!UICONTROL Day 2 Forecast Calendar Day Temperature Max Celsius] | 两天的天气预测。给定天的午夜至午夜每日最高温度。温度（摄氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 2 Forecast Calendar Day Temperature Max Fahrenheit] | 两天的天气预测。给定天的午夜至午夜每日最高温度。温度（华氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 2 Forecast Calendar Day Temperature Min Celsius] | 两天的天气预测。给定天的午夜至午夜日最低温度。温度（摄氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 2 Forecast Calendar Day Temperature Min Fahrenheit] | 两天的天气预测。给定天的午夜至午夜日最低温度。温度（华氏度） | `weather.forecast.day02Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 2 Forecast Day Cloud Cover Miles] | 两天的天气预测。白间的天气信息。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day02Forecast.day.cloudCover.inches` |
| [!UICONTROL Day 2 Forecast Day Cloud Cover Kilometers] | 两天的天气预测。白间的天气信息。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day02Forecast.day.cloudCover.kilometers` |
| [!UICONTROL Day 2 Forecast Day Precipitation Chance] | 两天的天气预测。白间的天气信息。降水概率（百分比）。 | `weather.forecast.day02Forecast.day.precipChance` |
| [!UICONTROL Day 2 Forecast Day Precipitation Type] | 两天的天气预测。白间的天气信息。降水形式（雨、雪、雨夹雪等）。 | `weather.forecast.day02Forecast.day.precipType` |
| [!UICONTROL Day 2 Forecast Day QPF Inches] | 两天的天气预测。白间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day02Forecast.day.qpf.inches` |
| [!UICONTROL Day 2 Forecast Day QPF Millimeters] | 两天的天气预测。白间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day02Forecast.day.qpf.millimeters` |
| [!UICONTROL Day 2 Forecast Day QPF Snow Centimeters] | 两天的天气预测。白间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day02Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL Day 2 Forecast Day QPF Snow Inches] | 两天的天气预测。白间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day02Forecast.day.qpfSnow.inches` |
| [!UICONTROL Day 2 Forecast Day Relative Humidity] | 两天的天气预测。白间的天气信息。空气的相对湿度，定义为空气中的水蒸气量与在恒定温度下使空气达到饱和度所需的水蒸气量之比。相对湿度始终以百分比表示。<br>范围 - 0 到 100。 | `weather.forecast.day02Forecast.day.relativeHumidity` |
| [!UICONTROL Day 2 Forecast Day Snow Range] | 两天的天气预测。白间的天气信息。可能的降雪量（1-3&quot;、3-6&quot; 等）。 | `weather.forecast.day02Forecast.day.snowRange` |
| [!UICONTROL Day 2 Forecast Day Temperature Celsius] | 两天的天气预测。白间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（摄氏度） | `weather.forecast.day02Forecast.day.temperature.celsius` |
| [!UICONTROL Day 2 Forecast Day Temperature Fahrenheit] | 两天的天气预测。白间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（华氏度） | `weather.forecast.day02Forecast.day.temperature.fahrenheit` |
| [!UICONTROL Day 2 Forecast Day Temperature Heat Index Celsius] | 两天的天气预测。白间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day02Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 2 Forecast Day Temperature Heat Index Fahrenheit] | 两天的天气预测。白间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day02Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 2 Forecast Day Temperature Wind Chill Celsius] | 两天的天气预测。白间的天气信息。根据温度和风速，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day02Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL Day 2 Forecast Day Temperature Wind Chill Fahrenheit] | 两天的天气预测。白间的天气信息。根据温度和风速，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day02Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 2 Forecast Day Thunder Index] | 两天的天气预测。白间的天气信息。雷暴影响某个地区的概率指数。0（无雷）到 5（严重雷暴的高风险）。 | `weather.forecast.day02Forecast.day.thunderIndex` |
| [!UICONTROL Day 2 Forecast Day UV Index] | 两天的天气预测。白间的天气信息。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day02Forecast.day.uvIndex` |
| [!UICONTROL Day 2 Forecast Day Wind Direction] | 两天的天气预测。白间的天气信息。风吹来的磁极风向（以度表示）。磁极方向在 0 度到 359 度之间变化，其中 0° 表示北，90° 表示东，180° 表示南，270° 表示西，依此类推。<br>范围 - 0&lt;=wind_dire_deg&lt;=350，以 10 度为间隔。 | `weather.forecast.day02Forecast.day.windDirection` |
| [!UICONTROL Day 2 Forecast Day Wind Gust Kilometers per Hour] | 两天的天气预测。白间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（公里/小时） | `weather.forecast.day02Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL Day 2 Forecast Day Wind Gust Miles per Hour] | 两天的天气预测。白间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（英里/小时） | `weather.forecast.day02Forecast.day.windGust.milesPerHour` |
| [!UICONTROL Day 2 Forecast Day Wind Speed Kilometers per Hour] | 两天的天气预测。白间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day02Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 2 Forecast Day Wind Speed Miles per Hour] | 两天的天气预测。白间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day02Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL Day 2 Forecast Night Cloud Cover Miles] | 两天的天气预测。夜间的天气信息。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day02Forecast.night.cloudCover.inches` |
| [!UICONTROL Day 2 Forecast Night Cloud Cover Kilometers] | 两天的天气预测。夜间的天气信息。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day02Forecast.night.cloudCover.kilometers` |
| [!UICONTROL Day 2 Forecast Night Precipitation Chance] | 两天的天气预测。夜间的天气信息。降水概率（百分比）。 | `weather.forecast.day02Forecast.night.precipChance` |
| [!UICONTROL Day 2 Forecast Night Precipitation Type] | 两天的天气预测。夜间的天气信息。降水形式（雨、雪、雨夹雪等）。 | `weather.forecast.day02Forecast.night.precipType` |
| [!UICONTROL Day 2 Forecast Night QPF Inches] | 两天的天气预测。夜间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day02Forecast.night.qpf.inches` |
| [!UICONTROL Day 2 Forecast Night QPF Millimeters] | 两天的天气预测。夜间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day02Forecast.night.qpf.millimeters` |
| [!UICONTROL Day 2 Forecast Night QPF Snow Centimeters] | 两天的天气预测。夜间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day02Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL Day 2 Forecast Night QPF Snow Inches] | 两天的天气预测。夜间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day02Forecast.night.qpfSnow.inches` |
| [!UICONTROL Day 2 Forecast Night Relative Humidity] | 两天的天气预测。夜间的天气信息。空气的相对湿度，定义为空气中的水蒸气量与在恒定温度下使空气达到饱和度所需的水蒸气量之比。相对湿度始终以百分比表示。<br>范围 - 0 到 100。 | `weather.forecast.day02Forecast.night.relativeHumidity` |
| [!UICONTROL Day 2 Forecast Night Snow Range] | 两天的天气预测。夜间的天气信息。可能的降雪量（1-3&quot;、3-6&quot; 等）。 | `weather.forecast.day02Forecast.night.snowRange` |
| [!UICONTROL Day 2 Forecast Night Temperature Celsius] | 两天的天气预测。夜间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（摄氏度） | `weather.forecast.day02Forecast.night.temperature.celsius` |
| [!UICONTROL Day 2 Forecast Night Temperature Fahrenheit] | 两天的天气预测。夜间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（华氏度） | `weather.forecast.day02Forecast.night.temperature.fahrenheit` |
| [!UICONTROL Day 2 Forecast Night Temperature Heat Index Celsius] | 两天的天气预测。夜间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day02Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 2 Forecast Night Temperature Heat Index Fahrenheit] | 两天的天气预测。夜间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day02Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 2 Forecast Night Temperature Wind Chill Celsius] | 两天的天气预测。夜间的天气信息。根据温度和风速，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day02Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL Day 2 Forecast Night Temperature Wind Chill Fahrenheit] | 两天的天气预测。夜间的天气信息。根据温度和风速，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day02Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 2 Forecast Night Thunder Index] | 两天的天气预测。夜间的天气信息。雷暴影响某个地区的概率指数。0（无雷）到 5（严重雷暴的高风险）。 | `weather.forecast.day02Forecast.night.thunderIndex` |
| [!UICONTROL Day 2 Forecast Night UV Index] | 两天的天气预测。夜间的天气信息。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day02Forecast.night.uvIndex` |
| [!UICONTROL Day 2 Forecast Night Wind Direction] | 两天的天气预测。夜间的天气信息。风吹来的磁极风向（以度表示）。磁极方向在 0 度到 359 度之间变化，其中 0° 表示北，90° 表示东，180° 表示南，270° 表示西，依此类推。<br>范围 - 0&lt;=wind_dire_deg&lt;=350，以 10 度为间隔。 | `weather.forecast.day02Forecast.night.windDirection` |
| [!UICONTROL Day 2 Forecast Night Wind Gust Kilometers per Hour] | 两天的天气预测。夜间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（公里/小时） | `weather.forecast.day02Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL Day 2 Forecast Night Wind Gust Miles per Hour] | 两天的天气预测。夜间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（英里/小时） | `weather.forecast.day02Forecast.night.windGust.milesPerHour` |
| [!UICONTROL Day 2 Forecast Night Wind Speed Kilometers per Hour] | 两天的天气预测。夜间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day02Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 2 Forecast Night Wind Speed Miles per Hour] | 两天的天气预测。夜间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day02Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL Day 2 Forecast QPF Inches] | 两天的天气预测。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day02Forecast.qpf.inches` |
| [!UICONTROL Day 2 Forecast QPF Millimeters] | 两天的天气预测。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day02Forecast.qpf.millimeters` |
| [!UICONTROL Day 2 Forecast QPF Snow Centimeters] | 两天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day02Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 2 Forecast QPF Snow Inches] | 两天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day02Forecast.qpfSnow.inches` |
| [!UICONTROL Day 3 Forecast Calendar Day Temperature Max Celsius] | 三天的天气预测。给定天的午夜至午夜每日最高温度。温度（摄氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 3 Forecast Calendar Day Temperature Max Fahrenheit] | 三天的天气预测。给定天的午夜至午夜每日最高温度。温度（华氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 3 Forecast Calendar Day Temperature Min Celsius] | 三天的天气预测。给定天的午夜至午夜日最低温度。温度（摄氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 3 Forecast Calendar Day Temperature Min Fahrenheit] | 三天的天气预测。给定天的午夜至午夜日最低温度。温度（华氏度） | `weather.forecast.day03Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 3 Forecast Day Cloud Cover Miles] | 三天的天气预测。白间的天气信息。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day03Forecast.day.cloudCover.inches` |
| [!UICONTROL Day 3 Forecast Day Cloud Cover Kilometers] | 三天的天气预测。白间的天气信息。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day03Forecast.day.cloudCover.kilometers` |
| [!UICONTROL Day 3 Forecast Day Precipitation Chance] | 三天的天气预测。白间的天气信息。降水概率（百分比）。 | `weather.forecast.day03Forecast.day.precipChance` |
| [!UICONTROL Day 3 Forecast Day Precipitation Type] | 三天的天气预测。白间的天气信息。降水形式（雨、雪、雨夹雪等）。 | `weather.forecast.day03Forecast.day.precipType` |
| [!UICONTROL Day 3 Forecast Day QPF Inches] | 三天的天气预测。白间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day03Forecast.day.qpf.inches` |
| [!UICONTROL Day 3 Forecast Day QPF Millimeters] | 三天的天气预测。白间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day03Forecast.day.qpf.millimeters` |
| [!UICONTROL Day 3 Forecast Day QPF Snow Centimeters] | 三天的天气预测。白间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day03Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL Day 3 Forecast Day QPF Snow Inches] | 三天的天气预测。白间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day03Forecast.day.qpfSnow.inches` |
| [!UICONTROL Day 3 Forecast Day Relative Humidity] | 三天的天气预测。白间的天气信息。空气的相对湿度，定义为空气中的水蒸气量与在恒定温度下使空气达到饱和度所需的水蒸气量之比。相对湿度始终以百分比表示。<br>范围 - 0 到 100。 | `weather.forecast.day03Forecast.day.relativeHumidity` |
| [!UICONTROL Day 3 Forecast Day Snow Range] | 三天的天气预测。白间的天气信息。可能的降雪量（1-3&quot;、3-6&quot; 等）。 | `weather.forecast.day03Forecast.day.snowRange` |
| [!UICONTROL Day 3 Forecast Day Temperature Celsius] | 三天的天气预测。白间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（摄氏度） | `weather.forecast.day03Forecast.day.temperature.celsius` |
| [!UICONTROL Day 3 Forecast Day Temperature Fahrenheit] | 三天的天气预测。白间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（华氏度） | `weather.forecast.day03Forecast.day.temperature.fahrenheit` |
| [!UICONTROL Day 3 Forecast Day Temperature Heat Index Celsius] | 三天的天气预测。白间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day03Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 3 Forecast Day Temperature Heat Index Fahrenheit] | 三天的天气预测。白间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day03Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 3 Forecast Day Temperature Wind Chill Celsius] | 三天的天气预测。白间的天气信息。根据温度和风速，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day03Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL Day 3 Forecast Day Temperature Wind Chill Fahrenheit] | 三天的天气预测。白间的天气信息。根据温度和风速，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day03Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 3 Forecast Day Thunder Index] | 三天的天气预测。白间的天气信息。雷暴影响某个地区的概率指数。0（无雷）到 5（严重雷暴的高风险）。 | `weather.forecast.day03Forecast.day.thunderIndex` |
| [!UICONTROL Day 3 Forecast Day UV Index] | 三天的天气预测。白间的天气信息。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day03Forecast.day.uvIndex` |
| [!UICONTROL Day 3 Forecast Day Wind Direction] | 三天的天气预测。白间的天气信息。风吹来的磁极风向（以度表示）。磁极方向在 0 度到 359 度之间变化，其中 0° 表示北，90° 表示东，180° 表示南，270° 表示西，依此类推。<br>范围 - 0&lt;=wind_dire_deg&lt;=350，以 10 度为间隔。 | `weather.forecast.day03Forecast.day.windDirection` |
| [!UICONTROL Day 3 Forecast Day Wind Gust Kilometers per Hour] | 三天的天气预测。白间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（公里/小时） | `weather.forecast.day03Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL Day 3 Forecast Day Wind Gust Miles per Hour] | 三天的天气预测。白间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（英里/小时） | `weather.forecast.day03Forecast.day.windGust.milesPerHour` |
| [!UICONTROL Day 3 Forecast Day Wind Speed Kilometers per Hour] | 三天的天气预测。白间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day03Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 3 Forecast Day Wind Speed Miles per Hour] | 三天的天气预测。白间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day03Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL Day 3 Forecast Night Cloud Cover Miles] | 三天的天气预测。夜间的天气信息。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day03Forecast.night.cloudCover.inches` |
| [!UICONTROL Day 3 Forecast Night Cloud Cover Kilometers] | 三天的天气预测。夜间的天气信息。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day03Forecast.night.cloudCover.kilometers` |
| [!UICONTROL Day 3 Forecast Night Precipitation Chance] | 三天的天气预测。夜间的天气信息。降水概率（百分比）。 | `weather.forecast.day03Forecast.night.precipChance` |
| [!UICONTROL Day 3 Forecast Night Precipitation Type] | 三天的天气预测。夜间的天气信息。降水形式（雨、雪、雨夹雪等）。 | `weather.forecast.day03Forecast.night.precipType` |
| [!UICONTROL Day 3 Forecast Night QPF Inches] | 三天的天气预测。夜间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day03Forecast.night.qpf.inches` |
| [!UICONTROL Day 3 Forecast Night QPF Millimeters] | 三天的天气预测。夜间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day03Forecast.night.qpf.millimeters` |
| [!UICONTROL Day 3 Forecast Night QPF Snow Centimeters] | 三天的天气预测。夜间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day03Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL Day 3 Forecast Night QPF Snow Inches] | 三天的天气预测。夜间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day03Forecast.night.qpfSnow.inches` |
| [!UICONTROL Day 3 Forecast Night Relative Humidity] | 三天的天气预测。夜间的天气信息。空气的相对湿度，定义为空气中的水蒸气量与在恒定温度下使空气达到饱和度所需的水蒸气量之比。相对湿度始终以百分比表示。<br>范围 - 0 到 100。 | `weather.forecast.day03Forecast.night.relativeHumidity` |
| [!UICONTROL Day 3 Forecast Night Snow Range] | 三天的天气预测。夜间的天气信息。可能的降雪量（1-3&quot;、3-6&quot; 等）。 | `weather.forecast.day03Forecast.night.snowRange` |
| [!UICONTROL Day 3 Forecast Night Temperature Celsius] | 三天的天气预测。夜间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（摄氏度） | `weather.forecast.day03Forecast.night.temperature.celsius` |
| [!UICONTROL Day 3 Forecast Night Temperature Fahrenheit] | 三天的天气预测。夜间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（华氏度） | `weather.forecast.day03Forecast.night.temperature.fahrenheit` |
| [!UICONTROL Day 3 Forecast Night Temperature Heat Index Celsius] | 三天的天气预测。夜间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day03Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 3 Forecast Night Temperature Heat Index Fahrenheit] | 三天的天气预测。夜间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day03Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 3 Forecast Night Temperature Wind Chill Celsius] | 三天的天气预测。夜间的天气信息。根据温度和风速，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day03Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL Day 3 Forecast Night Temperature Wind Chill Fahrenheit] | 三天的天气预测。夜间的天气信息。根据温度和风速，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day03Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 3 Forecast Night Thunder Index] | 三天的天气预测。夜间的天气信息。雷暴影响某个地区的概率指数。0（无雷）到 5（严重雷暴的高风险）。 | `weather.forecast.day03Forecast.night.thunderIndex` |
| [!UICONTROL Day 3 Forecast Night UV Index] | 三天的天气预测。夜间的天气信息。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day03Forecast.night.uvIndex` |
| [!UICONTROL Day 3 Forecast Night Wind Direction] | 三天的天气预测。夜间的天气信息。风吹来的磁极风向（以度表示）。磁极方向在 0 度到 359 度之间变化，其中 0° 表示北，90° 表示东，180° 表示南，270° 表示西，依此类推。<br>范围 - 0&lt;=wind_dire_deg&lt;=350，以 10 度为间隔。 | `weather.forecast.day03Forecast.night.windDirection` |
| [!UICONTROL Day 3 Forecast Night Wind Gust Kilometers per Hour] | 三天的天气预测。夜间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（公里/小时） | `weather.forecast.day03Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL Day 3 Forecast Night Wind Gust Miles per Hour] | 三天的天气预测。夜间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（英里/小时） | `weather.forecast.day03Forecast.night.windGust.milesPerHour` |
| [!UICONTROL Day 3 Forecast Night Wind Speed Kilometers per Hour] | 三天的天气预测。夜间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day03Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 3 Forecast Night Wind Speed Miles per Hour] | 三天的天气预测。夜间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day03Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL Day 3 Forecast QPF Inches] | 三天的天气预测。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day03Forecast.qpf.inches` |
| [!UICONTROL Day 3 Forecast QPF Millimeters] | 三天的天气预测。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day03Forecast.qpf.millimeters` |
| [!UICONTROL Day 3 Forecast QPF Snow Centimeters] | 三天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day03Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 3 Forecast QPF Snow Inches] | 三天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day03Forecast.qpfSnow.inches` |
| [!UICONTROL Day 5 Forecast Calendar Day Temperature Max Celsius] | 五天的天气预测。给定天的午夜至午夜每日最高温度。温度（摄氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 5 Forecast Calendar Day Temperature Max Fahrenheit] | 五天的天气预测。给定天的午夜至午夜每日最高温度。温度（华氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 5 Forecast Calendar Day Temperature Min Celsius] | 五天的天气预测。给定天的午夜至午夜日最低温度。温度（摄氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 5 Forecast Calendar Day Temperature Min Fahrenheit] | 五天的天气预测。给定天的午夜至午夜日最低温度。温度（华氏度） | `weather.forecast.day05Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 5 Forecast Day Cloud Cover Miles] | 五天的天气预测。白间的天气信息。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day05Forecast.day.cloudCover.inches` |
| [!UICONTROL Day 5 Forecast Day Cloud Cover Kilometers] | 五天的天气预测。白间的天气信息。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day05Forecast.day.cloudCover.kilometers` |
| [!UICONTROL Day 5 Forecast Day Precipitation Chance] | 五天的天气预测。白间的天气信息。降水概率（百分比）。 | `weather.forecast.day05Forecast.day.precipChance` |
| [!UICONTROL Day 5 Forecast Day Precipitation Type] | 五天的天气预测。白间的天气信息。降水形式（雨、雪、雨夹雪等）。 | `weather.forecast.day05Forecast.day.precipType` |
| [!UICONTROL Day 5 Forecast Day QPF Inches] | 五天的天气预测。白间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day05Forecast.day.qpf.inches` |
| [!UICONTROL Day 5 Forecast Day QPF Millimeters] | 五天的天气预测。白间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day05Forecast.day.qpf.millimeters` |
| [!UICONTROL Day 5 Forecast Day QPF Snow Centimeters] | 五天的天气预测。白间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day05Forecast.day.qpfSnow.centimeters` |
| [!UICONTROL Day 5 Forecast Day QPF Snow Inches] | 五天的天气预测。白间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day05Forecast.day.qpfSnow.inches` |
| [!UICONTROL Day 5 Forecast Day Relative Humidity] | 五天的天气预测。白间的天气信息。空气的相对湿度，定义为空气中的水蒸气量与在恒定温度下使空气达到饱和度所需的水蒸气量之比。相对湿度始终以百分比表示。<br>范围 - 0 到 100。 | `weather.forecast.day05Forecast.day.relativeHumidity` |
| [!UICONTROL Day 5 Forecast Day Snow Range] | 五天的天气预测。白间的天气信息。可能的降雪量（1-3&quot;、3-6&quot; 等）。 | `weather.forecast.day05Forecast.day.snowRange` |
| [!UICONTROL Day 5 Forecast Day Temperature Celsius] | 五天的天气预测。白间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（摄氏度） | `weather.forecast.day05Forecast.day.temperature.celsius` |
| [!UICONTROL Day 5 Forecast Day Temperature Fahrenheit] | 五天的天气预测。白间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（华氏度） | `weather.forecast.day05Forecast.day.temperature.fahrenheit` |
| [!UICONTROL Day 5 Forecast Day Temperature Heat Index Celsius] | 五天的天气预测。白间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day05Forecast.day.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 5 Forecast Day Temperature Heat Index Fahrenheit] | 五天的天气预测。白间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day05Forecast.day.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 5 Forecast Day Temperature Wind Chill Celsius] | 五天的天气预测。白间的天气信息。根据温度和风速，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day05Forecast.day.temperatureWindChill.celsius` |
| [!UICONTROL Day 5 Forecast Day Temperature Wind Chill Fahrenheit] | 五天的天气预测。白间的天气信息。根据温度和风速，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day05Forecast.day.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 5 Forecast Day Thunder Index] | 五天的天气预测。白间的天气信息。雷暴影响某个地区的概率指数。0（无雷）到 5（严重雷暴的高风险）。 | `weather.forecast.day05Forecast.day.thunderIndex` |
| [!UICONTROL Day 5 Forecast Day UV Index] | 五天的天气预测。白间的天气信息。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day05Forecast.day.uvIndex` |
| [!UICONTROL Day 5 Forecast Day Wind Direction] | 五天的天气预测。白间的天气信息。风吹来的磁极风向（以度表示）。磁极方向在 0 度到 359 度之间变化，其中 0° 表示北，90° 表示东，180° 表示南，270° 表示西，依此类推。<br>范围 - 0&lt;=wind_dire_deg&lt;=350，以 10 度为间隔。 | `weather.forecast.day05Forecast.day.windDirection` |
| [!UICONTROL Day 5 Forecast Day Wind Gust Kilometers per Hour] | 五天的天气预测。白间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（公里/小时） | `weather.forecast.day05Forecast.day.windGust.kilometersPerHour` |
| [!UICONTROL Day 5 Forecast Day Wind Gust Miles per Hour] | 五天的天气预测。白间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（英里/小时） | `weather.forecast.day05Forecast.day.windGust.milesPerHour` |
| [!UICONTROL Day 5 Forecast Day Wind Speed Kilometers per Hour] | 五天的天气预测。白间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day05Forecast.day.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 5 Forecast Day Wind Speed Miles per Hour] | 五天的天气预测。白间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day05Forecast.day.windSpeed.milesPerHour` |
| [!UICONTROL Day 5 Forecast Night Cloud Cover Miles] | 五天的天气预测。夜间的天气信息。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day05Forecast.night.cloudCover.inches` |
| [!UICONTROL Day 5 Forecast Night Cloud Cover Kilometers] | 五天的天气预测。夜间的天气信息。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day05Forecast.night.cloudCover.kilometers` |
| [!UICONTROL Day 5 Forecast Night Precipitation Chance] | 五天的天气预测。夜间的天气信息。降水概率（百分比）。 | `weather.forecast.day05Forecast.night.precipChance` |
| [!UICONTROL Day 5 Forecast Night Precipitation Type] | 五天的天气预测。夜间的天气信息。降水形式（雨、雪、雨夹雪等）。 | `weather.forecast.day05Forecast.night.precipType` |
| [!UICONTROL Day 5 Forecast Night QPF Inches] | 五天的天气预测。夜间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day05Forecast.night.qpf.inches` |
| [!UICONTROL Day 5 Forecast Night QPF Millimeters] | 五天的天气预测。夜间的天气信息。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day05Forecast.night.qpf.millimeters` |
| [!UICONTROL Day 5 Forecast Night QPF Snow Centimeters] | 五天的天气预测。夜间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day05Forecast.night.qpfSnow.centimeters` |
| [!UICONTROL Day 5 Forecast Night QPF Snow Inches] | 五天的天气预测。夜间的天气信息。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day05Forecast.night.qpfSnow.inches` |
| [!UICONTROL Day 5 Forecast Night Relative Humidity] | 五天的天气预测。夜间的天气信息。空气的相对湿度，定义为空气中的水蒸气量与在恒定温度下使空气达到饱和度所需的水蒸气量之比。相对湿度始终以百分比表示。<br>范围 - 0 到 100。 | `weather.forecast.day05Forecast.night.relativeHumidity` |
| [!UICONTROL Day 5 Forecast Night Snow Range] | 五天的天气预测。夜间的天气信息。可能的降雪量（1-3&quot;、3-6&quot; 等）。 | `weather.forecast.day05Forecast.night.snowRange` |
| [!UICONTROL Day 5 Forecast Night Temperature Celsius] | 五天的天气预测。夜间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（摄氏度） | `weather.forecast.day05Forecast.night.temperature.celsius` |
| [!UICONTROL Day 5 Forecast Night Temperature Fahrenheit] | 五天的天气预测。夜间的天气信息。以定义的测量单位表示的温度。范围 -140 到 140。温度（华氏度） | `weather.forecast.day05Forecast.night.temperature.fahrenheit` |
| [!UICONTROL Day 5 Forecast Night Temperature Heat Index Celsius] | 五天的天气预测。夜间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day05Forecast.night.temperatureHeatIndex.celsius` |
| [!UICONTROL Day 5 Forecast Night Temperature Heat Index Fahrenheit] | 五天的天气预测。夜间的天气信息。根据温度和湿度，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day05Forecast.night.temperatureHeatIndex.fahrenheit` |
| [!UICONTROL Day 5 Forecast Night Temperature Wind Chill Celsius] | 五天的天气预测。夜间的天气信息。根据温度和风速，暴露人员的体感温度。温度（摄氏度） | `weather.forecast.day05Forecast.night.temperatureWindChill.celsius` |
| [!UICONTROL Day 5 Forecast Night Temperature Wind Chill Fahrenheit] | 五天的天气预测。夜间的天气信息。根据温度和风速，暴露人员的体感温度。温度（华氏度） | `weather.forecast.day05Forecast.night.temperatureWindChill.fahrenheit` |
| [!UICONTROL Day 5 Forecast Night Thunder Index] | 五天的天气预测。夜间的天气信息。雷暴影响某个地区的概率指数。0（无雷）到 5（严重雷暴的高风险）。 | `weather.forecast.day05Forecast.night.thunderIndex` |
| [!UICONTROL Day 5 Forecast Night UV Index] | 五天的天气预测。夜间的天气信息。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day05Forecast.night.uvIndex` |
| [!UICONTROL Day 5 Forecast Night Wind Direction] | 五天的天气预测。夜间的天气信息。风吹来的磁极风向（以度表示）。磁极方向在 0 度到 359 度之间变化，其中 0° 表示北，90° 表示东，180° 表示南，270° 表示西，依此类推。<br>范围 - 0&lt;=wind_dire_deg&lt;=350，以 10 度为间隔。 | `weather.forecast.day05Forecast.night.windDirection` |
| [!UICONTROL Day 5 Forecast Night Wind Gust Kilometers per Hour] | 五天的天气预测。夜间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（公里/小时） | `weather.forecast.day05Forecast.night.windGust.kilometersPerHour` |
| [!UICONTROL Day 5 Forecast Night Wind Gust Miles per Hour] | 五天的天气预测。夜间的天气信息。此数据字段包含有关平均风速的突然和暂时变化的信息。报告始终显示观测期间记录的最大阵风速度。如果显示风速，则它是必填显示字段。阵风的速度可以用英里/小时或公里/小时表示。风速（英里/小时） | `weather.forecast.day05Forecast.night.windGust.milesPerHour` |
| [!UICONTROL Day 5 Forecast Night Wind Speed Kilometers per Hour] | 五天的天气预测。夜间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day05Forecast.night.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 5 Forecast Night Wind Speed Miles per Hour] | 五天的天气预测。夜间的天气信息。风被视为矢量；因此，风必须有方向和大小（速度）。当前条件下报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day05Forecast.night.windSpeed.milesPerHour` |
| [!UICONTROL Day 5 Forecast QPF Inches] | 五天的天气预测。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（英寸） | `weather.forecast.day05Forecast.qpf.inches` |
| [!UICONTROL Day 5 Forecast QPF Millimeters] | 五天的天气预测。预测的 12 或 24 小时期间的可测量降水量（液态水或液态水当量）。以毫米为单位测量。降水量（毫米） | `weather.forecast.day05Forecast.qpf.millimeters` |
| [!UICONTROL Day 5 Forecast QPF Snow Centimeters] | 五天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day05Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 5 Forecast QPF Snow Inches] | 五天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day05Forecast.qpfSnow.inches` |
| [!UICONTROL Day 7 Forecast Calendar Day Temperature Max Celsius] | 七天的天气预测。给定天的午夜至午夜每日最高温度。温度（摄氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 7 Forecast Calendar Day Temperature Max Fahrenheit] | 七天的天气预测。给定天的午夜至午夜每日最高温度。温度（华氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 7 Forecast Calendar Day Temperature Min Celsius] | 七天的天气预测。给定天的午夜至午夜日最低温度。温度（摄氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 7 Forecast Calendar Day Temperature Min Fahrenheit] | 七天的天气预测。给定天的午夜至午夜日最低温度。温度（华氏度） | `weather.forecast.day07Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 7 Forecast Cloud Cover Miles] | 七天的天气预测。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day07Forecast.cloudCover.inches` |
| [!UICONTROL Day 7 Forecast Cloud Cover Kilometers] | 七天的天气预测。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day07Forecast.cloudCover.kilometers` |
| [!UICONTROL Day 7 Forecast QPF Inches] | 七天的天气预测。预测的 24 小时期间的可测量降水量（液态水或液态水当量）。降水量（英寸） | `weather.forecast.day07Forecast.qpf.inches` |
| [!UICONTROL Day 7 Forecast QPF Millimeters] | 七天的天气预测。预测的 24 小时期间的可测量降水量（液态水或液态水当量）。降水量（毫米） | `weather.forecast.day07Forecast.qpf.millimeters` |
| [!UICONTROL Day 7 Forecast QPF Snow Centimeters] | 七天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day07Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 7 Forecast QPF Snow Inches] | 七天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day07Forecast.qpfSnow.inches` |
| [!UICONTROL Day 7 Forecast UV Index] | 七天的天气预测。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day07Forecast.uvIndex` |
| [!UICONTROL Day 7 Forecast Wind Direction] | 七天的天气预测。用磁化表示法表示的平均风向。 | `weather.forecast.day07Forecast.windDirection` |
| [!UICONTROL Day 7 Forecast Wind Speed Kilometers per Hour] | 七天的天气预测。预测的 12 小时预测期间的最大持续风速。<br>风被视为矢量；因此，风必须有方向和大小（速度）。预测中报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day07Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 7 Forecast Wind Speed Miles per Hour] | 七天的天气预测。预测的 12 小时预测期间的最大持续风速。<br>风被视为矢量；因此，风必须有方向和大小（速度）。预测中报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day07Forecast.windSpeed.milesPerHour` |
| [!UICONTROL Day 10 Forecast Calendar Day Temperature Max Celsius] | 十天的天气预测。给定天的午夜至午夜每日最高温度。温度（摄氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 10 Forecast Calendar Day Temperature Max Fahrenheit] | 十天的天气预测。给定天的午夜至午夜每日最高温度。温度（华氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 10 Forecast Calendar Day Temperature Min Celsius] | 十天的天气预测。给定天的午夜至午夜日最低温度。温度（摄氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 10 Forecast Calendar Day Temperature Min Fahrenheit] | 十天的天气预测。给定天的午夜至午夜日最低温度。温度（华氏度） | `weather.forecast.day10Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 10 Forecast Cloud Cover Miles] | 十天的天气预测。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day10Forecast.cloudCover.inches` |
| [!UICONTROL Day 10 Forecast Cloud Cover Kilometers] | 十天的天气预测。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day10Forecast.cloudCover.kilometers` |
| [!UICONTROL Day 10 Forecast QPF Inches] | 十天的天气预测。预测的 24 小时期间的可测量降水量（液态水或液态水当量）。降水量（英寸） | `weather.forecast.day10Forecast.qpf.inches` |
| [!UICONTROL Day 10 Forecast QPF Millimeters] | 十天的天气预测。预测的 24 小时期间的可测量降水量（液态水或液态水当量）。降水量（毫米） | `weather.forecast.day10Forecast.qpf.millimeters` |
| [!UICONTROL Day 10 Forecast QPF Snow Centimeters] | 十天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day10Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 10 Forecast QPF Snow Inches] | 十天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day10Forecast.qpfSnow.inches` |
| [!UICONTROL Day 10 Forecast UV Index] | 十天的天气预测。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day10Forecast.uvIndex` |
| [!UICONTROL Day 10 Forecast Wind Direction] | 十天的天气预测。用磁化表示法表示的平均风向。 | `weather.forecast.day10Forecast.windDirection` |
| [!UICONTROL Day 10 Forecast Wind Speed Kilometers per Hour] | 十天的天气预测。预测的 12 小时预测期间的最大持续风速。<br>风被视为矢量；因此，风必须有方向和大小（速度）。预测中报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day10Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 10 Forecast Wind Speed Miles per Hour] | 十天的天气预测。预测的 12 小时预测期间的最大持续风速。<br>风被视为矢量；因此，风必须有方向和大小（速度）。预测中报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day10Forecast.windSpeed.milesPerHour` |
| [!UICONTROL Day 14 Forecast Calendar Day Temperature Max Celsius] | 十四天的天气预测。给定天的午夜至午夜每日最高温度。温度（摄氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMax.celsius` |
| [!UICONTROL Day 14 Forecast Calendar Day Temperature Max Fahrenheit] | 十四天的天气预测。给定天的午夜至午夜每日最高温度。温度（华氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMax.fahrenheit` |
| [!UICONTROL Day 14 Forecast Calendar Day Temperature Min Celsius] | 十四天的天气预测。给定天的午夜至午夜日最低温度。温度（摄氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMin.celsius` |
| [!UICONTROL Day 14 Forecast Calendar Day Temperature Min Fahrenheit] | 十四天的天气预测。给定天的午夜至午夜日最低温度。温度（华氏度） | `weather.forecast.day14Forecast.calendarDayTemperatureMin.fahrenheit` |
| [!UICONTROL Day 14 Forecast Cloud Cover Miles] | 十四天的天气预测。白天平均云量（以百分比表示）。距离（英里）。 | `weather.forecast.day14Forecast.cloudCover.inches` |
| [!UICONTROL Day 14 Forecast Cloud Cover Kilometers] | 十四天的天气预测。白天平均云量（以百分比表示）。距离（公里）。 | `weather.forecast.day14Forecast.cloudCover.kilometers` |
| 第 14 天预测 QPF（英寸） | 十四天的天气预测。预测的 24 小时期间的可测量降水量（液态水或液态水当量）。降水量（英寸） | `weather.forecast.day14Forecast.qpf.inches` |
| [!UICONTROL Day 14 Forecast QPF Millimeters] | 十四天的天气预测。预测的 24 小时期间的可测量降水量（液态水或液态水当量）。降水量（毫米） | `weather.forecast.day14Forecast.qpf.millimeters` |
| [!UICONTROL Day 14 Forecast QPF Snow Centimeters] | 十四天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（厘米） | `weather.forecast.day14Forecast.qpfSnow.centimeters` |
| [!UICONTROL Day 14 Forecast QPF Snow Inches] | 十四天的天气预测。预测的 12 或 24 小时预测期间的可测量降水量（雪）。以厘米为单位测量。降雪量（英寸） | `weather.forecast.day14Forecast.qpfSnow.inches` |
| [!UICONTROL Day 14 Forecast UV Index] | 十四天的天气预测。12 小时预测期间的最大 UV 指数。 | `weather.forecast.day14Forecast.uvIndex` |
| 第 14 天预测风向 | 十四天的天气预测。用磁化表示法表示的平均风向。 | `weather.forecast.day14Forecast.windDirection` |
| [!UICONTROL Day 14 Forecast Wind Speed Kilometers per Hour] | 十四天的天气预测。预测的 12 小时预测期间的最大持续风速。<br>风被视为矢量；因此，风必须有方向和大小（速度）。预测中报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（公里/小时） | `weather.forecast.day14Forecast.windSpeed.kilometersPerHour` |
| [!UICONTROL Day 14 Forecast Wind Speed Miles per Hour] | 十四天的天气预测。预测的 12 小时预测期间的最大持续风速。<br>风被视为矢量；因此，风必须有方向和大小（速度）。预测中报告的风信息对应于 10 分钟平均值，称为持续风速。风速的突然或短暂变化称为“阵风”，并在单独的数据字段中报告。风向始终表示为“风从哪里吹来”，意思是北风由北向南吹。如果您在北风中面向北方，风就会吹到您的脸上。面朝南，北风就会吹到您的背上。风速（英里/小时） | `weather.forecast.day14Forecast.windSpeed.milesPerHour` |

## 触发因素 {#triggers}

触发器根据各种输入定义语义天气条件。

| 字段 | 描述 | XDM 路径 |
| --- | ---- | --- |
| [!UICONTROL Product Triggers] | 指示条件何时适合推动某些类别产品的销售。它们将映射到整数实体。可以从 IBM 获取完整列表。 | `weather.productTriggers` |
| [!UICONTROL Relative Triggers] | 基于人类感知的相对条件。诸如热或冷之类的东西。它们将映射到整数实体。可以从 IBM 获取完整列表。 | `weather.relativeTriggers` |
| [!UICONTROL Severe Weather Triggers] | 表示各种恶劣的天气条件，例如飓风或过量降雨。 | `weather.severeTriggers` |
