---
title: Advertising详细信息架构字段组
description: 了解Advertising详细信息架构字段组。
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 27%

---

# [!UICONTROL Advertising详细信息]架构字段组

[!UICONTROL Advertising详细信息]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组。 字段组为架构提供单个`advertising`对象，用于捕获与广告展示次数、点进次数和归因相关的信息。

![字段组结构](../../images/field-groups/advertising-details/structure.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `adAssetReference` | 对象 | 捕获有关广告的资源信息。 有关此对象结构的更多信息，请参阅[&#128279;](#adAssetReference)下面的子部分。 |
| `adAssetViewDetails` | 对象 | 捕获广告播放的视图详细信息。 有关此对象结构的更多信息，请参阅[&#128279;](#adAssetViewDetails)下面的子部分。 |
| `adViewability` | 对象 | 捕获最终用户看到的展示次数，如播放器音量、库版本、窗口状态和广告视区维度。 有关此对象结构的更多信息，请参阅[&#128279;](#adViewability)下面的子部分。 |
| `clicks` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 播发上的点击操作数。 |
| `completes` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 定时媒体资源观看至结束的次数。 这并不一定意味着最终用户观看了整个视频，因为他们可能跳过了前面。 |
| `conversions` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 预定义操作（或操作）触发事件进行性能评估的次数。 |
| `federated` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 指示体验事件是否通过数据联合（例如，客户之间的数据共享）创建。 |
| `firstQuartiles` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 数字视频广告以正常速度播放其持续时间25%的次数。 |
| `impressions` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 发送给最终用户的可能被查看的广告展示次数。 |
| `midpoints` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 数字视频广告以正常速度播放其持续时间50%的次数。 |
| `starts` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 数字视频广告开始播放的次数。 |
| `thirdQuartiles` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 数字视频广告以正常速度播放了其75%的时长的次数。 |
| `timePlayed` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 最终用户在特定的定时媒体资源上花费的时间。 |
| `downloadedPlayback` | 布尔值 | 当设置为`true`时，表示点击是由于播放下载的广告会话而生成的。 |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

`adAssetReference`对象捕获有关广告的资源信息。

![adAssetReference结构](../../images/field-groups/advertising-details/adAssetReference.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_dc.title` | 字符串 | 易于用户识别的广告资源名称。 |
| `_xmpDM.duration` | 整数 | 资源的长度或持续时间（以秒为单位）。 |
| `_id` | 字符串 | [Ad-ID标准](https://datatracker.ietf.org/doc/html/rfc8107)之后的广告资源的唯一标识符。 |
| `advertiser` | 字符串 | 广告中展现的产品所属的公司或品牌。 |
| `campaign` | 字符串 | 广告营销活动的ID。 |
| `creativeID` | 字符串 | 广告创意的 ID。 |
| `creativeURL` | 字符串 | 广告创意的 URL。 |
| `placementID` | 字符串 | 广告的版面ID。 |
| `siteID` | 字符串 | 广告网站的ID。 |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

`adAssetViewDetails`对象捕获广告播放的视图详细信息。

![adAssetViewDetails结构](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL 广告时间]](../../data-types/ad-break.md) | 描述如何将定时广告插入定时媒体。 |
| `index` | 整数 | 父广告时间内的广告索引。 例如，第一个广告的索引为`0`，第二个广告的索引为`1`。 |
| `playerName` | 字符串 | 负责呈现广告的播放器的名称。 |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

`adViewability`对象捕获最终用户看到的展示次数，例如播放器音量、库版本、窗口状态和广告视区维度。

![adViewability结构](../../images/field-groups/advertising-details/adViewability.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL 实施详细信息]](../../data-types/implementation-details.md) | 用于衡量可见性量度的库的名称和版本。 |
| `measuredAdNotVisible` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 指示广告在展示时不可见，如可见性库所测量。 |
| `measuredMuted` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 指示广告在展示时由可见性库测量为静音。 |
| `unmeasurableIframe` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 指示广告在展示时显示在非活动窗口中，它由可见性库测量。 |
| `unmeasurableOther` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 表示可见性库由于iframe中显示的广告而无法正确执行测量。 |
| `viewabilityEligibleImpressions` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 面向配备可见性库的最终用户的广告展示。 |
| `viewabilityCompletes` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 面向最终用户的广告的完成时间，该广告被可见性库视为可在完成时查看。 |
| `viewableFirstQuartiles` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 面向最终用户的广告的第一个四分位点，这些点被可见性库视为可在播放第一个四分位点时查看。 |
| `viewableImpressions` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 被可见性库视为可在播放两秒后查看的面向最终用户的广告的展示。 |
| `viewableMidpoints` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 被可见性库视为可在播放中点查看的面向最终用户的广告中点。 |
| `viewableThirdQuartiles` | [[!UICONTROL 度量值]](../../data-types/measure.md) | 面向最终用户的广告的第三个四分位点，这些点被可见性库视为可在播放第三个四分位点时查看。 |
| `activeWindow` | 布尔值 | 指示广告是否显示在用户设备的活动窗口中。 |
| `adHeight` | 整数 | 播放器的垂直像素数（在运行时测量）。如果播放器有额外的控件或缩略图，这可能会大于广告的尺寸。 |
| `adUnitDepth` | 整数 | 发布者可以在容器(iFrame)中嵌入广告单元，以限制广告仅访问页面代码。 此值描述广告单位显示在多少个容器中。 |
| `adWidth` | 整数 | 播放器的水平像素数（在运行时测量）。如果播放器有额外的控件或缩略图，这可能会大于广告的尺寸。 |
| `measurementEligible` | 布尔值 | 广告是否符合可见性的衡量标准。如果广告单元具有受支持的创意格式和标记类型，则广告符合条件。 |
| `percentViewable` | 整数 | 测量时被视为可见的广告中的像素百分比。 |
| `playerVolume` | 整数 | 播放器音量百分比（在运行时测量），其中`0`为静音，`100`为最大音量。 |
| `viewable` | 布尔值 | 指示广告在运行时是否可见。 当广告的至少50%可见至少一秒时，展示广告被视为可见。 当视频连续播放至少两秒且至少50%的广告可见时，视频广告被视为可见。 |
| `viewportHeight` | 整数 | 运行时测量的显示体验的窗口的垂直大小（以像素为单位）。 对于Web视图事件，此值表示浏览器视区高度。 |
| `viewportWidth` | 整数 | 运行时测量的显示体验的窗口的水平大小（以像素为单位）。 对于Web视图事件，此值表示浏览器视区宽度。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json)。
