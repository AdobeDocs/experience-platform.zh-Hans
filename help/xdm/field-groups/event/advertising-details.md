---
title: 广告详细信息架构字段组
description: 本文档概述了“广告详细信息”架构字段组。
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 8%

---

# [!UICONTROL 广告详细信息] 架构字段组

[!UICONTROL 广告详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供一个 `advertising` 架构的对象，用于捕获与广告展示次数、点进次数和归因相关的信息。

![字段组结构](../../images/field-groups/advertising-details/structure.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `adAssetReference` | 对象 | 捕获有关广告的资源信息。 请参阅 [以下子部分](#adAssetReference) 以了解有关此对象结构的更多信息。 |
| `adAssetViewDetails` | 对象 | 捕获广告播放的视图详细信息。 请参阅 [以下子部分](#adAssetViewDetails) 以了解有关此对象结构的更多信息。 |
| `adViewability` | 对象 | 捕获最终用户看到的展示次数，例如播放器音量、库版本、窗口状态和广告视区维度。 请参阅 [以下子部分](#adViewability) 以了解有关此对象结构的更多信息。 |
| `clicks` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 广告上的点击操作数。 |
| `completes` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 定时媒体资源被观看至结束的次数。 这并不一定意味着最终用户观看了整个视频，因为他们可能跳过了前面。 |
| `conversions` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 预定义操作（或操作）触发事件进行性能评估的次数。 |
| `federated` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 指示体验事件是否通过数据联合（例如，客户之间的数据共享）创建。 |
| `firstQuartiles` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 数字视频广告以正常速度播放其持续时间25%的次数。 |
| `impressions` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 发送给最终用户的可能被查看的广告展示次数。 |
| `midpoints` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 数字视频广告以正常速度播放其持续时间50%的次数。 |
| `starts` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 数字视频广告开始播放的次数。 |
| `thirdQuartiles` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 数字视频广告以正常速度播放其持续时间75%的次数。 |
| `timePlayed` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 最终用户在特定的定时媒体资源上花费的时间。 |
| `downloadedPlayback` | 布尔值 | 当设置为 `true`，表示点击是由于播放下载的广告会话而生成的。 |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

此 `adAssetReference` 对象捕获有关广告的资源信息。

![adAssetReference结构](../../images/field-groups/advertising-details/adAssetReference.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_dc.title` | 字符串 | 易于用户识别的广告资源名称。 |
| `_xmpDM.duration` | 整数 | 资源的长度或持续时间（以秒为单位）。 |
| `_id` | 字符串 | 广告资源的唯一标识符，位于以下位置之后 [Ad-ID标准](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | 字符串 | 广告中展现的产品所属的公司或品牌. |
| `campaign` | 字符串 | 广告营销活动的 ID. |
| `creativeID` | 字符串 | 广告创作的 ID. |
| `creativeURL` | 字符串 | 广告创作的 URL. |
| `placementID` | 字符串 | 广告的版面 ID. |
| `siteID` | 字符串 | 广告网站的 ID. |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

此 `adAssetViewDetails` 对象捕获广告播放的视图详细信息。

![adassetviewDetails结构](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL 广告时间]](../../data-types/ad-break.md) | 描述如何将定时广告插入定时媒体。 |
| `index` | 整数 | 父广告时间内的广告索引。 例如，第一个广告具有索引 `0` 第二个广告具有索引 `1`. |
| `playerName` | 字符串 | 负责呈现广告的播放器的名称. |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

此 `adViewability` object捕获最终用户看到的展示次数，例如播放器音量、库版本、窗口状态和广告视区维度。

![adViewability结构](../../images/field-groups/advertising-details/adViewability.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL 实施详细信息]](../../data-types/implementation-details.md) | 用于测量可见性量度的库的名称和版本。 |
| `measuredAdNotVisible` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 指示广告在展示时不可见，如可见性库测量的那样。 |
| `measuredMuted` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 指示广告在展示时由可见性库测量为静音。 |
| `unmeasurableIframe` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 指示广告显示在非活动窗口中，由展示时的可查看性库测量。 |
| `unmeasurableOther` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 指示由于iframe中显示的广告，可见性库无法正确执行测量。 |
| `viewabilityEligibleImpressions` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 面向配备可见性库的最终用户的广告展示。 |
| `viewabilityCompletes` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 面向最终用户的广告的完成时间，该广告被可见性库视为可在完成时查看。 |
| `viewableFirstQuartiles` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 面向最终用户的广告的第一个四分位点，这些点被可见性库视为可在播放第一个四分位点时查看。 |
| `viewableImpressions` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 被视为可见性库播放两秒后即可查看的面向最终用户的广告展示。 |
| `viewableMidpoints` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 面向最终用户的广告中点，这些广告被可见性库视为可在播放中点查看。 |
| `viewableThirdQuartiles` | [[!UICONTROL 衡量]](../../data-types/measure.md) | 面向最终用户的广告的第三个四分位点，这些点被可见性库视为可在播放第三个四分位点时查看。 |
| `activeWindow` | 布尔值 | 指示广告是否显示在用户设备的活动窗口中。 |
| `adHeight` | 整数 | 播放器的垂直像素数（在运行时测量）。 如果播放器有额外的控件或缩略图，这可能会大于广告的大小。 |
| `adUnitDepth` | 整数 | 发布者可以在容器(iFrame)中嵌入广告单元，以限制广告仅访问页面代码。 此值描述广告单位在其中显示的容器数。 |
| `adWidth` | 整数 | 播放器的水平像素数（在运行时测量）。 如果播放器有额外的控件或缩略图，这可能会大于广告的大小。 |
| `measurementEligible` | 布尔值 | 广告是否符合可见性测量的条件。 如果广告单元具有受支持的创意格式和标记类型，则广告符合条件。 |
| `percentViewable` | 整数 | 测量时被视为可见的广告中的像素百分比。 |
| `playerVolume` | 整数 | 在运行时测量的播放器音量百分比，其中 `0` 已静音，并且 `100` 是最大卷。 |
| `viewable` | 布尔值 | 指示广告在运行时是否可见。 当至少50%的广告在至少一秒内可见时，展示广告被视为可见。 当视频播放至少连续两秒且至少50%的广告可见时，视频广告被视为可见。 |
| `viewportHeight` | 整数 | 运行时测量的显示体验的窗口的垂直大小（以像素为单位）。 对于Web视图事件，此值表示浏览器视区高度。 |
| `viewportWidth` | 整数 | 运行时测量的显示体验的窗口的水平大小（以像素为单位）。 对于Web视图事件，此值表示浏览器视区宽度。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
