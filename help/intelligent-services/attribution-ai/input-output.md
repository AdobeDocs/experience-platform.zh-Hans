---
keywords: Experience Platform；快速入门；归因ai；热门主题；归因ai输入；归因ai输出；
feature: Attribution AI
title: 输入和输出Attribution AI
topic-legacy: Input and Output data for Attribution AI
description: 以下文档概述了Attribution AI中使用的不同输入和输出。
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: 3ea17aa57a5bfbc968f354b13d2ed107b2efa39b
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 3%

---

# 输入和输出 [!DNL Attribution AI]

以下文档概述了 [!DNL Attribution AI].

## [!DNL Attribution AI] 输入数据

Attribution AI通过分析以下数据集来计算算法得分：

- Adobe Analytics数据集使用 [Analytics源连接器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- 一般来自Adobe Experience Platform架构的体验事件(EE)数据集
- 消费者体验事件(CEE)数据集

您现在可以根据 **身份映射** （字段），前提是每个数据集共享相同的身份类型（命名空间），如ECID。 选择标识和命名空间后，将显示ID列完整性量度，该量度指示拼合的数据量。 要了解有关添加多个数据集的更多信息，请访问 [Attribution AI用户指南](./user-guide.md#identity).

默认情况下，渠道信息并非始终映射。 在某些情况下，如果mediaChannel（字段）为空，则在将字段映射到mediaChannel之前，您将无法“继续”，因为它是必需列。 如果在数据集中检测到渠道，则默认情况下会将其映射到mediaChannel。 其他列，例如 **媒体类型** 和 **媒体操作** 仍是可选的。

映射渠道字段后，继续执行“定义事件”步骤，在此步骤中，您可以选择转化事件、接触点事件，并从各个数据集中选择特定字段。

>[!IMPORTANT]
>
>Adobe Analytics源连接器可能需要长达四周的时间才能回填数据。 如果您最近设置了一个连接器，则应验证数据集是否具有Attribution AI所需的最小数据长度。 请查看 [历史数据](#data-requirements) 部分，以验证您是否有足够的数据来计算准确的算法得分。

有关设置 [!DNL Consumer Experience Event] (CEE)架构，请参阅 [智能服务数据准备](../data-preparation.md) 的双曲余切值。 有关映射Adobe Analytics数据的更多信息，请访问 [Analytics字段映射](../../sources/connectors/adobe-applications/analytics.md) 文档。

并非 [!DNL Consumer Experience Event] (CEE)架构对于Attribution AI是必选的。

您可以使用下面在架构或选定数据集中建议的任何字段配置接触点。

| 推荐列 | 需要 |
| --- | --- |
| 主标识字段 | 接触点/转化 |
| 时间戳 | 接触点/转化 |
| 渠道._type | 接触点 |
| Channel.mediaAction | 接触点 |
| Channel.mediaType | 接触点 |
| Marketing.trackingCode | 接触点 |
| Marketing.campaignname | 接触点 |
| Marketing.campaigngroup | 接触点 |
| Commerce | 转化 |

通常，归因会在“商务”下的转化列（如订单、购买和结账）上运行。 “渠道”和“营销”列用于定义Attribution AI的接触点(例如， `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`)。 为获得最佳结果和分析，强烈建议您包含尽可能多的转化和接触点列。 此外，您也不限于上述列。 您可以包含任何其他推荐或自定义列作为转化或接触点定义。

体验事件(EE)只要与配置接触点相关的渠道或营销活动信息存在于混合或传递字段之一中，数据集就无需明确包含渠道和营销混合。

>[!TIP]
>
>如果您在CEE架构中使用Adobe Analytics数据，则Analytics的接触点信息通常存储在 `channel.typeAtSource` (例如， `channel.typeAtSource = 'email'`)。

## 历史数据 {#data-requirements}

>[!IMPORTANT]
>
> Attribution AI正常运行所需的最小数据量如下：
> - 您需要提供至少3个月（90天）的数据才能运行良好的模型。
> - 您至少需要1000次转化。


Attribution AI需要历史数据作为模型培训的输入。 所需数据持续时间主要由两个关键因素决定：培训窗口和回顾窗口。 较短培训窗口的输入对最新趋势更敏感，而较长培训窗口有助于生成更稳定、更准确的模型。 使用最能代表您业务目标的历史数据来建模目标非常重要。

的 [培训窗口配置](./user-guide.md#training-window) 根据发生时间过滤为模型培训包含的转化事件。 目前，最低培训时间为1个季度（90天）。 的 [回顾窗口](./user-guide.md#lookback-window) 提供一个时间范围，用于指示在转化事件接触点之前应包含多少天与此转化事件相关。 这两个概念共同决定了应用程序所需的输入数据量（以天为单位）。

默认情况下，Attribution AI会将培训窗口定义为最近的2个季度（6个月），回顾窗口定义为56天。 换言之，模型将考虑过去2个季度内发生的所有已定义转化事件，并查找在关联转化事件之前56天内发生的所有接触点。

**公式**:

所需数据的最小长度=培训窗口+回顾窗口

>[!TIP]
>
> 具有默认配置的应用程序所需的最小数据长度为：2个季度（180天）+ 56天= 236天。

示例：

- 您希望对过去90天（3个月）内发生的转化事件进行归因，并跟踪转化事件发生前4周内发生的所有接触点。 输入数据的持续时间应该会持续过去90天+ 28天（4周）。 培训时间范围为90天，回顾时间范围为28天，总计为118天。

## Attribution AI输出数据

Attribution AI输出以下内容：

- [原始粒度分数](#raw-granular-scores)
- [汇总得分](#aggregated-attribution-scores)

**输出架构示例：**

![](./images/input-output/schema_output.gif)

### 原始粒度分数 {#raw-granular-scores}

Attribution AI会以尽可能最精细的粒度级别输出归因得分，以便您可以按任何得分列对得分进行细分。 要在UI中查看这些得分，请阅读 [查看原始分数路径](#raw-score-path). 要使用API下载分数，请访问 [下载Attribution AI分数](./download-scores.md) 文档。

>[!NOTE]
>
> 仅当满足以下任一条件时，才能从分数输出数据集的输入数据集中看到任何所需的报表列：
> - 报表列作为接触点或转化定义配置的一部分包含在配置页面中。
> - 报表列包含在其他分数数据集列中。


下表概述了原始分数示例输出中的架构字段：

| 列名称(DataType) | 可为空 | 描述 |
| --- | --- | --- |
| timestamp(DateTime) | False | 发生转化事件或观察的时间。 <br> **示例：** 2020-06-09T00:01:51.000Z |
| identityMap(Map) | True | 与CEE XDM格式类似的用户标识映射。 |
| eventType（字符串） | True | 此时间系列记录的主事件类型。 <br> **示例：** “订单”、“购买”、“访问” |
| eventMergeId（字符串） | True | 要关联或合并多个 [!DNL Experience Events] 实质上是相同事件或应合并的事件。 该代码将在摄取之前由数据生成器填充。 <br> **示例：** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id（字符串） | False | 时间系列事件的唯一标识符。 <br> **示例：** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId（对象） | False | 与您的联系人ID相关的顶级对象容器。 <br> **示例：** _atsdsnrmmsv2 |
| your_schema_name（对象） | False | 具有转化事件的所有与其关联的接触点事件及其元数据的分数行。 <br> **示例：** Attribution AI得分 — 型号名称__2020 |
| 分段（字符串） | True | 转化区段，如构建模型所依据的地域划分。 如果没有区段，则区段与conversionName相同。 <br> **示例：** ORDER_US |
| conversionName（字符串） | True | 在设置过程中配置的转换的名称。 <br> **示例：** 订单、潜在客户、访问 |
| 转化（对象） | False | 转换元数据列。 |
| dataSource（字符串） | True | 数据源的全局唯一标识。 <br> **示例：** Adobe Analytics |
| eventSource（字符串） | True | 实际事件发生时的来源。 <br> **示例：** Adobe.com |
| eventType（字符串） | True | 此时间系列记录的主事件类型。 <br> **示例：** 订购 |
| 地域（字符串） | True | 交付转化的地理位置 `placeContext.geo.countryCode`. <br> **示例：** 美国 |
| priceTotal（双精度） | True | 透过转换取得之收益 <br> **示例：** 99.9 |
| product（字符串） | True | 产品本身的XDM标识符。 <br> **示例：** RX 1080 ti |
| productType（字符串） | True | 产品的显示名称，显示给此产品视图的用户。 <br> **示例：** 戈普斯 |
| 数量（整数） | True | 转化期间的购买数量。 <br> **示例：** 1 1080立 |
| receivedTimestamp(DateTime) | True | 收到转化的时间戳。 <br> **示例：** 2020-06-09T00:01:51.000Z |
| skuId（字符串） | True | 库存单位(SKU)，由供应商定义的产品的唯一标识符。 <br> **示例：** MJ-03-XS-Black |
| timestamp(DateTime) | True | 转换的时间戳。 <br> **示例：** 2020-06-09T00:01:51.000Z |
| passThrough（对象） | True | 配置模型时由用户指定的其他得分数据集列。 |
| commerce_order_purchaseCity（字符串） | True | “其他得分”数据集列。 <br> **示例：** 城市：圣何塞 |
| customerProfile（对象） | False | 用于构建模型的用户的身份详细信息。 |
| 标识（对象） | False | 包含用于构建模型的用户的详细信息，例如 `id` 和 `namespace`. |
| id（字符串） | True | 用户的标识ID，如Cookie ID、AAID或MCID等。 <br> **示例：** 17348762725408656344688320891369597404 |
| 命名空间（字符串） | True | 用于构建路径以及由此构建模型的身份命名空间。 <br> **示例：** aaid |
| 接触点详细信息（对象数组） | True | 导致转化的接触点详细信息列表，按 | 接触点出现次数或时间戳。 |
| touchpointName（字符串） | True | 在设置过程中配置的接触点的名称。 <br> **示例：** PAID_SEARCH_CLICK |
| 分数（对象） | True | 接触点对此转化的贡献为得分。 有关此对象中生成的分数的详细信息，请参阅 [汇总归因分数](#aggregated-attribution-scores) 中。 |
| touchPoint（对象） | True | 接触点元数据。 有关此对象中生成的分数的详细信息，请参阅 [汇总分数](#aggregated-scores) 中。 |

### 查看原始分数路径(UI) {#raw-score-path}

您可以在UI中查看原始分数的路径。 首先选择 **[!UICONTROL 模式]** 然后，在Platform UI中，从 **[!UICONTROL 浏览]** 选项卡。

![选择您的架构](./images/input-output/schemas_browse.png)

接下来，在 **[!UICONTROL 结构]** 窗口， **[!UICONTROL 字段属性]** 选项卡。 在 **[!UICONTROL 字段属性]** 是映射到原始分数的路径字段。

![选择架构](./images/input-output/field_properties.png)

### 汇总归因得分 {#aggregated-attribution-scores}

如果日期范围小于30天，则可以从Platform UI中以CSV格式下载汇总的得分。

Attribution AI支持两类归因得分：算法得分和基于规则的得分。

Attribution AI会生成两种不同类型的算法得分：增量分数和受影响分数。 受影响的得分是每个营销接触点所负责的转化部分。 增量得分是营销接触点直接导致的边际影响量。 增量分数与受影响分数之间的主要区别在于，增量分数考虑了基线效果。 它不认为转化完全由之前的营销接触点引起。

以下是Adobe Experience Platform UI中的Attribution AI架构输出示例：

![](./images/input-output/schema_screenshot.png)

有关每个归因分数的更多详细信息，请参阅下表：

| 归因得分 | 描述 |
| ----- | ----------- |
| 受影响（算法） | 影响得分是每个营销接触点负责的转化部分。 |
| 增量（算法） | 增量得分是营销接触点直接导致的边际影响量。 |
| 首次接触 | 基于规则的归因得分，用于向转化路径上的初始接触点分配所有点数。 |
| 最后接触 | 基于规则的归因得分，可将所有点数分配到最接近转化的接触点。 |
| 线性 | 基于规则的归因得分，为转化路径上的每个接触点分配同等点数。 |
| U 型 | 基于规则的归因得分，将40%的点数分配给第一个接触点，40%的点数分配给最后一个接触点，而其他接触点将平均分配其余20%。 |
| 时间衰减 | 基于规则的归因分数，即离转化较近的接触点获得的点数多于距离转化时间较远的接触点。 |

**原始分数参考（归因分数）**

下表将归因得分映射到原始得分。 如果要下载原始分数，请访问 [下载Attribution AI分数](./download-scores.md) 文档。

| 归因得分 | 原始分数引用列 |
| --- | --- |
| 受影响（算法） | _tenantID.your_schema_name.element.touchpoint.algorithmicEffected |
| 增量（算法） | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicEffected |
| 首次接触 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| 最后接触 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| 线性 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U 型 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| 时间衰减 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### 汇总得分 {#aggregated-scores}

如果日期范围小于30天，则可以从Platform UI中以CSV格式下载汇总的得分。 有关每个聚合列的更多详细信息，请参阅下表。

| 列名称 | 约束 | 可为空 | 描述 |
| --- | --- | --- | --- |
| customrevents_date(DateTime) | 用户定义和固定格式 | False | 客户事件日期（YYYY-MM-DD格式）。 <br> **示例**:2016-05-02 |
| mediatouchpoints_date(DateTime) | 用户定义和固定格式 | True | YYYY-MM-DD格式的媒体接触点日期 <br> **示例**:2017-04-21 |
| 区段（字符串） | 已计算 | False | 转化区段，如构建模型所依据的地域划分。 如果没有区段，则区段与conversion_scope相同。 <br> **示例**:ORDER_AMER |
| conversion_scope（字符串） | 用户定义的 | False | 由用户配置的转化名称。 <br> **示例**:订单 |
| touchpoint_scope（字符串） | 用户定义的 | True | 由用户配置的接触点名称 <br> **示例**:PAID_SEARCH_CLICK |
| product（字符串） | 用户定义的 | True | 产品的XDM标识符。 <br> **示例**:CC |
| product_type（字符串） | 用户定义的 | True | 产品的显示名称，显示给此产品视图的用户。 <br> **示例**:gpu、笔记本电脑 |
| 地域（字符串） | 用户定义的 | True | 交付转化的地理位置(placeContext.geo.countryCode) <br> **示例**:美国 |
| event_type（字符串） | 用户定义的 | True | 此时间系列记录的主事件类型 <br> **示例**:付费转化 |
| media_type（字符串） | 枚举 | False | 描述媒体类型是付费、自有还是免费。 <br> **示例**:付费、自有 |
| 渠道（字符串） | 枚举 | False | 的 `channel._type` 属性，用于对 [!DNL Consumer Experience Event] XDM。 <br> **示例**:搜索 |
| 操作（字符串） | 枚举 | False | 的 `mediaAction` 属性用于提供体验事件媒体操作类型。 <br> **示例**:单击 |
| campaign_group（字符串） | 用户定义的 | True | 将多个营销活动分组在一起的营销活动组的名称，如“50%_DISCOUNT”。 <br> **示例**:商业 |
| campaign_name（字符串） | 用户定义的 | True | 用于识别营销活动（如“50%_DISCOUNT_USA”或“50%_DISCOUNT_ASIA”）的营销活动的名称。 <br> **示例**:感恩节大甩卖 |

**原始分数引用（汇总）**

下表将汇总的得分映射到原始得分。 如果要下载原始分数，请访问 [下载Attribution AI分数](./download-scores.md) 文档。 要从UI中查看原始分数路径，请访问 [查看原始分数路径](#raw-score-path) 在本文档中。

| 列名称 | 原始分数引用列 |
| --- | --- |
| customrevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segment（区段） | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| 产品 | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| 地域 | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| 操作 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |


## 后续步骤 {#next-steps}

准备数据并部署所有凭据和模式后，请首先按照 [Attribution AI用户指南](./user-guide.md). 本指南将指导您完成创建Attribution AI实例的过程。
