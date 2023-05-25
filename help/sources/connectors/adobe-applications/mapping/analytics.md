---
keywords: Experience Platform；主页；热门主题；Analytics映射字段；Analytics映射
solution: Experience Platform
title: Adobe Analytics源连接器的映射字段
description: Adobe Experience Platform允许您通过Analytics源摄取Adobe Analytics数据。 通过ADC摄取的某些数据可以直接从Analytics字段映射到体验数据模型(XDM)字段，而其他数据需要转换和特定功能才能成功映射。
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '3419'
ht-degree: 15%

---

# Analytics字段映射

Adobe Experience Platform允许您通过Analytics源摄取Adobe Analytics数据。 通过ADC摄取的某些数据可以直接从Analytics字段映射到体验数据模型(XDM)字段，而其他数据需要转换和特定功能才能成功映射。

![](../images/analytics-data-experience-platform.png)

## 直接映射字段

选择字段直接从Adobe Analytics映射到Experience Data Model (XDM)。

下表包含显示Analytics字段名称的列(*分析字段*)，则相应的XDM字段(*XDM字段*)及其类型(*XDM类型*)以及字段的描述(*描述*)。

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| Analytics 字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字符串 | 一个自定义变量，其范围可以是1-250。 每个组织将使用不同的这些自定义eVar。 |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | 字符串 | 自定义流量变量，其范围可以是1-75。 |
| m_browser | _experience.analytics.environment.browserID | 整数 | 浏览器的编号ID。 |
| m_browser_height | environment.browserDetails.viewportHeight | 整数 | 浏览器的高度（像素）。 |
| m_browser_width | environment.browserDetails.viewportWidth | 整数 | 浏览器的宽度（像素）。 |
| m_campaign | marketing.trackingCode | 字符串 | 在跟踪代码维度中使用的变量。 |
| m_channel | web.webPageDetails.siteSection | 字符串 | 在“网站区域”维度中使用的变量。 |
| m_domain | environment.domain | 字符串 | 在域维度中使用的变量。 这将基于用户的互联网服务提供商(ISP)。 |
| m_geo_city | placeContext.geo.city | 字符串 | 点击所在城市的名称。 这是基于点击的IP地址得出的。 |
| m_geo_dma | placeContext.geo.dmaID | 整数 | 点击的人口统计区域的数值ID。 这是基于点击的IP地址得出的。 |
| m_geo_region | placeContext.geo.stateProvince | 字符串 | 点击所在州或地区的名称。 这是基于点击的IP地址得出的。 |
| m_geo_zip | placeContext.geo.postalCode | 字符串 | 点击的邮政编码。 这是基于点击的IP地址得出的。 |
| m_keywords | search.keywords | 字符串 | 在“关键字”维度中使用的变量。 |
| m_os | _experience.analytics.environment.operatingSystemID | 整数 | 表示访客的操作系统的数值ID。 这是基于user_agent列进行的。 |
| m_page_url | web.webPageDetails.URL | 字符串 | 页面点击的URL。 |
| m_pagename_no_url | web.webPageDetails.</span>name | 字符串 | 用于填充页面维度的变量。 |
| m_referrer | web.webReferrer.URL | 字符串 | 上一页的页面URL。 |
| m_search_page_num | search.pageDepth | 整数 | 供所有搜索网页排名维度使用。指示用户在点击进入您的网站之前您的网站出现在搜索结果的哪一页。 |
| m_state | _experience.analytics.customDimensions.stateProvince | 字符串 | 状态变量。 |
| m_user_server | web.webPageDetails.server | 字符串 | 在服务器维度中使用的变量。 |
| m_zip | _experience.analytics.customDimensions.postalCode | 字符串 | 用于填充邮政编码维度的变量。 |
| accept_language | environment.browserDetails.acceptLanguage | 字符串 | 列出所有接受的语言，如Accept-Language HTTP标头所示。 |
| homepage | web.webPageDetails.isHomePage | 布尔 | 已不再使用。指示当前URL是否为浏览器的主页。 |
| ipv6 | environment.ipV6 | 字符串 |
| j_jscript | environment.browserDetails.javaScriptVersion | 字符串 | 浏览器支持的JavaScript版本。 |
| user_agent | environment.browserDetails.userAgent | 字符串 | HTTP标头中发送的用户代理字符串。 |
| mobileappid | 应用程序。</span>name | 字符串 | 移动设备应用程序ID，按以下格式存储： `[AppName][BundleVersion]`. |
| mobiledevice | device.model | 字符串 | 移动设备的名称。 在iOS上，它存储为逗号分隔的2位字符串。 第一个数字表示设备代，第二个数字表示设备系列。 |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | 字符串 | 由Mobile Services使用。 表示目标点。 |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | 数字 | 由Mobile Services使用。 表示兴趣点距离。 |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | 数字 | 从上下文数据变量 a.loc.acc 收集。指示收集时 GPS 的精度（以米为单位）。 |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | 字符串 | 从上下文数据变量 a.loc.category 收集。描述特定位置的类别。 |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | 字符串 | 从上下文数据变量a.loc.id收集。 给定目标点的标识符。 |
| video | media.mediaTimed.primaryAssetReference._id | 字符串 |  视频的名称。 |
| videoad | advertising.adAssetReference._id | 字符串 | 广告资源的标识符。 |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | 字符串 | 视频内容类型。 对于所有视频查看，此参数自动设置为“视频”。 |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | 字符串 | 视频广告所在的面板。 |
| videoadinpod | advertising.adAssetViewDetails.index | 整数 | 视频广告在面板中的位置。 |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | 字符串 | 视频播放器的名称。 |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | 字符串 | 视频频道。 |
| videoadplayername | advertising.adAssetViewDetails.playerName | 字符串 | 视频广告播放器的名称。 |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | 字符串 | 视频章节的名称 |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | 字符串 | 视频名称。 |
| videoadname | advertising.adAssetReference._dc.title | 字符串 | 视频广告的名称。 |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | 字符串 | 视频表演. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | 字符串 | 视频季。 |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | 字符串 | 视频剧集. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | 字符串 | 视频网络. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | 字符串 | 视频表演类型. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | 字符串 | 视频广告加载. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | 字符串 | 视频馈送类型. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | 数字 | Mobile Services 信标主要. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | 数字 | Mobile Services 信标次要. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | 字符串 | Mobile Services 信标 UUID. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | 字符串 | 视频会话ID。 |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | 数组 | 视频流派. | {title（对象）、description（对象）、type（对象）、meta：xdmType（对象）、items（字符串）、meta：xdmField（对象）} |
| mobileinstalls | application.firstLaunches | 对象 | 安装或重新安装后首次运行时会触发此事件 | {id （字符串），值（数字）} |
| mobileupgrades | application.upgrades | 对象 | 报告应用程序升级次数。 升级后或每当版本号更改时，在首次运行时触发。 | {id （字符串），值（数字）} |
| mobilelaunches | application.launches | 对象 | 应用程序已启动的次数。 | {id （字符串），值（数字）} |
| mobilecrashes | application.crashes | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| mobilemessageclicks | directMarketing.clicks | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videotime | media.mediaTimed.timePlayed | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videostart | media.mediaTimed.impressions | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videocomplete | media.mediaTimed.completes | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoadstart | advertising.impressions | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoadcomplete | advertising.completes | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoadtime | advertising.timePlayed | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoplay | media.mediaTimed.starts | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videototaltime | media.mediaTimed.totalTimePlayed | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | 对象 | 视频品质开始时间。 | {id （字符串），值（数字）} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | 对象 | 视频品质：缓冲计数 | {id （字符串），值（数字）} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | 对象 | 视频品质：缓冲时间 | {id （字符串），值（数字）} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | 对象 | 视频品质：比特率变化计数 | {id （字符串），值（数字）} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | 对象 | 视频品质：平均比特率 | {id （字符串），值（数字）} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | 对象 | 视频品质：错误计数 | {id （字符串），值（数字）} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoprogress10 | media.mediaTimed.progress10 | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoprogress25 | media.mediaTimed.progress25 | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoprogress50 | media.mediaTimed.progress50 | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoprogress75 | media.mediaTimed.progress75 | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoprogress95 | media.mediaTimed.progress95 | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videoresume | media.mediaTimed.resumes | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videopausecount | media.mediaTimed.pauses | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videopausetime | media.mediaTimed.pauseTime | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| videosecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | 整数 |

