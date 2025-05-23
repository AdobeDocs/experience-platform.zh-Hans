---
keywords: Experience Platform；分析；客户人工智能；热门主题；客户人工智能分析
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: 用客户人工智能发掘见解
description: 本文档用作在Intelligent Services客户人工智能用户界面中与服务实例见解交互的指南。
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '2449'
ht-degree: 1%

---

# 用Customer AI发现见解

客户人工智能，作为智能服务的一部分，为营销人员提供了利用Adobe Sensei来预测客户下一步动向的能力。 客户人工智能用于生成自定义倾向分数，如轮廓大规模的流失率和转化率。无需将业务需求转换为机器学习问题、选择算法、培训或部署，即可实现上述目标。

本文档用作在Intelligent Services客户人工智能用户界面中与服务实例见解交互的指南。

## 快速入门

为了利用客户人工智能的分析，您需要具有运行状态成功的服务实例。 要创建新服务实例，请访问[配置客户人工智能实例](./configure.md)。 如果您最近创建了一个服务实例，但该实例仍在训练和评分中，请留出24小时以使它完成运行。

## 服务实例概述

在[!DNL Adobe Experience Platform] UI的左侧导航中选择&#x200B;**[!UICONTROL 服务]**。 出现&#x200B;*服务*&#x200B;浏览器并显示可用的智能服务。 在客户人工智能的容器中，选择&#x200B;**[!UICONTROL 打开]**。

![在Adobe Experience Platform UI中导航到Customer AI服务实例。](../images/insights/navigate-to-service.png)

此时会显示“客户人工智能服务”页面。 此页面列出了客户人工智能的服务实例并显示其相关信息，包括实例名称、倾向类型、实例运行频率以及上次更新状态。

>[!NOTE]
>
>只有已完成成功评分运行的服务实例才会具有见解。

![Customer AI仪表板显示服务实例列表及其详细信息。](../images/insights/dashboard.png)

选择服务实例名称以开始。

![屏幕截图显示了在Customer AI仪表板中选择服务实例名称的过程。](../images/insights/click-the-name.png)

接下来，将显示该服务实例的见解页面，其中具有选择&#x200B;**[!UICONTROL 最新得分]**&#x200B;或&#x200B;**[!UICONTROL 性能摘要]**&#x200B;的选项。 默认选项卡&#x200B;**[!UICONTROL 最新得分]**&#x200B;提供数据的可视化图表。 本指南中对可视化图表以及您可以对数据执行的操作进行了更详细的说明。

**[!UICONTROL 绩效摘要]**&#x200B;选项卡显示每个倾向存储段的实际客户流失率或转化率。 若要了解详细信息，请参阅有关[性能摘要量度](#performance-metrics)的部分。

![Customer AI见解登陆页面，其中显示了用于浏览见解的各种可视化图表和选项。](../images/insights/landing_page_insights.png)

## 服务实例详细信息

有两种方法可以查看服务实例详细信息：在仪表板中或在服务实例中。

### 服务实例仪表板

要查看仪表板中服务实例详细信息的概览，请选择一个服务实例容器，从而避免附加到名称的超链接。 这将打开一个提供其他详细信息的右边栏。 这些控件包含以下内容：

- **[!UICONTROL 编辑]**：选择&#x200B;**[!UICONTROL 编辑]**&#x200B;允许您修改现有的服务实例。 您可以编辑实例的名称、描述和评分频率。
- **[!UICONTROL 克隆]**：选择&#x200B;**[!UICONTROL 克隆]**&#x200B;将复制当前选择的服务实例设置。 然后，您可以修改工作流以进行细微的调整，并将其重命名为新实例。
- **[!UICONTROL 删除]**：您可以删除服务实例，包括任何历史运行。
- **[!UICONTROL 数据源]**：此实例使用的数据集的链接。
- **[!UICONTROL 运行频率]**：评分运行的频率和时间。
- **[!UICONTROL 得分定义]**：您为此实例配置的目标快速概述。

