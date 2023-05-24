---
keywords: Experience Platform；首頁；熱門主題；Analytics對應欄位；Analytics對應
solution: Experience Platform
title: Adobe Analytics來源聯結器的對應欄位
description: Adobe Experience Platform可讓您透過Analytics來源擷取Adobe Analytics資料。 透過ADC擷取的某些資料可以直接從Analytics欄位對應到Experience Data Model (XDM)欄位，而其他資料需要轉換和特定函式才能成功對應。
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '3419'
ht-degree: 15%

---

# Analytics欄位對映

Adobe Experience Platform可讓您透過Analytics來源擷取Adobe Analytics資料。 透過ADC擷取的某些資料可以直接從Analytics欄位對應到Experience Data Model (XDM)欄位，而其他資料需要轉換和特定函式才能成功對應。

![](../images/analytics-data-experience-platform.png)

## 直接對應欄位

選取欄位會直接從Adobe Analytics對應至Experience Data Model (XDM)。

下表包含顯示Analytics欄位名稱的欄(*分析欄位*)，對應的XDM欄位(*XDM欄位*)及其型別(*XDM型別*)以及欄位描述(*說明*)。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| Analytics 字段 | XDM欄位 | XDM型別 | 描述 |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字符串 | 自訂變數，範圍為1到250。 每個組織使用這些自訂eVar的方式都會不同。 |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | 字符串 | 自訂流量變數，範圍為1到75。 |
| m_browser | _experience.analytics.environment.browserID | 整数 | 瀏覽器的編號ID。 |
| m_browser_height | environment.browserDetails.viewportHeight | 整数 | 瀏覽器高度（畫素）。 |
| m_browser_width | environment.browserDetails.viewportWidth | 整数 | 瀏覽器的寬度（畫素）。 |
| m_campaign | marketing.trackingCode | 字符串 | 用於追蹤代碼維度的變數。 |
| m_channel | web.webPageDetails.siteSection | 字符串 | 用於網站區段維度的變數。 |
| m_domain | environment.domain | 字符串 | 用於網域維度的變數。 這將根據使用者的網際網路服務提供者(ISP)而定。 |
| m_geo_city | placeContext.geo.city | 字符串 | 點選的城市名稱。 這是以點選的IP位址為基礎。 |
| m_geo_dma | placeContext.geo.dmaID | 整数 | 點選的人口統計區域數值ID。 這是以點選的IP位址為基礎。 |
| m_geo_region | placeContext.geo.stateProvince | 字符串 | 點選的狀態或區域名稱。 這是以點選的IP位址為基礎。 |
| m_geo_zip | placeContext.geo.postalCode | 字符串 | 點選的郵遞區號。 這是以點選的IP位址為基礎。 |
| m_keywords | search.keywords | 字符串 | 用於關鍵字維度的變數。 |
| m_os | _experience.analytics.environment.operatingSystemID | 整数 | 表示訪客的作業系統的數值ID。 這是根據user_agent資料行。 |
| m_page_url | web.webPageDetails.URL | 字符串 | 頁面點選的URL。 |
| m_pagename_no_url | web.webPageDetails.</span>name | 字符串 | 用來填入頁面維度的變數。 |
| m_referrer | web.webReferrer.URL | 字符串 | 上一頁的頁面URL。 |
| m_search_page_num | search.pageDepth | 整数 | 供所有搜索网页排名维度使用。指示用户在点击进入您的网站之前您的网站出现在搜索结果的哪一页。 |
| m_state | _experience.analytics.customDimensions.stateProvince | 字符串 | 狀態變數。 |
| m_user_server | web.webPageDetails.server | 字符串 | 用於伺服器維度的變數。 |
| m_zip | _experience.analytics.customDimensions.postalCode | 字符串 | 用來填入郵遞區號維度的變數。 |
| accept_language | environment.browserDetails.acceptLanguage | 字符串 | 列出所有接受的語言，如Accept-Language HTTP標頭所示。 |
| homepage | web.webPageDetails.isHomePage | 布尔 | 已不再使用。指出目前的URL是否為瀏覽器的首頁。 |
| ipv6 | environment.ipV6 | 字符串 |
| j_jscript | environment.browserDetails.javaScriptVersion | 字符串 | 瀏覽器支援的JavaScript版本。 |
| user_agent | environment.browserDetails.userAgent | 字符串 | HTTP標頭中傳送的使用者代理字串。 |
| mobileappid | 應用程式。</span>名稱 | 字符串 | 行動應用程式ID，以下列格式儲存： `[AppName][BundleVersion]`. |
| mobiledevice | device.model | 字符串 | 行動裝置的名稱。 在iOS上，這會儲存為逗號分隔的2位數字串。 第一個數字代表裝置代別，第二個數字代表裝置系列。 |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | 字符串 | 由Mobile Services使用。 代表地標。 |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | 数字 | 由Mobile Services使用。 代表興趣點距離。 |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | 数字 | 从上下文数据变量 a.loc.acc 收集。指示收集时 GPS 的精度（以米为单位）。 |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | 字符串 | 从上下文数据变量 a.loc.category 收集。描述特定位置的类别。 |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | 字符串 | 從內容資料變數a.loc.id收集。 给定目标点的标识符。 |
| video | media.mediaTimed.primaryAssetReference._id | 字符串 |  视频的名称。 |
| videoad | advertising.adAssetReference._id | 字符串 | 廣告資產的識別碼。 |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | 字符串 | 視訊內容型別。 對於所有視訊檢視，這會自動設定為「視訊」。 |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | 字符串 | 視訊廣告所在的Pod。 |
| videoadinpod | advertising.adAssetViewDetails.index | 整数 | 視訊廣告在Pod中的位置。 |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | 字符串 | 視訊播放器的名稱。 |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | 字符串 | 視訊頻道。 |
| videoadplayername | advertising.adAssetViewDetails.playerName | 字符串 | 視訊廣告播放器的名稱。 |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | 字符串 | 影片章節名稱 |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | 字符串 | 視訊名稱。 |
| videoadname | advertising.adAssetReference._dc.title | 字符串 | 視訊廣告的名稱。 |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series。_iptc4xmpExt.Name | 字符串 | 视频表演. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | 字符串 | 視訊季數。 |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | 字符串 | 视频剧集. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | 字符串 | 视频网络. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | 字符串 | 视频表演类型. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | 字符串 | 视频广告加载. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | 字符串 | 视频馈送类型. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | 数字 | Mobile Services 信标主要. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | 数字 | Mobile Services 信标次要. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | 字符串 | Mobile Services 信标 UUID. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | 字符串 | 視訊工作階段ID。 |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | 陣列 | 视频流派. | {title （物件）、description （物件）、type （物件）、meta：xdmType （物件）、items （字串）、meta：xdmField （物件）} |
| mobileinstalls | application.firstLaunches | 对象 | 這會在安裝或重新安裝後首次執行時觸發 | {id （字串），值（數字）} |
| mobileupgrades | application.upgrades | 对象 | 報告應用程式升級次數。 在升級後或每當版本號碼變更時首次執行時觸發。 | {id （字串），值（數字）} |
| mobilelaunches | application.launches | 对象 | 應用程式啟動次數。 | {id （字串），值（數字）} |
| mobilecrashes | application.crashes | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| mobilemessageclicks | directMarketing.clicks | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videotime | media.mediaTimed.timePlayed | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videostart | media.mediaTimed.impressions | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videocomplete | media.mediaTimed.completes | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoadstart | advertising.impressions | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoadcomplete | advertising.completes | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoadtime | advertising.timePlayed | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoplay | media.mediaTimed.starts | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videototaltime | media.mediaTimed.totalTimePlayed | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | 对象 | 視訊品質開始時間。 | {id （字串），值（數字）} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | 对象 | 视频品质：缓冲计数 | {id （字串），值（數字）} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | 对象 | 视频品质：缓冲时间 | {id （字串），值（數字）} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | 对象 | 视频品质：比特率变化计数 | {id （字串），值（數字）} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | 对象 | 视频品质：平均比特率 | {id （字串），值（數字）} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | 对象 | 视频品质：错误计数 | {id （字串），值（數字）} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoprogress10 | media.mediaTimed.progress10 | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoprogress25 | media.mediaTimed.progress25 | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoprogress50 | media.mediaTimed.progress50 | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoprogress75 | media.mediaTimed.progress75 | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoprogress95 | media.mediaTimed.progress95 | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videoresume | media.mediaTimed.resumes | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videopausecount | media.mediaTimed.pauses | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videopausetime | media.mediaTimed.pauseTime | 对象 | <!-- MISSING --> | {id （字串），值（數字）} |
| videosecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | 整数 |