{style="table-layout:auto"}

## 拆分映射字段

这些字段只有一个源，但映射到 **多个** xdm位置。

| Analytics 字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth， device.screenHeight | 整数 | 表示显示器分辨率的数值 ID。 |
| mobileosversion | environment.operatingSystem， environment.operatingSystemVersion | 字符串 | 移动设备操作系统版本。 |
| videoadlength | advertising.adAssetReference._xmpDM.duration | 整数 | 视频广告长度。 |

{style="table-layout:auto"}

## 生成的映射字段

来自ADC的选择字段需要转换，这需要Adobe Analytics直接复制以外的逻辑才能在XDM中生成。

下表包含显示Analytics字段名称的列(*分析字段*)，则相应的XDM字段(*XDM字段*)及其类型(*XDM类型*)以及字段的描述(*描述*)。

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| Analytics 字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 对象 | 自定义流量变量，范围从1到75 | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | 对象 | 由层次结构变量使用。 它包含 | 分隔的值列表。 | {values (array)， delimiter (string)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 数组 | 变量值的列表。 包含分隔的自定义值列表，具体取决于实施 | {value (string)， key (string)} |
| m_color | device.colorDepth | 整数 | 颜色深度ID，它基于c_color列的值。 |
| m_cookies | environment.browserDetails.cookiesEnabled | 布尔 | 在“Cookie支持”维度中使用的变量。 |
| m_event_list | commerce.purchases、commerce.productViews、commerce.productListOpens、commerce.checkouts、commerce.productListAdds、commerce.productListRemovals、commerce.productListViews | 对象 | 点击时触发的标准商务事件。 | {id （字符串），值（数字）} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100， _experience.analytics.event101to200.event200， _experience.analytics.event201to300.event201 - _experience.analytics.event201to300， _experience.event 301to400.event301 - _experience.analytics.event301to400.event400， _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500， _experience.analytics.event501to600 0， _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700， _experience.analytics.event701to800.event701 - _experience.analytics.event801to900， _experience.analytics.event801 0.event900， _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | 对象 | 点击时触发的自定义事件。 | {id （对象），值（对象）} |
| m_geo_country | placeContext.geo.countryCode | 字符串 | 点击来源国家/地区的缩写，基于IP地址。 |
| m_geo_latitude | placeContext.geo._架构.latitude | 数字 | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._架构.longitude | 数字 | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | 布尔 | 指示Java是否已启用的标记。 |
| m_latitude | placeContext.geo._架构.latitude | 数字 | <!-- MISSING --> |
| m_longitude | placeContext.geo._架构.longitude | 数字 | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | 字符串 | 仅在链接跟踪图像请求中使用的变量。 此变量包含下载链接、退出链接或单击的自定义链接的URL。 |
| m_page_event_var2 | web.webInteraction.name | 字符串 | 仅在链接跟踪图像请求中使用的变量。 这会列出链接的自定义名称（如果已指定）。 |
| m_page_type | web.webPageDetails.isErrorPage | 布尔 | 用于填充页面未找到维度的变量。 此变量应为空或包含“ErrorPage”。 |
| m_pagename_no_url | web.webPageDetails.pageViews.value | 数字 | 页面的名称（如果已设置）。 如果没有指定页面，此值将留空。 |
| m_paid_search | search.isPaid | 布尔 | 如果点击与付费搜索检测相匹配，则设置的标记。 |
| m_product_list | productListItems[].items | 数组 | 产品列表，通过products变量传入。 | {SKU （字符串）、数量（整数）、价格总计（数字）} |
| m_ref_type | web.webReferrer.type | 字符串 | 表示点击的反向链接类型的数值 ID。1表示网站内部，2表示其他网站，3表示搜索引擎，4表示硬盘，5表示用户端网络，6表示键入/书签式（无反向链接），7表示电子邮件，8表示无JavaScript，9表示社交网络。 |
| m_search_engine | search.searchEngine | 字符串 | 表示将访客引荐至您的网站的搜索引擎的数值ID。 |
| post_currency | commerce.order.currencyCode | 字符串 | 交易过程中使用的货币代码。 |
| post_cust_hit_time_gmt | timestamp | 字符串 | 这仅在启用了时间戳的数据集中使用。 这是随it一起发送的时间戳，基于Unix时间。 |
| post_cust_visid | identitymap | 对象 | 客户访客ID。 |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | 布尔 | 客户访客ID。 |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | 字符串 | 客户访客ID。 |
| post_visid_high + visid_low | identitymap | 对象 | 访问的唯一标识符。 |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | 字符串 | 访问的唯一标识符。 |
| post_visid_high | endUserIDs._experience.aaid.primary | 布尔 | 与visid_low结合使用，用来唯一标识访问。 |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | 字符串 | 与visid_low结合使用，用来唯一标识访问。 |
| post_visid_low | identitymap | 对象 | 与visid_high结合使用，用来唯一标识访问。 |
| hit_time_gmt | receivedTimestamp | 字符串 | 点击的时间戳，基于Unix时间。 |
| hitid_high + hitid_low | _id | 字符串 | 用于标识点击的唯一标识符。 |
| hitid_low | _id | 字符串 | 与hitid_high结合使用，用来唯一标识点击。 |
| IP | environment.ipV4 | 字符串 | IP地址，基于图像请求的HTTP标头。 |
| j_jscript | environment.browserDetails.javaScriptEnabled | 布尔 | 使用的JavaScript版本。 |
| mcvisid_high + mcvisid_low | identitymap | 对象 | Experience Cloud的访客ID。 |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | 字符串 | Experience CloudID (ECID)也称为MCID，有时用于命名空间。 |
| mcvisid_high | endUserIDs._体验.mcid.primary | 布尔 | Experience CloudID (ECID)也称为MCID，有时用于命名空间。 |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | 字符串 | Experience CloudID (ECID)也称为MCID，有时用于命名空间。 |
| mcvisid_low | identitymap | 对象 | Experience Cloud的访客ID。 |
| sdid_high + sdid_low | _experience.target.supplementalDataID | 字符串 | 点击拼接ID。 分析字段sdid_high和sdid_low是用于拼合两个（或更多）传入点击的补充数据ID。 |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | 字符串 | Mobile Services 信标邻近性. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | 整数 | 视频章节的名称。 |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | 整数 | 视频的长度。 |

{style="table-layout:auto"}

## 高级映射字段

选择字段（称为“后值”）需要更高级的转换，然后才能成功从Adobe Analytics字段映射到体验数据模型(XDM)。 执行这些高级转换涉及使用Adobe Experience Platform查询服务和预建函数(称为Adobe定义的函数)进行会话处理、归因和重复数据删除。

要了解有关使用查询服务执行此转换的更多信息，请访问 [Adobe定义的函数](../../../../query-service/sql/adobe-defined-functions.md) 文档。

下表包含显示Analytics字段名称的列(*分析字段*)，则相应的XDM字段(*XDM字段*)及其类型(*XDM类型*)以及字段的描述(*描述*)。

>[!NOTE]
>
>请向左/向右滚动以查看表格的全部内容。

| Analytics 字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | 字符串 | 一个自定义变量，其范围可以是1-250。 每个组织将使用不同的这些自定义eVar。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | 字符串 | 自定义流量变量，其范围可以是1-75。 |
| post_browser_height | environment.browserDetails.viewportHeight | 整数 | 浏览器的高度（像素）。 |
| post_browser_width | environment.browserDetails.viewportWidth | 整数 | 浏览器的宽度（像素）。 |
| post_campaign | marketing.trackingCode | 字符串 | 在跟踪代码维度中使用的变量。 |
| post_channel | web.webPageDetails.siteSection | 字符串 | 在“网站区域”维度中使用的变量。 |
| post_cust_visid | endUserIDs._experience.aacustomid.id | 字符串 | 自定义访客ID（如果已设置）。 |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | 字符串 | 访客访问到的第一个页面的URL。 |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | 字符串 | 在原始登入页面维度中使用的变量。 访客的登录页面的页面名称。 |
| post_keywords | search.keywords | 字符串 | 为点击收集的关键字。 |
| post_page_url | web.webPageDetails.URL | 字符串 | 页面点击的URL。 |
| post_pagename_no_url | web.webPageDetails.name | 字符串 | 用于填充页面维度的变量。 |
| post_purchaseid | commerce.order.purchaseID | 字符串 | 用于唯一标识购买的变量。 |
| post_referrer | web.webReferrer.URL | 字符串 | 上一页的URL。 |
| post_state | _experience.analytics.customDimensions.stateProvince | 字符串 | 状态变量。 |
| post_user_server | web.webPageDetails.server | 字符串 | 在服务器维度中使用的变量。 |
| post_zip | _experience.analytics.customDimensions.postalCode | 字符串 | 用于填充邮政编码维度的变量。 |
| 浏览器 | _experience.analytics.environment.browserID | 整数 | 浏览器的数值ID。 |
| 域 | environment.domain | 字符串 | 在域维度中使用的变量。 这将基于用户的互联网服务提供商(ISP)。 |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | 字符串 | 访客的第一个反向链接URL。 |
| geo_city | placeContext.geo.city | 字符串 | 点击所在城市的名称。 这是基于点击的IP地址得出的。 |
| geo_dma | placeContext.geo.dmaID | 整数 | 点击的人口统计区域的数值ID。 这是基于点击的IP地址得出的。 |
| geo_region | placeContext.geo.stateProvince | 字符串 | 点击所在州或地区的名称。 这是基于点击的IP地址得出的。 |
| geo_zip | placeContext.geo.postalCode | 字符串 | 点击的邮政编码。 这是基于点击的IP地址得出的。 |
| 操作系统 | _experience.analytics.environment.operatingSystemID | 整数 | 表示访客的操作系统的数值ID。 这是基于user_agent列进行的。 |
| search_page_num | search.pageDepth | 整数 | 此变量由所有搜索页面排名维度使用，并指示您网站的搜索结果页面 | 在用户点击进入您的网站之前出现在。 |
| visit_keywords | _experience.analytics.session.search.keywords | 字符串 | 在搜索关键字维度中使用的变量。 |
| visit_num | _experience.analytics.session.num | 整数 | 在访问数量维度中使用的变量。 此值从1开始，每当新访问开始时（每个用户），该值就会递增。 |
| visit_page_num | _experience.analytics.session.depth | 整数 | 在点击深度维度中使用的变量。 对于用户生成的每次点击，该值都会增加1，并在每次访问后重置。 |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | 字符串 | 访问的第一个反向链接。 |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | 整数 | 访问的第一个页面名称。 |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | 对象 | 自定义流量变量 1 至 75。 |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | 对象 | 由层次结构变量使用，并包含分隔的值列表。 | {values (array)， delimiter (string)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | 数组 | 变量值的列表。 包含分隔的自定义值列表，具体取决于实施。 | {value (string)， key (string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | 布尔 | 在“Cookie 支持”维度中使用的变量。 |
| post_event_list | commerce.purchases、commerce.productViews、commerce.productListOpens、commerce.checkouts、commerce.productListAdds、commerce.productListRemovals、commerce.productListViews | 对象 | 点击时触发的标准商务事件。 | {id （字符串），值（数字）} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100， _experience.analytics.event101to200.event200， _experience.analytics.event201to300.event201 - _experience.analytics.event201to300， _experience.event 301to400.event301 - _experience.analytics.event301to400.event400， _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500， _experience.analytics.event501to600 0， _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700， _experience.analytics.event701to800.event701 - _experience.analytics.event801to900， _experience.analytics.event801 0.event900， _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | 对象 | 点击时触发的自定义事件。 | {id （对象），值（对象）} |
| post_java_enabled | environment.browserDetails.javaEnabled | 布尔 | 指示Java是否已启用的标记。 |
| post_latitude | placeContext.geo._架构.latitude | 数字 | <!-- MISSING --> |
| post_longitude | placeContext.geo._架构.longitude | 数字 | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | 字符串 | 在图像请求中发送的点击类型（标准点击、下载链接、退出链接或单击的自定义链接）。 |
| post_page_event | web.webInteraction.linkClicks.value | 数字 | 在图像请求中发送的点击类型（标准点击、下载链接、退出链接或单击的自定义链接）。 |
| post_page_event_var1 | web.webInteraction.URL | 字符串 | 此变量仅用于链接跟踪图像请求。 这是下载链接、退出链接或单击的自定义链接的URL。 |
| post_page_event_var2 | web.webInteraction.name | 字符串 | 此变量仅用于链接跟踪图像请求。 这将是链接的自定义名称。 |
| post_page_type | web.webPageDetails.isErrorPage | 布尔 | 用于填充“页面未找到”维度。 此变量应为空或包含“ErrorPage” |
| post_pagename_no_url | web.webPageDetails.pageViews.value | 数字 | 页面的名称（如果已设置）。 如果没有指定页面，此值将留空。 |
| post_product_list | productListItems[].items | 数组 | 产品列表，通过products变量传入。 | {SKU （字符串）、数量（整数）、价格总计（数字）} |
| post_search_engine | search.searchEngine | 字符串 | 表示将访客引荐至您的网站的搜索引擎的数值ID。 |
| mvvar1_instances | .list.items[] | 对象 | 变量值的列表。 包含分隔的自定义值列表，具体取决于实施。 |
| mvvar2_instances | .list.items[] | 对象 | 变量值的列表。 包含分隔的自定义值列表，具体取决于实施。 |
|  | mvvar3_instances | .list.items[] | 对象 | 变量值的列表。 包含分隔的自定义值列表，具体取决于实施。 |
| 颜色 | device.colorDepth | 整数 | 颜色深度ID，基于c_color列的值。 |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | 字符串 | 数值ID，表示访客第一个反向链接的反向链接类型。 |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | 整数 | 访客第一次点击的时间戳（基于 Unix 时间）。 |
| geo_country | placeContext.geo.countryCode | 字符串 | 点击来源国家/地区的缩写，基于 IP 地址。 |
| geo_latitude | placeContext.geo._架构.latitude | 数字 | <!-- MISSING --> |
| geo_longiture | placeContext.geo._架构.longitude | 数字 | <!-- MISSING --> |
| paid_search | search.isPaid | 布尔 | 如果点击与付费搜索检测相匹配，则设置的标记。 |
| ref_type | web.webReferrer.type | 字符串 | 表示点击的反向链接类型的数字 ID。 |
| visit_paid_search | _experience.analytics.session.search.isPaid | 布尔 | 指示访问的第一次点击是否来自付费搜索点击的标志（1=付费，0=未付费）。 |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | 字符串 | 表示访问中使用的第一个反向链接的反向链接类型的数值 ID。 |
| visit_search_engine | _体验分析.session.search.searchEngine | 字符串 | 表示访问中使用的第一个搜索引擎的数值 ID。 |
| visit_start_time_gmt | _experience.analytics.session.timestamp | 整数 | 访问第一次点击的时间戳（以Unix时间表示）。 |

{style="table-layout:auto"}