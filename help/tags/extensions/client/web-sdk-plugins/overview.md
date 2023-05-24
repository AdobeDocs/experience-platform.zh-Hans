---
title: 常見Web SDK外掛程式擴充功能概觀
description: 瞭解Adobe Experience Platform中的「常用Web SDK外掛程式」標籤擴充功能。
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 49%

---

# 常見Web SDK外掛程式擴充功能概觀

>[!IMPORTANT]
>
>此擴充功能旨在搭配Adobe Experience Platform Web SDK擴充功能使用。 若要檢視預期與AppMeasurement搭配使用的版本資訊，請參閱 [常見Analytics外掛程式擴充功能](../plugins/overview.md).

本文介紹如何設定Web SDK外掛程式標籤擴充功能，並用來增強 [Adobe Experience Platform Web SDK擴充功能](../sdk/overview.md).

## 設定常見Web SDK外掛程式擴充功能

本節提供設定Web SDK外掛程式擴充功能時可用選項的參考資料。

>[!IMPORTANT]
>
>「常見Web SDK外掛程式」擴充功能的用途是擴充Adobe Experience Platform Web SDK擴充功能，但您不需要安裝此擴充功能，即可讓擴充功能如預期般運作。

## 將外掛程式新增至Adobe Experience Platform Web SDK擴充功能

除了使用「常用Web SDK外掛程式」擴充功能提供的下列原生資料元素之外，不需要任何設定，即可初始化或新增外掛程式至您的程式庫：

