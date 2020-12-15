---
keywords: Experience Platform;getting started;Attribution ai;popular topics;Attribution ai input;Attribution ai output;
solution: Experience Platform, Intelligent Services
title: Attribution AI输入和输出
topic: Input and Output data for Attribution AI
description: 以下文档概述了Attribution AI中使用的不同输入和输出。
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '2075'
ht-degree: 3%

---


# [!DNL Attribution AI] 输入和输出

以下文档概述了中使用的不同输入和输出 [!DNL Attribution AI]。

## [!DNL Attribution AI] 输入数据

[!DNL Attribution AI] 用数 [!DNL Consumer Experience Event] 据计算算法得分。 有关的更多详 [!DNL Consumer Experience Event]细信息，请参 [阅准备要在Intelligent Services文档中使用的数据](../data-preparation.md)。

(CEE)模式中的 [!DNL Consumer Experience Event] 所有列对于Attribution AI并非必填。

>[!NOTE]
>
> 以下9列是必填的，其他列是可选的，但建议／必需，如果您希望将相同的数据用于其他Adobe解决方案（如和） [!DNL Customer AI] ，则 [!DNL Journey AI]此。

| 必填列 | 需要 |
| --- | --- |
| 主标识字段 | 触点／转化 |
| 时间戳 | 触点／转化 |
| Channel._type | 触点 |
| Channel.mediaAction | 触点 |
| Channel.mediaType | 触点 |
| Marketing.trackingCode | 触点 |
| Marketing.campaignname | 触点 |
| Marketing.campaigngroup | 触点 |
| 商务 | 转化 |

通常，属性在“商务”下的转换列（如订单、购买和结帐）上运行。 强烈建议使用“渠道”和“营销”列来定义接触点，以便获得良好的洞察。 但是，您可以在上面的列中加入任何其他列，以配置为转换或触点定义。

以下列不是必需的，但建议您在CEE模式中包含这些列（如果您有可用的信息）。

**其他建议列：**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### 历史数据

>[!IMPORTANT]
>
> Attribution AI运行所需的最小数据量如下：
> - 您需要提供至少3个月（90天）的数据才能运行良好的模型。
> - 您至少需要1000个转化率。


Attribution AI需要历史数据作为模型培训的输入。 所需的数据持续时间主要由两个关键因素决定：培训窗口和回顾窗口。 使用较短的培训窗口进行输入会更敏感于近期趋势，而较长的培训窗口有助于生成更稳定、更准确的模型。 用最能代表您业务目标的历史数据来建立目标模型非常重要。

