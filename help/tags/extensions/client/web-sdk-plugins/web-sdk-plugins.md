---
title: “常用Web SDK插件”扩展概述
description: 了解Adobe Experience Platform中的“常用Web SDK插件”标记扩展。
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 0%

---

# “常用Web SDK插件”扩展概述

>[!IMPORTANT]
>
>该扩展将与Adobe Experience Platform Web SDK扩展一起使用。 要查看有关要与AppMeasurement一起使用的版本的信息，请参阅[常用Analytics插件扩展](../plugins/overview.md)的概述。

本文档介绍如何配置Web SDK插件标记扩展，以及如何使用它来增强[Adobe Experience Platform Web SDK扩展](../web-sdk/overview.md)。

## 配置“常用Web SDK插件”扩展

此部分提供有关配置Web SDK插件扩展时可用的选项的参考。

>[!IMPORTANT]
>
>“常用Web SDK插件”扩展旨在增强Adobe Experience Platform Web SDK扩展，但是，为了使扩展按预期运行，您不需要安装此扩展。

## 将插件添加到Adobe Experience Platform Web SDK扩展

除了使用由常用Web SDK插件扩展提供的以下本机数据元素之外，无需进行配置即可将插件初始化或添加到库中：

* [&#39;getAndPersistValue&#39;](web-sdk-plugins.md#getandpersistvalue)
* [&#39;getGeoCoordinates&#39;](#getgeocoordinates)
* [&#39;getNewRepeat&#39;](#getnewrepeat)
* [&#39;getPageName&#39;](#getpagename)
* [&#39;getPreviousValue&#39;](#getpreviousvalue)
* [&#39;getQueryParam&#39;](#getqueryparam)
* [&#39;getTimeParting&#39;](#gettimeparting)
* [&#39;getTimeSinceLastVisit&#39;](#gettimesincelastvisit)
* [&#39;getValOnce&#39;](#getvalonce)
* [&#39;getVisitDuration&#39;](#getvisitduration)
* [&#39;getVisitNum&#39;](#getvisitnum)
* [&#39;p_fo&#39;](#p_fo-page-first-only)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>此数据元素会设置Cookie并允许将用户生成的值存储在Cookie中。 有关更多信息，请参阅特定于插件的文档。

允许您设置和配置[`getAndPersistValue` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html?lang=zh-Hans)。 `getAndPersistValue`数据元素将值存储在Cookie中，稍后可在访问期间进行检索。

`getAndPersistValue`数据元素提供了以下参数：

* `vtp` （必需）：要在页面之间保留的值
* `cn` （可选）：用于存储值的Cookie的名称。 如果未设置此参数，则Cookie将命名为`"s_gapv"`
* `ex` （可选）：Cookie过期前的天数。 如果此参数为`0`或未设置，则Cookie将在访问结束时过期（处于非活动状态30分钟）。

如果已设置`vtp`参数中的变量，则数据元素会设置Cookie，然后返回Cookie值。 如果未设置`vtp`参数中的变量，则数据元素仅返回Cookie值。

### `getGeoCoordinates`

>[!IMPORTANT]
>
>此插件需要在客户端上拥有位置访问权限，但如果无法获取该权限，则不会引发异常。

允许您设置和配置[`getGeoCoordinates` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html?lang=zh-Hans)。 `getGeoCoordinates`数据元素捕获访客设备的经度和纬度。

`getGeoCoordinates`数据元素不使用任何参数。 它会返回以下值之一：

* `"geo coordinates not available"`：对于在插件运行时没有可用地理位置数据的设备。 此值在首次访问点击时很常见，尤其是当访客需要首先同意跟踪其位置时。
* `"error retrieving geo coordinates"`：当插件尝试检索设备位置时遇到任何错误时
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`：其中`[LATITUDE]/[LONGITUDE]`分别表示纬度和经度

### `getNewRepeat`

>[!IMPORTANT]
>
>此数据元素设置Cookie。 有关更多信息，请参阅特定于插件的文档。

允许您设置和配置[`getNewRepeat` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html?lang=zh-Hans)。 `getNewRepeat`数据元素确定网站访客是新访客还是所需天数内的回访访客。

`getNewRepeat`数据元素使用以下参数：

* `d` （整数，可选）：将访客重置回`"New"`的两次访问之间所需的最小天数。 如果未设置此参数，则默认为30天。

如果数据元素设置的Cookie不存在或已过期，则此数据元素将返回值`"New"`。 如果数据元素设置的Cookie存在，并且自当前点击以来的时间以及Cookie中设置的时间大于30分钟，则返回值`"Repeat"`。 在整个访问期间，此方法将返回相同的值。

### `getPageName`

允许您设置和配置[`getPageName` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html?lang=zh-Hans)。 `getPageName`数据元素为当前URL创建易读、友好的格式化版本。

`getPageName`数据元素使用以下参数：

* `si` （可选，字符串）：插入到字符串开头的ID，表示网站的ID。 此值可以是数字ID或友好名称。 如果未设置，则默认使用当前域。
* `qv` （可选，字符串）：以逗号分隔的查询字符串参数列表，其中包含在URL中找到的已添加到字符串的参数（如果可找到）
* `hv` （可选，字符串）：以逗号分隔的参数列表，其中包含在URL散列中找到的已添加到字符串的参数（如果可找到）
* `de` （可选，字符串）：用于拆分字符串各个部分的分隔符。 默认使用管道(`|`)。

数据元素会返回一个包含URL的友好格式版本的字符串。 此字符串通常会被分配给`pageName`变量，但也可以用于其他变量。

### `getPreviousValue`

>[!IMPORTANT]
>
>此数据元素会设置Cookie并允许将用户生成的值存储在Cookie中。 有关更多信息，请参阅特定于插件的文档。

允许您设置和配置[`getPreviousValue` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html?lang=zh-Hans)。 `getPreviousValue`数据元素将变量设置为在上一次点击时设置的值。

`getPreviousValue`数据元素使用以下参数：

* `v` （字符串，必需）：具有要传递给下一个图像请求的值的变量。 用于检索上一页值的常用变量为`s.pageName`。
* `c` （字符串，可选）：用于存储值的Cookie的名称。  如果未设置此参数，则默认为`"s_gpv"`。

调用此数据元素时，将返回Cookie中包含的字符串值。 然后，此插件会重置Cookie过期时间，并为其分配`v`参数中的变量值。 Cookie将在处于非活动状态30分钟后过期。

### `getQueryParam`

允许您设置和配置[`getQueryParam` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html?lang=zh-Hans)。 `getQueryParam`数据元素提取URL中包含的任何查询字符串参数的值。 在从登陆页面URL中提取内部和外部促销活动代码时，此插件非常有用。 在提取搜索词或其他查询字符串参数时，此插件也很有价值。 此数据元素在解析复杂URL（包括散列和包含多个查询字符串参数的URL）方面提供了强大的功能。

`getQueryParam`数据元素使用以下参数：

* `qsp` （必需）：包含要在URL中查找的查询字符串参数的逗号分隔列表。 不区分大小写。
* `de` （可选）：有多个查询字符串参数匹配时要使用的分隔符。 默认使用空字符串。
* `url`（可选）：要从中提取查询字符串参数值的自定义URL、字符串或变量。 默认为`window.location`。

调用此数据元素时，会根据上述参数和URL返回一个值：

* 如果找不到匹配的查询字符串参数，此方法将返回空字符串。
* 如果找到一个匹配的查询字符串参数，此方法将返回该查询字符串参数值。
* 如果找到一个匹配的查询字符串参数，但值为空，此方法将返回`true`。
* 如果找到多个匹配的查询字符串参数，此方法将返回一个字符串，其中每个参数值均由`de`参数中的字符串分隔。

### `getTimeParting`

允许您设置和配置[`getTimeParting` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html?lang=zh-Hans)。 `getTimeParting`数据元素捕获网站上发生任何可测量活动的时间的详细信息。 当您想要按给定日期范围内的任何可重复时间划分来细分指标时，此数据元素很有价值。 例如，您可以比较一周内某两天的转化率，如所有星期日的转化率与所有星期四的转化率。 您还可以比较一天内的不同时段，如比较所有上午与所有晚上。

`getTimeParting`数据元素使用以下参数：

`t` （可选但建议使用的字符串）：要将访客的本地时间转换为的时区的名称。  默认为UTC/GMT时间。 有关有效值的完整列表，请参阅Wikipedia上的[TZ时区数据库时区列表](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)。

常见的有效值包括：

* 东部时间`"America/New_York"`
* 中部时间`"America/Chicago"`
* 山地时间的`"America/Denver"`
* 太平洋时间的`"America/Los_Angeles"`

调用此数据元素将返回一个字符串，其中包含以管道(`|`)分隔的以下项：

* 当前年份
* 当前月份
* 日期
* 星期几
* 当前时间（上午/下午）

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>此数据元素设置Cookie。 有关更多信息，请参阅特定于插件的文档。

允许您设置和配置[`getTimeSinceLastVisit` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html?lang=zh-Hans)。 `getTimeSinceLastVisit`数据元素跟踪访客在距上次访问后多久返回您的网站。

`getTimeSinceLastVisit`数据元素不使用任何参数。 此方法将返回自访客上次访问网站以来经过的时间，并按以下格式存储该时间：

* 若距上次访问的间隔时间介于30分钟和1小时之间，则会以“0.5分钟”为基准将间隔时间设置为最接近的值。 例如，`"30.5 minutes"`，`"53 minutes"`
* 若距上次访问的间隔时间介于1小时和1天之间，则会以“0.25小时”为基准四舍五入到最接近的值。 例如，`"2.25 hours"`，`"7.5 hours"`
* 若距上次访问的间隔时间大于1天，则会以“1天”为基准将间隔时间四舍五入到最接近的值。 例如，`"1 day"`，`"3 days"`，`"9 days"`，`"372 days"`
* 如果访客之前未访问过，或间隔时间超过两年，则该值将设置为`"New Visitor"`。

### `getValOnce`

>[!IMPORTANT]
>
>此数据元素会设置Cookie并允许将用户生成的值存储在Cookie中。 有关更多信息，请参阅特定于插件的文档。

允许您设置和配置[`getValOnce` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html?lang=zh-Hans)。 `getValOnce`数据元素阻止将一个变量多次设置为等于同一个值。

`getValOnce`数据元素使用以下参数：

* `vtc` （必需，字符串）：要检查并确定之前是否已设置为相同值的变量
* `cn` （可选，字符串）：包含要检查的值的Cookie的名称。 默认为`"s_gvo"`
* `et` （可选，整数）：Cookie的过期时间（以天或分钟为单位，具体取决于`ep`参数）。 默认值为`0`，该值将在浏览器会话结束时过期
* `ep` （可选，字符串）：仅当还设置了`et`参数时才设置此参数。 如果希望`"m"`参数在几分钟内而不是几天内过期，请将此参数设置为`et`。 默认值为`"d"`，该值会以天为单位设置`et`参数。

如果`vtc`参数与Cookie值匹配，此方法将返回空字符串。 如果`vtc`参数与Cookie值不匹配，此方法会将`vtc`参数作为字符串返回。

### `getVisitDuration`

>[!IMPORTANT]
>
>此数据元素设置Cookie。 有关更多信息，请参阅特定于插件的文档。

允许您设置和配置[`getVisitDuration` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html?lang=zh-Hans)。 `getVisitDuration`数据元素跟踪访客在某个时间点之前在网站上停留的时间（以分钟为单位）。

`getVisitDuration`数据元素不使用任何参数。 它会返回以下值之一：

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` （其中`[x]`是自访客登录网站后所经过的时间，以分钟为单位）

### `getVisitNum`

>[!IMPORTANT]
>
>此数据元素设置Cookie。 有关更多信息，请参阅特定于插件的文档。

允许您设置和配置[`getVisitNum` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html?lang=zh-Hans)。 `getVisitNum`数据元素返回在所需天数内访问网站的所有访客的访问数量。

`getVisitNum`数据元素使用以下参数：

* `rp` （可选，整数或字符串）：访问量计数器重置前的天数。  如果未设置，则默认为`365`。
   * 如果此参数为`"w"`，则计数器将在周末（本周六晚上11:59）重置
   * 此参数为`"m"`时，计数器将在月末（本月的最后一天）重置
   * 如果此参数为`"y"`，则计数器将在年末（12月31日）重置
* `erp` （可选，布尔值）：如果`rp`参数是数字，则此参数可确定是否应延长访问量过期时间。 如果设置为`true`，则对您网站的后续点击将重置访问数量计数器。 如果设置为`false`，则当访问量计数器重置时，对您网站的后续点击将不会延期。 默认为`true`。 当`rp`参数为字符串时，此参数无效。

每当访客在处于非活动状态30分钟后返回到您的网站时，访问量就会增加。 调用此方法将返回一个表示访客当前访问数量的整数。

### `p_fo` （仅页面优先）

允许您设置和配置[`p_fo` Analytics插件](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html?lang=zh-Hans)。 `p_fo`数据元素是一个实用程序，用于检查特定JavaScript对象是否存在。 如果该对象不存在，则插件将创建该对象并返回`true`。 如果页面上已存在JavaScript对象，则返回`false`。 此数据元素可用于在页面上只运行一次代码。

`p_fo`数据元素使用以下参数：

* `on` （必需，字符串）：数据元素创建的JavaScript对象的名称（如果页面上不存在该对象）。

如果对象尚不存在，则此方法将返回`true`并创建该对象。 如果对象已存在，则此方法返回`false`。
