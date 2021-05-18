---
keywords: Experience Platform；入门；归因ai；热门话题；归因ai输入；归因ai输出；
solution: Experience Platform, Intelligent Services
title: 输入和输出Attribution AI
topic-legacy: Input and Output data for Attribution AI
description: 以下文档概述了Attribution AI中使用的不同输入和输出。
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: 91f586746c8d1db4e9219b261d7be36e572f1b50
workflow-type: tm+mt
source-wordcount: '2230'
ht-degree: 3%

---

# [!DNL Attribution AI]中的输入和输出

以下文档概述了[!DNL Attribution AI]中使用的不同输入和输出。

## [!DNL Attribution AI] 输入数据

Attribution AI通过分析以下数据集之一来计算算法得分：

- 消费者体验事件(CEE)数据集
- Adobe Analytics数据集（使用[Analytics源连接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)）

>[!IMPORTANT]
>
>Adobe Analytics源连接器回填数据最多可能需要4周。 如果您最近设置了连接器，则应验证数据集是否具有Attribution AI所需的最小数据长度。 请查看[历史数据](#data-requirements)部分，以验证您有足够的数据来计算准确的算法分数。

有关设置[!DNL Consumer Experience Event](CEE)模式的详细信息，请参阅[ Intelligent Services数据准备](../data-preparation.md)指南。 有关映射Adobe Analytics数据的详细信息，请访问[分析字段映射](../../sources/connectors/adobe-applications/analytics.md)文档。

并非[!DNL Consumer Experience Event](CEE)模式中的所有列对于Attribution AI都是必填的。

>[!NOTE]
>
> 以下9列是必填项，其他列是可选的，但建议/必需，如果要将相同数据用于其他Adobe解决方案，如[!DNL Customer AI]和[!DNL Journey AI]。

| 必填列 | 需要 |
| --- | --- |
| 主标识字段 | 触点/转化 |
| 时间戳 | 触点/转化 |
| Channel._type | 触点 |
| Channel.mediaAction | 触点 |
| Channel.mediaType | 触点 |
| Marketing.trackingCode | 触点 |
| Marketing.campaignname | 触点 |
| Marketing.campaigngroup | 触点 |
| 商务 | 转化 |

通常，归因在“商务”下的转换列（如订单、购买和结帐）上运行。 “渠道”和“营销”的列用于定义Attribution AI的接触点（例如，`channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`）。 为获得最佳结果和洞察，强烈建议您尽可能多地加入转化列和接触点列。 此外，您不仅限于上述列。 您可以将任何其他推荐或自定义列作为转换或触点定义。

>[!TIP]
>
>如果您在CEE模式中使用Adobe Analytics数据，则Analytics的触点信息通常存储在`channel.typeAtSource`中（例如`channel.typeAtSource = 'email'`）。

以下列不是必需的，但如果您有可用的信息，建议您将这些列包含在CEE模式中。

**其他建议列：**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

## 历史数据 {#data-requirements}

>[!IMPORTANT]
>
> Attribution AI运行所需的最小数据量如下：
> - 您需要提供至少3个月（90天）的数据才能运行良好的模型。
> - 您至少需要1000次转换。


Attribution AI需要历史数据作为模型培训的输入。 所需数据持续时间主要由两个关键因素决定：培训窗口和回顾窗口。 较短的培训窗口的输入对最新趋势更加敏感，而较长的培训窗口有助于生成更稳定、更准确的模型。 用最能代表您业务目标的历史数据来建模目标非常重要。

[培训窗口配置](./user-guide.md#training-window)过滤器转换事件设置为基于发生时间用于模型培训。 目前，最低培训窗口为1个季度（90天）。 [回顾窗口](./user-guide.md#lookback-window)提供一个时间范围，指示应包括与此转换事件相关的转换事件接触点之前的天数。 这两个概念共同决定了应用程序所需的输入数据量（以天为单位）。

默认情况下，Attribution AI将培训窗口定义为最近2个季度（6个月），将回顾窗口定义为56天。 换言之，该模型将考虑过去2个季度中发生的所有已定义转换事件，并查找在关联转换事件之前56天内发生的所有接触点。

**公式**:

所需数据的最小长度=培训窗口+回顾窗口

>[!TIP]
>
> 具有默认配置的应用程序所需的最小数据长度是：2个季度（180天）+ 56天= 236天。

示例 :

- 您要对过去90天（3个月）内发生的转换事件进行归因，并跟踪转换事件前4周内发生的所有接触点。 输入数据的持续时间应跨过过去90天+ 28天（4周）。 培训窗口为90天，回顾窗口为28天，总共为118天。

## Attribution AI输出数据

Attribution AI输出以下内容：

- [原始粒度](#raw-granular-scores)
- [汇总的分数](#aggregated-attribution-scores)

**输出模式示例：**

![](./images/input-output/schema_output.gif)

### 原始粒度分数{#raw-granular-scores}

Attribution AI以尽可能最细的粒度输出归因分数，以便您可以按任何分数列对分数进行分割和分割。 要在UI中视图这些得分，请阅读[查看原始得分路径](#raw-score-path)的部分。 要使用API下载分数，请访问以Attribution AI](./download-scores.md)文档下载分数的[。

>[!NOTE]
>
> 仅当以下任一条件为true时，您才能在分数输出数据集中查看输入数据集中的任何所需报告列：
> - 报告列作为触点或转换定义配置的一部分包含在配置页面中。
> - 报告列包含在其他得分数据集列中。


下表概述了原始分数示例输出中的模式字段：

| 列名(DataType) | 可为空 | 描述 |
| --- | --- | --- |
| timestamp(DateTime) | False | 发生转换事件或观察的时间。<br> **示例** :2020-06-09T00:01:51.000Z |
| identityMap(Map) | True | 与CEE XDM格式类似的用户的identityMap。 |
| eventType（字符串） | True | 此时间系列记录的主事件类型。<br> **示例** ：“订购”、“购买”、“访问” |
| eventMergeId（字符串） | True | 一个ID，用于将多个[!DNL Experience Events]关联或合并到一起，这些本质上是相同的事件或应合并。 这是在摄取之前由数据生成器填充的。<br> **示例** :575525617716-0-edc2ed37-1ab-4750-a820-1c2b3844b8c4 |
| _id（字符串） | False | 时间序列事件的唯一标识符。<br> **示例** :4461-edc2ed37-1ab-4750-a820-1c2b3844b8c4 |
| _tenantId（对象） | False | 与您的十分ID对应的顶级对象容器。 <br> **示例：** _atsdsnrmmsv2 |
| your_模式_name（对象） | False | 对与转换事件关联的所有触点事件及其元数据进行分数行。<br> **示例：** Attribution AI得分 — 模型名称__2020 |
| 分段（字符串） | True | 转换段，如构建模型时所依据的地域分段。 如果没有区段，则区段与conversionName相同。<br> **示例：** ORDER_US |
| conversionName（字符串） | True | 在设置过程中配置的转换的名称。<br> **示例：** 订单、潜在客户、访问 |
| 转换（对象） | False | 转换元数据列。 |
| dataSource(String) | True | 数据源的全局唯一标识。<br> **示例：** Adobe Analytics |
| eventSource（字符串） | True | 实际事件发生时的源。<br> **示例：** Adobe.com |
| eventType（字符串） | True | 此时间系列记录的主事件类型。<br> **示例：** Order |
| geo（字符串） | True | 转换的地理位置`placeContext.geo.countryCode`。<br> **示例：** US |
| priceTotal(多次) | True | 通过转换取得的收入<br> **示例：** 99.9 |
| product（字符串） | True | 产品本身的XDM标识符。<br> **示例：** RX 1080 ti |
| productType（字符串） | True | 产品的显示名称，显示给此产品视图的用户。<br> **示例：** Gpu |
| 数量（整数） | True | 转换期间购买的数量。<br> **示例：** 1 1080 ti |
| receivedTimestamp(DateTime) | True | 已接收转换的时间戳。<br> **示例** :2020-06-09T00:01:51.000Z |
| skuId（字符串） | True | 库存单位(SKU)，供应商定义的产品的唯一标识符。<br> **示例：** MJ-03-XS-Black |
| timestamp(DateTime) | True | 转换的时间戳。<br> **示例** :2020-06-09T00:01:51.000Z |
| passThrough(Object) | True | 配置模型时用户指定的其他得分数据集列。 |
| commerce_order_purchaseCity（字符串） | True | 其他得分数据集列。<br> **示例：** 城市：圣何塞 |
| customerProfile（对象） | False | 用于构建模型的用户的身份详细信息。 |
| identity(Object) | False | 包含用于构建模型（如`id`和`namespace`）的用户的详细信息。 |
| id（字符串） | True | 用户的标识ID，如cookie ID、AAID或MCID等<br> **示例：** 17348762725408656344688320891369597404 |
| 命名空间（字符串） | True | 用于构建路径的身份命名空间，进而构建模型。<br> **示例：** aaid |
| touchpointsDetail（对象数组） | True | 触点详细信息的列表，可导致按触点发生次数或时间戳排序的转换。 |
| touchpointName（字符串） | True | 在设置过程中配置的触点的名称。<br> **示例：** PAID_SEARCH_CLICK |
| 分数（对象） | True | 以分数形式对此转化做出触点贡献。 有关此对象中生成的得分的详细信息，请参阅[聚合归因得分](#aggregated-attribution-scores)部分。 |
| touchPoint(Object) | True | 触点元数据。 有关此对象中生成的得分的详细信息，请参阅[聚集得分](#aggregated-scores)部分。 |

### 查看原始分数路径(UI){#raw-score-path}

您可以在UI中视图原始分数的路径。 开始：在平台UI中选择&#x200B;**[!UICONTROL 模式]**，然后在&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中搜索并选择您的归因AI得分模式。

![选择模式](./images/input-output/schemas_browse.png)

接下来，在UI的&#x200B;**[!UICONTROL 结构]**&#x200B;窗口中选择一个字段，此时将打开&#x200B;**[!UICONTROL 字段属性]**&#x200B;选项卡。 在&#x200B;**[!UICONTROL 字段属性]**&#x200B;中是映射到原始分数的路径字段。

![选择模式](./images/input-output/field_properties.png)


### 归因得分{#aggregated-attribution-scores}

如果日期范围小于30天，则可以从平台UI以CSV格式下载汇总的分数。

Attribution AI支持两类别归因得分、算法和基于规则的得分。

Attribution AI产生两种不同类型的算法得分，增量和影响。 受影响的得分是每个营销接触点负责的转化的一部分。 增量得分是营销接触点直接造成的边际影响量。 增量得分和受影响得分之间的主要区别在于增量得分将基线效果考虑在内。 它并不认为转化纯粹是由之前的营销接触点引起的。

以下是Adobe Experience Platform UI中的Attribution AI模式输出示例：

![](./images/input-output/schema_screenshot.png)

有关这些归因分数的更多详细信息，请参阅下表：

| 归因分数 | 描述 |
| ----- | ----------- |
| 受影响（算法） | 受影响的分数是每个营销接触点负责的转化率的一部分。 |
| 增量（算法） | 增量得分是营销接触点直接造成的边际影响量。 |
| 首次接触 | 基于规则的归因得分，可将所有积分分配给转化路径上的初始触点。 |
| 最后接触 | 基于规则的归因得分，将所有信用分配给最接近转化的接触点。 |
| 线性 | 基于规则的归因得分，为转化路径上的每个接触点分配相同的信用。 |
| U 型 | 基于规则的归因得分，将40%的积分分配给第一个接触点，40%的积分分配给最后一个接触点，而其他接触点将其余20%平分。 |
| 时间衰减 | 基于规则的归因得分，即离转化更近的接触点获得的积分比距离转化时间更远的触点多。 |

**原始分数参考（归因分数）**

下表将归因分数与原始分数进行映射。 如果要下载原始分数，请访问下载Attribution AI](./download-scores.md)文档中的[分数。

| 归因分数 | 原始得分参考列 |
| --- | --- |
| 受影响（算法） | _tenantID.your_模式_name.element.touchpoint.algorithmicEffected |
| 增量（算法） | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.algorithmicEffected |
| 首次接触 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.firstTouch |
| 最后接触 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.lastTouch |
| 线性 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.linear |
| U 型 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.uShape |
| 时间衰减 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.decayUnits |

### 汇总得分{#aggregated-scores}

如果日期范围小于30天，则可以从平台UI以CSV格式下载汇总的分数。 有关这些聚合列的更多详细信息，请参阅下表。

| 列名 | 约束 | 可为空 | 描述 |
| --- | --- | --- | --- |
| customerevents_date(DateTime) | 用户定义和固定格式 | False | 客户事件日期（YYYY-MM-DD格式）。<br> **示例**:2016-05-02 |
| mediatouchpoints_date(DateTime) | 用户定义和固定格式 | True | YYYY-MM-DD格式<br>的媒体触点日期 **示例**:2017-04-21 |
| segment（字符串） | 已计算 | False | 转换区段，例如构建模型时所依据的地理区段。 如果没有区段，则区段与conversion_scope相同。<br> **示例**:ORDER_AMER |
| conversion_scope（字符串） | 用户定义 | False | 由用户配置的转换名称。<br> **示例**:订单 |
| touchpoint_scope（字符串） | 用户定义 | True | 用户<br>配置的触点名称 **示例**:PAID_SEARCH_CLICK |
| product（字符串） | 用户定义 | True | 产品的XDM标识符。<br> **示例**:CC |
| product_type（字符串） | 用户定义 | True | 产品的显示名称，显示给此产品视图的用户。<br> **示例**:gpu，笔记本电脑 |
| geo（字符串） | 用户定义 | True | 转换所在的地理位置(placeContext.geo.countryCode)<br> **示例**:美国 |
| 事件_type（字符串） | 用户定义 | True | 此时间序列记录<br>的主事件类型 **示例**:付费转换 |
| media_type（字符串） | 枚举 | False | 描述媒体类型是付费、自有还是免费。<br> **示例**:付费、自有 |
| 渠道（字符串） | 枚举 | False | `channel._type`属性，用于提供在[!DNL Consumer Experience Event] XDM中具有相似属性的渠道的粗略分类。 <br> **示例**:搜索 |
| action（字符串） | 枚举 | False | `mediaAction`属性用于提供体验事件媒体操作类型。<br> **示例**:单击 |
| 活动_group（字符串） | 用户定义 | True | 将多个活动组合在一起的活动组的名称，如“50%_DISCOUNT”。<br> **示例**:商业类 |
| 活动_name（字符串） | 用户定义 | True | 用于标识营销活动的活动的名称，如“50%_DISCOUNT_USA”或“50%_DISCOUNT_ASIA”。 <br> **示例**:感恩节大甩卖 |

**原始分数参考（汇总）**

下表将汇总的分数映射到原始分数。 如果要下载原始分数，请访问下载Attribution AI](./download-scores.md)文档中的[分数。 要从UI中视图原始分数路径，请访问此文档中[查看原始分数路径](#raw-score-path)的部分。

| 列名 | “原始分数”参考列 |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.timestamp |
| segment（区段） | _tenantID.your_模式_name.segmentation |
| conversion_scope | _tenantID.your_模式_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_模式_name.touchpointsDetail.element.touchpointName |
| product | _tenantID.your_模式_name.conversion.product |
| product_type | _tenantID.your_模式_name.conversion.product_type |
| 地 | _tenantID.your_模式_name.conversion.geo |
| 事件_type | eventType |
| media_type | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.mediaChannel |
| 行动 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.mediaAction |
| 活动_group | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.campaignGroup |
| 活动_name | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.campaignName |


## 后续步骤 {#next-steps}

准备数据并准备好所有凭据和模式后，请按照[Attribution AI用户指南](./user-guide.md)进行开始。 本指南将指导您逐步创建Attribution AI实例。