根据 [发生时间](./user-guide.md#training-window) ，为模型培训设置的培训窗口配置过滤器转换事件。 目前，最低培训窗口为1个季度（90天）。 回 [顾窗口提](./user-guide.md#lookback-window) 供一个时间框架，指示应包括与此转换事件相关的转换事件接触点之前的天数。 这两个概念一起决定了应用程序所需的输入数据量（以天为单位）。

默认情况下，Attribution AI将培训窗口定义为最近的2个季度（6个月），回顾窗口定义为56天。 换言之，该模型将考虑过去2个季度发生的所有已定义转换事件，并查找在相关转换事件前56天内发生的所有接触点。

**公式**:

所需数据的最小长度=培训窗口+回顾窗口

>[!TIP]
>
> 具有默认配置的应用程序所需的最小数据长度是：2个季度（180天）+ 56天= 236天。

示例 :

- 您希望对过去90天（3个月）内发生的转化事件进行归因，并跟踪转化事件前4周内发生的所有接触点。 输入数据的持续时间应跨越过去90天+ 28天（4周）。 培训窗口为90天，回顾窗口为28天，总计为118天。

## Attribution AI输出数据

Attribution AI输出以下内容：

- [原始粒度分数](#raw-granular-scores)
- [汇总得分](#aggregated-attribution-scores)

**输出模式示例：**

![](./images/input-output/schema_output.gif)

### 原始粒度分数 {#raw-granular-scores}

Attribution AI以尽可能最精细的级别输出归因得分，以便您可以按任何得分列对得分进行分割。 要在UI中视图这些得分，请阅读查看原始得分 [路径一节](#raw-score-path)。 要使用API下载分数，请访 [问Attribution AI文档下载分](./download-scores.md) 。

>[!NOTE]
>
> 仅当以下任一条件为真时，您才能在分数输出数据集中查看输入数据集中所需的报告列：
> - 报告列作为触点或转换定义配置的一部分包含在配置页面中。
> - 报告列包含在其他得分数据集列中。


下表概述了原始分数示例输出中的模式字段：

| 列名称(DataType) | 可为空 | 描述 |
| --- | --- | --- |
| timestamp(DateTime) | False | 发生转换事件或观察的时间。 <br> **示例：** 2020-06-09T00:01:51.000Z |
| identityMap（映射） | True | identityMap与CEE XDM格式类似的用户。 |
| eventType（字符串） | True | 此时间系列记录的主事件类型。 <br> **示例：** “订单”、“购买”、“访问” |
| eventMergeId（字符串） | True | 一个ID，用于关联或合并 [!DNL Experience Events] 本质上相同的事件或应合并的多个。 这是在摄取之前由数据生成器填充的。 <br> **示例：** 575525617716-0-edc2ed37-1ab-4750-a820-1c2b3844b8c4 |
| _id（字符串） | False | 时间序列事件的唯一标识符。 <br> **示例：** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId（对象） | False | 与您的坚定ID对应的顶级对象容器。 <br> **示例：** _atsdsnrmmsv2 |
| your_模式_name（对象） | False | 对与转换事件关联的所有触点事件及其元数据进行分数行。 <br> **示例：** Attribution AI分数——型号名称__2020 |
| 分段（字符串） | True | 转换段，如构建模型时所依据的地理分段。 如果缺少区段，则区段与conversionName相同。 <br> **示例：** ORDER_US |
| conversionName（字符串） | True | 在设置过程中配置的转换的名称。 <br> **示例：** 订单、潜在客户、访问 |
| 转换（对象） | False | 转换元数据列。 |
| dataSource（字符串） | True | 数据源的全局唯一标识。 <br> **示例：** Adobe Analytics |
| eventSource（字符串） | True | 实际事件发生时的源。 <br> **示例：** Adobe.com |
| eventType（字符串） | True | 此时间系列记录的主事件类型。 <br> **示例：** 订单 |
| geo（字符串） | True | 转化所在的地理位置 `placeContext.geo.countryCode`。 <br> **示例：** 美国 |
| priceTotal(多次) | True | 通过转换获得的收入 <br> **示例：** 99.9 |
| product（字符串） | True | 产品本身的XDM标识符。 <br> **示例：** RX 1080 ti |
| productType（字符串） | True | 此产品视图向用户显示的产品显示名称。 <br> **示例：** Gpus |
| 数量（整数） | True | 转换期间购买的数量。 <br> **示例：** 1 1080 ti |
| receivedTimestamp(DateTime) | True | 已收到转换的时间戳。 <br> **示例：** 2020-06-09T00:01:51.000Z |
| skuId（字符串） | True | 库存单位(SKU)，供应商定义的产品的唯一标识符。 <br> **示例：** MJ-03-XS-Black |
| timestamp(DateTime) | True | 转换的时间戳。 <br> **示例：** 2020-06-09T00:01:51.000Z |
| passThrough（对象） | True | 配置模型时用户指定的其他得分数据集列。 |
| commerce_order_purchaseCity（字符串） | True | Additional Score数据集列。 <br> **示例：** 城市：圣何塞 |
| customerProfile（对象） | False | 用于构建模型的用户的身份详细信息。 |
| identity（对象） | False | 包含用于构建模型的用户的详细信息，如 `id` 和 `namespace`。 |
| id（字符串） | True | 用户的标识ID，如cookie ID、AAID或MCID等。 <br> **示例：** 1734876272540865634468320891369597404 |
| 命名空间（字符串） | True | 标识命名空间用于构建路径，进而构建模型。 <br> **示例：** 阿艾德 |
| 触点详细信息（对象数组） | True | 触点详细信息的列表，导致按触点发生或时间戳排序的转换。 |
| touchpointName（字符串） | True | 在设置过程中配置的触点的名称。 <br> **示例：** PAID_SEARCH_CLICK |
| 分数（对象） | True | 以得分形式对此转化做出触点贡献。 有关在此对象中生成的分数的详细信息，请参阅聚 [合归因得分](#aggregated-attribution-scores) 部分。 |
| touchPoint（对象） | True | 触点元数据。 有关在此对象中生成的分数的详细信息，请参 [阅聚合得分](#aggregated-scores) 部分。 |

### 查看原始得分路径(UI) {#raw-score-path}

您可以在UI中视图原始分数的路径。 开始, **[!UICONTROL 在平台]** UI中选择模式 **[!UICONTROL ，然后在“浏览”选项卡中搜索并选择归因AI得分]** 模式。

![选择模式](./images/input-output/schemas_browse.png)

接下来，在UI的“结构 **[!UICONTROL ”窗口]** 中选择一个字段，“字 **[!UICONTROL 段属性]** ”选项卡打开。 Within **[!UICONTROL Field]** properties是映射到原始分数的路径字段。

![选择模式](./images/input-output/field_properties.png)


### 汇总的归因得分 {#aggregated-attribution-scores}

如果日期范围小于30天，可以从平台UI以CSV格式下载汇总的分数。

Attribution AI支持两类别归因得分、算法得分和基于规则的得分。

Attribution AI产生两种不同类型的算法得分，增量和影响。 受影响的得分是每个营销接触点负责的转化率的一部分。 增量得分是营销接触点直接造成的边际影响量。 增量得分和受影响得分之间的主要区别在于增量得分将基准效果考虑在内。 它不假定转化纯粹是由之前的营销接触点引起的。

以下是Adobe Experience PlatformUI中的Attribution AI模式输出示例：

![](./images/input-output/schema_screenshot.png)

有关这些归因得分的更多详细信息，请参阅下表：

| 归因得分 | 描述 |
| ----- | ----------- |
| 受影响（算法） | 受影响的得分是每个营销接触点负责的转化率的一部分。 |
| 增量（算法） | 增量得分是营销接触点直接造成的边际影响量。 |
| 首次接触 | 基于规则的归因得分，可在转化路径上将所有积分分配给初始触点。 |
| 最后接触 | 基于规则的归因得分，将所有信用分配给最接近转化的触点。 |
| 线性 | 基于规则的归因得分，为转化路径上的每个接触点分配相等的积分。 |
| U 型 | 基于规则的归因得分，将40%的积分分配给第一个触点，40%的积分分配给最后一个触点，而其他接触点将其余20%平分。 |
| 时间衰减 | 基于规则的归因得分，即离转化更近的接触点获得的积分比距离转化更远的接触点多。 |

**原始得分参考（归因得分）**

下表将归因分数与原始分数进行映射。 如果要下载原始分数，请访问Attribution AI文 [档中的下载分](./download-scores.md) 数。

| 归因得分 | 原始得分参考列 |
| --- | --- |
| 受影响（算法） | _tenantID.your_模式名称。element.touchpoint.algorithmicEffected |
| 增量（算法） | _tenantID.your_模式名。touchpointsDetail.element.touchpoint.algorithmicEffected |
| 首次接触 | _tenantID.your_模式名。touchpointsDetail.element.touchpoint.firstTouch |
| 最后接触 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.lastTouch |
| 线性 | _tenantID.your_模式名。touchpointsDetail.element.touchpoint.linear |
| U 型 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.uShape |
| 时间衰减 | _tenantID.your_模式名。touchpointsDetail.element.touchpoint.decayUnits |

### 汇总得分 {#aggregated-scores}

如果日期范围小于30天，可以从平台UI以CSV格式下载汇总的分数。 有关这些聚合列的更多详细信息，请参阅下表。

| 列名称 | 约束 | 可为空 | 描述 |
| --- | --- | --- | --- |
| customrevents_date(DateTime) | 用户定义和固定格式 | False | 客户事件日期，YYYY-MM-DD格式。 <br> **示例**:2016-05-02 |
| mediatouchpoints_date(DateTime) | 用户定义和固定格式 | True | YYYY-MM-DD格式的媒体触点日期 <br> **示例**:2017-04-21 |
| segment（字符串） | 已计算 | False | 转换段，如构建模型时所依据的地理分段。 如果缺少区段，则区段与conversion_scope相同。 <br> **示例**:ORDER_AMER |
| conversion_scope（字符串） | 用户定义 | False | 由用户配置的转换名称。 <br> **示例**:订单 |
| touchpoint_scope（字符串） | 用户定义 | True | 用户配置的触点名称 <br> **示例**:PAID_SEARCH_CLICK |
| product（字符串） | 用户定义 | True | 产品的XDM标识符。 <br> **示例**:CC |
| product_type（字符串） | 用户定义 | True | 此产品视图向用户显示的产品显示名称。 <br> **示例**:gpus，笔记本电脑 |
| geo（字符串） | 用户定义 | True | 转换所在的地理位置(placeContext.geo.countryCode) <br> **示例**:美国 |
| 事件类型（字符串） | 用户定义 | True | 此时间序列记录的主事件类型 <br> **示例**:付费转换 |
| media_type（字符串） | 枚举 | False | 描述媒体类型是付费、自有还是免费的。 <br> **示例**:付费、自有 |
| 渠道（字符串） | 枚举 | False | 用 `channel._type` 于为XDM中具有相似属性的渠道提供粗略分类的属 [!DNL Consumer Experience Event] 性。 <br> **示例**:搜索 |
| 操作（字符串） | 枚举 | False | 该 `mediaAction` 属性用于提供体验事件媒体操作类型。 <br> **示例**:单击 |
| 活动组（字符串） | 用户定义 | True | 将多个活动分组到一起的活动组的名称，如“50%_DISCOUNT”。 <br> **示例**:商业类 |
| 活动名称（字符串） | 用户定义 | True | 用于标识营销活动的活动的名称，如“50%_DISCOUNT_USA”或“50%_DISCOUNT_ASIA”。 <br> **示例**:感恩节大甩卖 |

**原始得分参考（汇总）**

下表将汇总的得分映射到原始得分。 如果要下载原始分数，请访问Attribution AI文 [档中的下载分](./download-scores.md) 数。 要从UI中视图原始得分路径，请访问有关在此文档中查 [看原始得分路径](#raw-score-path) 的部分。

| 列名称 | 原始分数引用列 |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_模式名称。touchpointsDetail.element.touchpoint.timestamp |
| segment（区段） | _tenantID.your_模式名称。segmentation |
| conversion_scope | _tenantID.your_模式名称。conversion.conversionName |
| 触点范围 | _tenantID.your_模式名称。touchpointsDetail.element.touchpointName |
| 产品 | _tenantID.your_模式名称。conversion.product |
| product_type | _tenantID.your_模式名称。conversion.product_type |
| 地理 | _tenantID.your_模式名称。conversion.geo |
| 事件类型 | eventType |
| media_type | _tenantID.your_模式名。touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_模式名。touchpointsDetail.element.touchpoint.mediaChannel |
| 行动 | _tenantID.your_模式名。touchpointsDetail.element.touchpoint.mediaAction |
| 活动组 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.campaignGroup |
| 活动名 | _tenantID.your_模式_name.touchpointsDetail.element.touchpoint.campaignName |


## 后续步骤 {#next-steps}

准备好数据并准备好所有凭据和模式后，请遵循Attribution AI用户指 [南进行开始](./user-guide.md)。 本指南将指导您逐步创建Attribution AI实例。