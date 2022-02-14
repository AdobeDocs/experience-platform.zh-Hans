---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；标识映射；身份映射；架构设计；映射；事件建模；最佳实践；事件；事件；
solution: Experience Platform
title: XDM ExperienceEvent类
topic-legacy: overview
description: 本文档概述了XDM ExperienceEvent类以及事件数据建模的最佳实践。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 07fdbf467f3dde16f9216db47099b92cbbfd18d2
workflow-type: tm+mt
source-wordcount: '1783'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 是一个标准的体验数据模型(XDM)类，它允许您在发生特定事件或达到一组特定条件时，为系统创建带有时间戳的快照。

体验事件是所发生事件的事实记录，包括所涉个人的时间点和身份。 事件可以是显式（直接可观察的人为行为）或隐式（不直接人为行为而引起），并且记录时没有汇总或解释。 有关在平台生态系统中使用此类的更多高级信息，请参阅 [XDM概述](../home.md#data-behaviors).

的 [!DNL XDM ExperienceEvent] 类本身为架构提供了多个与时间序列相关的字段。 摄取数据时，会自动填充其中某些字段的值：

![](../images/classes/experienceevent/structure.png)

| 属性 | 描述 |
| --- | --- |
| `_id` | 事件的唯一字符串标识符。 此字段用于跟踪单个事件的唯一性，防止重复数据，并在下游服务中查找该事件。 在某些情况下， `_id` 可以 [通用唯一标识符(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一标识符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>如果从源连接流式传输数据或直接从Parquet文件摄取数据，则应通过关联使事件具有唯一性的特定字段组合（如主ID、时间戳、事件类型等）来生成此值。 拼接值必须是 `uri-reference` 格式化的字符串，这意味着必须删除任何冒号字符。 之后，连接值应使用SHA-256或您选择的其他算法进行哈希处理。<br><br>要区分这一点很重要 **此字段不表示与个人相关的身份**，而是数据本身的记录。 与个人有关的身份数据应降级为 [身份字段](../schema/composition.md#identity) 由兼容的字段组提供。 |
| `eventMergeId` | 如果使用 [Adobe Experience Platform Web SDK](../../edge/home.md) 要摄取数据，此值表示被摄取的批次创建记录的ID。 在摄取数据时，系统会自动填充此字段。 不支持在Web SDK实施的上下文之外使用此字段。 |
| `eventType` | 表示事件类型或类别的字符串。 如果要区分同一架构和数据集中的不同事件类型，例如区分某个产品查看事件与某个零售公司的添加到购物车事件，则可以使用此字段。<br><br>此属性的标准值在 [附录节](#eventType)，包括其预期用例的描述。 此字段是一个可扩展枚举，这意味着您还可以使用自己的事件类型字符串对您跟踪的事件进行分类。<br><br>`eventType` 限制您在应用程序上每次点击只使用一个事件，因此您必须使用计算字段告知系统最重要的事件。 有关更多信息，请参阅 [计算字段的最佳实践](#calculated). |
| `producedBy` | 描述事件的制作者或来源的字符串值。 如果出于分段目的需要，可使用此字段过滤掉某些事件生成器。<br><br>此属性的一些建议值在 [附录节](#producedBy). 此字段是一个可扩展枚举，这意味着您还可以使用自己的字符串来表示不同的事件生成器。 |
| `identityMap` | 映射字段，其中包含事件所应用的个人的一组命名空间标识。 在摄取身份数据时，系统会自动更新此字段。 为了正确利用此字段 [实时客户资料](../../profile/home.md)，请勿尝试手动更新数据操作中字段的内容。<br /><br />请参阅 [架构组合基础知识](../schema/composition.md#identityMap) ，以了解其用例的详细信息。 |
| `timestamp` | 事件发生时的ISO 8601时间戳，格式如下 [RFC 3339第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6). 此时间戳必须在过去发生。 请参阅下面的章节 [时间戳](#timestamps) 以了解有关使用此字段的最佳实践。 |

{style=&quot;table-layout:auto&quot;}

## 事件建模的最佳实践

以下部分介绍了在Adobe Experience Platform中设计基于事件的体验数据模型(XDM)架构的最佳实践。

### 时间戳 {#timestamps}

根 `timestamp` 事件架构的字段可以 **仅** 表示事件本身的观察，且必须在过去发生。 如果您的分段用例需要使用将来可能发生的时间戳，则这些值必须在体验事件架构的其他位置受到限制。

例如，如果旅游和酒店业的企业正在为航班预订事件建模，则为类级别 `timestamp` 字段表示观察到预订事件的时间。 与事件相关的其他时间戳（如旅行预订的开始日期）应在标准字段组或自定义字段组提供的单独字段中捕获。

![](../images/classes/experienceevent/timestamps.png)

通过将类级别时间戳与事件架构中其他相关的日期时间值分开，您可以实施灵活的分段用例，同时在体验应用程序中保留客户历程的带有时间戳的帐户。

### 使用计算字段 {#calculated}

您的体验应用程序中的某些交互可能会导致多个相关事件，这些事件在技术上共享相同的事件时间戳，因此可以表示为单个事件记录。 例如，如果客户查看了您网站上的产品，则可能会生成具有两个潜在可能性的事件记录 `eventType` 值：“产品查看”事件(`commerce.productViews`)或通用的“页面查看”事件(`web.webpagedetails.pageViews`)。 在这些情况下，当在一次点击中捕获多个事件时，您可以使用计算字段捕获最重要的属性。

[Adobe Experience Platform数据准备](../../data-prep/home.md) 允许您在XDM中映射、转换和验证数据。 使用可用的 [映射函数](../../data-prep/functions.md) 由服务提供，在摄取到Experience Platform时，您可以调用逻辑运算符以对来自多事件记录的数据进行优先级排序、转换和/或整合。 在上例中，您可以指定 `eventType` 作为计算字段，当“产品查看”优先于“页面查看”时，它们会优先处理。

如果要通过UI手动将数据摄取到平台，请参阅 [计算字段](../../data-prep/ui/mapping.md#calculated-fields) 以了解有关如何创建计算字段的特定步骤。

如果您使用源连接将数据流式传输到平台，则可以将源配置为改用计算字段。 请参阅 [特定源的文档](../../sources/home.md) 有关如何在配置连接时实施计算字段的说明。

## 兼容的架构字段组 {#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 请参阅 [字段组名称更新](../field-groups/name-updates.md) 以了解更多信息。

Adobe提供了多个与 [!DNL XDM ExperienceEvent] 类。 以下是类的一些常用字段组的列表：

* [[!UICONTROL 促销活动营销详细信息]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 渠道详细信息]](../field-groups/event/channel-details.md)
* [[!UICONTROL 商务详细信息]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 设备更换详细信息]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL 餐饮预订]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL 最终用户ID详细信息]](../field-groups/event/enduserids.md)
* [[!UICONTROL 环境详细信息]](../field-groups/event/environment-details.md)
* [[!UICONTROL 航班预订]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0同意]](../field-groups/event/iab.md)
* [[!UICONTROL 住宿预订]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL 保留详细信息]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web详细信息]](../field-groups/event/web-details.md)

## 附录

以下部分包含有关 [!UICONTROL XDM ExperienceEvent] 类。

### 的接受值 `eventType` {#eventType}

下表概述了 `eventType`，及其定义：

| 值 | 定义 |
| --- | --- |
| `advertising.clicks` | 单击广告上的操作。 |
| `advertising.completes` | 已观看至结束定时媒体资产。 这不一定意味着查看者观看了整个视频，因为查看者可以跳到前面。 |
| `advertising.conversions` | 由客户执行的预定义操作，该操作会触发事件以进行性能评估。 |
| `advertising.federated` | 指示体验事件是否是通过数据联合（客户之间的数据共享）创建的。 |
| `advertising.firstQuartiles` | 数字视频广告以正常速度播放了其持续时间的25%。 |
| `advertising.impressions` | 向客户展示的广告，有可能被查看。 |
| `advertising.midpoints` | 数字视频广告以正常速度播放了其持续时间的50%。 |
| `advertising.starts` | 开始播放数字视频广告。 |
| `advertising.thirdQuartiles` | 数字视频广告以正常速度播放了其持续时间的75%。 |
| `advertising.timePlayed` | 描述用户在特定定时媒体资产上所花费的时间。 |
| `application.close` | 应用程序已关闭或已发送到后台。 |
| `application.launch` | 应用程序已启动或已置于前台。 |
| `commerce.checkouts` | 产品列表已发生结帐事件。 如果结帐流程中存在多个步骤，则可能会有多个结帐事件。 如果有多个步骤，则会使用每个事件的时间戳和引用的页面/体验来标识按顺序表示的每个单个事件（步骤）。 |
| `commerce.productListAdds` | 产品已添加到产品列表或购物车。 |
| `commerce.productListOpens` | 已初始化或创建新产品列表（购物车）。 |
| `commerce.productListRemovals` | 已从产品列表或购物车中删除一个或多个产品条目。 |
| `commerce.productListReopens` | 客户已重新激活不再可访问（放弃）的产品列表（购物车），例如通过再营销活动。 |
| `commerce.productListViews` | 产品列表或购物车已收到一个或多个查看。 |
| `commerce.productViews` | 产品已收到一个或多个查看。 |
| `commerce.purchases` | 已接受命令。 这是商务转化中唯一必需的操作。 购买事件必须引用产品列表。 |
| `commerce.saveForLaters` | 已保存产品列表供将来使用，如产品愿望列表。 |
| `decisioning.propositionDisplay` | 一个决策建议被展示给一个人。 |
| `decisioning.propositionInteract` | 一个人与决策建议互动。 |
| `delivery.feedback` | 投放的反馈事件，如电子邮件投放。 |
| `directMarketing.emailBounced` | 向人员发送的电子邮件已退回。 |
| `directMarketing.emailBouncedSoft` | 向人员发送的电子邮件已软退件。 |
| `directMarketing.emailClicked` | 人员单击了营销电子邮件中的链接。 |
| `directMarketing.emailDelivered` | 已成功将电子邮件发送给人员的电子邮件服务 |
| `directMarketing.emailOpened` | 某人打开了营销电子邮件。 |
| `directMarketing.emailUnsubscribed` | 从营销电子邮件取消订阅的用户。 |
| `inappmessageTracking.dismiss` | 应用程序内消息被取消。 |
| `inappmessageTracking.display` | 显示应用程序内消息。 |
| `inappmessageTracking.interact` | 与应用程序内消息进行了交互。 |
| `leadOperation.callWebhook` | 为响应某个线索，调用了网页挂接。 |
| `leadOperation.convertLead` | 商机已转换。 |
| `leadOperation.interestingMoment` | 为一个人录制了一个有趣的时刻。 |
| `leadOperation.newLead` | 已创建潜在客户。 |
| `leadOperation.scoreChanged` | 潜在客户的分数属性的值已更改。 |
| `leadOperation.statusInCampaignProgressionChanged` | 营销活动中潜在客户的状态已更改。 |
| `listOperation.addToList` | 将人员添加到营销列表。 |
| `listOperation.removeFromList` | 人员已从营销列表中删除。 |
| `message.feedback` | 向客户发送的消息的反馈事件，如已发送/退回/错误。 |
| `message.tracking` | 跟踪事件，如对发送给客户的消息执行打开/点击/自定义操作。 |
| `opportunityEvent.addToOpportunity` | 将人员添加到机会中。 |
| `opportunityEvent.opportunityUpdated` | 更新了机会。 |
| `opportunityEvent.removeFromOpportunity` | 人员被从机会中移走。 |
| `pushTracking.applicationOpened` | 人员从推送通知中打开了应用程序。 |
| `pushTracking.customAction` | 用户在推送通知中单击了自定义操作。 |
| `web.formFilledOut` | 某人在wep页上填写了表格。 |
| `web.webinteraction.linkClicks` | 已选择链接一次或多次。 |
| `web.webpagedetails.pageViews` | 网页已收到一个或多个查看。 |

{style=&quot;table-layout:auto&quot;}

### 的建议值 `producedBy` {#producedBy}

下表概述了 `producedBy`:

| 值 | 定义 |
| --- | --- |
| `self` | Self |
| `system` | 系统 |
| `salesRef` | 销售代表 |
| `customerRep` | 客户代表 |
