---
keywords: Analytics映射字段；Analytics映射
solution: Experience Platform
title: Adobe Analytics Source连接器的映射字段
description: 使用Adobe Analytics Source Connector将Analytics字段映射到XDM字段。
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 15d63db308ea9d2daf7660b463785d04ff94e296
workflow-type: tm+mt
source-wordcount: '2415'
ht-degree: 8%

---

# Analytics字段映射

Adobe Experience Platform允许您通过Analytics源摄取Adobe Analytics数据。 通过ADC摄取的某些数据可以直接从Analytics字段映射到体验数据模型(XDM)字段，而其他数据需要转换和特定函数才能成功映射。

![](../images/analytics-data-experience-platform.png)

## 直接映射字段

选择字段直接从Adobe Analytics映射到Experience Data Model (XDM)。

| Analytics字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ---------- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 字符串 | 自定义Analytics eVar。 每个组织可以以不同的方式使用eVar。 |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 字符串 | 自定义Analytics prop。 每个组织可以有不同的方式使用prop。 |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | 整数 | 浏览器的编号ID。 |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | 整数 | 浏览器的高度（像素）。 |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | 整数 | 浏览器的宽度（像素）。 |
| `m_campaign` | `marketing.trackingCode` | 字符串 | 在跟踪代码维度中使用的变量。 |
| `m_channel` | `web.webPageDetails.siteSection` | 字符串 | 在“网站区域”维度中使用的变量。 |
| `m_domain` | `environment.domain` | 字符串 | 在域维度中使用的变量。 它基于用户的互联网服务提供商(ISP)。 |
| `m_geo_city` | `placeContext.geo.city` | 字符串 | 点击所在城市的名称。 这是基于点击的IP地址。 |
| `m_geo_dma` | `placeContext.geo.dmaID` | 整数 | 点击人口统计区的数值ID。 这是基于点击的IP地址。 |
| `m_geo_region` | `placeContext.geo.stateProvince` | 字符串 | 点击所在州或地区的名称。 这是基于点击的IP地址。 |
| `m_geo_zip` | `placeContext.geo.postalCode` | 字符串 | 点击的邮政编码。 这是基于点击的IP地址。 |
| `m_keywords` | `search.keywords` | 字符串 | 在“关键字”维度中使用的变量。 |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 整数 | 表示访客的操作系统的数值ID。 这是基于user_agent列的。 |
| `m_page_url` | `web.webPageDetails.URL` | 字符串 | 页面点击的URL。 |
| `m_pagename` | `web.webPageDetails.pageViews.value` | 字符串 | 具有页面名称的点击上等于1。 这类似于Adobe Analytics页面查看次数量度。 |
| `m_referrer` | `web.webReferrer.URL` | 字符串 | 上一页的页面URL。 |
| `m_search_page_num` | `search.pageDepth` | 整数 | 供所有搜索页面排名维度使用。 指示用户在点击进入您的网站之前您的网站出现在搜索结果的哪个页面。 |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 字符串 | 状态变量。 |
| `m_user_server` | `web.webPageDetails.server` | 字符串 | 在服务器维度中使用的变量。 |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 字符串 | 用于填充邮政编码维度的变量。 |
| `accept_language` | `environment.browserDetails.acceptLanguage` | 字符串 | 列出所有接受的语言，如Accept-Language HTTP标头所示。 |
| `homepage` | `web.webPageDetails.isHomePage` | 布尔 | 已不再使用。 指示当前URL是否为浏览器的主页。 |
| `ipv6` | `environment.ipV6` | 字符串 |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | 字符串 | 浏览器支持的JavaScript版本。 |
| `user_agent` | `environment.browserDetails.userAgent` | 字符串 | HTTP标头中发送的用户代理字符串。 |
| `mobileappid` | `application.name` | 字符串 | 移动设备应用程序ID，以下列格式存储： `[AppName][BundleVersion]`。 |
| `mobiledevice` | `device.model` | 字符串 | 移动设备的名称。 在iOS上，它存储为逗号分隔的2位字符串。 第一个数字代表第几代设备，第二个数字代表设备系列。 |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | 字符串 | 由Mobile Services使用。 表示目标点。 |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | 数字 | 由Mobile Services使用。 表示兴趣点距离。 |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | 数字 | 从上下文数据变量a.loc.acc收集。 指示GPS在收集时的精度（以米为单位）。 |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | 字符串 | 从上下文数据变量a.loc.category收集。 描述特定位置的类别。 |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | 字符串 | 从上下文数据变量a.loc.id收集。 给定目标点的标识符。 |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | 字符串 | 视频的名称。 |
| `videoad` | `advertising.adAssetReference._id` | 字符串 | 广告资源的标识符。 |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | 字符串 | 视频内容类型。 对于所有视频查看，此参数自动设置为“视频”。 |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | 字符串 | 视频广告所在的面板。 |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | 整数 | 视频广告在面板中的位置。 |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | 字符串 | 视频播放器的名称。 |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | 字符串 | 视频频道。 |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | 字符串 | 视频广告播放器的名称。 |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | 字符串 | 视频章节的名称 |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | 字符串 | 视频名称。 |
| `videoadname` | `advertising.adAssetReference._dc.title` | 字符串 | 视频广告的名称。 |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | 字符串 | 视频节目。 |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | 字符串 | 视频季。 |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | 字符串 | 视频剧集。 |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | 字符串 | 视频网络。 |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | 字符串 | 视频节目类型。 |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | 字符串 | 视频广告加载。 |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | 字符串 | 视频馈送类型。 |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | 数字 | Mobile Services信标主要。 |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | 数字 | Mobile Services信标次要。 |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | 字符串 | 移动服务信标UUID。 |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | 字符串 | 视频会话ID |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | 数组 | 视频流派。 | {title（对象）、description（对象）、type（对象）、meta：xdmType（对象）、items（字符串）、meta：xdmField（对象）} |
| `mobileinstalls` | `application.firstLaunches` | 对象 | 在安装或重新安装后首次运行时会触发此事件 | {id （字符串），值（数字）} |
| `mobileupgrades` | `application.upgrades` | 对象 | 报告应用程序升级次数。 升级后或版本号更改后首次运行时触发。 | {id （字符串），值（数字）} |
| `mobilelaunches` | `application.launches` | 对象 | 应用程序已启动的次数。 | {id （字符串），值（数字）} |
| `mobilecrashes` | `application.crashes` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `mobilemessageclicks` | `directMarketing.clicks` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videotime` | `media.mediaTimed.timePlayed` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videostart` | `media.mediaTimed.impressions` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videocomplete` | `media.mediaTimed.completes` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoadstart` | `advertising.impressions` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoadcomplete` | `advertising.completes` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoadtime` | `advertising.timePlayed` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoplay` | `media.mediaTimed.starts` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | 对象 | 视频品质：开始时间。 | {id （字符串），值（数字）} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | 对象 | 视频品质：缓冲计数 | {id （字符串），值（数字）} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | 对象 | 视频品质：缓冲时间 | {id （字符串），值（数字）} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | 对象 | 视频品质：变化计数 | {id （字符串），值（数字）} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | 对象 | 视频品质：平均比特率 | {id （字符串），值（数字）} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | 对象 | 视频品质：错误计数 | {id （字符串），值（数字）} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoprogress10` | `media.mediaTimed.progress10` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoprogress25` | `media.mediaTimed.progress25` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoprogress50` | `media.mediaTimed.progress50` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoprogress75` | `media.mediaTimed.progress75` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoprogress95` | `media.mediaTimed.progress95` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videoresume` | `media.mediaTimed.resumes` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videopausecount` | `media.mediaTimed.pauses` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videopausetime` | `media.mediaTimed.pauseTime` | 对象 | <!-- MISSING --> | {id （字符串），值（数字）} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | 整数 |

{style="table-layout:auto"}

## 拆分映射字段

这些字段具有单个源，但映射到&#x200B;**多个** XDM位置。

| Analytics字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`，<br/>`device.screenHeight` | 整数 | 表示显示器分辨率的数值ID。 |
| `mobileosversion` | `environment.operatingSystem`，<br/>`environment.operatingSystemVersion` | 字符串 | 移动设备操作系统版本。 |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | 整数 | 视频广告长度。 |