* [`getAndPersistValue`](#getAndPersistValue)
* [`getGeoCoordinates`](#getGeoCoordinates)
* [`getNewRepeat`](#getNewRepeat)
* [&#39;getPagename&#39;](#getPagename)
* [`getPreviousValue`](#getPreviousValue)
* [`getQueryParam`](#getQueryParam)
* [`getTimeParting`](#getTimeParting)
* [`getTimeSinceLastVisit`](#getTimeSInceLastVisit)
* [`getValOnce`](#getValOnce)
* [`getVisitDuration`](#getVisitDuration)
* [`getVisitNum`](#getVisitNum)
* [&#39;pFo&#39;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>此資料元素會設定Cookie並允許將使用者產生的值儲存在Cookie中。 如需詳細資訊，請參閱外掛程式專屬檔案。

可讓您設定及設定 [`getAndPersistValue` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). 此 `getAndPersistValue` 資料元素會將值儲存在Cookie中，以便稍後造訪時擷取。

此 `getAndPersistValue` 資料元素提供下列引數：

* `vtp`（必需）：要在页面之间保留的值
* `cn`（可选）：用于存储值的 Cookie 的名称。如果未设置此参数，则将 Cookie 命名为 `"s_gapv"`
* `ex`（可选）：Cookie 过期前的天数。如果此参数为 `0` 或未设置，则 Cookie 将在访问结束时过期（处于不活动状态 30 分钟）。

如果變數位於 `vtp` 引數已設定，則資料元素會設定Cookie然後傳回Cookie值。 如果變數位於 `vtp` 引數未設定，則資料元素只會傳回Cookie值。

### `getGeoCoordinates`

>[!IMPORTANT]
>
>此外掛程式需要使用者端上的位置存取權，但若未取得，則不會擲回例外狀況。

可讓您設定及設定 [`getGeoCoordinates` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). 此 `getGeoCoordinates` 資料元素會擷取訪客裝置的經緯度。

此 `getGeoCoordinates` 資料元素不使用任何引數。 它会返回以下任一值：

* `"geo coordinates not available"`：对于在插件运行时没有可用地理位置数据的设备。此值在首次访问点击时很常见，特别是在访客需要首先准许跟踪其位置时。
* `"error retrieving geo coordinates"`：对于插件尝试检索设备位置时遇到任何错误的情况
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`：其中 [LATITUDE]/[LONGITUDE] 分别表示纬度和经度

### `getNewRepeat`

>[!IMPORTANT]
>
>此資料元素會設定Cookie。 如需詳細資訊，請參閱外掛程式專屬檔案。

可讓您設定及設定 [`getNewRepeat` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). 此 `getNewRepeat` 資料元素會判斷網站訪客是新訪客還是在指定天數內回訪的重複訪客。

此 `getNewRepeat` 資料元素會使用以下引數：

* `d`（整数，可选）：将访客重置回 `"New"` 的两次访问之间所需的最小天数。如果未设置此参数，则默认为 30 天。

此資料元素會傳回 `"New"` 如果資料元素設定的Cookie不存在或已過期。 它會傳回 `"Repeat"` 如果資料元素設定的Cookie存在，且自目前點選以來的時間量及Cookie中設定的時間超過30分鐘。 在整个访问期间，此方法将返回相同的值。

### `getPageName`

可讓您設定及設定 [`getPageName` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). 此 `getPageName` 資料元素可為目前的URL建立易讀、好記的格式化版本。

此 `getPageName` 資料元素會使用以下引數：

* `si`（可选，字符串）：插入到字符串开头的 ID，表示网站的 ID。此值可以是数字 ID 或友好名称。如果未设置此值，则将默认使用当前域。
* `qv`（可选，字符串）：以逗号分隔的查询字符串参数列表，其中包含在 URL 中找到的已添加到字符串的参数（如果可找到）
* `hv`（可选，字符串）：以逗号分隔的参数列表，其中包含在 URL 散列中找到的已添加到字符串的参数（如果可找到）
* `de`（可选，字符串）：用于拆分字符串各个部分的分隔符。默认使用管道分隔符 (`|`)。

資料元素會傳回包含易記格式化版URL的字串。 此字符串通常会被分配给 `pageName` 变量，但也可以用于其他变量。

### `getPreviousValue`

>[!IMPORTANT]
>
>此資料元素會設定Cookie並允許將使用者產生的值儲存在Cookie中。 如需詳細資訊，請參閱外掛程式專屬檔案。

可讓您設定及設定 [`getPreviousValue` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). 此 `getPreviousValue` 資料元素會將變數設定為先前點選上設定的值。

此 `getPreviousValue` 資料元素會使用以下引數：

* `v`（字符串，必需）：具有要传递给下一个图像请求的值的变量。用于检索上一页值的常用变量为 `s.pageName`。
* `c`（字符串，可选）：用于存储值的 Cookie 的名称。如果未设置此参数，则将默认使用 `"s_gpv"`。

當您呼叫此資料元素時，它會傳回Cookie中包含的字串值。 然后，此插件会重置 Cookie 过期时间，并为其分配 `v` 参数中的变量值。该 Cookie 将在处于非活动状态 30 分钟后过期。

### `getQueryParam`

可讓您設定及設定 [`getQueryParam` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). 此 `getQueryParam` 資料元素會擷取URL中包含的任何查詢字串引數的值。 在从登录页面 URL 中提取内部和外部促销活动代码时，此插件非常有用。在提取搜索词或其他查询字符串参数时，此插件也非常有价值。此資料元素提供完善的功能，可剖析複雜的URL，包括雜湊和包含多個查詢字串引數的URL。

此 `getQueryParam` 資料元素會使用以下引數：

* `qsp`（必需）：包含要在 URL 中查找的查询字符串参数列表，以逗号分隔。此列表不区分大小写。
* `de`（可选）：当有多个匹配的查询字符串参数时使用的分隔符。默认使用空字符串。
* `url`（可选）：要从中提取查询字符串参数值的自定义 URL、字符串或变量。默认值为 `window.location`。

呼叫此資料元素會根據上述引數和URL傳回值：

* 如果找不到匹配的查询字符串参数，此方法将返回空字符串。
* 如果找到一个匹配的查询字符串参数，此方法将返回该查询字符串参数值。
* 如果找到一个匹配的查询字符串参数，但其值为空，此方法将返回 `true`。
* 如果找到多个匹配的查询字符串参数，此方法将返回一个字符串，其中每个参数值均由 `de` 参数中的字符串分隔。

### `getTimeParting`

可讓您設定及設定 [`getTimeParting` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html?lang=zh-Hans). 此 `getTimeParting` 資料元素會擷取網站上發生任何可測量活動的時間詳細資訊。 如果您想要依指定日期範圍內任何可重複的時間區隔來劃分量度，此資料元素就十分實用。 例如，您可以比较一周内某两天的转化率，如所有星期日的转化率与所有星期四的转化率。您还可以比较一天内的不同时段，如比较所有上午与所有晚上。

此 `getTimeParting` 資料元素會使用以下引數：

`t`（可选但建议使用的字符串）：要将访客的本地时间转换到的时区的名称。默认为 UTC/GMT 时间。請參閱 [TZ資料庫時區清單](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) 在Wikipedia上以取得有效值的完整清單。

常见有效值包括：

* `"America/New_York"`（表示东部时间）
* `"America/Chicago"`（表示中部时间）
* `"America/Denver"`（表示山地时间）
* `"America/Los_Angeles"`（表示太平洋时间）

呼叫此資料元素會傳回包含下列內容的字串，並以縱線字元(`|`)：

* 当前年份
* 当前月份
* 当前日期
* 星期几
* 当前时间（上午/下午）

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>此資料元素會設定Cookie。 如需詳細資訊，請參閱外掛程式專屬檔案。

可讓您設定及設定 [`getTimeSinceLastVisit` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). 此 `getTimeSinceLastVisit` 資料元素會追蹤訪客從上次造訪到下次回訪您網站經過的時間長度。

此 `getTimeSinceLastVisit` 資料元素不使用任何引數。 此方法将返回距访客上次访问网站的间隔时间，并按以下列格式存储该时间：

* 若距上次访问的间隔时间介于 30 分钟和 1 小时之间，则会以“0.5 分钟”为基准将间隔时间四舍五入到最接近的值。例如 `"30.5 minutes"`、`"53 minutes"`
* 若距上次访问的间隔时间介于 1 小时和 1 天之间，则会以“0.25 小时”为基准将间隔时间四舍五入到最接近的值。例如 `"2.25 hours"`、`"7.5 hours"`
* 若距上次访问的间隔时间大于 1 天，则会以“1 天”为基准将间隔时间四舍五入到最接近的值。例如 `"1 day"`、`"3 days"`、`"9 days"`、`"372 days"`
* 如果访客之前未访问过，或间隔时间超过两年，则会将该值设为 `"New Visitor"`。

### `getValOnce`

>[!IMPORTANT]
>
>此資料元素會設定Cookie並允許將使用者產生的值儲存在Cookie中。 如需詳細資訊，請參閱外掛程式專屬檔案。

可讓您設定及設定 [`getValOnce` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). 此 `getValOnce` 資料元素可防止變數多次設為等於相同值。

此 `getValOnce` 資料元素會使用以下引數：

* `vtc`（必需，字符串）：要检查并确定之前是否已设置为相同值的变量
* `cn`（可选，字符串）：包含要检查的值的 Cookie 的名称。默认为 `"s_gvo"`
* `et`（可选，整数）：Cookie 的过期时间（以天或分钟为单位，具体取决于 `ep` 参数）。默认值为 `0`，该值表示将在浏览器会话结束时过期
* `ep`（可选，字符串）：仅当还同时设置了 `et` 参数时才会设置此参数。如果希望 `et` 的过期时间以分钟而不是以天为单位，请将此参数设置为 `"m"`。默认值为 `"d"`，该值会以天为单位设置 `et` 参数。

如果 `vtc` 参数与 Cookie 值相匹配，此方法将返回空字符串。如果 `vtc` 参数与 Cookie 值不匹配，此方法会将 `vtc` 参数作为字符串返回。

### `getVisitDuration`

>[!IMPORTANT]
>
>此資料元素會設定Cookie。 如需詳細資訊，請參閱外掛程式專屬檔案。

可讓您設定及設定 [`getVisitDuration` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). 此 `getVisitDuration` 資料元素會追蹤訪客截至該時間點為止在網站上逗留的時間長度，以分鐘為單位。

此 `getVisitDuration` 資料元素不使用任何引數。 它会返回以下任一值：

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"`（其中 `[x]` 是自访客登录网站后所经过的时间，以分钟为单位）

### `getVisitNum`

>[!IMPORTANT]
>
>此資料元素會設定Cookie。 如需詳細資訊，請參閱外掛程式專屬檔案。

可讓您設定及設定 [`getVisitNum` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). 此 `getVisitNum` 資料元素會傳回在指定天數內造訪過網站的所有訪客造訪次數。

此 `getVisitNum` 資料元素會使用以下引數：

* `rp`（可选，整数或字符串）：访问量计数器重置前的天数。如果未设置此参数，则将默认使用 `365`。
   * 如果将此参数设置为 `"w"`，则计数器将在周末（本周六晚上 11:59）重置
   * 如果将此参数设置为 `"m"`，则计数器将在月末（本月的最后一天）重置
   * 如果将此参数设置为 `"y"`，则计数器将在年末（12 月 31 日）重置
* `erp`（可选，布尔）：如果 `rp` 参数是数字，则此参数可确定是否应延长访问量过期时间。如果设置为 `true`，则对您网站的后续点击将重置访问数量计数器。如果设置为 `false`，则当访问数量计数器重置时，对您网站的后续点击将不会延期。默认为 `true`。如果 `rp` 参数为字符串，此参数将无效。

每当访客在处于非活动状态 30 分钟后返回到您的网站时，访问数量便会增加。调用此方法将返回一个表示访客当前访问数量的整数。

### `p_fo` （僅限頁面優先）

可讓您設定及設定 [`p_fo` Analytics外掛程式](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). 此 `p_fo` 資料元素是公用程式，可檢查特定JavaScript物件是否存在。 如果特定对象不存在，则此插件将创建该对象并返回 `true`。如果页面上已存在特定 JavaScript 对象，则将返回 `false`。若要在頁面上執行一次程式碼，此資料元素相當實用。

此 `p_fo` 資料元素會使用以下引數：

* `on` （必要，字串）：頁面上尚未存在物件時，資料元素所建立的JavaScript物件名稱。

如果对象尚不存在，则此方法将返回 `true` 并创建该对象。如果对象已存在，则此方法将返回 `false`。
