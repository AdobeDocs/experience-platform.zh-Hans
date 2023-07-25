---
title: 用户档案仪表板客户人工智能小组件
description: 了解客户人工智能如何提供有关您组织的Real-time Customer Profile数据的流失或倾向的重要见解。
hide: true
hidefromtoc: true
source-git-commit: e14067606e4c4868c926433129d835c7b0a7a18f
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 2%

---

# 用户档案仪表板客户人工智能小组件 {#customer-ai-profiles-widgets}

Customer AI 用于生成自定义倾向分数，如个人档案大规模的流失率和转化率。客户人工智能通过分析现有的消费者体验事件数据来预测客户流失或转化倾向分数，从而实现这一点。 这些高精度的客户倾向模型允许进行更精确的分段和定位。 此 [得分分布](#customer-ai-distribution-of-scores) 和 [评分摘要](#customer-ai-scoring-summary) 分析会在您的受众中展示该划分。 它们会突出显示哪些用户档案具有高度/低度/中度的倾向性，以及它们在用户档案计数中的分布方式。

<!-- 
The links when required:
* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores) 
-->

## [!UICONTROL 得分的客户人工智能分布] {#customer-ai-distribution-of-scores}

此 [!UICONTROL 得分的客户人工智能分布] 构件按倾向分数对配置文件总数进行分类。 用户档案计数的分布由AI模型和选定的合并策略确定，然后以5%的增量进行可视化以指示其倾向。 用户档案倾向性采用分别以绿色、黄色和红色表示的“高”、“中”和“低”颜色编码。 沿Y轴提供用户档案计数，沿X轴提供倾向分数。

>[!NOTE]
>
>如果可视化图表是转化倾向得分，则高分以绿色显示，低分以红色显示。 如果您预计客户流失倾向，则流失倾向会逆转，高分以红色显示，低分以绿色显示。 无论您选择哪种倾向类型，中段都会保持黄色。

确定倾向分数的AI模型是从小组件标题下的下拉选择器中选择的。 下拉列表包含所有已配置的Customer AI模型的列表。 从可用模型列表中为您的分析选择适当的AI模型。 如果没有可用的客户人工智能模型，则小部件中的一条消息将指导您配置至少一个客户人工智能模型，并提供指向客户人工智能模型配置页面的超链接。 有关说明，请参阅文档 [如何配置客户人工智能实例](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>选择概述选项卡正下方的下拉列表，以更改用于确定分析中包含哪些配置文件的合并策略。 请参阅以下部分 [合并策略](#merge-policies) 以获取简要说明，或 [合并策略概述](../../profile/merge-policies/overview.md) 以了解更多详细信息。

要导航到所选客户人工智能模型的详细分析页面，请选择 **[!UICONTROL 查看模型详细信息]**.

![包含的Experience Platform受众功能板 [!UICONTROL 得分的客户人工智能分布] 构件和 [!UICONTROL 查看模型详细信息] 突出显示。](../images/segments/customer-ai-distribution-of-scores.png)

此时将显示详细的模型分析页面。

![客户人工智能的分析页面。](../images/profiles/customer-ai-insights-page.png)

有关客户人工智能的更多信息，请访问 [探索见解UI指南](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## [!UICONTROL 客户人工智能评分摘要] {#customer-ai-scoring-summary}

此构件显示已评分的用户档案总数，并将它们分类为分别包含高、中和低倾向性的绿色、黄色和红色存储桶。 圆环图说明了高、中和低倾向性之间用户档案的比例组成。 用户档案符合75岁以上的高倾向性、25至74岁之间的中倾向性和24岁以下的低倾向性条件。 图例指示颜色代码和倾向性阈值。 当光标悬停在圆环图的相应部分上时，会在对话框中显示高、中和低倾向的配置文件计数。

构件标题下的下拉菜单提供了所有已配置的Customer AI模型的列表。 从可用模型列表中为您的分析选择适当的AI模型。 如果没有可用的客户人工智能模型，则小部件中的一条消息将指导您配置至少一个客户人工智能模型，并提供指向客户人工智能模型配置页面的超链接。 请参阅相关文档 [如何配置客户人工智能实例](../../intelligent-services/customer-ai/user-guide/configure.md) 以获取详细说明。

>[!NOTE]
>
>计算的配置文件总数取决于所选的合并策略。 要更改使用的合并策略，请选择概述选项卡正下方的下拉菜单。 请参阅以下部分 [合并策略](#merge-policies) 以获取简要说明，或 [合并策略概述](../../profile/merge-policies/overview.md) 以了解更多详细信息。

![突出显示具有客户人工智能评分摘要构件的Experience Platform受众仪表板。](../images/segments/customer-ai-scoring-summary.png)

要导航到所选客户人工智能模型的详细分析页面，请选择 **[!UICONTROL 查看模型详细信息]**. 有关客户人工智能的更多信息，请访问 [探索见解UI指南](../../intelligent-services/customer-ai/user-guide/discover-insights.md).