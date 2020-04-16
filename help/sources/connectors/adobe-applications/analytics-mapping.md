---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 分析映射字段
topic: overview
translation-type: tm+mt
source-git-commit: 9f0200af0310eafbcc1851b089cfc254cb34af8f

---


# 分析映射字段

Adobe Experience Platform允许您通过Analytics Data Connector(ADC)获取Adobe Analytics数据。 通过ADC摄取的某些数据可以直接从Analytics字段映射到Experience Data Model(XDM)字段，而其他数据需要转换和特定函数才能成功映射。

![](images/analytics-data-experience-platform.png)

## 直接映射字段

选择的字段会直接从Adobe Analytics映射到体验数据模型(XDM)。

下表包括显示“分析”字段(*Analytics字段*)的名称、相应的XDM字段(*XDM字段*)及其类型(**** XDM类型)的列，以及字段(DescriptionComplicationConternation)的说明。

>[!NOTE] 请向左／向右滚动以视图表的完整内容。

| 分析字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVar250 | 字符串 | 一个自定义变量，范围为1-250。 每个组织都将以不同方式使用这些自定义eVar。 |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | 字符串 | 自定义流量变量，范围为1-75。 |
| m_browser | _experience.analytics.环境.browserID | 整数 | 浏览器的编号ID。 |
| m_browser_height | environment.browserDetails.viewportHeight | 整数 | 浏览器的高度（以像素为单位）。 |
| m_browser_width | environment.browserDetails.viewportWidth | 整数 | 浏览器的宽度（以像素为单位）。 |
| m_活动 | marketing.trackingCode | 字符串 | “跟踪代码”维中使用的变量。 |
| m_渠道 | web.webPageDetails.siteSection | 字符串 | 在“站点区域”维中使用的变量。 |
| m_domain | environment.domain | 字符串 | 域维中使用的变量。 这将基于用户的Internet服务提供商(ISP)。 |
| m_geo_city | placeContext.geo.city | 字符串 | 受袭城市的名称。 这基于点击的IP地址。 |
| m_geo_dma | placeContext.geo.dmaID | 整数 | 点击的人口统计区域的数字ID。 这基于点击的IP地址。 |
| m_geo_region | placeContext.geo.stateProvince | 字符串 | 点击的州或地区的名称。 这基于点击的IP地址。 |
| m_geo_zip | placeContext.geo.postalCode | 字符串 | 点击的ZIP代码。 这基于点击的IP地址。 |
| m_keywords | search.keywords | 字符串 | 关键字维中使用的变量。 |
| m_os | _experience.analytics.环境.operatingSystemID | 整数 | 表示访客操作系统的数字ID。 这基于user_agent列。 |
| m_page_url | web.webPageDetails.URL | 字符串 | 点击页面的URL。 |
| m_pagename_no_url | web.webPageDetails.</span>name | 字符串 | 用于填充页面维的变量。 |
| m_推荐人 | web.webReferrer.URL | 字符串 | 上一页的页面URL。 |
| m_search_page_num | search.pageDepth | 整数 | 由“全部搜索页面排名”维使用。 指示在用户点击到您的站点之前，您的站点显示的搜索结果页面。 |
| m_state | _experience.analytics.customDimensions.stateProvince | 字符串 | 状态变量。 |
| m_user_server | web.webPageDetails.server | 字符串 | 服务器维中使用的变量。 |
| m_zip | _experience.analytics.customDimensions.postalCode | 字符串 | 用于填充邮政编码维度的变量。 |
| accept_language | environment.browserDetails.acceptLanguage | 字符串 | 列表所有已接受的语言，如Accept-Language HTTP头中所示。 |
| homepage | web.webPageDetails.isHomePage | 布尔 | 已不再使用。指示当前URL是否为浏览器的主页。 |
| ipv6 | environment.ipV6 | 字符串 |
| j_jscript | environment.browserDetails.javaScriptVersion | 字符串 | 浏览器支持的JavaScript版本。 |
| user_agent | environment.browserDetails.userAgent | 字符串 | HTTP头中发送的用户代理字符串。 |
| mobileappid | application.</span>name | 字符串 | 以下格式存储的移动应用程序ID: `[AppName][BundleVersion]`. |
| mobiledevice | device.model | 字符串 | 移动设备的名称。 在iOS上，它以逗号分隔的2位字符串形式存储。 第一数字表示设备生成，第二数字表示设备系列。 |
| pointinterest | placeContext.POIinteraction.POIDetail.</span>name | 字符串 | 由移动服务使用。 表示兴趣点。 |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | 数字 | 由移动服务使用。 表示目标距离。 |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | 数字 | 从上下文数据变量 a.loc.acc 收集。指示收集时 GPS 的精度（以米为单位）。 |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | 字符串 | 从上下文数据变量 a.loc.category 收集。描述特定位置的类别。 |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | 字符串 | 从上下文数据变量a.loc.id收集。 给定目标点的标识符。 |
| video | media.mediaTimed.primaryAssetReference._id | 字符串 |  视频的名称。 |
| videoad | advertising.adAssetReference._id | 字符串 | 广告资产的标识符。 |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | 字符串 | 视频内容类型。 对于所有视频视图，该选项会自动设置为“视频”。 |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | 字符串 | 视频广告所在的窗格。 |
| videoadinpod | advertising.adAssetViewDetails.index | 整数 | 视频广告在窗格中的位置。 |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | 字符串 | 视频播放器的名称。 |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | 字符串 | 视频渠道。 |
| videoadplayername | advertising.adAssetViewDetails.playerName | 字符串 | 视频广告播放器的名称。 |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | 字符串 | 视频章节的名称 |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | 字符串 | 视频名称。 |
| videoadname | advertising.adAssetReference._dc.title | 字符串 | 视频广告的名称。 |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series。_iptc4xmpExt.Name | 字符串 | 视频表演. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season。_iptc4xmpExt.Name | 字符串 | 视频季。 |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Ipesore。_iptc4xmpExt.Name | 字符串 | 视频剧集. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | 字符串 | 视频网络. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | 字符串 | 视频表演类型. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | 字符串 | 视频广告加载. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | 字符串 | 视频馈送类型. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | 数字 | Mobile Services 信标主要. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | 数字 | Mobile Services 信标次要. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | 字符串 | Mobile Services 信标 UUID. |
| videossessionid | media.mediaTimed.primaryAssetViewDetails._id | 字符串 | 视频会话ID。 |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | 阵列 | 视频流派. | {title(Object), description(Object), type(Object), meta:xdmType(Object), items(string), meta:xdmField(Object)} |
| mobileinstalls | application.firstLaunches | 对象 | 安装或重新安装后的第一次运行时触发 | {id(string), value(number)} |
| mobileupgrades | application.upgrades | 对象 | 报告应用程序升级的数量。 在升级后或随时更改版本号时首次运行时触发。 | {id(string), value(number)} |
| mobilelaunches | application.launches | 对象 | 应用程序启动的次数。 | {id(string), value(number)} |
| mobilecrashes | application.crashes | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| mobilemessageclicks | directMarketing.clicks | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videotime | media.mediaTimed.timePlayed | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videostart | media.mediaTimed.impressions | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videocomplete | media.mediaTimed.completes | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| 视频段视图 | media.mediaTimed.mediaSegmentViews | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoadstart | advertising.impressions | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoadcomplete | advertising.completes | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoadtime | advertising.timePlayed | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoplay | media.mediaTimed.starts | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videototaltime | media.mediaTimed.totalTimePlayed | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | 对象 | 视频质量的开始时间。 | {id(string), value(number)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | 对象 | 视频质量缓冲区计数 | {id(string), value(number)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | 对象 | 视频品质：缓冲时间 | {id(string), value(number)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | 对象 | 视频质量更改计数 | {id(string), value(number)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | 对象 | 视频质量平均比特率 | {id(string), value(number)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | 对象 | 视频质量错误计数 | {id(string), value(number)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoprogress10 | media.mediaTimed.progress10 | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoprogress25 | media.mediaTimed.progress25 | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoprogress50 | media.mediaTimed.progress50 | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoprogress75 | media.mediaTimed.progress75 | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoprogress95 | media.mediaTimed.progress95 | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videoresume | media.mediaTimed.resumes | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videopausecount | media.mediaTimed.pauses | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videopausetime | media.mediaTimed.pauseTime | 对象 | <!-- MISSING --> | {id(string), value(number)} |
| videosecondsincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | 整数 |

## 拆分映射字段

这些字段有一个源，但映射到多 **个** XDM位置。

| 分析字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth、device.screenHeight | 整数 | 表示显示器分辨率的数字ID。 |
| mobileosversion | 环境.operatingSystem、环境.operatingSystemVersion | 字符串 | 移动操作系统版本。 |
| videoadlength | advertising.adAssetReference._xmpDM.duration | 整数 | 视频广告长度。 |

## 生成的映射字段

需要转换来自ADC的选定字段，这要求逻辑不局限于Adobe Analytics的直接副本，以便在XDM中生成。

下表包括显示“分析”字段(*Analytics字段*)的名称、相应的XDM字段(*XDM字段*)及其类型(**** XDM类型)的列，以及字段(DescriptionComplicationConternation)的说明。

>[!NOTE] 请向左／向右滚动以视图表的完整内容。

| 分析字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 对象 | 自定义流量变量，范围从1到75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarcies.hier1 - _experience.analytics.customDimensions.hier5 | 对象 | 由层次变量使用。 它包含 | 分隔值列表。 | {values(array), delimiter(string)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.列表.列表1.列表[] - _experience.analytics.customDimensions.列表.列表3.列表[] | 阵列 | 列表变量值。 包含自定义值的分隔列表，具体取决于实现 | {value(string), key(string)} |
| m_color | device.colorDepth | 整数 | 颜色深度ID，它基于c_color列的值。 |
| m_cookies | environment.browserDetails.cookiesEnabled | 布尔 | “Cookie支持”维中使用的变量。 |
| m_事件_列表 | commerce.purchases、commerce.productViews、commerce.productListOpens、commerce.checkouts、commerce.productListAdds、commerce.productListMelvets、commerce.productListViews | 对象 | 标准商务事件在点击时触发。 | {id(string), value(number)} |
| m_事件_列表 | _experience.analytics.事件1to100.事件1 - _experience.analytics.事件1to100.事件100, _experience.analytics.事件101to200.事件101 - _experience.analytics.事件101to200.事件100.事件_experience.analytics.jecvigy201to300.jecvigy201 - _experience.analytics.jecvigy201to300.jecvigy300, _experience.analytics.jecvigy301to40.jevigigy301 - _experie.analytics.jective事件301to400.jective400, _experience.analytics.jective401to500.juctival401 - _experience.analytics.jectivation401to500, _experience.analytics.jity.jictics.jitytics.jection.jection505050501.je.jiv.je.jection.jiv.jiv.j.jiv.jiviv.jictiv.j.事件1to600.事件501 - _experience.analytics.事件501to600.事件600, _experience.analytics.事件601to700.事件601 - _experience.analytics.事件601to700.事件_experience.analytics.jecvigy701to800.jecvigy701 - _experience.analytics.jecvigy701to800.jecvigy800, _experience.analytics.jecvigy801to90.jevigy801 - _experience.analytics.jective事件801到900.jective900, _experience.analytics.jective901到1000.jectivation901 - _experience.analytics.jectivation901到1000.jevetive | 对象 | 点击时触发的自定义事件。 | {id(Object), value(Object)} |
| m_geo_country | placeContext.geo.countryCode | 字符串 | 点击源国的缩写，基于IP。 |
| m_geo_latitude | placeContext.geo._模式.latitude | 数字 | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._模式.longitude | 数字 | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | 布尔 | 指示是否启用Java的标志。 |
| m_latitude | placeContext.geo._模式.latitude | 数字 | <!-- MISSING --> |
| m_longitude | placeContext.geo._模式.longitude | 数字 | <!-- MISSING --> |
| m_page_事件_var1 | web.webInteraction.URL | 字符串 | 仅用于链接跟踪图像请求的变量。 此变量包含所点击的下载链接、退出链接或自定义链接的URL。 |
| m_page_事件_var2 | web.webInteraction.name | 字符串 | 仅用于链接跟踪图像请求的变量。 此列表链接的自定义名称（如果已指定）。 |
| m_page_type | web.webPageDetails.isErrorPage | 布尔 | 用于填充“找不到页面”维的变量。 此变量应为空或包含“ErrorPage”。 |
| m_pagename_no_url | web.webPageDetails.pageViews.value | 数字 | 页面的名称（如果设置）。 如果未指定页面，则此值将留空。 |
| m_paid_search | search.isPaid | 布尔 | 在点击与付费搜索检测匹配时设置的标记。 |
| m_product_列表 | productListItems[].items | 阵列 | 产品列表，通过产品变量传递。 | {SKU（字符串）, quantity(integer), priceTotal(number)} |
| m_ref_type | web.webReferrer.type | 字符串 | 表示点击的参照类型的数字ID。 1表示网站内部，2表示其他网站，3表示搜索引擎，4表示硬盘，5表示USENET,6表示输入／书签(无推荐人),7表示电子邮件，8表示无JavaScript,9表示社交网络。 |
| m_search_engine | search.searchEngine | 字符串 | 表示将访客引用到站点的搜索引擎的数字ID。 |
| post_currency | commerce.order.currencyCode | 字符串 | 在事务处理期间使用的货币代码。 |
| post_cust_hit_time_gmt | timestamp | 字符串 | 这仅用于启用时间戳的数据集。 这是随其发送的基于Unix时间的时间戳。 |
| post_cust_visid | identityMap | 对象 | 客户访客ID。 |
| post_cust_visid | endUserID。_experience.aacustomid.primary | 布尔 | 客户访客ID。 |
| post_cust_visid | endUserID。_experience.aacustomid.命名空间.code | 字符串 | 客户访客ID。 |
| post_visid_high + visid_low | identityMap | 对象 | 访问的唯一标识符。 |
| post_visid_high + visid_low | endUserID。_experience.aaid.id | 字符串 | 访问的唯一标识符。 |
| post_visid_high | endUserID。_experience.aaid.primary | 布尔 | 与visid_low一起使用以唯一标识访问。 |
| post_visid_high | endUserID。_experience.aaid.命名空间.code | 字符串 | 与visid_low一起使用以唯一标识访问。 |
| post_visid_low | identityMap | 对象 | 与visid_high一起使用以唯一标识访问。 |
| hit_time_gmt | receivedTimestamp | 字符串 | 点击的时间戳，基于Unix时间。 |
| hitid_high + hitid_low | _id | 字符串 | 用于标识点击的唯一标识符。 |
| hitid_low | _id | 字符串 | 与hitid_high一起使用以唯一标识点击。 |
| ip | environment.ipV4 | 字符串 | IP地址，基于图像请求的HTTP头。 |
| j_jscript | environment.browserDetails.javaScriptEnabled | 布尔 | 使用的JavaScript版本。 |
| mcvisid_high + mcvisid_low | identityMap | 对象 | Experience Cloud访客ID。 |
| mcvisid_high + mcvisid_low | endUserID。_experience.mcid.id | 字符串 | Experience Cloud访客ID。 |
| mcvisid_high | endUserID。_experience.mcid.primary | 布尔 | Experience Cloud访客ID。 |
| mcvisid_high | endUserID。_experience.mcid.命名空间.code | 字符串 | Experience Cloud访客ID。 |
| mcvisid_low | identityMap | 对象 | Experience Cloud访客ID。 |
| sdid_high + sdid_low | _experience.目标.supplementalDataID | 字符串 | 点击“拼接ID”。 分析字段sdid_high和sdid_low是用于拼接两个（或多个）传入点击的补充数据ID。 |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | 字符串 | Mobile Services 信标邻近性. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | 整数 | 视频章节的名称。 |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | 整数 | 视频的长度。 |

## 高级映射字段

选择字段（称为“后置值”）需要更高级的转换，然后才能将它们从Adobe Analytics字段成功映射到体验数据模型(XDM)。 执行这些高级转换需要使用Adobe Experience Platform查询服务和预建函数（称为Adobe定义的函数）进行会话化、归因和外部重复数据删除。

要了解有关使用查询服务执行此转换的更多信息，请访问 [Adobe定义的函数文档](../../../query-service/sql/adobe-defined-functions.md) 。

下表包括显示“分析”字段(*Analytics字段*)的名称、相应的XDM字段(*XDM字段*)及其类型(**** XDM类型)的列，以及字段(DescriptionComplicationConternation)的说明。

>[!NOTE] 请向左／向右滚动以视图表的完整内容。

| 分析字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVar250 | 字符串 | 一个自定义变量，范围为1-250。 每个组织都将以不同方式使用这些自定义eVar。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | 字符串 | 自定义流量变量，范围为1-75。 |
| post_browser_height | environment.browserDetails.viewportHeight | 整数 | 浏览器的高度（以像素为单位）。 |
| post_browser_width | environment.browserDetails.viewportWidth | 整数 | 浏览器的宽度（以像素为单位）。 |
| post_活动 | marketing.trackingCode | 字符串 | “跟踪代码”维中使用的变量。 |
| post_渠道 | web.webPageDetails.siteSection | 字符串 | 在“站点区域”维中使用的变量。 |
| post_cust_visid | endUserID。_experience.aacustomid.id | 字符串 | 自定义访客ID（如果已设置）。 |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | 字符串 | 访客到达的第一页的URL。 |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | 字符串 | 在“条目页面原始”维中使用的变量。 访客的条目页面的页面名称。 |
| post_keywords | search.keywords | 字符串 | 为点击收集的关键字。 |
| post_page_url | web.webPageDetails.URL | 字符串 | 点击页面的URL。 |
| post_pagename_no_url | web.webPageDetails.name | 字符串 | 用于填充页面维的变量。 |
| post_purchaseid | commerce.order.purchaseID | 字符串 | 用于唯一标识购买的变量。 |
| post_推荐人 | web.webReferrer.URL | 字符串 | 上一页的URL。 |
| post_state | _experience.analytics.customDimensions.stateProvince | 字符串 | 状态变量。 |
| post_user_server | web.webPageDetails.server | 字符串 | 服务器维中使用的变量。 |
| post_zip | _experience.analytics.customDimensions.postalCode | 字符串 | 用于填充邮政编码维度的变量。 |
| 浏览器 | _experience.analytics.环境.browserID | 整数 | 浏览器的数字ID。 |
| 域 | environment.domain | 字符串 | 域维中使用的变量。 这将基于用户的Internet服务提供商(ISP)。 |
| first_hit_推荐人 | _experience.analytics.endUser.firstWeb.webReferrer.URL | 字符串 | 访客的第一个引用URL。 |
| geo_city | placeContext.geo.city | 字符串 | 受袭城市的名称。 这基于点击的IP地址。 |
| geo_dma | placeContext.geo.dmaID | 整数 | 点击的人口统计区域的数字ID。 这基于点击的IP地址。 |
| geo_region | placeContext.geo.stateProvince | 字符串 | 点击的州或地区的名称。 这基于点击的IP地址。 |
| geo_zip | placeContext.geo.postalCode | 字符串 | 点击的ZIP代码。 这基于点击的IP地址。 |
| os | _experience.analytics.环境.operatingSystemID | 整数 | 表示访客操作系统的数字ID。 这基于user_agent列。 |
| search_page_num | search.pageDepth | 整数 | 此变量由“所有搜索页面排名”维度使用，并指示站点的搜索结果页面 | 在用户点击您的站点之前显示。 |
| visit_keywords | _experience.analytics.session.search.keywords | 字符串 | “搜索关键字”维中使用的变量。 |
| visit_num | _experience.analytics.session.num | 整数 | “访问次数”维中使用的变量。 此开始为1，每次新访问开始（每个用户）都会递增。 |
| visit_page_num | _experience.analytics.session.depth | 整数 | “命中深度”维中使用的变量。 对于用户生成的每次点击，此值将增加1，并在每次访问后重置。 |
| visit_推荐人 | _experience.analytics.session.web.webReferrer.URL | 字符串 | 访问的第一推荐人. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | 整数 | 访问的第一个页面名称。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 对象 | 自定义流量变量1-75。 |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarcies.hier1 - _experience.analytics.customDimensions.hier5 | 对象 | 由层次变量使用，并包含一个分隔的值列表。 | {values(array), delimiter(string)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.列表.列表1.列表[] - _experience.analytics.customDimensions.列表.列表3.列表[] | 阵列 | 变量值的列表。 包含自定义值的分隔列表，具体取决于实现。 | {value(string), key(string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | 布尔 | 用于Cookie支持维度的变量。 |
| post_事件_列表 | commerce.purchases、commerce.productViews、commerce.productListOpens、commerce.checkouts、commerce.productListAdds、commerce.productListMelvets、commerce.productListViews | 对象 | 标准商务事件在点击时触发。 | {id(string), value(number)} |
| post_事件_列表 | _experience.analytics.事件1to100.事件1 - _experience.analytics.事件1to100.事件100, _experience.analytics.事件101to200.事件101 - _experience.analytics.事件101to200.事件100.事件_experience.analytics.jecvigy201to300.jecvigy201 - _experience.analytics.jecvigy201to300.jecvigy300, _experience.analytics.jecvigy301to40.jevigigy301 - _experie.analytics.jective事件301to400.jective400, _experience.analytics.jective401to500.juctival401 - _experience.analytics.jectivation401to500, _experience.analytics.jity.jictics.jitytics.jection.jection505050501.je.jiv.je.jection.jiv.jiv.j.jiv.jiviv.jictiv.j.事件1to600.事件501 - _experience.analytics.事件501to600.事件600, _experience.analytics.事件601to700.事件601 - _experience.analytics.事件601to700.事件_experience.analytics.jecvigy701to800.jecvigy701 - _experience.analytics.jecvigy701to800.jecvigy800, _experience.analytics.jecvigy801to90.jevigy801 - _experience.analytics.jective事件801到900.jective900, _experience.analytics.jective901到1000.jectivation901 - _experience.analytics.jectivation901到1000.jevetive | 对象 | 点击时触发的自定义事件。 | {id(Object), value(Object)} |
| post_java_enabled | environment.browserDetails.javaEnabled | 布尔 | 指示是否启用Java的标志。 |
| post_latitude | placeContext.geo._模式.latitude | 数字 | <!-- MISSING --> |
| post_longitude | placeContext.geo._模式.longitude | 数字 | <!-- MISSING --> |
| post_page_事件 | web.webInteraction.type | 字符串 | 在图像请求中发送的点击类型（标准点击、下载链接、退出链接或单击的自定义链接）。 |
| post_page_事件 | web.webInteraction.linkClicks.value | 数字 | 在图像请求中发送的点击类型（标准点击、下载链接、退出链接或单击的自定义链接）。 |
| post_page_事件_var1 | web.webInteraction.URL | 字符串 | 此变量仅用于链接跟踪图像请求。 这是下载链接、退出链接或单击的自定义链接的URL。 |
| post_page_事件_var2 | web.webInteraction.name | 字符串 | 此变量仅用于链接跟踪图像请求。 这将是链接的自定义名称。 |
| post_page_type | web.webPageDetails.isErrorPage | 布尔 | 它用于填充“找不到页面”维。 此变量应为空或包含“ErrorPage” |
| post_pagename_no_url | web.webPageDetails.pageViews.value | 数字 | 页面的名称（如果设置）。 如果未指定页面，则此值将留空。 |
| post_product_列表 | productListItems[].items | 阵列 | 产品列表，通过产品变量传递。 | {SKU（字符串）, quantity(integer), priceTotal(number)} |
| post_search_engine | search.searchEngine | 字符串 | 表示将访客引用到站点的搜索引擎的数字ID。 |
| mvvar1_instances | .列表.items[] | 对象 | 列表变量值。 包含自定义值的分隔列表，具体取决于实现。 |
| mvvar2_instances | .列表.items[] | 对象 | 列表变量值。 包含自定义值的分隔列表，具体取决于实现。 |
|  | mvvar3_instances | .列表.items[] | 对象 | 列表变量值。 包含自定义值的分隔列表，具体取决于实现。 |
| 颜色 | device.colorDepth | 整数 | 颜色深度ID，基于c_color列的值。 |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | 字符串 | 数字ID，表示推荐人的第一个推荐人的访客类型。 |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | 整数 | 在Unix时间中访客的首次点击的时间戳。 |
| geo_country | placeContext.geo.countryCode | 字符串 | 根据IP，受到打击的国家的缩写。 |
| geo_latitude | placeContext.geo._模式.latitude | 数字 | <!-- MISSING --> |
| geo_longitude | placeContext.geo._模式.longitude | 数字 | <!-- MISSING --> |
| paid_search | search.isPaid | 布尔 | 在点击与付费搜索检测匹配时设置的标记。 |
| ref_type | web.webReferrer.type | 字符串 | 表示点击的参照类型的数字ID。 |
| visit_paid_search | _experience.analytics.session.search.isPaid | 布尔 | 一个标志（1=付费，0=未付费），指示访问的第一次点击是否来自付费搜索点击。 |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | 字符串 | 表示访问第一个推荐人的推荐人类型的数字ID。 |
| visit_search_engine | _experience.analytics.session.search.searchEngine | 字符串 | 访问的第一个搜索引擎的数字ID。 |
| visit_开始_time_gmt | _experience.analytics.session.timestamp | 整数 | 在Unix时间中首次点击访问的时间戳。 |
