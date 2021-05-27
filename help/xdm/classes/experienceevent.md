---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；标识映射；身份映射；架构设计；映射；事件建模；最佳实践；事件；事件；
solution: Experience Platform
title: XDM ExperienceEvent类
topic-legacy: overview
description: 本文档概述了XDM ExperienceEvent类以及事件数据建模的最佳实践。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 是一个标准的体验数据模型(XDM)类，它允许您在发生特定事件或达到一组特定条件时，为系统创建带有时间戳的快照。

体验事件是所发生事件的事实记录，包括所涉个人的时间点和身份。 事件可以是显式（直接可观察的人为行为）或隐式（不直接人为行为而引起），并且记录时没有汇总或解释。 有关在平台生态系统中使用此类的更多高级信息，请参阅[XDM概述](../home.md#data-behaviors)。

[!DNL XDM ExperienceEvent]类本身为架构提供了多个与时间序列相关的字段。 摄取数据时，会自动填充其中某些字段的值：

![](../images/classes/experienceevent/structure.png)

| 属性 | 描述 |
| --- | --- |
| `_id` | 事件的唯一字符串标识符。 此字段用于跟踪单个事件的唯一性，防止重复数据，并在下游服务中查找该事件。<br><br>在某些情况下， `_id` 可以是通 [用唯一标识符(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一标识符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。在Adobe Experience Platform数据准备中，此值可以使用[`uuid`或`guid`映射函数](../../data-prep/functions.md#special-operations)生成。<br><br>如果从源连接流式传输数据或直接从Parquet文件摄取数据，则应通过关联使事件具有唯一性的特定组合字段（如主ID、时间戳、事件类型等）来生成此值。<br><br>务必要区分的是， **此字段不表示与个人相关的身份**，而是表示数据本身的记录。与人员有关的身份数据应被降级到由兼容mixin提供的[身份字段](../schema/composition.md#identity)。 |
| `eventMergeId` | 如果使用[Adobe Experience Platform Web SDK](../../edge/home.md)来摄取数据，则表示被摄取的批处理的ID，该ID会导致创建记录。 在摄取数据时，系统会自动填充此字段。 不支持在Web SDK实施的上下文之外使用此字段。 |
| `eventType` | 表示事件类型或类别的字符串。 如果要区分同一架构和数据集中的不同事件类型，例如区分某个产品查看事件与某个零售公司的添加到购物车事件，则可以使用此字段。<br><br>此属性的标准值在附录 [部分](#eventType)中提供，包括其预期用例的描述。此字段是一个可扩展枚举，这意味着您还可以使用自己的事件类型字符串对您跟踪的事件进行分类。 |
| `producedBy` | 描述事件的制作者或来源的字符串值。 如果出于分段目的需要，可使用此字段过滤掉某些事件生成器。<br><br>此属性的一些建议值在附录 [部分](#producedBy)中提供。此字段是一个可扩展枚举，这意味着您还可以使用自己的字符串来表示不同的事件生成器。 |
| `identityMap` | 映射字段，其中包含事件所应用的个人的一组命名空间标识。 在摄取身份数据时，系统会自动更新此字段。 为了正确使用[实时客户资料](../../profile/home.md)的此字段，请不要尝试在数据操作中手动更新字段的内容。<br /><br />有关架构组合基础知识的用例的更 [多信息，请](../schema/composition.md#identityMap) 参阅标识映射一节。 |
| `timestamp` | 事件发生时的ISO 8601时间戳，按照[RFC 3339第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6)进行格式设置。 此时间戳必须在过去发生。 请参阅[时间戳](#timestamps)上的以下部分，以了解有关使用此字段的最佳实践。 |

{style=&quot;table-layout:auto&quot;}

## 事件建模的最佳实践

以下部分介绍了在Adobe Experience Platform中设计基于事件的体验数据模型(XDM)架构的最佳实践。

### 时间戳 {#timestamps}

事件架构的根`timestamp`字段只能&#x200B;****&#x200B;表示事件本身的观察，且必须在过去发生。 如果您的分段用例需要使用将来可能发生的时间戳，则这些值必须在体验事件架构的其他位置受到限制。

例如，如果旅游和酒店业的企业正在为航班预订事件建模，则类级别`timestamp`字段表示预订事件被观察到的时间。 与事件相关的其他时间戳（如旅行预订的开始日期）应在标准或自定义混合输入提供的单独字段中捕获。

![](../images/classes/experienceevent/timestamps.png)

通过将类级别时间戳与事件架构中其他相关的日期时间值分开，您可以实施灵活的分段用例，同时在体验应用程序中保留客户历程的带有时间戳的帐户。

### 使用计算字段

您的体验应用程序中的某些交互可能会导致多个相关事件，这些事件在技术上共享相同的事件时间戳，因此可以表示为单个事件记录。 例如，如果客户查看了您网站上的某个产品，则可能会生成一条事件记录，其中既包含“产品查看”属性，又包含一些重叠的通用“页面查看”属性。 在这些情况下，当在记录中捕获多个事件时，您可以使用计算字段捕获最重要的属性。

[Adobe Experience Platform Data ](../../data-prep/home.md) Prepack允许您在XDM中映射、转换和验证数据。使用服务提供的可用[映射函数](../../data-prep/functions.md) ，在摄取到Experience Platform时，可以调用逻辑运算符以优先排序、转换和/或整合来自多事件记录的数据。

如果要通过UI手动将数据摄取到平台，请参阅[将CSV文件映射到XDM](../../ingestion/tutorials/map-a-csv-file.md)中的指南，以了解有关如何创建计算字段的特定步骤。

如果您使用源连接将数据流式传输到平台，则可以将源配置为改用计算字段。 有关如何在配置连接时实施计算字段的说明，请参阅特定源](../../sources/home.md)的[文档。

## 兼容的架构字段组{#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../field-groups/name-updates.md)上的文档。

Adobe提供了多个用于[!DNL XDM ExperienceEvent]类的标准字段组。 以下是类的一些常用字段组的列表：

* [[!UICONTROL 最终用户ID详细信息]](../field-groups/event/enduserids.md)
* [[!UICONTROL 环境详细信息]](../field-groups/event/environment-details.md)

## 附录

以下部分包含有关[!UICONTROL XDM ExperienceEvent]类的其他信息。

### `eventType`的已接受值 {#eventType}

下表概述了`eventType`的已接受值及其定义：

| 值 | 定义 |
| --- | --- |
| `advertising.completes` | 已观看至结束定时媒体资产。 这不一定意味着查看者观看了整个视频，因为查看者可以跳到前面。 |
| `advertising.timePlayed` | 描述用户在特定定时媒体资产上所花费的时间。 |
| `advertising.federated` | 指示体验事件是否是通过数据联合（客户之间的数据共享）创建的。 |
| `advertising.clicks` | 单击广告上的操作。 |
| `advertising.conversions` | 由客户执行的预定义操作，该操作会触发事件以进行性能评估。 |
| `advertising.firstQuartiles` | 数字视频广告以正常速度播放了其持续时间的25%。 |
| `advertising.impressions` | 向客户展示的广告，有可能被查看。 |
| `advertising.midpoints` | 数字视频广告以正常速度播放了其持续时间的50%。 |
| `advertising.starts` | 开始播放数字视频广告。 |
| `advertising.thirdQuartiles` | 数字视频广告以正常速度播放了其持续时间的75%。 |
| `web.webpagedetails.pageViews` | 网页已收到一个或多个查看。 |
| `web.webinteraction.linkClicks` | 已选择链接一次或多次。 |
| `commerce.checkouts` | 产品列表已发生结帐事件。 如果结帐流程中存在多个步骤，则可能会有多个结帐事件。 如果有多个步骤，则会使用每个事件的时间戳和引用的页面/体验来标识按顺序表示的每个单个事件（步骤）。 |
| `commerce.productListAdds` | 产品已添加到产品列表或购物车。 |
| `commerce.productListOpens` | 已初始化或创建新产品列表（购物车）。 |
| `commerce.productListRemovals` | 已从产品列表或购物车中删除一个或多个产品条目。 |
| `commerce.productListReopens` | 客户已重新激活不再可访问（放弃）的产品列表（购物车），例如通过再营销活动。 |
| `commerce.productListViews` | 产品列表或购物车已收到一个或多个查看。 |
| `commerce.productViews` | 产品已收到一个或多个查看。 |
| `commerce.purchases` | 已接受命令。 这是商务转化中唯一必需的操作。 购买事件必须引用产品列表。 |
| `commerce.saveForLaters` | 已保存产品列表供将来使用，如产品愿望列表。 |
| `delivery.feedback` | 投放的反馈事件，如电子邮件投放。 |
| `message.feedback` | 向客户发送的消息的反馈事件，如已发送/退回/错误。 |
| `message.tracking` | 跟踪事件，如对发送给客户的消息执行打开/点击/自定义操作。 |

{style=&quot;table-layout:auto&quot;}

### `producedBy`的建议值 {#producedBy}

下表概述了`producedBy`的一些已接受值：

| 值 | 定义 |
| --- | --- |
| `self` | Self |
| `system` | 系统 |
| `salesRef` | 销售代表 |
| `customerRep` | 客户代表 |
