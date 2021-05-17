---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；个人用户档案；字段；模式;模式；标识映射；标识映射；模式设计；映射；映射；合并模式;合并
solution: Experience Platform
title: XDM ExperienceEvent类
topic-legacy: overview
description: 本文档概述了XDM ExperienceEvent类。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 是标准的体验事件模型(XDM)类，它允许您在特定数据发生或达到特定条件集时创建系统的时间戳快照。

体验事件是已发生事件的事实记录，包括所涉及个人的时间点和身份。 事件可以是显式（直接可观察的人类行为）或隐式（在没有直接人类行为的情况下提出），并且记录时不加总和或解释。 有关在平台生态系统中使用此类的详细信息，请参阅[ XDM概述](../home.md#data-behaviors)。

[!DNL XDM ExperienceEvent]类本身为模式提供了多个与时间序列相关的字段。 在摄取数据时，会自动填充其中某些字段的值：

![](../images/classes/experienceevent/structure.png)

| 属性 | 描述 |
| --- | --- |
| `_id` | 事件的唯一字符串标识符。 此字段用于跟踪单个事件的唯一性、防止重复事件并在下游服务中查找该数据。<br><br>在某些情况下， `_id` 可以是 [通用唯一标识符(](https://tools.ietf.org/html/rfc4122) UUID) [或](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)全局唯一标识符(GUID)。在Adobe Experience Platform数据准备中，可以使用[`uuid`或`guid`映射函数](../../data-prep/functions.md#special-operations)生成此值。<br><br>如果要从源连接流式传输数据或直接从Parce文件中摄取数据，则应通过连接使其唯一的特定组合字段(如主ID、时间戳、事件类型等)来生成此值。<br><br>必须指出的是， **该字段不代表与个人有关的身份**，而是数据本身的记录。应将与个人有关的身份数据降级到由兼容混合器提供的[身份字段](../schema/composition.md#identity)。 |
| `eventMergeId` | 如果使用[Adobe Experience Platform Web SDK](../../edge/home.md)来收录数据，则这表示导致创建记录的已收录批的ID。 数据摄取时，系统会自动填充此字段。 不支持在Web SDK实施的上下文之外使用此字段。 |
| `eventType` | 一个字符串，它指示事件的类型或类别。 如果要区分同一模式和数据集中的不同事件类型，例如区分产品视图事件和零售公司的附加购物车事件，则可以使用此字段。<br><br>此属性的标准值在附录部分中 [提供](#eventType)，包括其预期用例的说明。此字段是可扩展枚举，这意味着您还可以使用自己的事件类型字符串对正在跟踪的事件进行分类。 |
| `producedBy` | 一个字符串值，它描述事件的生成者或来源。 此字段可用于过滤出某些事件生成器（如果需要）以用于分段。<br><br>附录部分中提供了此属性的一些建 [议值](#producedBy)。此字段是可扩展的枚举，这意味着您还可以使用自己的字符串来表示不同的事件生成器。 |
| `identityMap` | 一个映射字段，其中包含事件所应用的个人的一组命名空间标识。 系统会在摄取标识数据时自动更新此字段。 为了将此字段正确用于[实时客户用户档案](../../profile/home.md)，请不要尝试手动更新数据操作中字段的内容。<br /><br />有关模式合成的用例的详细信 [息，请参](../schema/composition.md#identityMap) 阅合成基础知识中有关标识映射的部分。 |
| `timestamp` | 事件发生时的ISO 8601时间戳，格式按照[RFC 3339第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节进行。 此时间戳必须在过去发生。 请参阅[timestamps](#timestamps)的下节，了解有关使用此字段的最佳实践。 |

## 事件建模的最佳实践

以下部分介绍了在Adobe Experience Platform中设计基于事件的体验模式模型(XDM)的最佳实践。

### 时间戳 {#timestamps}

事件模式的根`timestamp`字段只能&#x200B;****&#x200B;表示事件本身的观察，并且必须在过去出现。 如果您的细分使用案例需要使用将来可能发生的时间戳，则这些值必须在您的体验事件模式的其他位置受到限制。

例如，如果旅游和酒店业中的企业正在为航班预订事件建模，则类级别`timestamp`字段表示遵守预订事件的时间。 与事件相关的其他时间戳(如旅行预订的开始日期)应在标准或自定义混合提供的单独字段中捕获。

![](../images/classes/experienceevent/timestamps.png)

通过将类级时间戳与您的事件模式中其他相关的日期时间值分开，您可以实施灵活的分段用例，同时在您的体验应用程序中保留一个有时间戳的客户旅程帐户。

### 使用计算字段

您的体验应用程序中的某些交互可能导致多个相关事件，从技术上讲，它们共享相同的事件时间戳，因此可以表示为单个事件记录。 例如，如果客户在您的网站上视图产品，则可能会生成一条事件记录，其中既包含“产品视图”属性，又包含一些重叠的通用“页面视图”属性。 在这些情况下，当记录中捕获了多个事件时，您可以使用计算字段来捕获最重要的属性。

[Adobe Experience Platform Data ](../../data-prep/home.md) Prep允许您在XDM之间映射、转换和验证数据。使用服务提供的可用[映射函数](../../data-prep/functions.md)，在将数据引入Experience Platform时，可以调用逻辑运算符来对来自多事件记录的数据进行优先级排序、转换和/或合并。

如果要通过UI手动将数据引入平台，请参阅[将CSV文件映射到XDM](../../ingestion/tutorials/map-a-csv-file.md)的指南，了解有关如何创建计算字段的特定步骤。

如果您使用源连接将数据流化到平台，则可以配置源以改用计算字段。 有关如何在配置连接时实现计算字段的说明，请参阅特定源](../../sources/home.md)的[文档。

## 兼容的模式字段组{#field-groups}

>[!NOTE]
>
>多个字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../field-groups/name-updates.md)上的文档。

Adobe提供多个标准字段组，以用于[!DNL XDM ExperienceEvent]类。 以下是某类一些常用字段组的列表:

* [[!UICONTROL 最终用户ID详细信息]](../field-groups/event/enduserids.md)
* [[!UICONTROL 环境详细信息]](../field-groups/event/environment-details.md)

## 附录

下节包含有关[!UICONTROL XDM ExperienceEvent]类的其他信息。

### `eventType`的已接受值 {#eventType}

下表概述了`eventType`的已接受值及其定义：

| 值 | 定义 |
| --- | --- |
| `advertising.completes` | 已观看超时媒体资产完成。 这并不一定意味着查看者观看了整个视频，因为查看者可能跳过了前面。 |
| `advertising.timePlayed` | 描述用户在特定定时媒体资产上所花费的时间。 |
| `advertising.federated` | 指示是否通过数据联盟（客户之间的数据共享）创建了体验事件。 |
| `advertising.clicks` | 在广告上单击操作。 |
| `advertising.conversions` | 由客户执行的预定义操作，触发事件进行绩效评估。 |
| `advertising.firstQuartiles` | 数字视频广告以正常速度播放了25%的持续时间。 |
| `advertising.impressions` | 对可能被观看的客户的广告印象。 |
| `advertising.midpoints` | 数字视频广告以正常速度播放了50%的持续时间。 |
| `advertising.starts` | 数字视频广告已开始播放。 |
| `advertising.thirdQuartiles` | 数字视频广告以正常速度播放了75%的持续时间。 |
| `web.webpagedetails.pageViews` | 网页已收到一个或多个视图。 |
| `web.webinteraction.linkClicks` | 已选择一个或多个链接。 |
| `commerce.checkouts` | 产品事件发生结帐列表。 如果结帐过程中有多个步骤，则可能有多个结帐事件。 如果有多个步骤，则每个事件的时间戳和引用的页面/体验将用于标识按顺序表示的每个单独事件（步骤）。 |
| `commerce.productListAdds` | 产品已添加到产品列表或购物车。 |
| `commerce.productListOpens` | 新产品列表（购物车）已初始化或创建。 |
| `commerce.productListRemovals` | 一个或多个产品条目已从产品列表或购物车中删除。 |
| `commerce.productListReopens` | 客户已重新激活不再可访问（放弃）的产品列表（购物车），例如通过再营销活动。 |
| `commerce.productListViews` | 产品列表或购物车已收到一个或多个视图。 |
| `commerce.productViews` | 产品已收到一个或多个视图。 |
| `commerce.purchases` | 已接受命令。 这是商务转换中唯一必需的操作。 购买事件必须引用产品列表。 |
| `commerce.saveForLaters` | 已保存产品列表供将来使用，如产品愿望列表。 |
| `delivery.feedback` | 投放的反馈事件，如电子邮件投放。 |
| `message.feedback` | 反馈事件，如发送给客户的消息的已发送/弹出/错误。 |
| `message.tracking` | 跟踪事件，如对发送给客户的消息执行打开/单击/自定义操作。 |

### `producedBy`的建议值 {#producedBy}

下表概述了`producedBy`的一些已接受值：

| 值 | 定义 |
| --- | --- |
| `self` | Self |
| `system` | 系统 |
| `salesRef` | 销售代表 |
| `customerRep` | 客户代表 |
