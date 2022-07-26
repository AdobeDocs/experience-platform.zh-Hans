---
title: 广告详细信息架构字段组
description: 本文档概述了广告详细信息架构字段组。
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 9%

---

# [!UICONTROL 广告详细信息] 架构字段组

[!UICONTROL 广告详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供了 `advertising` 对象到架构，该架构可捕获与广告展示次数、点进次数和归因相关的信息。

![字段组结构](../../images/field-groups/advertising-details/structure.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `adAssetReference` | 对象 | 捕获有关广告的资产信息。 请参阅 [下文](#adAssetReference) 以了解有关此对象结构的详细信息。 |
| `adAssetViewDetails` | 对象 | 捕获广告播放的视图详细信息。 请参阅 [下文](#adAssetViewDetails) 以了解有关此对象结构的详细信息。 |
| `adViewability` | 对象 | 捕获最终用户看到的展示次数，如播放器卷、库版本、窗口状态和广告视区维度。 请参阅 [下文](#adViewability) 以了解有关此对象结构的详细信息。 |
| `clicks` | [[!UICONTROL 测量]](../../data-types/measure.md) | 广告上的点击操作数。 |
| `completes` | [[!UICONTROL 测量]](../../data-types/measure.md) | 已观看至定时媒体资产结束的次数。 这不一定意味着最终用户观看了整个视频，因为他们可能跳过了前面。 |
| `conversions` | [[!UICONTROL 测量]](../../data-types/measure.md) | 预定义操作（或操作）触发事件以进行性能评估的次数。 |
| `federated` | [[!UICONTROL 测量]](../../data-types/measure.md) | 指示体验事件是否是通过数据联合（如客户之间的数据共享）创建的。 |
| `firstQuartiles` | [[!UICONTROL 测量]](../../data-types/measure.md) | 数字视频广告以正常速度播放其持续时间的25%的次数。 |
| `impressions` | [[!UICONTROL 测量]](../../data-types/measure.md) | 发送给最终用户的广告展示次数，并且可能会被查看。 |
| `midpoints` | [[!UICONTROL 测量]](../../data-types/measure.md) | 数字视频广告以正常速度播放其持续时间的50%的次数。 |
| `starts` | [[!UICONTROL 测量]](../../data-types/measure.md) | 数字视频广告开始播放的次数。 |
| `thirdQuartiles` | [[!UICONTROL 测量]](../../data-types/measure.md) | 数字视频广告以正常速度播放其持续时间的75%的次数。 |
| `timePlayed` | [[!UICONTROL 测量]](../../data-types/measure.md) | 最终用户在特定定时媒体资产上所花费的时间。 |
| `downloadedPlayback` | 布尔型 | 当设置为 `true`，表示点击是由于播放下载的广告会话而生成的。 |

{style=&quot;table-layout:auto&quot;}

## `adAssetReference` {#adAssetReference}

的 `adAssetReference` 对象会捕获有关广告的资产信息。

![adAssetReference结构](../../images/field-groups/advertising-details/adAssetReference.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_dc.title` | 字符串 | 广告资产的友好且用户可读的名称。 |
| `_xmpDM.duration` | 整数 | 资产的长度或持续时间（以秒为单位）。 |
| `_id` | 字符串 | 广告资产的唯一标识符，位于 [广告ID标准](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | 字符串 | 广告中展现的产品所属的公司或品牌. |
| `campaign` | 字符串 | 广告营销活动的 ID. |
| `creativeID` | 字符串 | 广告创作的 ID. |
| `creativeURL` | 字符串 | 广告创作的 URL. |
| `placementID` | 字符串 | 广告的版面 ID. |
| `siteID` | 字符串 | 广告网站的 ID. |

{style=&quot;table-layout:auto&quot;}

## `adAssetViewDetails` {#adAssetViewDetails}

的 `adAssetViewDetails` 对象会捕获广告播放的视图详细信息。

![adAssetViewDetails结构](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL 广告时间]](../../data-types/ad-break.md) | 描述如何将定时广告插入到定时媒体中。 |
| `index` | 整数 | 广告在父广告时间内的索引。 例如，第一个广告具有索引 `0` 第二个广告有索引 `1`. |
| `playerName` | 字符串 | 负责呈现广告的播放器的名称. |

{style=&quot;table-layout:auto&quot;}

## `adViewability` {#adViewability}

的 `adViewability` 对象可捕获最终用户看到的展示次数，如播放器卷、库版本、窗口状态和广告视区维度。

![adViewability结构](../../images/field-groups/advertising-details/adViewability.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL 实施详细信息]](../../data-types/implementation-details.md) | 用于测量可见性量度的库的名称和版本。 |
| `measuredAdNotVisible` | [[!UICONTROL 测量]](../../data-types/measure.md) | 表示广告在展示时不可见，由可见性库测量。 |
| `measuredMuted` | [[!UICONTROL 测量]](../../data-types/measure.md) | 指示广告在展示时被可视性库测量为静音。 |
| `unmeasurableIframe` | [[!UICONTROL 测量]](../../data-types/measure.md) | 指示广告在展示时显示在不活动窗口中，由可见性库测量。 |
| `unmeasurableOther` | [[!UICONTROL 测量]](../../data-types/measure.md) | 指示由于广告显示在iframe中，因此视区库无法正确执行测量。 |
| `viewabilityEligibleImpressions` | [[!UICONTROL 测量]](../../data-types/measure.md) | 带有可视性库工具的广告向最终用户的展示。 |
| `viewabilityCompletes` | [[!UICONTROL 测量]](../../data-types/measure.md) | 在可见性库视为可在完成时查看的最终用户完成广告。 |
| `viewableFirstQuartiles` | [[!UICONTROL 测量]](../../data-types/measure.md) | 广告的第一个四分位数给最终用户，该最终用户被视为可在可见性库播放的第一个四分位数处查看。 |
| `viewableImpressions` | [[!UICONTROL 测量]](../../data-types/measure.md) | 在可视性库播放两秒钟后，被视为可查看的最终用户对广告的展示次数。 |
| `viewableMidpoints` | [[!UICONTROL 测量]](../../data-types/measure.md) | 广告的中点，给被视为在播放的中点处观看的最终用户。 |
| `viewableThirdQuartiles` | [[!UICONTROL 测量]](../../data-types/measure.md) | 广告的三分位数给最终用户，该用户被视为可在播放的三分位数处观看，可见性库将其视为可见。 |
| `activeWindow` | 布尔型 | 指示广告是否显示在用户设备的活动窗口中。 |
| `adHeight` | 整数 | 播放器的垂直像素数，在运行时测量。 如果播放器具有额外的控件或缩略图，则此值可能大于广告的大小。 |
| `adUnitDepth` | 整数 | 发布者可以在容器(iFrame)中嵌入广告单元，以限制广告仅访问页面代码。 此值描述广告单元在中显示的容器数。 |
| `adWidth` | 整数 | 播放器的水平像素数，在运行时测量。 如果播放器具有额外的控件或缩略图，则此值可能大于广告的大小。 |
| `measurementEligible` | 布尔型 | 广告是否符合可查看性测量条件。 如果广告单元具有受支持的创作格式和标记类型，则该广告符合条件。 |
| `percentViewable` | 整数 | 在测量时被视为可见的广告中的像素百分比。 |
| `playerVolume` | 整数 | 运行时测量的播放器音量百分比，其中 `0` 静音和 `100` 是最大卷数。 |
| `viewable` | 布尔型 | 指示广告在运行时是否可查看。 当至少50%的广告在至少一秒内可见时，即视为可查看展示广告。 当视频连续播放至少两秒时，至少50%的广告可见，则视为可观看视频广告。 |
| `viewportHeight` | 整数 | 在运行时测量内部显示体验的窗口的垂直大小（以像素为单位）。 对于Web视图事件，此值表示浏览器视区高度。 |
| `viewportWidth` | 整数 | 在运行时测量内部显示体验的窗口的水平大小（以像素为单位）。 对于Web视图事件，此值表示浏览器视区宽度。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
