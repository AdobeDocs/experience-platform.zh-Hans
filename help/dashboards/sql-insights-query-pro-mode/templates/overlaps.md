---
title: 高级受众重叠
description: 了解如何使用高级受众重叠仪表板分析受众交叉点并做出数据驱动型决策。 筛选受众、比较重叠并导出见解以改进定位策略。
source-git-commit: 90d5f00648a80d735b92c3bdc540f1ad18ff38f5
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 2%

---

# 高级受众重叠

通过分析不同受众区段与[!UICONTROL 高级受众重叠]仪表板的交叉方式，获得宝贵的见解以优化受众分段和定位策略。 检查列表量度，以识别重叠、优化分段并减少冗余消息传递。 最终，您可以利用这些见解来创建更有针对性的营销活动和高效的营销工作。 在此仪表板上，您可以查看受众交叉点、应用过滤器和执行详细的重叠分析，以制定数据驱动型决策并改善参与结果。

## 筛选受众 {#filter-audiences}

要筛选重叠分析的特定受众，请选择筛选器图标（![筛选器图标）。](../../../images/icons/filter-icon-white.png))以打开[!UICONTROL 筛选器]对话框。 在此处，您可以在重叠模板中添加或删除受众以优化您的分析。

![高级受众与突出显示的过滤器图标重叠。](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-filter-icon.png)

出现[!UICONTROL 筛选器]对话框。 要选择重叠分析的受众，请从&#x200B;**[!UICONTROL 受众]**&#x200B;下拉列表中选择一个受众名称。 您添加的任何受众的名称都会显示在下拉列表下方，并带有标记。 添加后，您可以通过名称选择“X”来删除它们。 要删除所有应用的筛选器，请选择&#x200B;**[!UICONTROL 全部清除]**。

## 应用的过滤器 {#applied-filters}

应用过滤器后（屏幕快照示例中为[!UICONTROL Amoxicilin区段]），显示的受众数据将被缩小。 您选择添加的任何其他受众将显示在[!UICONTROL 高级受众重叠]图表上方的[!UICONTROL 按]筛选标记旁边。

![高级受众与高亮显示的Amoxicilin区段筛选功能板重叠。](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-applied-filters.png)

## 高级受众重叠表 {#advanced-audience-overlaps-table}

仪表板的主要部分显示[!UICONTROL 高级受众重叠]表，该表提供了不同区段之间受众重叠的详细比较。 表列如下：

| 列名 | 描述 |
|------------------------------------|----------------------------------------------------------------------------------------------|
| **[!UICONTROL Source_Segment_Name]** | 正在分析的原始受众（例如“阿莫西林区段”）。 |
| **[!UICONTROL 重叠区段名称]** | 将重叠与进行比较的受众（例如，“血糖> 100”）。 |
| **[!UICONTROL Source_Segment_Audience_Count]** | 源受众的配置文件总数。 |
| **[!UICONTROL Overlap_Segment_Audience_Count]** | 重叠受众的大小，具体取决于重叠。 |
| **[!UICONTROL Overlap_Audience_Count]** | 源和重叠受众之间的实际重叠受众的大小。 |

{style="table-layout:auto"}

## 导出分析 {#export-insights}

过滤并分析受众后，可导出数据以供进一步离线分析或报告。 要导出您的分析，请选择表右上角的&#x200B;**[!UICONTROL 导出]**。 此时将显示打印PDF对话框，允许您将数据保存为PDF或打印。

![高级受众与突出显示的导出内容重叠。](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-export.png)

要返回[!UICONTROL 模板]概述，请选择&#x200B;**[!UICONTROL 模板]**。

![高级受众与突出显示的模板重叠。](../../images/sql-insights-query-pro-mode/templates/audience-overlaps-navigation.png)

## 后续步骤

阅读本文档后，您已了解如何使用&#x200B;**[!UICONTROL 高级受众重叠]**&#x200B;仪表板分析受众交叉点并做出数据驱动型决策。 要进一步优化受众分段和定位策略，请探索其他数据Distiller模板，这些模板可提供有价值的见解。 请参阅[受众趋势](./trends.md)、[受众比较](./comparison.md)和[受众标识重叠](./identity-overlaps.md) UI指南，以继续增强您的受众参与和分段工作。

