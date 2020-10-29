---
title: 在Adobe Analytics自动映射变量
seo-title: 使用Adobe Experience PlatformWeb SDK在Adobe Analytics自动映射变量
description: 了解在Adobe Analytics使用Experience PlatformWeb SDK自动映射哪些变量
seo-description: 了解在Adobe Analytics使用Experience PlatformWeb SDK自动映射哪些变量
keywords: adobe analytics;variables;analytics;automatic map;automatically mapped;
translation-type: tm+mt
source-git-commit: 8e3bef77b84e40c836a6279a9a3e3901565c9920
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---


# 自动映射到 [!DNL Analytics]

以下是Adobe Experience Platform自动映射到 [!DNL Edge Network] 的变量列表 [!DNL Analytics]。

| XDM字段路径 | [!DNL Analytics Query String] / HTTP 标头 | 描述 |
| ---------- | ------------------------- | ----------------------------------------- |
| `commerce.order.purchaseID` | `pi` | AppMeasurement查询参数PURCHASEID映射。 |
| `commerce.order.currencyCode` | `cc` | AppMeasurement查询参数CURRENCY映射。 |
| `commerce.purchases.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_PURCHASE `,`。 |
| `commerce.productViews.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_PROD_视图 `,`。 |
| `commerce.productListOpens.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_OPEN `,`。 |
| `commerce.productListViews.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_视图 `,`。 |
| `commerce.checkouts.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_CHECKOUT `,`。 |
| `commerce.productListAdds.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_ADD `,`。 |
| `commerce.productListRemovals.value` | `events` | AppMeasurement查询参数事件列表全部映射（使用分隔符），转换为COMMERCE_SC_REMOVE `,`。 |
| `commerce.productViews.id` | `events` | （可选）事件 `prodView` 序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.productListOpens.id` | `events` | （可选）事件 `scOpen` 序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.productListViews.id` | `events` | （可选）事件 `scView` 序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.productListAdds.id` | `events` | （可选）事件 `scAdd` 序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.productListRemovals.id` | `events` | （可选）事件 `scRemove` 序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.checkouts.id` | `events` | （可选）事件 `scCheckout` 序列化。 如果排除此字段(即，对于无序列化事件)，系统将生成它自己的ID值并分配给实体。 |
| `commerce.checkouts.id` | `events` | `scCheckout` 事件序列化. |
| `device.screenHeight` | `s` | AppMeasurement查询参数屏幕分辨率映射。 |
| `device.screenWidth` | `s` | AppMeasurement查询参数屏幕分辨率映射。 |
| `productlistitems.[N].lineitemid` | `products` | AppMeasurement查询参数产品类别映射。 |
| `productlistitems.[N].name` | `products` | AppMeasurement查询参数产品名称映射。 |
| `productlistitems.[N].quantity` | `products` | AppMeasurement查询参数产品数量映射。 |
| `productlistitems.[N].pricetotal` | `products` | AppMeasurement查询参数产品价格映射。 |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | AppMeasurement上下文数据。 |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | AppMeasurement上下文数据。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | AppMeasurement上下文数据。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | AppMeasurement上下文数据。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | AppMeasurement上下文数据。 |
| `media.mediaTimed.starts.value` | `c.a.media.view` | AppMeasurement上下文数据。 |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | AppMeasurement上下文数据。 |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | AppMeasurement上下文数据。 |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | AppMeasurement上下文数据。 |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | AppMeasurement上下文数据。 |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | AppMeasurement上下文数据。 |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | AppMeasurement上下文数据。 |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | AppMeasurement上下文数据。 |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | AppMeasurement上下文数据。 |
| `environment.browserDetails.userAgent` | `User-Agent` | 这是HTTP头映射，HEADER_USER_AGENT。 |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | 这是HTTP头映射，HEADER_ACCEPT_LANGUAGE。 |
| `environment.browserDetails.cookiesEnabled` | `k` | 转换为BOOLEAN_TO_YN的AppMeasurement查询参数COOKIE映射。 |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement查询参数J_JSCRIPT映射。 |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement查询参数JAVA_ENABLED映射，转换为BOOLEAN_TO_YN。 |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement查询参数BROWSER_HEIGHT映射。 |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement查询参数BROWSER_WIDTH映射。 |
| `environment.connectionType` | `ct` | AppMeasurement查询参数CT_CONNECT_TYPE映射。 |
| `device.colorDepth` | `c` | AppMeasurement查询参数C_COLOR映射。 |
| `placeContext.geo.stateProvince` | `state` | AppMeasurement查询参数STATE映射。 |
| `placeContext.geo.postalCode` | `zip` | AppMeasurement查询参数ZIP映射。 |
| `placeContext.geo.latitude` | `lat` | AppMeasurement查询参数LATITUDE映射。 |
| `placeContext.geo.longitude` | `lon` | AppMeasurement查询参数LONGITUDE映射。 |
| `web.webPageDetails.server` | `sv` | AppMeasurement查询参数USER_SERVER映射。 |
| `web.webPageDetails.name` | `gn` | AppMeasurement查询参数PAGENAME映射。 |
| `web.webPageDetails.URL` | `g` | AppMeasurement查询参数PAGE_URL映射。 |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement查询参数HOMEPAGE映射（转换为BOOLEAN_TO_YN）。 |
| `web.webReferrer.URL` | `r` | AppMeasurement查询参数推荐人映射。 |
| `web.webInteraction.type` | `pe` | AppMeasurement查询参数PAGE_事件映射（转换为CLICK_MAP_TYPE）。 |
| `web.webInteraction.URL` | `pev1` | AppMeasurement查询参数PAGE_事件_VAR1映射。 |
| `web.webInteraction.name` | `pev2` | AppMeasurement查询参数PAGE_事件_VAR2映射。 |
| `web.webPageDetails.siteSection` | `ch` | AppMeasurement查询参数渠道映射。 |
| `web.webPageDetails.errorPage` | `pageType` | AppMeasurement查询参数PAGE_TYPE_FULL映射（转换ERROR_PAGE_TYPE）。 |
| `application.id` | `c.a.appid` | AppMeasurement上下文数 `c.a.appid` 据映射。 |
| `application.launches.value` | `c.a.launches` | AppMeasurement上下文数 `c.a.launches` 据映射。 |
| `marketing.trackingCode` | `v0` | AppMeasurement查询参数活动映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement上下文数 `a.media.name` 据映射。 |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement上下文数 `c.a.media.length` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement上下文数 `c.a.contentType` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement上下文数 `c.a.media.playerName` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement上下文数 `c.a.media.channel` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement上下文数 `c.a.media.segment` 据映射。 |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement上下文数 `c.a.media.friendlyName` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement上下文数 `c.a.media.sdkVersion` 据映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement上下文数 `c.a.media.show` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement上下文数 `c.a.media.format` 据映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement上下文数 `c.a.media.season` 据映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement上下文数 `c.a.media.episode` 据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement上下文数 `c.a.media.network` 据映射。 |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | 转换为VEDIO_ `c.a.media.type` SHOW_TYPE的AppMeasurement上下文数据映射。 |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement上下文数 `c.a.media.feed` 据映射。 |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement上下文数 `c.a.media.timePlayed` 据映射。 |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement上下文数 `c.a.media.totalTimePlayed` 据映射。 |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement上下文数 `c.a.media.federated` 据映射。 |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement上下文数 `c.a.media.pauseCount` 据映射。 |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement上下文数 `c.a.media.pauseTime` 据映射。 |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement上下文数 `c.a.media.resume` 据映射。 |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | 转换为VIDEO_ `c.a.media.type` SHOW_TYPE的AppMeasurement上下文数据映射。 |
| `identityMap.ECID.[0].id` | `mid` | AppMeasurement查询参数MID映射。 |