![服务实例面板，显示名称、描述、评分频率和其他配置选项等详细信息。](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>如果评分运行失败，则会提供错误消息。 错误消息列在右边栏的&#x200B;**上次运行详细信息**&#x200B;下，该错误消息仅对失败的运行可见。

在客户人工智能中针对失败的评分运行显示了![错误消息。](../images/insights/failed-run.png)

### 显示更多分析下拉列表

查看服务实例的其他详细信息的第二种方法位于分析页面中。 选择右上方的&#x200B;**[!UICONTROL 显示更多]**&#x200B;以填充下拉列表。 其中列出了详细信息，例如得分定义、创建时间、倾向类型和使用的数据集。 有关列出的任何属性的详细信息，请访问[配置客户人工智能实例](./configure.md)。

![Customer AI数据集预览弹出窗口显示多个数据集，其中包含颜色编码的键以便于识别。](../images/insights/landing-show-more.png)

### Customer AI数据集预览弹出框

如果客户人工智能使用了多个数据集，则会提供一个标记为&#x200B;**[!UICONTROL Multiple]**&#x200B;的超链接，其后跟有括号`()`中的数据集数。

![显示颜色编码键的多个数据集预览，用于轻松识别客户人工智能中使用的数据集。](../images/insights/insights-multi-datasets.png)

选择多个数据集链接将打开客户人工智能数据集预览弹出框。 预览中的每种颜色表示一个数据集，如数据集列左侧的颜色键中所示。 在此示例中，您可以看到只有&#x200B;**数据集1**&#x200B;包含`PROP1`列。

![数据集预览弹出框显示选定实例的其他详细信息。](../images/insights/dataset-preview.png)

### 编辑实例

要编辑实例，请在右上角导航中选择&#x200B;**[!UICONTROL 编辑]**。

客户人工智能界面中的![编辑按钮。](../images/insights/edit-button.png)

此时将显示“编辑”对话框，允许您编辑实例的名称、描述、状态和评分频率。 要确认更改并关闭对话框，请选择右下角的&#x200B;**[!UICONTROL 保存]**。

![编辑实例弹出框显示用于修改客户人工智能实例的名称、描述、状态和评分频率的选项。](../images/insights/edit-instance.png)

### 更多操作

**[!UICONTROL 更多操作]**&#x200B;按钮位于&#x200B;**[!UICONTROL 编辑]**&#x200B;旁边的右上角导航区域中。 选择&#x200B;**[!UICONTROL 更多操作]**&#x200B;将打开一个下拉菜单，允许您选择以下操作之一：

- **[!UICONTROL 克隆]**：选择&#x200B;**[!UICONTROL 克隆]**&#x200B;将复制服务实例设置。 然后，您可以修改工作流以进行细微的调整，并将其重命名为新实例。
- **[!UICONTROL 删除]**：删除实例。
- **[!UICONTROL 访问得分]**：选择&#x200B;**[!UICONTROL 访问得分]**&#x200B;将打开一个对话框，其中提供了指向[下载客户人工智能得分](./download-scores.md)教程的链接，该对话框还提供了进行API调用所需的数据集ID。
- **[!UICONTROL 查看运行历史记录]**：将显示一个对话框，其中包含与服务实例关联的所有评分运行的列表。

![显示克隆、删除、访问得分和查看运行历史记录等选项的更多操作下拉列表。](../images/insights/more-actions.png)

## 评分汇总 {#scoring-summary}

评分摘要显示评分的用户档案总数，并将它们分类为包含高、中和低倾向的分段。 根据得分范围确定倾向时段，低值小于24，中值为25至74，高值大于74。 每个存储桶都有一个与图例对应的颜色。

>[!NOTE]
>
>如果是转化倾向分数，则高分以绿色显示，低分以红色显示。 如果您预计客户流失倾向，则流失倾向会逆转，高分以红色显示，低分以绿色显示。 无论您选择哪种倾向类型，中段都会保持黄色。

![已评分用户档案的可视化图表，这些用户档案分为高、中和低倾向存储段，每个存储段均以不同的颜色表示。](../images/insights/scoring-summary.png)

您可以将鼠标悬停在环上的任何颜色上以查看附加信息，例如属于某个存储段的配置文件百分比和总数。

![显示高、中、低倾向区间个人资料分布的评分环可视化图表。](../images/insights/scoring-ring.png)

## 得分分布

**[!UICONTROL 分数分布]**&#x200B;卡会根据分数为您提供群体的可视化摘要。 您在[!UICONTROL 分数分布]卡中看到的颜色表示生成的倾向分数的类型。 将鼠标悬停在任何评分分配上会提供属于该分配的准确计数。

![显示客户人工智能中不同倾向区间得分分布的可视化图表。](../images/insights/distribution-of-scores.png)

## 影响因素

对于每个得分分段，将生成一张卡片，其中显示该分段的前10个影响因素。 影响因素会为您提供有关客户属于各种分数存储桶原因的更多详细信息。

![每个倾向区间的影响因素可视化图表，突出显示影响客户行为的前10个因素。](../images/insights/influential-factors.png)

### 影响因素明细

将鼠标悬停在任何主要影响因素上会进一步细分数据。 将为您概述为什么某些用户档案属于倾向存储桶。 根据因素，可以为您提供数字、分类或布尔值。 下面的示例按区域显示分类值。

![显示所选倾向性存储桶影响因素详细细分的深入可视化图表。](../images/insights/drilldown.png)

此外，通过使用深入分析，您可以比较分布系数（如果它出现在两个或更多倾向分段中），并使用这些值创建更具体的区段。 以下示例说明了第一个用例：

![跨倾向存储桶的分布因素比较，突出显示影响因素的差异。](../images/insights/drilldown-compare.png)

您可以看到，转化倾向较低的用户档案最近访问adobe.com网页的可能性较小。 “上次web访问间隔天数”因子的覆盖率仅为8%，而中倾向性用户档案的覆盖率则为26%。 使用这些数字，您可以比较系数每个时段内的分配。 此信息可用于推断Webvisit中的回访间隔在低倾向性存储桶中的影响较小，因为它在中倾向性存储桶中的影响较小。

### 创建区段

选择低、中、高倾向的任何分段中的&#x200B;**[!UICONTROL 创建区段]**&#x200B;按钮，会将您重定向到区段生成器。

>[!NOTE]
>
>**[!UICONTROL 创建区段]**&#x200B;按钮仅在为数据集启用实时客户配置文件时可用。 有关如何启用实时客户个人资料的更多信息，请访问[实时客户个人资料概述](../../../rtcdp/overview.md)。

![按钮，用于从客户人工智能分析中的影响因素创建区段。](../images/insights/influential-factors-create-segment.png)

![按钮，用于从客户人工智能分析中的影响因素创建区段。](../images/insights/create-segment.png)

区段生成器用于定义区段。 从“分析”页面中选择&#x200B;**[!UICONTROL 创建区段]**&#x200B;时，客户人工智能会自动将所选分段信息添加到该区段。 要完成创建区段，只需填写位于区段生成器用户界面右边栏中的&#x200B;**Name**&#x200B;和&#x200B;**Description**&#x200B;容器。 为区段指定名称和描述后，选择右上方的&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>由于倾向分数将写入个人资料，因此与任何其他个人资料属性一样，它们在区段生成器中可用。 当您导航到区段生成器以创建新区段时，您可以在命名空间Customer AI下看到所有各种倾向分数。

![区段保存界面显示保存前要输入区段名称和说明的字段。](../images/insights/segment-saving.png)

要在Experience Platform UI中查看新区段，请在左侧导航中选择&#x200B;**[!UICONTROL 区段]**。 此时会显示&#x200B;**[!UICONTROL 浏览]**&#x200B;页面并显示所有可用区段。

![区段仪表板，显示Experience Platform UI中所有可用区段的列表。](../images/insights/Segments-dashboard.png)

## 历史绩效 {#historical-performance}

**[!UICONTROL 性能摘要]**&#x200B;选项卡显示实际客户流失率或转化率，这些流失率或转化率被划分到客户人工智能评分的每个倾向分段中。

![性能摘要选项卡显示不同倾向分段的流失率或转化率，并包含按日期范围过滤和查看单个评分运行结果的选项。](../images/insights/summary_tab.png)

最初，仅显示预期汇率（虚线）。 当评分运行尚未发生并且数据尚不可用时，会显示预期比率。 但是，一旦结果窗口过去，预计比率将替换为实际比率（实线）。

将鼠标悬停在这些行上会显示该时段中该天的日期和实际/预期费率。

![显示高、中、低倾向类别中用户档案分布的流失倾向桶可视化图表。](../images/insights/churn_tab.png)

您可以筛选所显示的预期速率和实际速率的时间范围。 选择&#x200B;**日历图标** ![图标](/help/images/icons/calendar.png)然后选择新的日期范围。 每个分段中的结果都会更新并在新日期范围内显示。

![日期选择器显示按特定日期范围筛选结果的选项。](../images/insights/date_selector.png)

### 个人评分运行率

**[!UICONTROL 性能摘要]**&#x200B;选项卡的下半部分显示每个评分运行的结果。 选择右上方的下拉日期以显示不同评分运行的结果。

根据您预测的是流失还是转化，[!UICONTROL 分数分布]图形将显示每个增量中流失/转化和未流失/转化的用户档案分布。

![显示流失/转化和未流失/未转化类别中用户档案分布的单个评分运行结果的可视化。](../images/insights/scoring_tab.png)

## 模型评估 {#model-evaluation}

除了在历史绩效选项卡上跟踪一段时间内的预测和实际结果外，营销人员还可以通过模型评估选项卡提高模型质量的透明度。 您可以使用提升和收益图来确定使用预测模型与随机定位之间的差异。 此外，您还可以确定在每次得分截止值时捕获多少积极结果。 这对于细分以及使投资回报率与营销行动相协调非常有用。

### 提升图

![提升图显示预测模型优于随机定位。 早期十分位提升值较高表示模型强。](../images/user-guide/lift-chart.png)

提升图可衡量使用预测模型而不是随机定位的改进情况。

高质量的模型指标包括：

- 前几位小数中的提升值较高。 这意味着该模型能够很好地识别具有最高兴趣行为倾向的用户。
- 提升值降序。 这意味着得分较高的客户比得分较低的用户更有可能采取感兴趣的行动。

### 收益图

![收益图说明了通过定位高倾向用户与随机定位获得的积极结果的累计百分比。](../images/user-guide/gains-chart.png)

累积收益表衡量通过定位分数超过特定阈值而捕获的积极结果的百分比。 在按倾向性得分从高到低对客户进行分类后，群体被分为十分位，即10个大小相等的群组。 一个完美的模型能把所有积极结果都纳入最高分的十分位数中。 基线随机定位方法可按照组规模的比例捕获积极结果 — 以30%的用户为目标将获得30%的结果。

高质量的模型指标包括：

- 累积收益很快接近100%。
- 该模型的累计收益曲线更接近图表的左上角。
- 累积收益表可用于确定分段和定位的得分截止值。 例如，如果该模型在前两个得分十分位数中捕获了70%的积极结果，则以百分位得分> 80的用户为目标，预计将捕获大约70%的积极结果。

### AUC（曲线下的区域）

AUC反映了得分排名与预测目标发生之间的关系强度。 0.5的&#x200B;**AUC**&#x200B;意味着模型并不比随机猜测好。 **AUC**&#x200B;为1意味着该模型可以完美地预测谁将执行相关操作。

## 后续步骤

本文档概述了客户人工智能服务实例提供的见解。 您现在可以继续阅读有关[在客户人工智能中下载得分](./download-scores.md)的教程，或者浏览提供的其他[Adobe Intelligent Services](../../home.md)指南。

## 其他资源

以下视频概述了如何使用客户人工智能查看模型和影响因素的输出。

>[!VIDEO](https://video.tv.adobe.com/v/36591?learn=on&quality=12&captions=chi_hans)