{style="table-layout:auto"}

## 分割對應欄位

這些欄位有單一來源，但對應至 **多個** xdm位置。

| Analytics 字段 | XDM欄位 | XDM型別 | 描述 |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth， device.screenHeight | 整数 | 表示显示器分辨率的数值 ID。 |
| mobileosversion | environment.operatingSystem， environment.operatingSystemVersion | 字符串 | 行動作業系統版本。 |
| videoadlength | advertising.adAssetReference._xmpDM.duration | 整数 | 視訊廣告長度。 |

{style="table-layout:auto"}

## 產生的對應欄位

來自ADC的選取欄位需要轉換，其邏輯需要超越來自Adobe Analytics的直接副本，才能在XDM中產生。

下表包含顯示Analytics欄位名稱的欄(*分析欄位*)，對應的XDM欄位(*XDM欄位*)及其型別(*XDM型別*)以及欄位描述(*說明*)。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| Analytics 字段 | XDM欄位 | XDM型別 | 描述 |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 对象 | 自訂流量變數，範圍從1到75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | 对象 | 由階層變數使用。 它包含 | 分隔值清單。 | {values （陣列）， delimiter （字串）} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 陣列 | 變數值的清單。 包含分隔的自訂值清單（視實作而定） | {value (string)， key (string)} |
| m_color | device.colorDepth | 整数 | 色彩深度ID，以c_color欄的值為基礎。 |
| m_cookies | environment.browserDetails.cookiesEnabled | 布尔 | 用於「Cookie支援」維度的變數。 |
| m_event_list | commerce.purchases， commerce.productViews， commerce.productListOpens， commerce.checkouts， commerce.productListAdds， commerce.productListRemovals， commerce.productListViews | 对象 | 點選時觸發的標準商務事件。 | {id （字串），值（數字）} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100， _experience.analytics.event101to200.event200， _experience.analytics.event201to300.event201 - _experience.analytics.event201to300， _experience.event 301to400.event301 - _experience.analytics.event301to400.event400， _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500， _experience.analytics.event501to600 0， _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700， _experience.analytics.event701to800.event701 - _experience.analytics.event801to900， _experience.analytics.event801 0.event900， _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | 对象 | 點選時觸發的自訂事件。 | {id （物件），值（物件）} |
| m_geo_country | placeContext.geo.countryCode | 字符串 | 根據IP的點選來源國家/地區縮寫。 |
| m_geo_latitude | placeContext.geo._結構描述.latitude | 数字 | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._結構描述.longitude | 数字 | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | 布尔 | 表示Java是否已啟用的旗標。 |
| m_latitude | placeContext.geo._結構描述.latitude | 数字 | <!-- MISSING --> |
| m_longitude | placeContext.geo._結構描述.longitude | 数字 | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | 字符串 | 僅用於連結追蹤影像要求的變數。 此變數包含下載連結、退出連結或自訂連結點選的URL。 |
| m_page_event_var2 | web.webInteraction.name | 字符串 | 僅用於連結追蹤影像要求的變數。 這會列出連結的自訂名稱（如果已指定）。 |
| m_page_type | web.webPageDetails.isErrorPage | 布尔 | 用來填入找不到頁面維度的變數。 此變數應為空白或包含「ErrorPage」。 |
| m_pagename_no_url | web.webPageDetails.pageViews.value | 数字 | 頁面名稱（如果已設定）。 若未指定頁面，此值會留空。 |
| m_paid_search | search.isPaid | 布尔 | 如果點選符合付費搜尋偵測，則會設定此旗標。 |
| m_product_list | productListItems[].items | 陣列 | 產品清單，透過產品變數傳入。 | {SKU （字串）、數量（整數）、priceTotal （數字）} |
| m_ref_type | web.webReferrer.type | 字符串 | 表示点击的反向链接类型的数值 ID。1表示網站內、2表示其他網站、3表示搜尋引擎、4表示硬碟、5表示USENET、6表示「分類/建立書籤（無反向連結）」、7表示電子郵件、8表示無JavaScript、9表示「社交網路」。 |
| m_search_engine | search.searchEngine | 字符串 | 表示將訪客反向連結至您網站的搜尋引擎數值ID。 |
| post_currency | commerce.order.currencyCode | 字符串 | 交易过程中使用的货币代码。 |
| post_cust_hit_time_gmt | timestamp | 字符串 | 這僅用於啟用時間戳記的資料集。 這是根據Unix時間隨其傳送的時間戳記。 |
| post_cust_visid | identityMap | 物件 | 客戶訪客ID。 |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | 布尔 | 客戶訪客ID。 |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | 字符串 | 客戶訪客ID。 |
| post_visid_high + visid_low | identityMap | 物件 | 造訪的唯一識別碼。 |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | 字符串 | 造訪的唯一識別碼。 |
| post_visid_high | endUserIDs._experience.aaid.primary | 布尔 | 搭配visid_low使用以專門識別造訪。 |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | 字符串 | 搭配visid_low使用以專門識別造訪。 |
| post_visid_low | identityMap | 物件 | 搭配visid_high使用以專門識別造訪。 |
| hit_time_gmt | receivedTimestamp | 字符串 | 點選的時間戳記，以Unix時間為基礎。 |
| hitid_high + hitid_low | _id | 字符串 | 用於識別點選的唯一識別碼。 |
| hitid_low | _id | 字符串 | 搭配hitid_high使用以專門識別點選。 |
| IP | environment.ipV4 | 字符串 | IP位址，根據影像要求的HTTP標頭。 |
| j_jscript | environment.browserDetails.javaScriptEnabled | 布尔 | 使用的JavaScript版本。 |
| mcvisid_high + mcvisid_low | identityMap | 物件 | Experience Cloud的訪客ID。 |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | 字符串 | Experience CloudID (ECID)也稱為MCID，有時用於名稱空間。 |
| mcvisid_high | endUserIDs._experience.mcid.primary | 布尔 | Experience CloudID (ECID)也稱為MCID，有時用於名稱空間。 |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | 字符串 | Experience CloudID (ECID)也稱為MCID，有時用於名稱空間。 |
| mcvisid_low | identityMap | 物件 | Experience Cloud的訪客ID。 |
| sdid_high + sdid_low | _experience.target.supplementalDataID | 字符串 | 點選拼接ID。 分析欄位sdid_high和sdid_low是用於彙整兩個（或更多）傳入點選的補充資料ID。 |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | 字符串 | Mobile Services 信标邻近性. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | 整数 | 視訊章節的名稱。 |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | 整数 | 視訊的長度。 |

