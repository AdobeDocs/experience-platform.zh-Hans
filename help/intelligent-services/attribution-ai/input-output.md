---
keywords: Experience Platform；快速入门；归因人工智能；热门主题；归因人工智能输入；归因人工智能输出；
feature: Attribution AI
title: Attribution AI中的输入和输出
description: 以下文档概述了归因人工智能中使用的不同输入和输出。
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2474'
ht-degree: 3%

---

# [!DNL Attribution AI]中的输入和输出

以下文档概述了[!DNL Attribution AI]中使用的不同输入和输出。

## [!DNL Attribution AI]输入数据

归因人工智能通过分析以下数据集计算算法分数：

- 使用[Analytics源连接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)的Adobe Analytics数据集
- Adobe Experience Platform架构中的Experience Event (EE)数据集
- Consumer Experience Event (CEE)数据集

如果每个数据集共享相同的身份类型（命名空间）（如ECID），您现在可以基于&#x200B;**身份映射** （字段）从不同来源添加多个数据集。 选择身份和命名空间后，将显示ID列完整性量度，这些量度指示要拼合的数据量。 要了解有关添加多个数据集的更多信息，请访问[归因人工智能用户指南](./user-guide.md#identity)。

默认情况下，并不总是映射渠道信息。 在某些情况下，如果mediaChannel（字段）为空，则在将字段映射到mediaChannel之前，您将无法“继续”，因为它是必需列。 如果在数据集中检测到渠道，则默认情况下会将其映射到mediaChannel。 其他列（如&#x200B;**媒体类型**&#x200B;和&#x200B;**媒体操作**）仍是可选的。

映射渠道字段后，请继续执行“定义事件”步骤，在该步骤中，您可以选择转化事件、接触点事件，然后从单个数据集中选择特定字段。