{style="table-layout:auto"}

## 生成的映射字段

必须转换来自ADC的选择字段，这要求在XDM中生成来自Adobe Analytics的直接副本以外的逻辑。

| Analytics字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 对象 | 自定义Analytics属性，配置为列表属性。 它包含分隔的值列表。 | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 对象 | 由层次结构变量使用。 它包含分隔的值列表。 | {values (array)， delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 数组 | 自定义Analytics列表变量。 包含分隔的值列表。 | {值（字符串），键（字符串）} |
| `m_color` | `device.colorDepth` | 整数 | 颜色深度ID，它基于c_color列的值。 |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | 布尔 | 在“Cookie支持”维度中使用的变量。 |
| `m_event_list` | `commerce.purchases`，<br/>`commerce.productViews`，<br/>`commerce.productListOpens`，<br/>`commerce.checkouts`，<br/>`commerce.productListAdds`，<br/>`commerce.productListRemovals`，<br/>`commerce.productListViews` | 对象 | 点击时触发的标准商务事件。 | {id （字符串），值（数字）} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 对象 | 点击时触发的自定义事件。 | {id（对象），值（对象）} |
| `m_geo_country` | `placeContext.geo.countryCode` | 字符串 | 点击来源国家/地区的缩写，基于IP地址。 |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | 数字 | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | 数字 | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | 布尔 | 指示Java™是否已启用的标记。 |
| `m_latitude` | `placeContext.geo._schema.latitude` | 数字 | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | 数字 | <!-- MISSING --> |
| `m_page_event_var1` | `web.webInteraction.URL` | 字符串 | 仅在链接跟踪图像请求中使用的变量。 此变量包含下载链接、退出链接或单击的自定义链接的URL。 |
| `m_page_event_var2` | `web.webInteraction.name` | 字符串 | 仅在链接跟踪图像请求中使用的变量。 这会列出链接的自定义名称（如果已指定）。 |
| `m_page_type` | `web.webPageDetails.isErrorPage` | 布尔 | 用于填充页面未找到维度的变量。 此变量应为空或包含“ErrorPage”。 |
| `m_pagename_no_url` | `web.webPageDetails.name` | 数字 | 页面的名称（如果已设置）。 如果未指定页面，此值将留空。 |
| `m_paid_search` | `search.isPaid` | 布尔 | 如果点击与付费搜索检测相匹配，则设置此标记。 |
| `m_product_list` | `productListItems[].items` | 数组 | 产品列表，通过products变量传入。 | {SKU （字符串）、数量（整数）、价格总计（数字）} |
| `m_ref_type` | `web.webReferrer.type` | 字符串 | 表示点击的反向链接类型的数值ID。<br/>`1`：网站内<br/>`2`：其他网站<br/>`3`：搜索引擎<br/>`4`：硬盘<br/>`5`：未发送<br/>`6`：已输入/添加书签（无反向链接）<br/>`7`：电子邮件<br/>`8`：无JavaScript<br/>`9`：社交网络 |
| `m_search_engine` | `search.searchEngine` | 字符串 | 表示将访客引荐至您的网站的搜索引擎的数值ID。 |
| `post_currency` | `commerce.order.currencyCode` | 字符串 | 交易期间使用的货币代码。 |
| `post_cust_hit_time_gmt` | `timestamp` | 字符串 | 这仅在启用了时间戳的数据集中使用。 这是随点击发送的时间戳，基于UNIX®时间。 |
| `post_cust_visid` | `identityMap` | 对象 | 客户访客ID。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | 布尔 | 客户访客ID。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | 字符串 | 客户访客ID。 |
| `post_visid_high` + `visid_low` | `identityMap` | 对象 | 访问的唯一标识符。 |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | 字符串 | 访问的唯一标识符。 |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | 布尔 | 与`visid_low`一起使用以唯一标识访问。 |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | 字符串 | 与`visid_low`一起使用以唯一标识访问。 |
| `post_visid_low` | `identityMap` | 对象 | 与visid_high结合使用，用来唯一标识访问。 |
| `hit_time_gmt` | `receivedTimestamp` | 字符串 | 点击的时间戳，基于UNIX®时间。 |
| `hitid_high` + `hitid_low` | `_id` | 字符串 | 用于标识点击的唯一标识符。 |
| `hitid_low` | `_id` | 字符串 | 与hitid_high一起使用，唯一标识点击。 |
| `ip` | `environment.ipV4` | 字符串 | IP地址，基于图像请求的HTTP标头。 |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | 布尔 | 使用的JavaScript版本。 |
| `mcvisid_high` + `mcvisid_low` | identityMap | 对象 | Experience Cloud访客ID。 |
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | 字符串 | Experience Cloud ID (ECID)也称为MCID，有时用于命名空间。 |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | 布尔 | Experience Cloud ID (ECID)也称为MCID，有时用于命名空间。 |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | 字符串 | Experience Cloud ID (ECID)也称为MCID，有时用于命名空间。 |
| `mcvisid_low` | `identityMap` | 对象 | Experience Cloud访客ID。 |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | 字符串 | 点击拼接ID。 分析字段sdid_high和sdid_low是用于拼合两个（或更多）传入点击的补充数据ID。 |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | 字符串 | Mobile Services信标邻近性。 |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | 整数 | 视频章节的名称。 |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | 整数 | 视频的长度。 |

{style="table-layout:auto"}

## 高级映射字段

在Adobe使用处理规则、VISTA规则和查找表调整其值后，选择字段（称为“post values”）将包含数据。 大多数post值具有预处理的对应项。

Analytics Source Connector将预处理的数据发送到Experience Platform的数据集中。 您可以使用转换将此数据转换为其经过后处理的对应数据。 要了解有关使用查询服务执行这些转换的更多信息，请参阅查询服务用户指南中的[Adobe定义的函数](/help/query-service/sql/adobe-defined-functions.md)。

要了解有关使用查询服务执行这些转换的更多信息，请参阅查询服务用户指南中的[Adobe定义的函数](/help/query-service/sql/adobe-defined-functions.md)。

| Analytics字段 | XDM字段 | XDM类型 | 描述 |
| --------------- | --------- | -------- | ---------- |
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 字符串 | 自定义Analytics eVar。 每个组织可以以不同的方式使用eVar。 |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 字符串 | 自定义Analytics prop。 每个组织可以有不同的方式使用prop。 |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | 整数 | 浏览器的高度（像素）。 |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | 整数 | 浏览器的宽度（像素）。 |
| `post_campaign` | `marketing.trackingCode` | 字符串 | 在跟踪代码维度中使用的变量。 |
| `post_channel` | `web.webPageDetails.siteSection` | 字符串 | 在“网站区域”维度中使用的变量。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | 字符串 | 自定义访客ID（如果已设置）。 |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | 字符串 | 访客访问到的第一个页面的URL。 |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | 字符串 | 在原始登入页面维度中使用的变量。 访客的登录页面的页面名称。 |
| `post_keywords` | `search.keywords` | 字符串 | 为点击收集的关键字。 |
| `post_page_url` | `web.webPageDetails.URL` | 字符串 | 页面点击的URL。 |
| `post_pagename` | `web.webPageDetails.pageViews.value` | 字符串 | 具有页面名称的点击上等于1。 这类似于Adobe Analytics页面查看次数量度。 |
| `post_purchaseid` | `commerce.order.purchaseID` | 字符串 | 用于唯一标识购买的变量。 |
| `post_referrer` | `web.webReferrer.URL` | 字符串 | 上一页的URL。 |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 字符串 | 状态变量。 |
| `post_user_server` | `web.webPageDetails.server` | 字符串 | 在服务器维度中使用的变量。 |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 字符串 | 用于填充邮政编码维度的变量。 |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | 整数 | 浏览器的数值ID。 |
| `domain` | `environment.domain` | 字符串 | 在域维度中使用的变量。 它基于用户的互联网服务提供商(ISP)。 |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | 字符串 | 访客的第一个反向链接URL。 |
| `geo_city` | `placeContext.geo.city` | 字符串 | 点击所在城市的名称。 这是基于点击的IP地址。 |
| `geo_dma` | `placeContext.geo.dmaID` | 整数 | 点击人口统计区的数值ID。 这是基于点击的IP地址。 |
| `geo_region` | `placeContext.geo.stateProvince` | 字符串 | 点击所在州或地区的名称。 这是基于点击的IP地址。 |
| `geo_zip` | `placeContext.geo.postalCode` | 字符串 | 点击的邮政编码。 这是基于点击的IP地址。 |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 整数 | 表示访客的操作系统的数值ID。 这是基于user_agent列的。 |
| `search_page_num` | `search.pageDepth` | 整数 | 此变量由所有搜索页面排名维度使用，它指示您网站的搜索结果页面 | 在用户点击进入您的网站之前出现在。 |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | 字符串 | 在搜索关键字维度中使用的变量。 |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | 整数 | 在访问数量维度中使用的变量。 此值从1开始，每当新访问开始（每个用户）时，该值就会递增。 |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | 整数 | 在点击深度维度中使用的变量。 对于用户生成的每次点击，此值增加1，并在每次访问后重置。 |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | 字符串 | 访问的第一个反向链接。 |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | 整数 | 访问的第一个页面名称。 |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 对象 | 自定义Analytics属性，配置为列表属性。 它包含分隔的值列表。 |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 对象 | 由层次结构变量使用并包含分隔的值列表。 | {values (array)， delimiter (string)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 数组 | 变量值的列表。 包含分隔的自定义值列表，具体取决于实施。 | {值（字符串），键（字符串）} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | 布尔 | 在“Cookie支持”维度中使用的变量。 |
| `post_event_list` | `commerce.purchases`，<br/>`commerce.productViews`，<br/>`commerce.productListOpens`，<br/>`commerce.checkouts`，<br/>`commerce.productListAdds`，<br/>`commerce.productListRemovals`，<br/>`commerce.productListViews` | 对象 | 点击时触发的标准商务事件。 | {id （字符串），值（数字）} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 对象 | 点击时触发的自定义事件。 | {id（对象），值（对象）} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | 布尔 | 指示Java™是否已启用的标记。 |
| `post_latitude` | `placeContext.geo._schema.latitude` | 数字 | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | 数字 | <!-- MISSING --> |
| `post_page_event` | `web.webInteraction.type` | 字符串 | 在图像请求中发送的点击类型（标准点击、下载链接、退出链接或单击的自定义链接）。 |
| `post_page_event` | `web.webInteraction.linkClicks.value` | 数字 | 如果点击是链接点击，则等于1。 这类似于Adobe Analytics中的“页面事件”量度。 |
| `post_page_event_var1` | `web.webInteraction.URL` | 字符串 | 此变量仅在链接跟踪图像请求中使用。 它是已单击下载链接、退出链接或自定义链接的URL。 |
| `post_page_event_var2` | `web.webInteraction.name` | 字符串 | 此变量仅在链接跟踪图像请求中使用。 它是链接的自定义名称。 |
| `post_page_type` | `web.webPageDetails.isErrorPage` | 布尔 | 用于填充未找到页面维度。 此变量应为空或包含“ErrorPage” |
| `post_pagename_no_url` | `web.webPageDetails.name` | 数字 | 页面的名称（如果已设置）。 如果未指定页面，此值将留空。 |
| `post_product_list` | `productListItems[].items` | 数组 | 产品列表，通过products变量传入。 | {SKU （字符串）、数量（整数）、价格总计（数字）} |
| `post_search_engine` | `search.searchEngine` | 字符串 | 表示将访客引荐至您的网站的搜索引擎的数值ID。 |
| `mvvar1_instances` | `.list.items[]` | 对象 | 变量值列表。 包含分隔的自定义值列表，具体取决于实施。 |
| `mvvar2_instances` | `.list.items[]` | 对象 | 变量值列表。 包含分隔的自定义值列表，具体取决于实施。 |
| `mvvar3_instances` | `.list.items[]` | 对象 | 变量值列表。 包含分隔的自定义值列表，具体取决于实施。 |
| `color` | `device.colorDepth` | 整数 | 颜色深度ID，基于c_color列的值。 |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | 字符串 | 数值ID，表示访客的第一个反向链接的反向链接类型。 |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | 整数 | 访客第一次点击的时间戳(以UNIX®时间表示)。 |
| `geo_country` | `placeContext.geo.countryCode` | 字符串 | 点击来源国家/地区的缩写，基于IP地址。 |
| `geo_latitude` | `placeContext.geo._schema.latitude` | 数字 | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | 数字 | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | 布尔 | 如果点击与付费搜索检测相匹配，则设置此标记。 |
| `ref_type` | `web.webReferrer.type` | 字符串 | 表示点击的反向链接类型的数值ID。 |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | 布尔 | 指示访问的第一次点击是否来自付费搜索点击的标志（1=付费，0=未付费）。 |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | 字符串 | 表示访问的第一个反向链接的反向链接类型的数值ID。 |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | 字符串 | 访问的第一个搜索引擎的数值ID。 |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | 整数 | 访问首次点击的时间戳(以UNIX®时间表示)。 |

{style="table-layout:auto"}