{style="table-layout:auto"}

## 進階對應欄位

選取欄位（稱為「postvalues」）需要更進階的轉換，才能成功地從Adobe Analytics欄位對應到Experience Data Model (XDM)。 執行這些進階轉換涉及使用Adobe Experience Platform查詢服務和預先建立的函式(稱為Adobe定義的函式)進行工作階段化、歸因和重複資料刪除。

若要進一步瞭解如何使用查詢服務執行此轉換，請造訪 [Adobe定義的函式](../../../../query-service/sql/adobe-defined-functions.md) 說明檔案。

下表包含顯示Analytics欄位名稱的欄(*分析欄位*)，對應的XDM欄位(*XDM欄位*)及其型別(*XDM型別*)以及欄位描述(*說明*)。

>[!NOTE]
>
>請向左/向右捲動以檢視表格的完整內容。

| Analytics 字段 | XDM欄位 | XDM型別 | 描述 |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字符串 | 自訂變數，範圍為1到250。 每個組織使用這些自訂eVar的方式都會不同。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | 字符串 | 自訂流量變數，範圍為1到75。 |
| post_browser_height | environment.browserDetails.viewportHeight | 整数 | 瀏覽器高度（畫素）。 |
| post_browser_width | environment.browserDetails.viewportWidth | 整数 | 瀏覽器的寬度（畫素）。 |
| post_campaign | marketing.trackingCode | 字符串 | 用於追蹤代碼維度的變數。 |
| post_channel | web.webPageDetails.siteSection | 字符串 | 用於網站區段維度的變數。 |
| post_cust_visid | endUserIDs._experience.aacustomid.id | 字符串 | 自訂訪客ID （如果已設定）。 |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | 字符串 | 訪客到達的第一個頁面的URL。 |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | 字符串 | 用於登入頁面原始維度的變數。 訪客登入頁面的頁面名稱。 |
| post_keywords | search.keywords | 字符串 | 為點選收集的關鍵字。 |
| post_page_url | web.webPageDetails.URL | 字符串 | 頁面點選的URL。 |
| post_pagename_no_url | web.webPageDetails.name | 字符串 | 用來填入頁面維度的變數。 |
| post_purchaseid | commerce.order.purchaseID | 字符串 | 用來唯一識別購買的變數。 |
| post_referrer | web.webReferrer.URL | 字符串 | 上一頁的URL。 |
| post_state | _experience.analytics.customDimensions.stateProvince | 字符串 | 狀態變數。 |
| post_user_server | web.webPageDetails.server | 字符串 | 用於伺服器維度的變數。 |
| post_zip | _experience.analytics.customDimensions.postalCode | 字符串 | 用來填入郵遞區號維度的變數。 |
| 瀏覽器 | _experience.analytics.environment.browserID | 整数 | 瀏覽器的數值ID。 |
| 網域 | environment.domain | 字符串 | 用於網域維度的變數。 這將根據使用者的網際網路服務提供者(ISP)而定。 |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | 字符串 | 訪客的第一個反向連結URL。 |
| geo_city | placeContext.geo.city | 字符串 | 點選的城市名稱。 這是以點選的IP位址為基礎。 |
| geo_dma | placeContext.geo.dmaID | 整数 | 點選的人口統計區域數值ID。 這是以點選的IP位址為基礎。 |
| geo_region | placeContext.geo.stateProvince | 字符串 | 點選的狀態或區域名稱。 這是以點選的IP位址為基礎。 |
| geo_zip | placeContext.geo.postalCode | 字符串 | 點選的郵遞區號。 這是以點選的IP位址為基礎。 |
| 作業系統 | _experience.analytics.environment.operatingSystemID | 整数 | 表示訪客的作業系統的數值ID。 這是根據user_agent資料行。 |
| search_page_num | search.pageDepth | 整数 | 此變數供所有搜尋頁面排名維度使用，並會指出您網站的搜尋結果頁面 | 出現在使用者點進您的網站之前。 |
| visit_keywords | _experience.analytics.session.search.keywords | 字符串 | 用於搜尋關鍵字維度的變數。 |
| visit_num | _experience.analytics.session.num | 整数 | 用於造訪次數維度的變數。 這會從1開始，並在每次新造訪開始時（每位使用者）增加。 |
| visit_page_num | _experience.analytics.session.depth | 整数 | 用於點選深度維度的變數。 使用者產生的每次點選此值都會增加1，並在每次造訪後重設。 |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | 字符串 | 造訪的第一個反向連結。 |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | 整数 | 访问的第一个页面名称。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 对象 | 自定义流量变量 1 至 75。 |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | 对象 | 由階層變數使用，並包含分隔的值清單。 | {values （陣列）， delimiter （字串）} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 陣列 | 變數值的清單。 包含分隔的自訂值清單（視實作而定）。 | {value (string)， key (string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | 布尔 | 在“Cookie 支持”维度中使用的变量。 |
| post_event_list | commerce.purchases， commerce.productViews， commerce.productListOpens， commerce.checkouts， commerce.productListAdds， commerce.productListRemovals， commerce.productListViews | 对象 | 點選時觸發的標準商務事件。 | {id （字串），值（數字）} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100， _experience.analytics.event101to200.event200， _experience.analytics.event201to300.event201 - _experience.analytics.event201to300， _experience.event 301to400.event301 - _experience.analytics.event301to400.event400， _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500， _experience.analytics.event501to600 0， _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700， _experience.analytics.event701to800.event701 - _experience.analytics.event801to900， _experience.analytics.event801 0.event900， _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | 对象 | 點選時觸發的自訂事件。 | {id （物件），值（物件）} |
| post_java_enabled | environment.browserDetails.javaEnabled | 布尔 | 表示Java是否已啟用的旗標。 |
| post_latitude | placeContext.geo._結構描述.latitude | 数字 | <!-- MISSING --> |
| post_longitude | placeContext.geo._結構描述.longitude | 数字 | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | 字符串 | 影像要求中傳送的點選型別（標準點選、下載連結、退出連結或自訂連結已點按）。 |
| post_page_event | web.webInteraction.linkClicks.value | 数字 | 影像要求中傳送的點選型別（標準點選、下載連結、退出連結或自訂連結已點按）。 |
| post_page_event_var1 | web.webInteraction.URL | 字符串 | 此變數僅用於連結追蹤影像要求。 這是下載連結、退出連結或自訂連結點選的URL。 |
| post_page_event_var2 | web.webInteraction.name | 字符串 | 此變數僅用於連結追蹤影像要求。 這將是連結的自訂名稱。 |
| post_page_type | web.webPageDetails.isErrorPage | 布尔 | 用於填入找不到頁面維度。 此變數應為空白或包含「ErrorPage」 |
| post_pagename_no_url | web.webPageDetails.pageViews.value | 数字 | 頁面名稱（如果已設定）。 若未指定頁面，此值會留空。 |
| post_product_list | productListItems[].items | 陣列 | 產品清單，透過產品變數傳入。 | {SKU （字串）、數量（整數）、priceTotal （數字）} |
| post_search_engine | search.searchEngine | 字符串 | 表示將訪客反向連結至您網站的搜尋引擎數值ID。 |
| mvvar1_instances | .list.items[] | 对象 | 變數值的清單。 包含分隔的自訂值清單（視實作而定）。 |
| mvvar2_instances | .list.items[] | 对象 | 變數值的清單。 包含分隔的自訂值清單（視實作而定）。 |
|  | mvvar3_instances | .list.items[] | 对象 | 變數值的清單。 包含分隔的自訂值清單（視實作而定）。 |
| 顏色 | device.colorDepth | 整数 | 色彩深度ID，根據c_color欄的值。 |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | 字符串 | 數值ID，代表訪客第一個反向連結的反向連結型別。 |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | 整数 | 访客第一次点击的时间戳（基于 Unix 时间）。 |
| geo_country | placeContext.geo.countryCode | 字符串 | 点击来源国家/地区的缩写，基于 IP 地址。 |
| geo_latitude | placeContext.geo._結構描述.latitude | 数字 | <!-- MISSING --> |
| geo_longiture | placeContext.geo._結構描述.longitude | 数字 | <!-- MISSING --> |
| paid_search | search.isPaid | 布尔 | 如果點選符合付費搜尋偵測，則會設定此旗標。 |
| ref_type | web.webReferrer.type | 字符串 | 表示点击的反向链接类型的数字 ID。 |
| visit_paid_search | _experience.analytics.session.search.isPaid | 布尔 | 指出造訪的第一次點選是否來自付費搜尋點選的旗標（1=付費，0=未付費）。 |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | 字符串 | 表示访问中使用的第一个反向链接的反向链接类型的数值 ID。 |
| visit_search_engine | _experience.analytics.session.search.searchEngine | 字符串 | 表示访问中使用的第一个搜索引擎的数值 ID。 |
| visit_start_time_gmt | _experience.analytics.session.timestamp | 整数 | 造訪之第一次點選的時間戳記（以Unix時間表示）。 |

{style="table-layout:auto"}