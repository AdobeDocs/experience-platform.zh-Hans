---
keywords: Experience Platform;insights;attribution ai;popular topics
solution: Experience Platform
title: 在归因人工智能中发现洞察
topic: Attribution AI insights
translation-type: tm+mt
source-git-commit: 0f6424c5afbf9b23016e1c40d156f6226f853cd6

---


# 在归因人工智能中发现洞察

归因AI服务实例提供的洞察可用于帮助制定和衡量与营销绩效和投资回报相关的营销决策。 选择服务实例可提供可视化和过滤器，帮助您了解客户旅程每个阶段每次客户互动的影响。

此文档可作为与Adobe Intelligent Services用户界面中的服务实例洞察交互的指南。

## 入门指南

为了利用归因AI的洞察，您需要有一个运行状态成功的服务实例。 要创建新的服务实例，请访问 [Attribution AI用户界面指南](./user-guide.md)。 如果您最近创建了一个服务实例，但该实例仍在培训和评分中，请允许24小时以便它完成运行。

## 服务实例洞察概述

在Adobe Experience Platform UI中，单击左侧导 **航中** 的“服务”。 将显 *示“服务* ”浏览器并显示可用的Adobe Intelligent Services。 在“归因AI”容器中，单击“打 **开”**。

![访问实例](./images/insights/open_Attribution_ai.png)

此时将显示“归因AI”服务页面。 本页列表了归因AI的服务实例并显示了相关信息，包括实例的名称、转换事件、实例的运行频率以及上次更新的状态。 单击服务实例名称开始。

>[!NOTE] 只能选择已成功完成评分运行的服务实例。

![创建实例](./images/insights/select-service-instance.png)

接下来，将显示该服务实例的洞察页面，其中为您提供了可视化信息和大量与数据交互的过滤器。 本指南中将更详细地说明可视化和过滤器。

![设置页面](./images/insights/landing-page.png)

### 服务实例详细信息

要视图服务实例的其他详细信息，请 **单击右上角** 的“显示更多”。

![显示更多](./images/insights/show-more.png)

此时将显示详细的列表。 有关所列任何属性的详细信息，请访问 [Attribution AI用户指南](./user-guide.md)。

![显示详细信息](./images/insights/advanced-details.png)

### 编辑实例

要编辑实例，请在右上 *方的导航* 中单击“编辑”。
![单击编辑按钮](./images/insights/edit-button.png)

此时会显示编辑对话框，允许您编辑实例的说明和评分频率。 要确认更改并关闭对话框，请单 *击右下角的* “编辑”。

![编辑快照](./images/insights/edit-popover.png)

### 更多操作

“ *更多操作* ”按钮位于“编辑”旁边的右上导 *航中*。 单击 **更多操作** ，将打开一个下拉列表，允许您选择以下操作之一：

- **删除**:删除实例。
- **下载摘要数据**:下载包含摘要数据的CSV文件。
- **访问分数**:单击“ *访问得分* ”可将您重定向到 [“归因人工智能”教程的访问得分](./download-scores.md)。
- **视图运行历史**:此时会显示一个列表，其中包含与服务实例关联的所有评分运行。

![更多操作](./images/insights/more-actions.png)

## 筛选数据

归因人工智能洞察允许您过滤数据并根据选定过滤器自动更新UI视觉元素。

>[!NOTE] 默认情况下，除了将“归因模型”过滤器设置为“增量和受影响的归因转换”外，每个过滤器都设置为“全部” ** 。

### 转换事件

在归因AI中创建新实例时，其中一个必填字段是“转化事件”。 转化事件是确定营销活动（如电子商务订单、店内购买和网站访问）影响的业务目标。

在实例中，“转 *换事件* ”下拉列表允许您选择为实例定义的任何事件以过滤数据。 选择特定事件会更改UI可视化，以仅填充属于这些事件的转换。

![转化事件](./images/insights/conversion-event.png)

### 归因模型

单击 *归因模型* ，将打开一个下拉菜单，其中提供所有不同的归因模型。 您可以选择多个模型来比较结果。 有关不同归因模型及其工作方式的更多信息，请访问归因人工智能概述，其中包含一个包含每个模型相关信息的表。 [](./overview.md)

![归因模型](./images/insights/attribution-model.png)

### 产品

产 *品过滤器* ，允许您从创建实例时最初摄取的任何产品中进行选择。 单击下拉列表，然后使用搜索功能快速选择要比较的所有产品。

![产品过滤器](./images/insights/product-filter.png)

### 地理

“地 *理位置* ”筛选器基于基于区域的模型填充国家代码。 根据您的数据，此过滤器可能存在，也可能不存在。

>[!NOTE] 国家／地区代码长度为两个字符。 完整的列表可在 [ISO 3166-1 alpha-2此处找到](https://datahub.io/core/country-list)。

### 地区

>[!NOTE] 仅当您在创建服务实例时在Attribution AI用户界面指南中执 [行了可选的基于区域的步骤](./user-guide.md#region-based-modeling-optional) ，此过滤器才存在。

此过滤器允许您选择在实例创建过程中设置的任何区域。

### Channel

单击 *渠道* 过滤器会显示包含所有可用营销渠道的下拉列表。 您可以选择多个渠道来比较它们。

![Channel](./images/insights/channel.png)

### Date Range

单击日历图标以打开日期范围快显视窗。 开始和结束转换事件日期决定在UI中填充的数据量。 您可以选择缩小或扩大日期范围，以集中或扩大已填充的数据量。

![日期范围](./images/insights/display-date-range.png)

## 数据概述

概述 *卡按归因模型* ，显示您的总转化率。 总数会根据您使用本文档中以前概述的过滤器进行搜索的具体程度而更改。 选择更多模型会向“概述”添加其他圆，每个圆的颜色都与图例对应。

![概述](./images/insights/Overview.png)

## 每周趋势

“每 *周趋势* ”卡按您在筛选过程中设置的日期范围细分您的总转化率。

![趋势](./images/insights/weekly-trends.png)

单击“ *Weekly trends* ”（每周趋势）卡右上角的省略号会显示一个下拉框，允许您选择每日、每周或每月趋势。

将指针悬停在特定归因模型的数据线上可创建一个快显窗口，其中显示该日期的转换总数。

![悬停趋势](./images/insights/weekly-trend-hover.png)

## 按渠道细分

“按 *渠道细分* ”卡用于确定与每个渠道相关的转换总数。 此卡可帮助决定每个渠道的有效性和投资回报。

![细分渠道](./images/insights/channel-breakdown.png)

单击按渠道划分卡右上角的省略 *号* ，将打开一个下拉列表，允许您根据接触点填充数据。

![触点](./images/insights/breakdown-by-touchpoints.png)

## 顶级活动

“ *顶级活动* ”卡显示活动的概述以及活动在每个渠道中的执行情况。 此信息卡可帮助您的团队了解特定活动对特定渠道的有效性，并提供进一步投资的洞察。

![顶级活动](./images/insights/top-campaigns.png)

## 后续步骤

过滤完数据并能够显示相应的信息后，您便可以选择访问分数。 有关如何访问得分的详细指南，请访问归因AI教 [程中的访问得分](./download-scores.md) 。 此外，您还可以下载摘要数据，如更多操作 [中所示](#more-actions)。 选择“下载摘要数据”将下载按日期汇总的摘要数据。