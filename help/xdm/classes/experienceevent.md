---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；身份映射；身份映射；架构设计；映射；事件建模；事件建模；最佳实践；事件；事件；
solution: Experience Platform
title: XDM ExperienceEvent类
description: 本文档概述了XDM ExperienceEvent类以及事件数据建模的最佳实践。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 是一个标准Experience Data Model (XDM)类，它允许您在发生特定事件或达到一组特定条件时，创建系统的带时间戳快照。

体验事件是所发生事件的事实记录，包括时间点和所涉及个人的身份。 事件可以是显式的（直接可观察的人类行为）或隐式的（在没有直接人类行为的情况下引发），并且记录时不进行聚集或解释。 有关此类在平台生态系统中使用的更多高级信息，请参阅 [XDM概述](../home.md#data-behaviors).

此 [!DNL XDM ExperienceEvent] 类本身为架构提供了多个与时序相关的字段。 其中两个字段(`_id` 和 `timestamp`)为 **必需** 对于所有基于类的架构，而其余架构是可选的。 某些字段的值会在摄取数据时自动填充。

![Platform UI中显示的XDM ExperienceEvent的结构](../images/classes/experienceevent/structure.png)

| 属性 | 描述 |
| --- | --- |
| `_id`<br>**(必需)** | 事件的唯一字符串标识符。 此字段用于跟踪单个事件的唯一性，防止数据重复，并在下游服务中查找该事件。 在某些情况下， `_id` 可以是 [通用唯一标识符(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一标识符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>如果要从源连接流式传输数据或直接从Parquet文件中摄取，则应通过连接使事件唯一的字段的特定组合来生成此值，如主ID、时间戳、事件类型等。 连接值必须为 `uri-reference` 带格式的字符串，这意味着必须删除任何冒号字符。 之后，应该使用SHA-256或您选择的其他算法对拼接值进行哈希处理。<br><br>区分以下内容非常重要： **此字段不表示与个人相关的身份**&#x200B;而不是数据记录本身。 与人员相关的身份数据应委派到 [标识字段](../schema/composition.md#identity) 由兼容的字段组提供。 |
| `eventMergeId` | 如果使用 [Adobe Experience Platform Web SDK](../../edge/home.md) 要摄取数据，这表示导致创建记录的摄取批次的ID。 此字段在数据摄取时由系统自动填充。 不支持在Web SDK实施的上下文之外使用此字段。 |
| `eventType` | 一个字符串，指明事件的类型或类别。 如果要区分同一架构和数据集中的不同事件类型（例如，将产品查看事件与零售公司的添加到购物车事件区分开），则可以使用此字段。<br><br>此属性的标准值提供在 [附录部分](#eventType)，包括预期使用案例的描述。 此字段是一个可扩展的枚举，这意味着您还可以使用自己的事件类型字符串对正在跟踪的事件进行分类。<br><br>`eventType` 限制您只能对应用程序上的每次点击使用单个事件，因此您必须使用计算字段让系统知道哪个事件最重要。 有关更多信息，请参阅以下部分： [计算字段的最佳实践](#calculated). |
| `producedBy` | 描述事件的制作者或起源的字符串值。 如果需要，此字段可用于过滤掉某些事件生成器，以实现分段。<br><br>此属性的一些建议值提供在 [附录部分](#producedBy). 此字段是一个可扩展的枚举，这意味着您还可以使用自己的字符串来表示不同的事件生成器。 |
| `identityMap` | 一个映射字段，其中包含事件应用于的个人的一组命名空间标识。 此字段在摄取身份数据时由系统自动更新。 为了正确使用此字段 [Real-time Customer Profile](../../profile/home.md)中，请勿尝试在数据操作中手动更新字段内容。<br /><br />请参阅中有关身份映射的部分 [模式组合基础](../schema/composition.md#identityMap) 以了解有关其用例的更多信息。 |
| `timestamp`<br>**(必需)** | 事件发生时间的ISO 8601时间戳，格式为 [RFC 3339第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6). 此时间戳必须发生在过去。 请参阅以下部分： [时间戳](#timestamps) 以获取有关使用此字段的最佳实践。 |

{style="table-layout:auto"}

## 事件建模的最佳实践

以下部分介绍了在Adobe Experience Platform中设计基于事件的Experience Data Model (XDM)架构的最佳实践。

### 时间戳 {#timestamps}

根 `timestamp` 事件架构的字段可以 **仅限** 表示对事件本身的观察，并且必须发生在过去。 如果您的分段用例需要使用将来可能发生的时间戳，则这些值必须限制在体验事件架构中的其他位置。

例如，如果旅游和酒店业的某个企业正在建模航班预订事件，则班级级别 `timestamp` 字段表示观察到预订事件的时间。 与事件相关的其他时间戳（如旅行预订的开始日期）应捕获在标准或自定义字段组提供的单独字段中。

![突出显示航班预订和开始日期的示例体验事件架构。](../images/classes/experienceevent/timestamps.png)

通过将类级别时间戳与事件架构中的其他相关日期时间值分开，您可以实施灵活的分段用例，同时保留体验应用程序中客户历程的时间戳记帐户。

### 使用计算字段 {#calculated}

体验应用程序中的某些交互可能会导致技术上共享同一事件时间戳的多个相关事件，因此可以表示为单个事件记录。 例如，如果客户查看了您网站上的产品，这可能会导致事件记录具有两种可能性 `eventType` 值：“产品查看”事件(`commerce.productViews`)或通用“页面查看”事件(`web.webpagedetails.pageViews`)。 在这些情况下，您可以在单次点击中捕获多个事件时，使用计算字段捕获最重要的属性。

[Adobe Experience Platform数据准备](../../data-prep/home.md) 允许您映射、转换和验证XDM之间的数据。 使用可用的 [映射函数](../../data-prep/functions.md) 通过此服务，您可以调用逻辑运算符，以便在数据被引入Experience Platform时优先考虑多事件记录中的数据、转换数据和/或合并这些数据。 在上面的示例中，您可以指定 `eventType` 作为计算字段，每当“产品视图”发生时，都会优先于“页面视图”。

如果您是通过UI手动将数据摄取到Platform，请参阅上的指南 [计算字段](../../data-prep/ui/mapping.md#calculated-fields) 有关如何创建计算字段的特定步骤。

如果您要使用源连接将数据流式传输到Platform，则可以配置源以利用计算字段。 请参阅 [特定源的文档](../../sources/home.md) 有关如何在配置连接时实施计算字段的说明。

## 兼容的架构字段组 {#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 查看文档 [字段组名称更新](../field-groups/name-updates.md) 了解更多信息。

Adobe提供了多个标准字段组以用于 [!DNL XDM ExperienceEvent] 类。 以下是类的一些常用字段组的列表：

* [[!UICONTROL Adobe Analytics ExperienceEvent完整扩展]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL 余额转帐]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL 营销活动详细信息]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 信息卡操作]](../field-groups/event/card-actions.md)
* [[!UICONTROL 渠道详细信息]](../field-groups/event/channel-details.md)
* [[!UICONTROL 商业详细信息]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 存款明细]](../field-groups/event/deposit-details.md)
* [[!UICONTROL 设备以旧换新详细信息]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL 餐饮预订]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL 最终用户ID详细信息]](../field-groups/event/enduserids.md)
* [[!UICONTROL 环境详细信息]](../field-groups/event/environment-details.md)
* [[!UICONTROL 航班预订]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0同意]](../field-groups/event/iab.md)
* [[!UICONTROL 住宿预订]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL 报价请求详细信息]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL 预订详细信息]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web详细信息]](../field-groups/event/web-details.md)

