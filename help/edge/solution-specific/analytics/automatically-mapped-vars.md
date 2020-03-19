---
title: Analytics中自动映射的变量
seo-title: 使用Adobe Experience Platform Web SDK在Analytics中自动映射变量
description: 了解在Analytics中使用Experience Platform Web SDK自动映射哪些变量
seo-description: 了解在Analytics中使用Experience Platform Web SDK自动映射哪些变量
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）Analytics中自动映射的变量

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

以下是Adobe Experience Platform Edge Network自动映射到Analytics的变量列表。

| XDM字段路径 | 分析查询字符串/HTTP头 | 描述 |
| ---------- | ------------------------- | -------- |
| `environment.browserDetails.userAgent` | `User-Agent` | 这是HTTP头映射，HEADER_USER_AGENT。 |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | 这是HTTP头映射，HEADER_ACCEPT_LANGUAGE。 |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement查询参数COOKIE映射，转换为BOOLEAN_TO_YN。 |
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
| `web.webPageDetails.homePage` | `hp` | AppMeasurement查询参数HOMEPAGE映射，转换为BOOLEAN_TO_YN。 |
| `web.webReferrer.URL` | `r` | AppMeasurement查询参数REFERRER映射。 |
| `application.id` | `c.a.appid` | AppMeasurement上下文数据 `c.a.appid` 映射。 |
| `application.launches.value` | `c.a.launches` | AppMeasurement上下文数据 `c.a.launches` 映射。 |
| `marketing.trackingCode` | `v0` | AppMeasurement查询参数CAMPAIGN映射。 |
| `commerce.purchaseID` | `pi` | AppMeasurement查询参数PURCHASEID映射。 |
| `commerce.currencyCode` | `cc` | AppMeasurement查询参数CURRENCY映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement上下文数据 `a.media.name` 映射。 |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement上下文数据 `c.a.media.length` 映射。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement上下文数据 `c.a.contentType` 映射。 |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement上下文数据 `c.a.media.playerName` 映射。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement上下文数据 `c.a.media.channel` 映射。 |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement上下文数据 `c.a.media.segment` 映射。 |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement上下文数据 `c.a.media.friendlyName` 映射。 |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement上下文数据 `c.a.media.sdkVersion` 映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement上下文数据 `c.a.media.show` 映射。 |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement上下文数据 `c.a.media.format` 映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement上下文数据 `c.a.media.season` 映射。 |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement上下文数据 `c.a.media.episode` 映射。 |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement上下文数据 `c.a.media.network` 映射。 |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement上下文数 `c.a.media.type` 据映射与转换VEDIO_SHOW_TYPE。 |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement上下文数据 `c.a.media.feed` 映射。 |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement上下文数据 `c.a.media.timePlayed` 映射。 |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement上下文数据 `c.a.media.totalTimePlayed` 映射。 |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement上下文数据 `c.a.media.federated` 映射。 |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement上下文数据 `c.a.media.pauseCount` 映射。 |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement上下文数据 `c.a.media.pauseTime` 映射。 |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement上下文数据 `c.a.media.resume` 映射。 |
| `identitymap.ecid.[0].id` | `mid` | AppMeasurement查询参数MID映射。 |