>[!IMPORTANT]
>
>Adobe Analytics Source Connector最多可能需要四周才能回填数据。 如果您最近设置了连接器，则应验证数据集是否具有归因人工智能所需的最小数据长度。 请查看[历史数据](#data-requirements)部分，以验证您是否有足够的数据来计算准确的算法分数。

有关设置[!DNL Consumer Experience Event] (CEE)架构的更多详细信息，请参阅[Intelligent Services数据准备](../data-preparation.md)指南。 有关映射Adobe Analytics数据的更多信息，请访问[Analytics字段映射](../../sources/connectors/adobe-applications/analytics.md)文档。

并非所有[!DNL Consumer Experience Event] (CEE)架构中的列都是归因人工智能的必要列。

您可以使用架构或选定数据集中下面推荐的任何字段配置接触点。

| 建议的列 | 需要 |
| --- | --- |
| 主要标识字段 | 接触点/转化 |
| 时间戳 | 接触点/转化 |
| 渠道。_type | 接触点 |
| Channel.mediaAction | 接触点 |
| Channel.mediaType | 接触点 |
| Marketing.trackingCode | 接触点 |
| Marketing.campaignname | 接触点 |
| Marketing.campaigngroup | 接触点 |
| Commerce | 转化 |

通常，归因在“商务”下的订单、购买和结账等转化列上运行。 “渠道”和“营销”列用于定义归因人工智能的接触点（例如，`channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`）。 为获得最佳结果和见解，强烈建议您包含尽可能多的转化和接触点列。 此外，您不仅可以使用上述列。 您可以包含任何其他推荐列或自定义列作为转化或接触点定义。

只要与配置接触点相关的渠道或营销活动信息存在于某个mixin或传递字段中，体验事件(EE)数据集就不需要显式地包含渠道和营销mixin。

>[!TIP]
>
>如果您在CEE架构中使用Adobe Analytics数据，Analytics的接触点信息通常存储在`channel.typeAtSource`中（例如，`channel.typeAtSource = 'email'`）。

## 历史数据 {#data-requirements}

>[!IMPORTANT]
>
> Attribution AI运行所需的最少数据量如下所示：
> - 您需要提供至少3个月（90天）的数据才能运行良好的模型。
> - 您至少需要1000次转化。

归因人工智能需要历史数据作为模型训练的输入。 所需的数据持续时间主要取决于两个关键因素：训练窗口和回顾窗口。 训练窗口较短的输入对近期趋势更敏感，而训练窗口较长的输入有助于生成更稳定、更准确的模型。 使用最能代表您的业务目标的历史数据为目标建模非常重要。

[训练窗口配置](./user-guide.md#training-window)根据发生时间筛选设置为用于模型训练的转化事件。 目前，最低培训时段为1季度（90天）。 [回顾时间范围](./user-guide.md#lookback-window)提供了一个时间范围，用于指示应包含与转化事件相关的转化事件接触点之前的天数。 这两个概念共同决定了应用程序所需的输入数据量（以天为单位测量）。

默认情况下，归因人工智能将培训时段定义为最近的2季度（6个月），回顾时段定义为56天。 换言之，该模型将考虑过去2个季度发生的所有已定义转化事件，并查找在相关转化事件之前56天内发生的所有接触点。

**公式**：

所需的最小数据长度=训练时段+回顾时段

>[!TIP]
>
> 具有默认配置的应用程序所需的最小数据长度为：2季度（180天）+ 56天= 236天。

示例：

- 您要归因最近90天（3个月）内发生的转化事件，并跟踪在转化事件之前4周内发生的所有接触点。 输入数据持续时间应跨越过去90天+ 28天（4周）。 培训时段为90天，回顾时段为28天，共计118天。

## 归因人工智能输出数据

归因人工智能输出以下内容：

- [原始粒度分数](#raw-granular-scores)
- [汇总分数](#aggregated-attribution-scores)

**示例输出架构：**

![](./images/input-output/schema_output.gif)

### 原始粒度分数 {#raw-granular-scores}

归因人工智能尽可能输出最细粒度级别的归因分数，以便您按任意分数列对分数进行细分。 要在UI中查看这些得分，请阅读[查看原始得分路径](#raw-score-path)中的部分。 要使用API下载得分，请访问[在归因人工智能](./download-scores.md)文档中下载得分。

>[!NOTE]
>
> 仅当满足以下任一条件时，您才能在得分输出数据集的输入数据集中看到任何所需的报表列：
> - 报告列作为接触点或转化定义配置的一部分包含在配置页面中。
> - 报表列包含在附加得分数据集列中。

下表概述了原始分数示例输出中的架构字段：

| 列名称（数据类型） | 可为空 | 描述 |
| --- | --- | --- |
| timestamp (DateTime) | False | 转化事件或观察发生的时间。<br> **示例：** 2020-06-09T00:01:51.000Z |
| identityMap（映射） | True | 与CEE XDM格式类似的用户的identityMap。 |
| eventType（字符串） | True | 此时间序列记录的主要事件类型。<br> **示例：** &quot;Order&quot;、&quot;Purchase&quot;、&quot;Visit&quot; |
| eventMergeId（字符串） | True | 一个ID，用于将多个[!DNL Experience Events]关联或合并到一起，这些ID基本上是同一事件或应合并的事件。 这旨在摄取之前由数据制作者填充。<br> **示例：** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id（字符串） | False | 时间序列事件的唯一标识符。<br> **示例：** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId（对象） | False | 与您的暂时ID对应的顶级对象容器。<br> **示例：** _atsdsnrmmsv2 |
| your_schema_name（对象） | False | 使用转化事件对行进行评分，包括与行及其元数据关联的所有接触点事件。<br> **示例：**&#x200B;归因人工智能分数 — 模型名称__2020 |
| 分段（字符串） | True | 转化区段，例如构建模型所针对的地理分段。 如果缺少区段，则区段与conversionName相同。<br> **示例：** ORDER_US |
| conversionName（字符串） | True | 在安装期间配置的转换的名称。<br> **示例：**&#x200B;订单，潜在客户，访问 |
| 转换（对象） | False | 转换元数据列。 |
| 数据源（字符串） | True | 数据源的全局唯一标识。<br> **示例：** Adobe Analytics |
| eventSource（字符串） | True | 实际事件发生时的源。<br> **示例：** Adobe.com |
| eventType（字符串） | True | 此时间序列记录的主要事件类型。<br> **示例：**&#x200B;订单 |
| 地域（字符串） | True | 转换传递的地理位置`placeContext.geo.countryCode`。<br> **示例：** US |
| priceTotal（双精度） | True | 通过转换<br>获得的收入 **示例：** 99.9 |
| product（字符串） | True | 产品本身的XDM标识符。<br> **示例：** RX 1080 ti |
| productType（字符串） | True | 在此产品视图中向用户显示的产品显示名称。<br> **示例：** Gpu |
| 数量（整数） | True | 转换期间购买的数量。<br> **示例：** 1 1080 ti |
| receivedTimestamp (DateTime) | True | 已收到转换的时间戳。<br> **示例：** 2020-06-09T00:01:51.000Z |
| skuId（字符串） | True | 库存单位(SKU)，供应商定义的产品的唯一标识符。<br> **示例：** MJ-03-XS-Black |
| timestamp (DateTime) | True | 转换的时间戳。<br> **示例：** 2020-06-09T00:01:51.000Z |
| passThrough（对象） | True | 配置模型时用户指定的其他得分数据集列。 |
| commerce_order_purchaseCity（字符串） | True | 其他得分数据集列。<br> **示例：**&#x200B;城市：圣何塞 |
| customerProfile（对象） | False | 用于构建模型的用户的身份详细信息。 |
| identity（对象） | False | 包含用于构建模型的用户的详细信息，如`id`和`namespace`。 |
| id（字符串） | True | 用户的身份ID，如Cookie ID、Adobe Analytics ID (AAID)或Experience Cloud ID （ECID，也称为MCID或访客ID）等。<br> **示例：** 17348762725408656344688320891369597404 |
| 命名空间（字符串） | True | 用于构建路径并因此构建模型的身份命名空间。<br> **示例：** aaid |
| touchpointsDetail（对象数组） | True | 导致转化的接触点详细信息列表，排序方式： | 接触点发生次数或时间戳。 |
| touchpointName（字符串） | True | 在安装期间配置的接触点的名称。<br> **示例：** PAID_SEARCH_CLICK |
| 分数（对象） | True | 作为得分的接触点对此转化的贡献。 有关此对象内生成的分数的更多信息，请参阅[聚合的归因分数](#aggregated-attribution-scores)部分。 |
| touchPoint（对象） | True | 接触点元数据。 有关此对象内生成的分数的更多信息，请参阅[聚合分数](#aggregated-scores)部分。 |

### 查看原始得分路径(UI) {#raw-score-path}

您可以在UI中查看原始分数的路径。 首先，在Experience Platform UI中选择&#x200B;**[!UICONTROL 架构]**，然后在&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中搜索并选择您的归因人工智能得分架构。

![选择您的架构](./images/input-output/schemas_browse.png)

接下来，在UI的&#x200B;**[!UICONTROL 结构]**&#x200B;窗口中选择一个字段，**[!UICONTROL 字段属性]**&#x200B;选项卡将打开。 在&#x200B;**[!UICONTROL 字段属性]**&#x200B;中，是映射到原始分数的路径字段。

![选择架构](./images/input-output/field_properties.png)

### 总归因分数 {#aggregated-attribution-scores}

如果日期范围少于30天，则可以从Experience Platform UI以CSV格式下载汇总分数。

归因人工智能支持两类归因分数：算法分数和基于规则的分数。

归因人工智能生成两种不同类型的算法分数，增量分数和影响分数。 影响分数是每个营销接触点负责的转化率部分。 增量分数是营销接触点直接造成的边际影响量。 增量分数和影响分数之间的主要区别在于，增量分数将基线影响考虑在内。 它不假设转化完全由先前的营销接触点引起。

下面快速查看Adobe Experience Platform UI中的归因人工智能架构输出示例：

![](./images/input-output/schema_screenshot.png)

有关每个归因分数的更多详细信息，请参阅下表：

| 归因分数 | 描述 |
| ----- | ----------- |
| 影响（算法） | 影响分数是每个营销接触点负责的转化率部分。 |
| 增量（算法） | 增量分数是营销接触点直接造成的边际影响量。 |
| 首次接触 | 基于规则的归因得分，将所有信用分配给转化路径上的初始接触点。 |
| 最后接触 | 基于规则的归因得分，可将所有信用分配给最接近转化的接触点。 |
| 线性 | 基于规则的归因得分，它将信用平等分配给转化路径上的每个接触点。 |
| U型 | 基于规则的归因得分，将40%的点数分配给第一个接触点，将40%的点数分配给最后一个接触点，其他接触点平分剩余的20%。 |
| 时间衰减 | 基于规则的归因得分，其中距离转化较近的接触点比距离转化较远的接触点获得更多的点数。 |

**原始得分参考（归因得分）**

下表将归因分数映射到原始分数。 如果要下载原始分数，请访问Attribution AI中的[下载分数](./download-scores.md)文档。

| 归因分数 | 原始得分引用列 |
| --- | --- |
| 影响（算法） | _tenantID.your_schema_name.element.touchpoint.algorithmicInfessible |
| 增量（算法） | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInffected |
| 首次接触 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| 最后接触 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| 线性 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U型 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| 时间衰减 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### 汇总分数 {#aggregated-scores}

如果日期范围少于30天，则可以从Experience Platform UI以CSV格式下载汇总分数。 有关每个聚合列的更多详细信息，请参阅下表。

| 列名称 | 约束 | 可为空 | 描述 |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | 用户定义的固定格式 | False | 客户事件日期，格式为YYYY-MM-DD。<br> **示例**： 2016-05-02 |
| mediatouchpoints_date (DateTime) | 用户定义的固定格式 | True | 媒体接触点日期，YYYY-MM-DD格式<br> **示例**： 2017-04-21 |
| segment（字符串） | 已计算 | False | 转化区段，例如构建模型所针对的地域划分。 如果缺少区段，则区段与conversion_scope相同。<br> **示例**： ORDER_AMER |
| conversion_scope（字符串） | 用户定义的 | False | 用户配置的转换的名称。<br> **示例**： ORDER |
| touchpoint_scope（字符串） | 用户定义的 | True | 用户<br>配置的接触点名称 **示例**： PAID_SEARCH_CLICK |
| product（字符串） | 用户定义的 | True | 产品的XDM标识符。<br> **示例**： CC |
| product_type（字符串） | 用户定义的 | True | 在此产品视图中向用户显示的产品显示名称。<br> **示例**： gpu，笔记本电脑 |
| 地域（字符串） | 用户定义的 | True | 进行转换的地理位置(placeContext.geo.countryCode) <br> **示例**： US |
| event_type（字符串） | 用户定义的 | True | 此时间序列记录<br>的主要事件类型 **示例**：付费转化 |
| media_type（字符串） | 枚举 | False | 描述媒体类型是付费媒体、自有媒体还是免费媒体。<br> **示例**：付费，拥有 |
| channel（字符串） | 枚举 | False | `channel._type`属性，用于在[!DNL Consumer Experience Event] XDM中提供对具有相似属性的渠道的粗略分类。<br> **示例**：搜索 |
| 操作（字符串） | 枚举 | False | `mediaAction`属性用于提供一种体验事件媒体操作。<br> **示例**：单击 |
| campaign_group（字符串） | 用户定义的 | True | 营销活动组的名称，其中多个营销活动归为一组，如“50%_DISCOUNT”。<br> **示例**：商业 |
| campaign_name（字符串） | 用户定义的 | True | 用于标识营销活动的活动名称，如“50%_DISCOUNT_USA”或“50%_DISCOUNT_ASIA”。<br> **示例**：感恩节促销 |

**原始得分参考（汇总）**

下表将汇总分数映射到原始分数。 如果要下载原始分数，请访问Attribution AI中的[下载分数](./download-scores.md)文档。 若要从UI中查看原始得分路径，请访问此文档中[查看原始得分路径](#raw-score-path)上的部分。

| 列名称 | 原始得分引用列 |
| --- | --- |
| customerevents_date | 时间戳 |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| 区段 | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| 接触点范围 | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| 产品 | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| 地域 | _tenantID.your_schema_name.conversion.geo |
| event_type | 事件类型 |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| 渠道 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| 操作 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - Attribution AI仅使用更新的数据进行进一步的训练和评分。 同样，当您请求删除数据时，客户人工智能会限制使用已删除的数据。
> - 归因人工智能利用Experience Platform数据集。 为了支持品牌可能收到的消费者权限请求，品牌应使用Experience Platform Privacy Service提交消费者访问和删除请求，以通过数据湖、身份服务和实时客户配置文件删除他们的数据。
> - 我们用于模型输入/输出的所有数据集将遵循Experience Platform准则。 Experience Platform数据加密适用于静态和传输中的数据。 请参阅文档以了解有关[数据加密](../../../help/landing/governance-privacy-security/encryption.md)的更多信息

## 后续步骤 {#next-steps}

准备好数据并准备好所有凭据和架构后，请按照[归因人工智能用户指南](./user-guide.md)开始。 本指南将指导您为归因人工智能创建实例。