## 附录

以下部分包含有关 [!UICONTROL XDM ExperienceEvent] 类。

### 接受的值 `eventType` {#eventType}

下表概述了接受的值 `eventType`，以及它们的定义：

| 值 | 定义 |
| --- | --- |
| `advertising.clicks` | 单击广告上的操作。 |
| `advertising.completes` | 定时媒体资源已观看至结束。 这并不一定意味着观看者观看了整个视频，因为观看者可以跳过前面。 |
| `advertising.conversions` | 客户执行的预定义操作，触发性能评估事件。 |
| `advertising.federated` | 指示体验事件是否通过数据联合（客户之间共享数据）创建。 |
| `advertising.firstQuartiles` | 一个数字视频广告以正常速度播放了其25%的时长。 |
| `advertising.impressions` | 对可能观看的客户的广告展示。 |
| `advertising.midpoints` | 数字视频广告以正常速度播放了其50%的时长。 |
| `advertising.starts` | 数字视频广告已开始播放。 |
| `advertising.thirdQuartiles` | 一个数字视频广告以正常速度播放了其75%的时长。 |
| `advertising.timePlayed` | 描述用户在特定定时媒体资源上花费的时间。 |
| `application.close` | 应用程序已关闭或发送到后台。 |
| `application.launch` | 应用程序已启动或进入前台。 |
| `commerce.checkouts` | 产品列表发生了签出事件。 如果结账过程包含多个步骤，则可能有多个结账事件。 如果有多个步骤，则使用每个事件的时间戳和引用的页面/体验来标识每个单独的事件（步骤），并按顺序表示。 |
| `commerce.productListAdds` | 产品已添加到产品列表或购物车。 |
| `commerce.productListOpens` | 新产品列表（购物车）已初始化或创建。 |
| `commerce.productListRemovals` | 已从产品列表或购物车中删除一个或多个产品条目。 |
| `commerce.productListReopens` | 客户已重新激活不再可访问（已放弃）的产品列表（购物车），例如通过再营销活动。 |
| `commerce.productListViews` | 产品列表或购物车已收到一个或多个视图。 |
| `commerce.productViews` | 产品已收到一个或多个视图。 |
| `commerce.purchases` | 已接受订单。 这是商业转换中唯一需要的操作。 购买事件必须引用产品列表。 |
| `commerce.saveForLaters` | 已保存产品列表以供将来使用，例如产品愿望清单。 |
| `decisioning.propositionDisplay` | 向个人显示决策建议。 |
| `decisioning.propositionInteract` | 与决策建议交互的人。 |
| `delivery.feedback` | 投放的反馈事件，例如电子邮件投放。 |
| `directMarketing.emailBounced` | 发送给某人的电子邮件已退回。 |
| `directMarketing.emailBouncedSoft` | 发送给某人的电子邮件软退回。 |
| `directMarketing.emailClicked` | 用户单击了营销电子邮件中的链接。 |
| `directMarketing.emailDelivered` | 电子邮件已成功发送到人员的电子邮件服务 |
| `directMarketing.emailOpened` | 人员已打开营销电子邮件。 |
| `directMarketing.emailUnsubscribed` | 取消订阅营销电子邮件的人员。 |
| `inappmessageTracking.dismiss` | 已取消应用程序内消息。 |
| `inappmessageTracking.display` | 显示应用程序内消息。 |
| `inappmessageTracking.interact` | 与应用程序内消息进行了交互。 |
| `leadOperation.callWebhook` | 为响应潜在客户，调用了webhook。 |
| `leadOperation.convertLead` | 商机已转化。 |
| `leadOperation.interestingMoment` | 为一个人录制了一个有趣的时刻。 |
| `leadOperation.newLead` | 已创建潜在客户。 |
| `leadOperation.scoreChanged` | 商机的得分属性的值已更改。 |
| `leadOperation.statusInCampaignProgressionChanged` | 营销活动中的商机状态已更改。 |
| `listOperation.addToList` | 已将人员添加到营销列表。 |
| `listOperation.removeFromList` | 从营销列表中删除了一个人员。 |
| `message.feedback` | 发送给客户的消息的反馈事件，例如已发送/退回/错误。 |
| `message.tracking` | 跟踪事件，如对发送给客户的消息的打开/点击/自定义操作。 |
| `opportunityEvent.addToOpportunity` | 已向机会添加个人。 |
| `opportunityEvent.opportunityUpdated` | 机会已更新。 |
| `opportunityEvent.removeFromOpportunity` | 人员已从机会中删除。 |
| `pushTracking.applicationOpened` | 用户从推送通知中打开了应用程序。 |
| `pushTracking.customAction` | 人员单击了推送通知中的自定义操作。 |
| `web.formFilledOut` | 有人在wep页面上填写表单。 |
| `web.webinteraction.linkClicks` | 已选择链接一次或多次。 |
| `web.webpagedetails.pageViews` | 网页已收到一个或多个视图。 |

{style="table-layout:auto"}

### 建议值 `producedBy` {#producedBy}

下表概述了一些接受的值 `producedBy`：

| 值 | 定义 |
| --- | --- |
| `self` | 自身 |
| `system` | 系统 |
| `salesRef` | 销售代表 |
| `customerRep` | 客户代表 |
