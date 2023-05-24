---
title: 在Adobe Experience Platform Web SDK中自動對應的Adobe Analytics變數
description: 瞭解透過Experience PlatformWeb SDK在Adobe Analytics中自動對應的變數
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: adobe analytics；變數；analytics；自動對應；自動對應；
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 6%

---

# 自動對應的變數 [!DNL Analytics]

以下是Adobe Experience Platform Edge Network自動對應至Adobe Analytics的變數清單。 有關Adobe Analytics資料彙集查詢引數的詳細資訊，請參閱 [Analytics實作指南](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html?lang=zh-Hans).

>[!NOTE]
>本頁資訊也適用於Adobe Mobile SDK。

| XDM 字段路径 | [!DNL Analytics Query String] / HTTP 标头 | 描述 |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | AppMeasurement內容資料 `c.a.appid` 對應。 |
| application.launches.value | c.a.launches | AppMeasurement內容資料 `c.a.launches` 對應。 |
| commerce.checkouts.id | 事件 | `scCheckout` 事件序列化。 如果排除此欄位（亦即針對非序列化事件），則系統會產生自己的ID值，並將其指定給實體。 |
| commerce.checkouts.value | 事件 | AppMeasurement查詢引數EVENT_LIST_FULL與轉換COMMERCE_SC_CHECKOUT對應，使用分隔字元 `,`. |
| commerce.order.currencyCode | cc | AppMeasurement查詢引數CURRENCY對應。 |
| commerce.order.purchaseID | pi | AppMeasurement查詢引數PURCHASEID對應。 |
| commerce.productListAdds.id | 事件 | `scAdd` 事件序列化。 如果排除此欄位（亦即針對非序列化事件），則系統會產生自己的ID值，並將其指定給實體。 |
| commerce.productListAdds.value | 事件 | AppMeasurement查詢引數EVENT_LIST_FULL與轉換COMMERCE_SC_ADD對應，使用分隔字元 `,`. |
| commerce.productListOpens.id | 事件 | `scOpen` 事件序列化。 如果排除此欄位（亦即針對非序列化事件），則系統會產生自己的ID值，並將其指定給實體。 |
| commerce.productListOpens.value | 事件 | AppMeasurement查詢引數EVENT_LIST_FULL與轉換COMMERCE_SC_OPEN對應，使用分隔字元 `,`. |
| commerce.productListRemovals.id | 事件 | `scRemove` 事件序列化。 如果排除此欄位（亦即針對非序列化事件），則系統會產生自己的ID值，並將其指定給實體。 |
| commerce.productListRemovals.value | 事件 | AppMeasurement查詢引數EVENT_LIST_FULL與轉換COMMERCE_SC_REMOVE對應，使用分隔字元 `,`. |
| commerce.productListViews.id | 事件 | `scView` 事件序列化。 如果排除此欄位（亦即針對非序列化事件），則系統會產生自己的ID值，並將其指定給實體。 |
| commerce.productListViews.value | 事件 | AppMeasurement查詢引數EVENT_LIST_FULL與轉換COMMERCE_SC_VIEW對應，使用分隔字元 `,`. |
| commerce.productViews.id | 事件 | `prodView` 事件序列化。 如果排除此欄位（亦即針對非序列化事件），則系統會產生自己的ID值，並將其指定給實體。 |
| commerce.productViews.value | 事件 | AppMeasurement查詢引數EVENT_LIST_FULL與轉換COMMERCE_PROD_VIEW對應，使用分隔字元 `,`. |
| commerce.purchases.value | 事件 | AppMeasurement查詢引數EVENT_LIST_FULL與轉換COMMERCE_PURCHASE對應，使用分隔字元 `,`. |
| device.colorDepth | c | AppMeasurement查詢引數C_COLOR對應。 |
| device.screenHeight | s | AppMeasurement查詢引數熒幕解析度對應。 |
| device.screenWidth | s | AppMeasurement查詢引數熒幕解析度對應。 |
| environment.browserDetails.acceptLanguage | Accept-Language | 這是HTTP標頭對應，HEADER_ACCEPT_LANGUAGE。 |
| environment.browserDetails.cookiesEnabled | k | 使用轉換BOOLEAN_TO_YN的AppMeasurement查詢引數COOKIE對應。 |
| environment.browserDetails.javaEnabled | v | AppMeasurement查詢引數JAVA_ENABLED與轉換BOOLEAN_TO_YN的對應。 |
| environment.browserDetails.javaScriptVersion | j | AppMeasurement查詢引數J_JSCRIPT對應。 |
| environment.browserDetails.userAgent | User-Agent | 這是HTTP標頭對應，HEADER_USER_AGENT。 |
| environment.browserDetails.viewportHeight | bh | AppMeasurement查詢引數BROWSER_HEIGHT對應。 |
| environment.browserDetails.viewportWidth | bw | AppMeasurement查詢引數BROWSER_WIDTH對應。 |
| environment.connectionType | ct | AppMeasurement查詢引數CT_CONNECT_TYPE對應。 |
| environment.ipV4 | X-Forwarded-For | 這是HTTP標頭對應，X-FORWARDED-FOR。 |
| identityMap.ECID[0].id | mid | AppMeasurement查詢引數MID對應。 |
| marketing.trackingCode | v0 | AppMeasurement查詢引數CAMPAIGN對應。 |
| media.mediaTimed.completes.value | c.a.media.complete | AppMeasurement內容資料。 |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view， c.a.media.timePlayed， c.a.media.play | AppMeasurement內容資料。 |
| media.mediaTimed.federated.value | c.a.media.federated | AppMeasurement內容資料 `c.a.media.federated` 對應。 |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | AppMeasurement內容資料。 |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | AppMeasurement內容資料。 |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | AppMeasurement內容資料。 |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | AppMeasurement內容資料 `c.a.media.pauseTime` 對應。 |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | AppMeasurement內容資料 `c.a.media.pauseCount` 對應。 |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | AppMeasurement內容資料 `c.a.media.friendlyName` 對應。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | AppMeasurement內容資料 `c.a.media.episode` 對應。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | AppMeasurement內容資料 `c.a.media.season` 對應。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | AppMeasurement內容資料 `a.media.name` 對應。 |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | AppMeasurement內容資料 `c.a.media.show` 對應。 |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement內容資料 `c.a.media.type` 與轉換VEDIO_SHOW_TYPE對映。 |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement內容資料 `c.a.media.type` 與轉換VIDEO_SHOW_TYPE對映。 |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | AppMeasurement內容資料 `c.a.media.length` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | AppMeasurement內容資料。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | AppMeasurement內容資料 `c.a.media.channel` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | AppMeasurement內容資料 `c.a.contentType` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | AppMeasurement內容資料 `c.a.media.network` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | AppMeasurement內容資料 `c.a.media.segment` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | AppMeasurement內容資料 `c.a.media.playerName` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | AppMeasurement內容資料 `c.a.media.sdkVersion` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | AppMeasurement內容資料 `c.a.media.feed` 對應。 |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | AppMeasurement內容資料 `c.a.media.format` 對應。 |
| media.mediaTimed.progress10.value | c.a.media.progress10 | AppMeasurement內容資料。 |
| media.mediaTimed.progress95.value | c.a.media.progress95 | AppMeasurement內容資料。 |
| media.mediaTimed.resumes.value | c.a.media.resume | AppMeasurement內容資料 `c.a.media.resume` 對應。 |
| media.mediaTimed.starts.value | c.a.media.view | AppMeasurement內容資料。 |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | AppMeasurement內容資料。 |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | AppMeasurement內容資料 `c.a.media.timePlayed` 對應。 |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | AppMeasurement內容資料 `c.a.media.totalTimePlayed` 對應。 |
| placeContext.geo.latitude | lat | AppMeasurement查詢引數LATITUDE對應。 |
| placeContext.geo.longitude | lon | AppMeasurement查詢引數LONGITUDE對應。 |
| placeContext.geo.postalCode | zip | AppMeasurement查詢引數ZIP對應。 |
| placeContext.geo.stateProvince | state | AppMeasurement查詢引數STATE對應。 |
| productListItems[N].lineItemId | products | AppMeasurement查詢引數產品類別對應。 |
| productlistitems[N].name | products | AppMeasurement查詢引數產品名稱對應。 |
| productlistitems[N].priceTotal | products | AppMeasurement查詢引數產品價格對應。 |
| productlistitems[N].quantity | products | AppMeasurement查詢引數產品數量對應。 |
| web.webInteraction.URL | pev1 | AppMeasurement查詢引數PAGE_EVENT_VAR1對應。 |
| web.webInteraction.name | pev2 | AppMeasurement查詢引數PAGE_EVENT_VAR2對應。 |
| web.webInteraction.type | pe | `web.webInteraction.type=other` 至 `pe=lnk_o`； `web.webInteraction.type=download` 至 `pe=lnk_d`； `web.webInteraction.type=exit` 至 `pe=lnk_e` |
| web.webPageDetails.URL | g | AppMeasurement查詢引數PAGE_URL對應。 |
| web.webPageDetails.errorPage | pageType | 具有轉換ERROR_PAGE_TYPE的AppMeasurement查詢引數PAGE_TYPE_FULL對應。 |
| web.webPageDetails.homePage | hp | 轉換BOOLEAN_TO_YN的AppMeasurement查詢引數HOMEPAGE對應。 |
| web.webPageDetails.name | gn | AppMeasurement查詢引數PAGENAME對應。 |
| web.webPageDetails.server | sv | AppMeasurement查詢引數USER_SERVER對應。 |
| web.webPageDetails.siteSection | ch | AppMeasurement查詢引數CHANNEL對應。 |
| web.webReferrer.URL | r | AppMeasurement查詢引數REFERRER對應。 |

{style="table-layout:auto"}
