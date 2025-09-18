---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；身份映射；身份映射；架构设计；映射；事件建模；事件建模；最佳实践；事件；事件；
solution: Experience Platform
title: XDM ExperienceEvent类
description: 了解XDM ExperienceEvent类和事件数据建模的最佳实践。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: f00b195567c22f69c05909e76906c8770da4b9d0
workflow-type: tm+mt
source-wordcount: '2777'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent]类

[!DNL XDM ExperienceEvent]是一个标准的体验数据模型(XDM)类。 此类用于在发生特定事件或达到特定条件集时创建带时间戳的系统快照。

体验事件是所发生事件的事实记录，包括时间点和所涉及人员的身份。 事件可以是显式的（直接可观察的人类行为）或隐式的（在没有直接人类行为的情况下引发），并且无需聚合或解释即可记录。 有关在Experience Platform生态系统中使用此类的更多高级信息，请参阅[XDM概述](../home.md#data-behaviors)。

[!DNL XDM ExperienceEvent]类本身为架构提供了多个与时间序列相关的字段。 其中两个字段（`_id`和`timestamp`）对于基于此类的所有架构都是&#x200B;**必填**，而其余字段是可选的。 在摄取数据时，会自动填充某些字段的值。

![Experience Platform UI中显示的XDM ExperienceEvent结构。](../images/classes/experienceevent/structure.png)

| 属性 | 描述 |
| --- | --- |
| `_id`<br>**（必需）** | Experience Event Class `_id`字段唯一标识摄取到Adobe Experience Platform中的各个事件。 此字段用于跟踪单个事件的唯一性，防止数据重复，并在下游服务中查找该事件。<br><br>在检测到重复事件的地方，Experience Platform应用程序和服务可能会以不同的方式处理重复。 例如，如果配置文件存储中已存在具有相同`_id`的事件，则删除配置文件服务中的重复事件。 但是，这些事件仍将记录在数据湖中。<br><br>在某些情况下，`_id`可以是[通用唯一标识符(UUID)](https://datatracker.ietf.org/doc/html/rfc4122)或[全局唯一标识符(GUID)](https://learn.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。<br><br>如果从源连接流式传输数据或直接从Parquet文件中摄取，则应当通过连接特定字段组合生成此值，这些字段组合使事件具有唯一性。 可连接的事件示例包括主ID、时间戳、事件类型等。 连接值必须为`uri-reference`格式字符串，这意味着必须删除任何冒号字符。 之后，应该使用SHA-256或您选择的其他算法对拼接值进行哈希处理。<br><br>请务必注意，**此字段不表示与个人**&#x200B;相关的身份，而是数据本身的记录。 与人员相关的身份数据应委托给兼容字段组提供的[身份字段](../schema/composition.md#identity)。 |
| `eventMergeId` | 如果使用[Adobe Experience Platform Web SDK](/help/web-sdk/home.md)摄取数据，则表示导致创建记录的摄取批次的ID。 此字段在数据摄取时由系统自动填充。 不支持在Web SDK实施的上下文之外使用此字段。 |
| `eventType` | 一个字符串，它指示事件的类型或类别。 如果要区分同一架构和数据集中的不同事件类型（例如，将产品查看事件与零售公司的添加到购物车事件区分开来），则可以使用此字段。<br><br>此属性的标准值在[附录部分](#eventType)中提供，包括预期使用案例的说明。 此字段是可扩展的枚举，这意味着您还可以使用自己的事件类型字符串对正在跟踪的事件进行分类。<br><br>`eventType`限制您在应用程序上每次点击只使用单个事件，因此您必须使用计算字段让系统知道哪个事件最重要。 有关详细信息，请参阅[计算字段的最佳实践](#calculated)部分。 |
| `producedBy` | 描述事件生成者或来源的字符串值。 如果需要，可以使用此字段过滤掉某些事件生成器，以用于分段目的。<br><br>该属性的某些建议值在[附录部分](#producedBy)中提供。 此字段是可扩展的枚举，这意味着您还可以使用自己的字符串来表示不同的事件生成器。 |
| `identityMap` | 一个映射字段，其中包含事件应用于的个人的一组命名空间标识。 此字段在摄取身份数据时由系统自动更新。 要为[实时客户档案](../../profile/home.md)正确使用此字段，请不要尝试在数据操作中手动更新字段的内容。<br /><br />有关其用例的更多信息，请参阅[架构组合基础知识](../schema/composition.md#identityMap)中关于标识映射的部分。 |
| `timestamp`<br>**（必需）** | 事件发生时间的ISO 8601时间戳，按照[RFC 3339第5.6](https://datatracker.ietf.org/doc/html/rfc3339)节格式设置。 此时间戳&#x200B;**必须**&#x200B;是过去的时间，但&#x200B;**必须**&#x200B;是从1970年开始的时间。 有关使用此字段的最佳实践，请参阅下面有关[时间戳](#timestamps)的部分。 |

{style="table-layout:auto"}

## 事件建模的最佳实践

以下部分介绍了在Adobe Experience Platform中设计基于事件的体验数据模型(XDM)架构的最佳实践。

### 时间戳 {#timestamps}

事件架构的根`timestamp`字段只能&#x200B;**2&rbrace;表示事件本身的观察结果，并且必须发生在过去。**&#x200B;但是，事件&#x200B;**必须**&#x200B;从1970年起发生。 如果分段用例需要使用将来可能发生的时间戳，则这些值必须限制在体验事件架构中的其他位置。

例如，如果旅游和酒店业的某家公司正在建模航班预订事件，则班级`timestamp`字段表示观察到预订事件的时间。 与事件相关的其他时间戳（如旅行预订的开始日期）应捕获在标准或自定义字段组提供的单独字段中。

![突出显示航班预订和开始日期的体验事件架构示例。](../images/classes/experienceevent/timestamps.png)

通过将类级别时间戳与事件架构中的其他相关日期时间值分开，您可以实施灵活的分段用例，同时保留体验应用程序中客户历程的时间戳帐户。

### 使用计算字段 {#calculated}

体验应用程序中的某些交互可能会导致技术上共享同一事件时间戳的多个相关事件，因此可以表示为单个事件记录。 例如，如果客户查看了您网站上的产品，这可能会导致事件记录具有两个潜在的`eventType`值：“产品查看”事件(`commerce.productViews`)或通用的“页面查看”事件(`web.webpagedetails.pageViews`)。 在这些情况下，您可以在单次点击中捕获多个事件时，使用计算字段捕获最重要的属性。

使用[Adobe Experience Platform数据准备](../../data-prep/home.md)来映射、转换和验证XDM中的数据。 使用该服务提供的可用[映射函数](../../data-prep/functions.md)，您可以调用逻辑运算符，以便在将数据引入Experience Platform时排列多事件记录数据的优先级、转换和/或合并这些数据。 在上述示例中，您可以指定`eventType`作为计算字段，无论何时发生“产品查看”与“页面查看”，该字段都会优先处理“产品查看”。

如果您是通过UI将数据手动摄取到Experience Platform，请参阅[计算字段](../../data-prep/ui/mapping.md#calculated-fields)指南，以了解有关如何创建计算字段的特定步骤。

如果您要使用源连接将数据流式传输到Experience Platform，则可以配置源以利用计算字段。 有关如何在配置连接时实施计算字段的说明，请参阅特定源[的](../../sources/home.md)文档。

## 兼容的架构字段组 {#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 有关详细信息，请参阅有关[字段组名称更新](../field-groups/name-updates.md)的文档。

Adobe提供了多个标准字段组以用于[!DNL XDM ExperienceEvent]类。 以下是类的一些常用字段组的列表：

* [[!UICONTROL Adobe Analytics ExperienceEvent完整扩展]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL 余额转帐]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL 营销活动详细信息]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 卡片操作]](../field-groups/event/card-actions.md)
* [[!UICONTROL 渠道详细信息]](../field-groups/event/channel-details.md)
* [[!UICONTROL Commerce详细信息]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 存款详细信息]](../field-groups/event/deposit-details.md)
* [[!UICONTROL 设备以旧换新详细信息]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL 餐饮预订]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL 最终用户ID详细信息]](../field-groups/event/enduserids.md)
* [[!UICONTROL 环境详细信息]](../field-groups/event/environment-details.md)
* [[!UICONTROL 航班预订]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0同意]](../field-groups/event/iab.md)
* [[!UICONTROL 住宿预订]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL MediaAnalytics交互详细信息]](../field-groups/event/mediaanalytics-interaction.md)
* [[!UICONTROL 报价请求详细信息]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL 预订详细信息]](../field-groups/event/reservation-details.md)
* [[!UICONTROL Web详细信息]](../field-groups/event/web-details.md)

