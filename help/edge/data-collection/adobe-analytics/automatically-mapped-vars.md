---
title: Adobe Experience Platform Web SDK中自动映射的Adobe Analytics变量
description: 了解哪些变量通过Experience PlatformWeb SDK在Adobe Analytics中自动映射
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics；变量；analytics；自动映射；自动映射；
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 6%

---

# 变量自动映射到 [!DNL Analytics]

以下是Adobe Experience Platform Edge Network自动映射到Adobe Analytics中的变量列表。 有关Adobe Analytics数据收集查询参数的详细信息，请参阅 [Analytics实施指南](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html?lang=zh-Hans).

>[!NOTE]
>本页上的信息也适用于AdobeMobile SDK。

| XDM 字段路径 | [!DNL Analytics Query String] / HTTP 标头 | 描述 |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | AppMeasurement上下文数据 `c.a.appid` 映射。 |
| application.launches.value | c.a.launches | AppMeasurement上下文数据 `c.a.launches` 映射。 |
| commerce.checkouts.id | 事件 | `scCheckout` 事件序列化。 如果排除此字段（即对于未序列化的事件），则系统会生成自己的ID值并将其分配给实体。 |
| commerce.checkouts.value | 事件 | AppMeasurement查询参数EVENT_LIST_FULL与转化COMMERCE_SC_CHECKOUT的映射，使用分隔符 `,`. |
| commerce.order.currencyCode | 抄送 | AppMeasurement查询参数CURRENCY映射。 |
| commerce.order.purchaseID | pi | appmeasurement查询参数PURCHASEID映射。 |
| commerce.productListAdds.id | 事件 | `scAdd` 事件序列化。 如果排除此字段（即对于未序列化的事件），则系统会生成自己的ID值并将其分配给实体。 |
| commerce.productListAdds.value | 事件 | AppMeasurement查询参数EVENT_LIST_FULL与转化COMMERCE_SC_ADD的映射，使用分隔符 `,`. |
| commerce.productListOpens.id | 事件 | `scOpen` 事件序列化。 如果排除此字段（即对于未序列化的事件），则系统会生成自己的ID值并将其分配给实体。 |
| commerce.productListOpens.value | 事件 | AppMeasurement查询参数EVENT_LIST_FULL与转化COMMERCE_SC_OPEN的映射，使用分隔符 `,`. |
| commerce.productListRemovals.id | 事件 | `scRemove` 事件序列化。 如果排除此字段（即对于未序列化的事件），则系统会生成自己的ID值并将其分配给实体。 |
| commerce.productListRemovals.value | 事件 | 带有转化COMMERCE_SC_REMOVE的AppMeasurement查询参数EVENT_LIST_FULL映射，使用分隔符 `,`. |
| commerce.productListViews.id | 事件 | `scView` 事件序列化。 如果排除此字段（即对于未序列化的事件），则系统会生成自己的ID值并将其分配给实体。 |
| commerce.productListViews.value | 事件 | AppMeasurement查询参数EVENT_LIST_FULL与转化COMMERCE_SC_VIEW的映射，使用分隔符 `,`. |
| commerce.productViews.id | 事件 | `prodView` 事件序列化。 如果排除此字段（即对于未序列化的事件），则系统会生成自己的ID值并将其分配给实体。 |
| commerce.productViews.value | 事件 | AppMeasurement查询参数EVENT_LIST_FULL与转化COMMERCE_PROD_VIEW的映射，使用分隔符 `,`. |
| commerce.purchases.value | 事件 | AppMeasurement查询参数EVENT_LIST_FULL与转化COMMERCE_PURCHASE的映射，使用分隔符 `,`. |
| device.colorDepth | c | appmeasurement查询参数C_COLOR映射。 |
| device.screenHeight | s | AppMeasurement查询参数屏幕分辨率映射。 |
| device.screenWidth | s | AppMeasurement查询参数屏幕分辨率映射。 |
| environment.browserDetails.acceptLanguage | Accept-Language | 这是HTTP标头映射HEADER_ACCEPT_LANGUAGE。 |
| environment.browserDetails.cookiesEnabled | k | 通过转换BOOLEAN_TO_YN进行AppMeasurement查询参数COOKIE映射。 |
| environment.browserDetails.javaEnabled | v | AppMeasurement查询参数JAVA_ENABLED映射，转化为BOOLEAN_TO_YN。 |
| environment.browserDetails.javaScriptVersion | j | appmeasurement查询参数J_JSCRIPT映射。 |
| environment.browserDetails.userAgent | User-Agent | 这是HTTP标头映射HEADER_USER_AGENT。 |
| environment.browserDetails.viewportHeight | bh | appmeasurement查询参数BROWSER_HEIGHT映射。 |
| environment.browserDetails.viewportWidth | bw | appmeasurement查询参数BROWSER_WIDTH映射。 |
| environment.connectionType | ct | AppMeasurement查询参数CT_CONNECT_TYPE映射。 |
| environment.ipV4 | X-Forwarded-For | 这是HTTP标头映射，X-FORWARDED-FOR。 |
| identityMap.ECID[0].id | mid | appmeasurement查询参数MID映射。 |
| marketing.trackingCode | v0 | appmeasurement查询参数CAMPAIGN映射。 |
| media.mediaTimed.completes.value | c.a.media.complete | appmeasurement上下文数据。 |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view， c.a.media.timePlayed， c.a.media.play | appmeasurement上下文数据。 |
| media.mediaTimed.federated.value | c.a.media.federated | AppMeasurement上下文数据 `c.a.media.federated` 映射。 |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | appmeasurement上下文数据。 |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | appmeasurement上下文数据。 |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | appmeasurement上下文数据。 |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | AppMeasurement上下文数据 `c.a.media.pauseTime` 映射。 |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | AppMeasurement上下文数据 `c.a.media.pauseCount` 映射。 |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | appmeasurement上下文数据。 |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | AppMeasurement上下文数据 `c.a.media.friendlyName` 映射。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | appmeasurement上下文数据。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | AppMeasurement上下文数据 `c.a.media.episode` 映射。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | appmeasurement上下文数据。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | appmeasurement上下文数据。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | AppMeasurement上下文数据 `c.a.media.season` 映射。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | AppMeasurement上下文数据 `a.media.name` 映射。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | AppMeasurement上下文数据 `c.a.media.show` 映射。 |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement上下文数据 `c.a.media.type` 使用转换VEDIO_SHOW_TYPE进行映射。 |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement上下文数据 `c.a.media.type` 使用转换VIDEO_SHOW_TYPE进行映射。 |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | AppMeasurement上下文数据 `c.a.media.length` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | appmeasurement上下文数据。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | AppMeasurement上下文数据 `c.a.media.channel` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | AppMeasurement上下文数据 `c.a.contentType` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | AppMeasurement上下文数据 `c.a.media.network` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | AppMeasurement上下文数据 `c.a.media.segment` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | AppMeasurement上下文数据 `c.a.media.playerName` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | AppMeasurement上下文数据 `c.a.media.sdkVersion` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | AppMeasurement上下文数据 `c.a.media.feed` 映射。 |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | AppMeasurement上下文数据 `c.a.media.format` 映射。 |
| media.mediaTimed.progress10.value | c.a.media.progress10 | appmeasurement上下文数据。 |
| media.mediaTimed.progress95.value | c.a.media.progress95 | appmeasurement上下文数据。 |
| media.mediaTimed.resumes.value | c.a.media.resume | AppMeasurement上下文数据 `c.a.media.resume` 映射。 |
| media.mediaTimed.starts.value | c.a.media.view | appmeasurement上下文数据。 |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | appmeasurement上下文数据。 |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | AppMeasurement上下文数据 `c.a.media.timePlayed` 映射。 |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | AppMeasurement上下文数据 `c.a.media.totalTimePlayed` 映射。 |
| placeContext.geo.latitude | lat | appmeasurement查询参数LATITUDE映射。 |
| placeContext.geo.longitude | lon | AppMeasurement查询参数LONGITUDE映射。 |
| placeContext.geo.postalCode | zip | appmeasurement查询参数ZIP映射。 |
| placeContext.geo.stateProvince | state | AppMeasurement查询参数状态映射。 |
| productListItems[N].lineItemId | products | AppMeasurement查询参数产品类别映射。 |
| productlistitems[N].name | products | AppMeasurement查询参数产品名称映射。 |
| productlistitems[N].priceTotal | products | AppMeasurement查询参数产品价格映射。 |
| productlistitems[N].quantity | products | AppMeasurement查询参数产品数量映射。 |
| web.webInteraction.URL | pev1 | AppMeasurement查询参数PAGE_EVENT_VAR1映射。 |
| web.webInteraction.name | pev2 | AppMeasurement查询参数PAGE_EVENT_VAR2映射。 |
| web.webInteraction.type | pe | `web.webInteraction.type=other` 到 `pe=lnk_o`； `web.webInteraction.type=download` 到 `pe=lnk_d`； `web.webInteraction.type=exit` 到 `pe=lnk_e` |
| web.webPageDetails.URL | g | AppMeasurement查询参数PAGE_URL映射。 |
| web.webPageDetails.errorPage | pageType | 具有转换ERROR_PAGE_TYPE的AppMeasurement查询参数PAGE_TYPE_FULL映射。 |
| web.webPageDetails.homePage | 马力 | 转换BOOLEAN_TO_YN的AppMeasurement查询参数HOMEPAGE映射。 |
| web.webPageDetails.name | gn | appmeasurement查询参数PAGENAME映射。 |
| web.webPageDetails.server | sv | AppMeasurement查询参数USER_SERVER映射。 |
| web.webPageDetails.siteSection | ch | appmeasurement查询参数CHANNEL映射。 |
| web.webReferrer.URL | r | appmeasurement查询参数REFERRER映射。 |

{style="table-layout:auto"}
