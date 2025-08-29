---
title: Adobe Advertising Cloud ExperienceEvent完整扩展架构字段组
description: 了解Adobe Advertising Cloud ExperienceEvent完整扩展架构字段组。
badgeBeta: label="Beta 版" type="Informative"
source-git-commit: adfd0220b8bc53c44abc76a711b148a7e03edb7a
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 7%

---

# [!UICONTROL Adobe Advertising Cloud ExperienceEvent完整扩展]架构字段组

>[!AVAILABILITY]
>
>[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]字段组当前为测试版。 文档和功能可能会发生变化。

[!UICONTROL Adobe Advertising Cloud ExperienceEvent Full Extension]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组，用于捕获Adobe Advertising收集的常用量度（以前称为“[!DNL Advertising Cloud]”）。

本文档介绍了[!DNL Advertising Cloud]扩展字段组的结构和用例。

>[!NOTE]
>
>您还可以在Experience Platform UI[中查找此字段组](../../ui/explore.md)或在[公共XDM存储库](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)中查看完整的架构。

## 字段组结构

字段组为架构提供单个`_experience`对象，它本身包含单个`adcloud`对象。

![字段组[!DNL Advertising Cloud]的顶级字段](../../images/field-groups/advertising-full-extension/full-schema.png "字段组 [!DNL Advertising Cloud] 的顶级字段")

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `adDeliveryDetails` | 对象 | 广告投放详细信息。 有关此对象内容的更多信息，请参阅[对象`adDeliveryDetails`的下方](#adDeliveryDetails)子部分。 |
| `advertisement` | 对象 | 数字广告详细信息。 有关此对象内容的更多信息，请参阅广告对象[的下方](#advertisement)子部分。 |
| `campaign` | 对象 | 营销活动层级详细信息。 有关此对象内容的更多信息，请参阅促销活动对象[的下方](#campaign-campaign)子部分。 |
| `conversionDetails` | 对象 | 广告的转化详细信息。 有关此对象内容的更多信息，请参阅[下面的](#conversionDetails)子部分。 |
| `eventType` | 字符串 | Adobe Advertising事件类型。 |
| `fees` | 对象 | Advertising费用详细信息。 有关此对象内容的更多信息，请参阅费用对象[的下方](#fees)子部分。 |
| `inventory` | 对象 | 库存详细信息。 有关此对象内容的更多信息，请参阅[下面的](#inventory)子部分。 |
| `productDetails` | 对象 | 产品广告详细信息。 有关此对象内容的更多信息，请参阅productDetails对象[的下方](#productDetails)子部分。 |
| `stitchId` | 字符串 | Adobe Advertising广告服务器中的ID，用于跟踪在阻止第三方Cookie的浏览器上的点进转化。 |

## `adDeliveryDetails` {#adDeliveryDetails}

adDeliveryDetails对象提供有关投放广告的位置和方式的信息，包括投放网站和位置标识符。

![显示`adDeliveryDetails`对象及其字段的架构图。](../../images/field-groups/advertising-full-extension/adDeliveryDetails.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `placementWebsite` | 字符串 | 显示广告的网站。 |
| `siteLinkText` | 字符串 | 在广告中选择的实际站点链接。 |
| `interestLocationID` | 字符串 | 从搜索查询推断的位置。 例如，对“Goa中的酒店”的查询会返回Goa的ID，而不管用户的实际浏览位置如何。 |
| `physicalLocationID` | 字符串 | 用户的浏览位置，由广告网络中的引用ID表示。 此ID不是可读的位置名称（例如城市或国家/地区），而是广告网络为识别地理目标而分配的代码。 |

## `advertisement` {#advertisement}

广告对象描述有关数字广告的详细信息，例如其标识符、类型、创意、定位和相关关键词。

![显示`advertisement`对象及其字段的架构图。](../../images/field-groups/advertising-full-extension/advertisement.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `adId` | 字符串 | 与此事件关联的广告的标识符。 此ID与Ad-ID行业标准无关。 |
| `runtime` | 字符串 | 广告单元的运行时，与浏览器或操作系统的运行时不同。 可能的值包括： `unknown`和`HTML5`。 |
| `adClass` | 字符串 | 驾驶事件的广告类： `display`、`video`或`social`。 |
| `adUnitType` | 字符串 | 在浏览器或设备中呈现广告的代码的标识符。 可能的值包括：<ul><li>`linearVideo`：线性视频</li><li>`interactiveVideo`：交互式视频</li><li>`banner`：横幅，</li><li>`richMediaBanner`：富媒体横幅，</li><li>`newsFeedVideo`：新闻源视频，</li><li>`newsFeedDisplay`：新闻源显示，</li><li>`HTML5`： HTML5，</li><li>`inPageVideo`：在页面视频中，</li><li>`inPageDisplay`：在页面显示中，</li><li>`facebook`： Facebook，</li><li>`twitter`： Twitter，</li><li>`linearTv`：线性电视，</li><li>`vod`：点播视频</li></ul> |
| `promotedAssetId` | 字符串 | 与此事件关联的广告中促销的资源的标识符。 |
| `creativeID` | 字符串 | 与此事件关联的广告创意（例如横幅、视频或社交广告）的标识符。 |
| `keywordID` | 字符串 | 用户在触发此事件的搜索查询中输入的关键字标识符。 |
| `keyword` | 字符串 | 客户竞价的列表关键字。 |
| `isDynamicSearchAd` | 布尔值 | 指示事件是否来自动态搜索播发。 |
| `audienceID` | 字符串 | 广告定向的受众区段的标识符。 |
| `adGroupID` | 字符串 | 与触发此事件的广告关联的广告组的标识符。 |
| `campaignID` | 字符串 | 与触发此事件的广告关联的营销活动的标识符。 |
| `networkType` | 字符串 | 发生事件的网络类型。 可能的值包括： <ul><li>`search`：播发显示在搜索网络上。</li><li>`content`：播发显示在内容网络上。</li></ul> |
| `matchType` | 字符串 | 关键字匹配类型。 可能的值包括： <ul><li>`exact`：关键字的完全匹配</li><li>`broad`：关键字的广泛匹配</li><li>`phrase`：关键字的短语匹配</li></ul> |

## `campaign` {#campaign}

营销活动对象定义广告营销活动层次结构，包括帐户、广告商、投放位置和包标识符以及货币详细信息。

![显示`campaign`对象及其字段的架构图。](../../images/field-groups/advertising-full-extension/campaign.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `accountId` | 字符串 | 帐户的标识符。 |
| `dspId` | 字符串 | 定义营销活动的Demand Side Platform (DSP)的标识符。 通常，此标识符是Adobe Advertising Cloud DSP的ID。 |
| `campaignId` | 字符串 | 营销活动的标识符。 |
| `placementId` | 字符串 | 投放位置的标识符。 |
| `packageId` | 字符串 | Advertising DSP包的标识符。 |
| `advertiserId` | 字符串 | 广告商的标识符。 |
| `experimentId` | 字符串 | 试验的标识符。 |
| `sampleGroupId` | 字符串 | 示例组的标识符。 |
| `currency` | 字符串 | 账户的ISO 4217计费货币代码。 使用正则表达式模式^[A-Z]{3}$（三个大写字母）。 例如：USD、EUR。 |

## `conversionDetails` {#conversionDetails}

conversionDetails对象可捕获广告转化的跟踪信息，包括跟踪代码、身份和转化属性。

显示![对象及其字段的`conversionDetails`架构图。](../../images/field-groups/advertising-full-extension/conversionDetails.png "conversionDetails字段")

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `trackingCode` | 字符串 | 事件的转化跟踪代码。 有关可能格式的列表，请参阅[AMO ID格式](https://experienceleague.adobe.com/en/docs/advertising/integrations/customer-journey-analytics/ids#amo-id-formats)。 |
| `trackingIdentities` | 字符串 | 事件的EF ID或跟踪身份详细信息。 有关可能格式的列表，请参阅[EF ID格式](https://experienceleague.adobe.com/en/docs/advertising/integrations/customer-journey-analytics/ids#ef-id-formats)。 |
| `conversionProperties` | 对象 | 转化属性的映射，表示为键值对字符串的数组（如`subscriptions=253`）。 |

## `fees` {#fees}

费用对象可捕获按Advertising DSP、帐户和广告商划分的媒体、数据和其他广告成本。

![显示`fees`对象及其字段的架构图。](../../images/field-groups/advertising-full-extension/fees.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `DSPMediaFees` | 数值 | 由Advertising DSP计费的媒体费用。 |
| `DSPDataFees` | 数值 | Advertising DSP收取的数据费用。 |
| `DSPOtherFees` | 数值 | Advertising DSP可收取的其他费用。 |
| `accountMediaFees` | 数值 | 账户的媒体费用，但Advertising DSP不计费。 |
| `accountDataFees` | 数值 | 帐户的数据费用，但Advertising DSP不对这些数据收费。 |
| `accountOtherFees` | 数值 | 账户的其他费用，但Advertising DSP不计费。 |
| `advertiserMediaFees` | 数值 | 从该帐户向广告商收取的媒体广告商费用。 |
| `advertiserDataFees` | 数值 | 从该帐户向广告商收取的其他广告商费用。 |
| `advertiserOtherFees` | 数值 | 从该帐户向广告商收取的其他广告商费用。 |
| `billableMediaNetSpend` | 数值 | 用于媒体广告的可计费净支出。 |
| `totalMediaNetSpend` | 数值 | 用于媒体广告的总净支出。 |
| `billableDataNetSpend` | 数值 | 数据广告的可计费净支出。 |
| `billableOtherNetSpend` | 数值 | 用于其他类型广告的可计费净支出。 |
| `totalBillableNetSpend` | 数值 | 可记帐净支出总计。 |
| `totalNonBillableNetSpend` | 数值 | 不可计费的净支出总计。 |
| `totalNetSpend` | 数值 | 总净支出。 |

## `inventory` {#inventory}

清单对象记录有关广告清单商机的详细信息，包括会话数据、合作伙伴代码、网站ID、成本货币和分段规则。

![显示`inventory`对象及其字段的架构图。](../../images/field-groups/advertising-full-extension/inventory.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `sessionId` | 字符串 | 与体验事件关联的会话ID，用于链接同一会话中发生的独立事件。 |
| `feedID` | 字符串 | 发布者、广告交换和其他功能的复合ID。 |
| `sspPartnerCode` | 字符串 | Adobe Advertising Cloud接收库存机会的合作伙伴（交换）。 |
| `siteID` | 字符串 | 提供广告展示的网站的标识符。 |
| `costCurrency` | 字符串 | 用于为广告机会向合作伙伴付款的ISO 4217货币代码。 该值必须遵循正则表达式模式^[A-Z]{3}$（三个大写字母）。 例如：USD、EUR。 |
| `inventorySourceId` | 字符串 | 投放此机会的Adobe Advertising Cloud库存来源的ID。 |
| `segment` | 对象 | 与用户分段规则相关的详细信息。 其属性包括：<ul><li>`attributablePartnerId` （字符串）：拥有attributeSegmentId的区段提供程序的标识符。</li><li>`attributableSegmentId` （字符串）：投放位置定位规则中用于用户定位的点数区段。 用于跟踪成本和支付合作伙伴。</li><li>`segments`（字符串）：用户所属的用户区段a\)与广告所定位的用户区段b\)的交集。 这不是拍卖时用户所属的区段的完整列表。</li></ul> |
| `optimizationTag` | 字符串 | 与优化相关的标记。 |
| `attributableDeviceGraphId` | 字符串 | 归因于转化事件的设备图的标识符。 |

## `productDetails` {#productDetails}

`productDetails`对象包含有关[!DNL Adobe Advertising Search, Social, & Commerce]的购物广告中特色产品的信息，包括产品标识符、国家/地区、语言、分区、标题和广告类型。

![显示`productDetails`对象及其字段的架构图。](../../images/field-groups/advertising-full-extension/productDetails.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `productID` | 字符串 | 与此事件关联的广告中特色产品的标识符。 |
| `country` | 字符串 | 与活动关联的广告中所展示产品的销售国家/地区。 |
| `language` | 字符串 | 您的产品信息的语言，如客户的商家中心数据馈送中所示。 |
| `partitionID` | 字符串 | 与此事件中的广告关联的产品组的标识符。 |
| `title` | 字符串 | 广告中显示的产品标题。 |
| `adType` | 字符串 | [!DNL Google]购物营销活动中使用的产品的广告类型。 可能的值包括：<ul><li>`pla_with_pog`：事件来自通过购物广告进行的购买时</li><li>`pla`：事件来自购物广告时。</li><li>`pla_multichannel`：当购物广告中的事件包含“在线”和“本地”购物渠道的选项时。</li><li>`pla_with_promotion`：当购物广告中的事件显示商家促销活动时。</li></ul> |

## 后续步骤

本文档介绍了[!DNL Advertising Cloud]扩展字段组的结构和用例。 有关字段组本身的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/adcloud/experienceevent-all.schema.json)。

如果您使用此字段组通过Adobe Experience Platform Web SDK收集[!DNL Advertising]数据，请参阅[配置数据流](../../../datastreams/overview.md)指南，了解如何将数据映射到服务器端的XDM。