## 附录

以下部分包含有关[!UICONTROL XDM ExperienceEvent]类的其他信息。

### `eventType`的接受值 {#eventType}

下表概述了`eventType`的接受值及其定义：

| 值 | 定义 |
| --- | --- |
| `advertising.clicks` | 此事件跟踪选择播发的操作何时发生。 |
| `advertising.completes` | 此事件跟踪定时媒体资源在何时观看完毕。 这并不一定意味着观看者观看了整个视频，因为观看者可以跳过前面。 |
| `advertising.conversions` | 此事件跟踪客户执行的预定义操作，该操作会触发绩效评估事件。 |
| `advertising.federated` | 此事件跟踪体验事件是否通过数据联合（客户之间的数据共享）创建。 |
| `advertising.firstQuartiles` | 此事件跟踪数字视频广告何时以正常速度播放了其25%的时长。 |
| `advertising.impressions` | 此事件跟踪对有可能被查看的客户的广告展示次数。 |
| `advertising.midpoints` | 此事件跟踪数字视频广告何时以正常速度播放了其50%的时长。 |
| `advertising.starts` | 此事件跟踪数字视频广告何时开始播放。 |
| `advertising.thirdQuartiles` | 此事件跟踪数字视频广告何时以正常速度播放了其75%的时长。 |
| `advertising.timePlayed` | 此事件可跟踪用户在特定定时媒体资源上花费的时间。 |
| `application.close` | 此事件跟踪应用程序何时关闭或发送到后台。 |
| `application.launch` | 此事件跟踪应用程序启动或进入前台的时间。 |
| `click` | **已弃用**，请改用`decisioning.propositionInteract`。 |
| `commerce.backofficeCreditMemoIssued` | 此事件跟踪向客户发出信用通知的时间。 |
| `commerce.backofficeOrderCancelled` | 此事件跟踪以前启动的购买流程在完成前何时终止。 |
| `commerce.backofficeOrderItemsShipped` | 此事件会跟踪购买的项目实际发运给客户的时间。 |
| `commerce.backofficeOrderPlaced` | 此事件跟踪订单的投放情况。 |
| `commerce.backofficeShipmentCompleted` | 此事件用于跟踪整个发运流程的成功完成。 |
| `commerce.checkouts` | 此事件跟踪产品列表何时发生签出事件。 如果结账过程包含多个步骤，则可能有多个结账事件。 如果有多个步骤，则会使用时间戳和每个事件的引用页面/体验来标识每个单独事件（步骤），并按顺序表示。 |
| `commerce.productListAdds` | 此事件会跟踪产品何时添加到产品列表或购物车。 |
| `commerce.productListOpens` | 此事件跟踪新产品列表（购物车）何时已初始化或创建。 |
| `commerce.productListRemovals` | 此事件会跟踪从产品列表或购物车中删除产品条目的时间。 |
| `commerce.productListReopens` | 此事件会跟踪客户何时重新激活不再可访问（已放弃）的产品列表（购物车），例如通过再营销活动。 |
| `commerce.productListViews` | 此事件会跟踪产品列表或购物车何时收到视图。 |
| `commerce.productViews` | 此事件跟踪产品何时收到一个或多个视图。 |
| `commerce.purchases` | 此事件跟踪订单何时被接受。 这是商业转换中唯一需要执行的操作。 购买事件必须具有引用的产品列表。 |
| `commerce.saveForLaters` | 此事件会跟踪产品列表在保存以供将来使用，例如产品愿望清单。 |
| `decisioning.propositionDisplay` | 当Web SDK自动发送有关页面上所显示内容的信息时，将使用此事件。 但是，如果您已经以其他方式包括显示信息（例如通过页面点击的顶部和底部），则不需要此事件类型。 对于页面点击的底部，您可以选择喜欢的任何事件类型。 |
| `decisioning.propositionDismiss` | 在取消Adobe Journey Optimizer应用程序内消息或内容卡时，将使用此事件类型。 |
| `decisioning.propositionFetch` | 用于指示某个事件主要用于获取决策。 Adobe Analytics将自动删除此事件。 |
| `decisioning.propositionInteract` | 此事件类型用于跟踪个性化内容上的交互（例如点击）。 |
| `decisioning.propositionSend` | 此事件会跟踪何时决定向潜在客户发送推荐或选件以供考虑。 |
| `decisioning.propositionTrigger` | 此类型的事件由[Web SDK](../../web-sdk/home.md)存储在本地存储中，但未发送到Experience Edge。 每次满足规则集时，都会生成一个事件并将其存储在本地存储中（如果该设置已启用）。 |
| `delivery.feedback` | 此事件跟踪投放的反馈事件，如电子邮件投放。 |
| `directMarketing.emailBounced` | 此事件可跟踪发送给人员的电子邮件何时退回。 |
| `directMarketing.emailBouncedSoft` | 此事件可跟踪发送给人员的电子邮件何时软退回。 |
| `directMarketing.emailClicked` | 此事件可跟踪用户何时单击营销电子邮件中的链接。 |
| `directMarketing.emailDelivered` | 此事件跟踪电子邮件何时成功发送到人员的电子邮件服务。 |
| `directMarketing.emailOpened` | 此事件可跟踪人员何时打开营销电子邮件。 |
| `directMarketing.emailSent` | 此事件可跟踪营销电子邮件何时发送给人员。 |
| `directMarketing.emailUnsubscribed` | 此事件跟踪人员何时取消订阅营销电子邮件。 |
| `display` | **已弃用**，请改用`decisioning.propositionDisplay`。 |
| `inappmessageTracking.dismiss` | 此事件跟踪何时取消应用程序内消息。 |
| `inappmessageTracking.display` | 此事件会跟踪应用程序内消息的显示时间。 |
| `inappmessageTracking.interact` | 此事件会跟踪与应用程序内消息交互的时间。 |
| `leadOperation.callWebhook` | 此事件跟踪何时调用webhook来响应潜在客户。 |
| `leadOperation.changeCampaignStream` | 此事件表示特定业务商机的营销或参与策略发生变化。 |
| `leadOperation.changeEngagementCampaignCadence` | 此事件会跟踪在营销活动中商机与的参与频率何时发生更改。 |
| `leadOperation.convertLead` | 此事件跟踪商机何时转化。 |
| `leadOperation.interestingMoment` | 此事件跟踪何时为人员录制了有趣的时刻。 |
| `leadOperation.mergeLeads` | 此事件会跟踪来自引用同一实体的多个潜在客户的信息何时合并。 |
| `leadOperation.newLead` | 此事件会跟踪销售线索的创建时间。 |
| `leadOperation.scoreChanged` | 此事件跟踪商机的得分属性值何时更改。 |
| `leadOperation.statusInCampaignProgressionChanged` | 此事件跟踪营销活动中的商机状态何时已更改。 |
| `listOperation.addToList` | 此事件会跟踪将人员添加到营销列表的时间。 |
| `listOperation.removeFromList` | 此事件跟踪人员从营销列表中移除的时间。 |
| `media.adBreakComplete` | 此事件表示广告时间的结束。 |
| `media.adBreakStart` | 此事件表示广告时间的开始。 |
| `media.adComplete` | 此事件表示广告结束。 |
| `media.adSkip` | 此事件在跳过广告时发出信号。 |
| `media.adStart` | 此事件表示广告的开始。 |
| `media.bitrateChange` | 此事件在比特率发生更改时发出信号。 |
| `media.bufferStart` | 缓冲开始时发送`media.bufferStart`事件类型。 没有特定的`bufferResume`事件类型；在发生`play`事件后发送`bufferStart`事件时，将视为已恢复缓冲。 |
| `media.chapterComplete` | 此事件表示章节结束。 |
| `media.chapterSkip` | 当用户向前或向后跳到其他部分或章节时，将触发此事件。 |
| `media.chapterStart` | 此事件表示章节的开始。 |
| `media.downloaded` | 此事件跟踪媒体下载内容的发生时间。 |
| `media.error` | 此事件表示媒体播放期间发生错误。 |
| `media.pauseStart` | 此事件跟踪何时发生`pauseStart`事件。 当用户启动媒体播放暂停时，将触发此事件。 没有恢复事件类型。 在`pauseStart`后发送播放事件时推断为恢复。 |
| `media.ping` | `media.ping`事件类型用于指示正在进行的播放状态。 对于主内容，在播放期间必须每10秒发送一次此事件，从播放开始后的10秒开始。 对于广告内容，必须在广告跟踪期间每秒发送一次。 Ping事件不应在请求正文中包含参数映射。 |
| `media.play` | 当播放器从其他状态(如`media.play` `playing` （用户恢复时）或`buffering,` （恢复时），包括自动播放等场景)转换为`paused`状态时发送`error`事件类型。 此事件由播放器的`on('Playing')`回调触发。 |
| `media.sessionComplete` | 当到达主内容的结尾时，将发送此事件。 |
| `media.sessionEnd` | 当用户放弃查看并且不太可能返回时，`media.sessionEnd`事件类型会通知Media Analytics后端立即关闭会话。 如果未发送此事件，则会话将在处于不活动状态10分钟后超时，或者播放头未移动30分钟后超时。 任何使用该会话ID的后续媒体调用都将被忽略。 |
| `media.sessionStart` | `media.sessionStart`事件类型随会话启动调用一起发送。 在收到响应时，将从Location标头中提取会话ID，并将其用于对收集服务器的所有后续事件调用。 |
| `media.statesUpdate` | 此事件跟踪何时发生`statesUpdate`事件。 播放器状态跟踪功能可以附加到音频或视频流。 标准状态为： `fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`和`inFocus`。 |
| `opportunityEvent.addToOpportunity` | 此事件跟踪人员添加到商机的时间。 |
| `opportunityEvent.opportunityUpdated` | 此事件跟踪销售机会的更新时间。 |
| `opportunityEvent.removeFromOpportunity` | 此事件跟踪人员从机会中删除的时间。 |
| `personalization.request` | **已弃用**，请改用`decisioning.propositionFetch`。 |
| `pushTracking.applicationOpened` | 此事件跟踪人员从推送通知中打开应用程序的时间。 |
| `pushTracking.customAction` | 此事件跟踪人员何时在推送通知中选择了自定义操作。 |
| `web.formFilledOut` | 此事件跟踪人员在网页上填写表单的时间。 |
| `web.webinteraction.linkClicks` | 事件表示Web SDK已自动记录链接点击。 |
| `web.webpagedetails.pageViews` | 此事件类型是将点击标记为页面查看的标准方法。 |
| `location.entry` | 此事件跟踪人员或设备在特定位置的进入。 |
| `location.exit` | 此事件跟踪人员或设备从特定位置的退出。 |

{style="table-layout:auto"}

### `producedBy`的建议值 {#producedBy}

下表概述了`producedBy`的一些接受值：

| 值 | 定义 |
| --- | --- |
| `self` | 自身 |
| `system` | 系统 |
| `salesRef` | 销售代表 |
| `customerRep` | 客户代表 |
