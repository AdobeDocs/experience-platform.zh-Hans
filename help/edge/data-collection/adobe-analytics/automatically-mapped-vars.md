---
title: 在Adobe Analytics自动映射变量
seo-title: 使用Adobe Experience PlatformWeb SDK在Adobe Analytics自动映射变量
description: 了解在Adobe Analytics使用Experience PlatformWeb SDK自动映射哪些变量
seo-description: 了解在Adobe Analytics使用Experience PlatformWeb SDK自动映射哪些变量
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
translation-type: tm+mt
source-git-commit: b81c0c450ddee4b0c0abedfd8ca53c3a599fb3cb
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# 自动映射到 [!DNL Analytics]

以下是Adobe Experience Platform自动映射到 [!DNL Edge Network] 的变量列表 [!DNL Analytics]。

| XDM字段路径 | [!DNL Analytics Query String] / HTTP 标头 | 描述 |
| ---------- | ------------------------- | ----------------------------------------- |
| `application.id` | `c.a.appid` | AppMeasurement上下文数 `c.a.appid` 据映射。 |
| `application.launches.value` | `c.a.launches` | AppMeasurement上下文数 `c.a.launches` 据映射。 |
| `commerce.checkouts.id` | `events` | `scCheckout` 事件序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.checkouts.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_CHECKOUT `,`。 |
| `commerce.order.currencyCode` | `cc` | AppMeasurement查询参数CURRENCY映射。 |
| `commerce.order.purchaseID` | `pi` | AppMeasurement查询参数PURCHASEID映射。 |
| `commerce.productListAdds.id` | `events` | `scAdd` 事件序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.productListAdds.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_ADD `,`。 |
| `commerce.productListOpens.id` | `events` | `scOpen` 事件序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.productListOpens.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_OPEN `,`。 |
| `commerce.productListRemovals.id` | `events` | `scRemove` 事件序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.productListRemovals.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_REMOVE `,`。 |
| `commerce.productListViews.id` | `events` | `scView` 事件序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.productListViews.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_视图 `,`。 |
| `commerce.productViews.id` | `events` | `prodView` 事件序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.productViews.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_PROD_视图 `,`。 |
| `commerce.purchases.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_PURCHASE `,`。 |
| `device.colorDepth` | `c` | AppMeasurement查询参数C_COLOR映射。 |
| `device.screenHeight` | `s` | AppMeasurement查询参数屏幕分辨率映射。 |
| `device.screenWidth` | `s` | AppMeasurement查询参数屏幕分辨率映射。 |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | 这是HTTP头映射，HEADER_ACCEPT_LANGUAGE。 |
| `environment.browserDetails.cookiesEnabled` | `k` | 转换为BOOLEAN_TO_YN的AppMeasurement查询参数COOKIE映射。 |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement查询参数JAVA_ENABLED映射，转换为BOOLEAN_TO_YN。 |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement查询参数J_JSCRIPT映射。 |
| `environment.browserDetails.userAgent` | `User-Agent` | 这是HTTP头映射，HEADER_USER_AGENT。 |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement查询参数BROWSER_HEIGHT映射。 |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement查询参数BROWSER_WIDTH映射。 |
| `environment.connectionType` | `ct` | AppMeasurement查询参数CT_CONNECT_TYPE映射。 |
| `environment.ipV4` | `X-Forwarded-For` | 这是HTTP头映射，X-FORWARDED-FOR。 |
| `identityMap.ECID.[0].id` | `mid` | AppMeasurement查询参数MID映射。 |
| `marketing.trackingCode` | `v0` | AppMeasurement查询参数活动映射。 |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | AppMeasurement上下文数据。 |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | AppMeasurement上下文数据。 |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement上下文数 `c.a.media.federated` 据映射。 |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | AppMeasurement上下文数据。 |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | AppMeasurement上下文数据。 |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | AppMeasurement上下文数据。 |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement上下文数 `c.a.media.pauseTime` 据映射。 |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement上下文数 `c.a.media.pauseCount` 据映射。 |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | AppMeasurement上下文数据。 |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement上下文数 `c.a.media.friendlyName` 据映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | AppMeasurement上下文数据。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement上下文数 `c.a.media.episode` 据映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | AppMeasurement上下文数据。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | AppMeasurement上下文数据。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement上下文数 `c.a.media.season` 据映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement上下文数 `a.media.name` 据映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement上下文数 `c.a.media.show` 据映射。 |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | 转换为VEDIO_ `c.a.media.type` SHOW_TYPE的AppMeasurement上下文数据映射。 |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | 转换为VIDEO_ `c.a.media.type` SHOW_TYPE的AppMeasurement上下文数据映射。 |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement上下文数 `c.a.media.length` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | AppMeasurement上下文数据。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement上下文数 `c.a.media.channel` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement上下文数 `c.a.contentType` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement上下文数 `c.a.media.network` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement上下文数 `c.a.media.segment` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement上下文数 `c.a.media.playerName` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement上下文数 `c.a.media.sdkVersion` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement上下文数 `c.a.media.feed` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement上下文数 `c.a.media.format` 据映射。 |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | AppMeasurement上下文数据。 |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | AppMeasurement上下文数据。 |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement上下文数 `c.a.media.resume` 据映射。 |
| `media.mediaTimed.starts.value` | `c.a.media.view` | AppMeasurement上下文数据。 |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | AppMeasurement上下文数据。 |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement上下文数 `c.a.media.timePlayed` 据映射。 |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement上下文数 `c.a.media.totalTimePlayed` 据映射。 |
| `placeContext.geo.latitude` | `lat` | AppMeasurement查询参数LATITUDE映射。 |
| `placeContext.geo.longitude` | `lon` | AppMeasurement查询参数LONGITUDE映射。 |
| `placeContext.geo.postalCode` | `zip` | AppMeasurement查询参数ZIP映射。 |
| `placeContext.geo.stateProvince` | `state` | AppMeasurement查询参数STATE映射。 |
| `productlistitems.[N]._[NAME_SPACE].*` | `products` | AppMeasurement查询参数产品销售事件/Evars映射。 |
| `productlistitems.[N].name` | `products` | AppMeasurement查询参数产品名称映射。 |
| `productlistitems.[N].priceTotal` | `products` | AppMeasurement查询参数产品价格映射。 |
| `productlistitems.[N].quantity` | `products` | AppMeasurement查询参数产品数量映射。 |
| `web.webInteraction.URL` | `pev1` | AppMeasurement查询参数PAGE_事件_VAR1映射。 |
| `web.webInteraction.name` | `pev2` | AppMeasurement查询参数PAGE_事件_VAR2映射。 |
| `web.webInteraction.type` | `pe` | `web.webInteraction.type=other` 至 `pe=lnk_o`; `web.webInteraction.type=download` 至 `pe=lnk_d`; `web.webInteraction.type=exit` to `pe=lnk_e` |
| `web.webPageDetails.URL` | `g` | AppMeasurement查询参数PAGE_URL映射。 |
| `web.webPageDetails.errorPage` | `pageType` | AppMeasurement查询参数PAGE_TYPE_FULL映射（转换ERROR_PAGE_TYPE）。 |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement查询参数HOMEPAGE映射（转换为BOOLEAN_TO_YN）。 |
| `web.webPageDetails.name` | `gn` | AppMeasurement查询参数PAGENAME映射。 |
| `web.webPageDetails.server` | `sv` | AppMeasurement查询参数USER_SERVER映射。 |
| `web.webPageDetails.siteSection` | `ch` | AppMeasurement查询参数渠道映射。 |
| `web.webReferrer.URL` | `r` | AppMeasurement查询参数推荐人映射。 |
