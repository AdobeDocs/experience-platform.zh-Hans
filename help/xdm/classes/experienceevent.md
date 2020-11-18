---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: XDM ExperienceEvent类
topic: overview
description: 此文档概述了XDM ExperienceEvent类。
translation-type: tm+mt
source-git-commit: 4d109244e57799c7e3837ceee3e2f5d17fbf0a18
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 1%

---


# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 是一个标准XDM类，它允许您在发生特定事件或达到特定条件集时创建系统的时间戳快照。

体验事件是已发生事件的事实记录，包括时间点和相关个人的身份。 事件可以是显式（直接可观察的人类行为）或隐式（在没有直接人类行为的情况下提出），记录时无需汇总或解释。 有关在平台生态系统中使用此类的详细信息，请参阅XDM [概述](../home.md#data-behaviors)。

类 [!DNL XDM ExperienceEvent] 本身为模式提供多个与时间序列相关的字段。 摄取数据时，将自动填充其中某些字段的值：

<img src="../images/classes/experienceevent.png" width="650" /><br />

| 属性 | 描述 |
| --- | --- |
| `_id` | 事件的唯一、由系统生成的字符串标识符。 此字段用于跟踪单个事件的唯一性、防止重复事件并在下游服务中查找该。 由于此字段是系统生成的，因此在数据获取过程中不应为其提供显式值。<br><br>必须区分的是，该字 **段不代** 表与个人有关的身份，而是数据本身的记录。 应将与个人有关的身份数据降级到 [身份字段](../schema/composition.md#identity) 。 |
| `eventMergeId` | 导致创建记录的所摄取批的ID。 该字段在数据获取时由系统自动填充。 |
| `eventType` | 指示记录的主事件类型的字符串。 附录部分提供了已接受的值及其 [定义](#eventType)。 |
| `identityMap` | 一个映射字段，它包含事件所应用的个人的一组命名空间标识。 系统会在摄取身份数据时自动更新此字段。 为了将此字段正确用于实 [时客户用户档案](../../profile/home.md)，请不要尝试手动更新数据操作中字段的内容。<br /><br />有关模式组合的更多信息，请 [参阅组合基础](../schema/composition.md#identityMap) 中有关标识映射的部分。 |
| `timestamp` | 事件或观察发生的时间。 所有日期时间值必须以 [RFC 3339格式](https://tools.ietf.org/html/rfc3339) 提供。 |

## 兼容混音 {#mixins}

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请 [参阅混合名称](../mixins/name-updates.md) 更新文档。

Adobe提供多个标准混音供类使 [!DNL XDM ExperienceEvent] 用。 以下是某个类常用混音的列表:

* [[!UICONTROL 最终用户ID详细信息]](../mixins/event/enduserids.md)
* [[!UICONTROL 环境详细信息]](../mixins/event/environment-details.md)

## 附录

以下部分包含有关XDM ExperienceEvent类 [!UICONTROL 的其他信] 息。

### xdm:eventType的已接受值 {#eventType}

下表概述了已接受的 `xdm:eventType`值及其定义：

| 值 | 定义 |
| --- | --- |
| `advertising.completes` | 已观看定时媒体资产完成。 这并不一定意味着观看者观看了整个视频，因为观看者可能已跳过了前面。 |
| `advertising.timePlayed` | 描述用户在特定定时媒体资产上所花费的时间。 |
| `advertising.federated` | 指示是否通过数据联盟创建体验事件（客户之间的数据共享）。 |
| `advertising.clicks` | 单击广告上的操作。 |
| `advertising.conversions` | 由客户执行的预定义操作，触发事件进行绩效评估。 |
| `advertising.firstQuartiles` | 数字视频广告以正常速度播放了25%的持续时间。 |
| `advertising.impressions` | 对有可能被观看的客户的广告印象。 |
| `advertising.midpoints` | 数字视频广告以正常速度播放了50%的持续时间。 |
| `advertising.starts` | 数字视频广告已开始播放。 |
| `advertising.thirdQuartiles` | 数字视频广告以正常速度播放了75%的持续时间。 |
| `web.webpagedetails.pageViews` | 网页已收到一个或多个视图。 |
| `web.webinteraction.linkClicks` | 链接已收到一次或多次点击。 |
| `commerce.checkouts` | 产品事件发生结帐列表。 如果一个结帐过程中有多个步骤，则可能存在多个结帐事件。 如果有多个步骤，则每个事件的时间戳和引用的页面／体验将用于标识按顺序表示的每个事件（步骤）。 |
| `commerce.productListAdds` | 产品已添加到产品列表或购物车。 |
| `commerce.productListOpens` | 新产品列表（购物车）已初始化或创建。 |
| `commerce.productListRemovals` | 一个或多个产品条目已从产品列表或购物车中删除。 |
| `commerce.productListReopens` | 不再可访问（放弃）的产品列表（购物车）已被客户重新激活，如通过再营销活动。 |
| `commerce.productListViews` | 产品列表或购物车已收到一个或多个视图。 |
| `commerce.productViews` | 产品已收到一个或多个视图。 |
| `commerce.purchases` | 已接受命令。 这是商务转换中唯一的必需操作。 购买事件必须引用产品列表。 |
| `commerce.saveForLaters` | 已保存产品列表供将来使用，如产品愿望列表。 |
| `delivery.feedback` | 投放的反馈事件，如电子邮件投放。 |
| `message.feedback` | 反馈事件，如发送给客户的消息的已发送／弹回／错误。 |
| `message.tracking` | 跟踪事件，如对发送给客户的消息执行打开／单击／自定义操作。 |