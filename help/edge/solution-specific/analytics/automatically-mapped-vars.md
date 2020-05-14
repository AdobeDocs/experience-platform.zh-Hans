---
title: 在Analytics中自动映射变量
seo-title: 使用Adobe Experience Platform Web SDK在分析中自动映射变量
description: 了解在Analytics中使用Experience Platform Web SDK自动映射哪些变量
seo-description: 了解在Analytics中使用Experience Platform Web SDK自动映射哪些变量
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# 在Analytics中自动映射变量

以下是Adobe Experience Platform Edge Network自动映射到Analytics的变量列表。

| XDM字段路径 | 分析查询字符串/HTTP头 | 描述 |
| ---------- | ------------------------- | -------- |
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
| `application.id` | `c.a.appid` | AppMeasurement上下文数 `c.a.appid` 据映射。 |
| `application.launches.value` | `c.a.launches` | AppMeasurement上下文数 `c.a.launches` 据映射。 |
| `marketing.trackingCode` | `v0` | AppMeasurement查询参数活动映射。 |
| `commerce.purchaseID` | `pi` | AppMeasurement查询参数PURCHASEID映射。 |
| `commerce.currencyCode` | `cc` | AppMeasurement查询参数CURRENCY映射。 |
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
| `identitymap.ecid.[0].id` | `mid` | AppMeasurement查询参数MID映射。 |
