---
keywords: Experience Platform；用户指南；归因ai；热门主题；区域
solution: Experience Platform, Intelligent Services
title: Attribution AIUI指南
topic: '用户指南 '
description: 此文档用作与Intelligent Services用户界面中的Attribution AI交互的指南。
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
translation-type: tm+mt
source-git-commit: 013f8d99fc394477177fdbf7eb9dd9b8ce94b88f
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 1%

---

# Attribution AIUI指南

Attribution AI是智能服务的一部分，是一种多渠道算法归因服务，用于计算客户交互对指定结果的影响和增量影响。 利用 Attribution AI，营销人员可以通过了解客户旅程各个阶段每个客户互动的影响来衡量和优化营销和广告支出。

此文档用作与Intelligent Services用户界面中的Attribution AI交互的指南。

## 创建实例

在[!DNL Adobe Experience Platform] UI中，单击左侧导航中的&#x200B;**[!UICONTROL Services]**。 出现&#x200B;**[!UICONTROL Services]**&#x200B;浏览器并显示可用的Adobe智能服务。 在Attribution AI容器中，单击&#x200B;**[!UICONTROL Open]**。

![访问您的实例](./images/user-guide/open_Attribution_ai.png)

将显示Attribution AI服务页面。 本页列表Attribution AI的服务实例并显示相关信息，包括实例名称、转换事件、实例的运行频率以及上次更新的状态。

您可以在&#x200B;**[!UICONTROL Create instance]**&#x200B;容器的右下侧找到&#x200B;**[!UICONTROL Total conversion events scored]**&#x200B;量度。 此量度跟踪当前日历年度中由Attribution AI计分的转换事件总数，包括所有沙箱环境和任何已删除的服务实例。

![](./images/user-guide/total_conversions.png)

使用UI右侧的控件可以编辑、克隆和删除服务实例。 要显示这些控件，请从现有&#x200B;**[!UICONTROL Service instances]**&#x200B;中选择一个实例。 控件包含以下信息：

- **[!UICONTROL Edit]**:选择 **[!UICONTROL Edit]** 后，您可以修改现有服务实例。您可以编辑实例的名称、描述、状态和评分频率。
- **[!UICONTROL Clone]**:选择 **[!UICONTROL Clone]** 将复制选定的服务实例。然后，您可以修改工作流以进行细微调整，并将其重命名为新实例。
- **[!UICONTROL Delete]**:您可以删除包含任何历史运行的服务实例。
- **[!UICONTROL Data source]**:指向此实例使用的数据集的链接。
- **[!UICONTROL Last run details]**:仅在运行失败时显示。此处显示有关运行失败原因的信息，如错误代码。

![](./images/user-guide/side_panel.png)

- **[!UICONTROL Conversion events]**:为此实例配置的转换事件的快速概述。
- **[!UICONTROL Lookback window]**:您定义的时间范围，指示在转换事件接触点之前的天数。
- **[!UICONTROL Touchpoints]**:创建此实例时定义的所有接触点的列表。

![](./images/user-guide/side_panel_2.png)

选择&#x200B;**[!UICONTROL Create instance]**&#x200B;开始。

![创建实例](./images/user-guide/landing_page.png)

接下来，将显示Attribution AI的设置页，您可以在该页中提供基本信息并为实例指定数据集。

![设置页面](./images/user-guide/setup_attribution.png)

### 命名实例

在&#x200B;**[!UICONTROL Basic information]**&#x200B;下，为服务实例提供名称和可选说明。

![命名实例](./images/user-guide/naming_instance.png)

### 选择数据集

填写基本信息后，单击标有&#x200B;**选择数据集**&#x200B;的下拉列表以选择您的数据集。 数据集用于训练模型并对其生成的后续数据进行评分。 从下拉选择器中选择Attribution AI集时，只列出与数据兼容且符合体验数据模型(XDM)模式的数据集。 选择数据集后，单击右上角的&#x200B;**下一步**&#x200B;以继续进入定义事件页。

>[!TIP]
>
>Adobe Analytics数据集通过Analytics Source Connector受支持。

![设置页面](./images/user-guide/dataset_selector.png)

## 定义事件

有三种不同类型的输入数据用于定义事件:

- **转化事件:** 确定营销活动（如电子商务订单、店内购买和网站访问）影响的业务目标。
- **回顾窗口：** 提供一个时间范围，指示应包括转换事件接触点之前的天数。
- **接触点：** 收件人、个人或Cookie级营销事件，用于评估转换的数字或基于收入的影响。

### 定义转换事件{#define-conversion-events}

要定义转换事件，您需要为事件提供一个名称，并通过单击&#x200B;**输入字段名称**&#x200B;下拉菜单选择事件类型。

![“](./images/user-guide/conversion_event_2.png)

选择事件后，其右侧将显示新的下拉列表。 第二个下拉列表用于通过使用操作为您的事件提供更多上下文。 对于此转换事件，使用默认操作&#x200B;*exists*。

>[!NOTE]
>
>当您定义事件时，将更新&#x200B;*转换名称*&#x200B;下的字符串。

![无](./images/user-guide/conversion_event_1.png)

**[!UICONTROL Add event]**&#x200B;和&#x200B;**[!UICONTROL Add Group]**&#x200B;按钮用于进一步定义转换。 根据您所定义的转换，您可能需要使用&#x200B;**[!UICONTROL Add event]**&#x200B;和&#x200B;**[!UICONTROL Add group]**&#x200B;按钮来提供更多上下文。

![添加事件](./images/user-guide/add_event.png)

单击&#x200B;**[!UICONTROL Add event]**&#x200B;可创建其他字段，这些字段可使用与上述相同的方法填充。 这样做会将AND语句添加到转换名称下的字符串定义中。 单击&#x200B;**x**&#x200B;以删除已添加的事件。

![添加事件菜单](./images/user-guide/add_event_result.png)

单击&#x200B;**[!UICONTROL Add Group]**&#x200B;可选择创建与原始字段分开的其他字段。 添加组后，将显示蓝色&#x200B;*和*&#x200B;按钮。 单击&#x200B;**和**&#x200B;可以选择将参数更改为包含“Or”。 “或”用于定义多个成功的转换路径。 “And”扩展了转换路径以包含其他条件。

![使用和](./images/user-guide/and_or.png)

如果需要多个转换，请单击&#x200B;**添加转换**&#x200B;以创建新的转换卡。 您可以重复上述过程来定义多个转换。

![添加转换](./images/user-guide/add_conversion.png)

### 定义回顾窗口{#lookback-window}

定义完转换后，您需要确认回顾窗口。 使用箭头键或单击默认值(56)，指定您希望包含接触点的转换事件前的天数。 接触点在下一步中定义。

![回顾](./images/user-guide/lookback_window.png)

### 定义接触点

定义接触点的工作流类似于[定义转换](#define-conversion-events)。 最初，您需要命名触点，并从&#x200B;*输入字段名称*&#x200B;下拉菜单中选择触点值。 选择后，将显示运算符下拉列表，其默认值为“exists”。 单击下拉列表以显示操作符的列表。

![运算符](./images/user-guide/operators.png)

为此触点的目的，请选择&#x200B;**等于**。

![步骤1](./images/user-guide/touchpoint_step1.png)

选择触点的运算符后，*输入字段值*&#x200B;即可用。 *输入字段值*&#x200B;的下拉值将根据您之前选择的运算符和触点值填充。 如果某个值未填充到下拉列表中，则可以手动键入该值。 单击下拉列表，然后选择&#x200B;**单击**。

>[!NOTE]
>
>运算符“exists”和“not exists”没有与它们关联的字段值。

![触点下拉列表](./images/user-guide/touchpoint_dropdown.png)

*添加事件*&#x200B;和&#x200B;*添加组*&#x200B;按钮用于进一步定义触点。 由于接触点周围的复杂特性，对于单个接触点具有多个事件和组的情况并不罕见。

单击&#x200B;**添加事件**&#x200B;后，可添加其他字段。 单击&#x200B;**x**&#x200B;以删除已添加的事件。

![添加事件](./images/user-guide/touchpoint_add_event.png)

单击&#x200B;**添加组**&#x200B;可以选择创建与原始字段分开的其他字段。 添加组后，将显示蓝色&#x200B;*和*&#x200B;按钮。 单击&#x200B;**和**&#x200B;更改参数，新参数“Or”用于定义多个成功路径。 此特定接触点只有一条成功路径，因此不需要“Or”。

![触点概述](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>使用&#x200B;*触点名称*&#x200B;下的字符串可快速查看您的触点。 请注意，该字符串与触点的名称匹配。

![](./images/user-guide/touchpoint_string.png)

您可以通过单击&#x200B;**添加触点**&#x200B;并重复上述过程来添加其他触点。

![添加触点](./images/user-guide/add_touchpoint.png)

定义完所有必要的接触点后，向上滚动并单击右上角的&#x200B;**下一步**&#x200B;以继续执行最后一步。

![完成定义](./images/user-guide/define_event_next.png)

## 高级培训和评分设置

Attribution AI中的最后一页是用于设置培训和得分的&#x200B;**[!UICONTROL Advanced]**&#x200B;页。

![新页面](./images/user-guide/advanced_settings.png)

### 计划培训

使用&#x200B;*计划*，您可以选择要进行评分的一周中的日期和时间。

单击&#x200B;*评分频率*&#x200B;下的下拉列表，在每日、每周和每月评分之间进行选择。 接下来，选择您希望进行评分的星期。 可以选择多天。 再次单击一天可取消选择它。

![计划培训](./images/user-guide/schedule_training.png)

要更改要进行评分的一天中的时间，请单击时钟图标。 在显示的新叠加中，输入要进行评分的日期。 在叠加外部单击以关闭它。

>[!NOTE]
>
>完成每个评分过程最多可能需要24小时。

![时钟图标](./images/user-guide/time_of_day.png)

### 其他得分数据集列（可选）

默认情况下，将为标准模式中的每个服务实例创建分数数据集。 您可以选择根据“转换”事件和“触点”配置向得分数据集输出添加其他列。 开始通过从输入数据集中选择列，您随后可以拖放这些列以更改顺序，方法是按住汉堡包图标上的鼠标左键。

![分数据集列添加](./images/user-guide/Add-score-dataset.png)

### 基于区域的建模（可选）{#region-based-modeling-optional}

您客户的行为可能因国家和地区而有很大差异。 对于全球企业，使用基于国家或基于区域的模型可以提高归因准确性。 添加的每个区域都使用该区域的数据创建新模型。

要定义新区域，请单击&#x200B;**[!UICONTROL Add region]**&#x200B;进行开始。 在显示的容器中，提供区域的名称。 从&#x200B;**[!UICONTROL Enter Field Name]**&#x200B;下拉列表中只填充一个值(&quot;placeContext.geo.countryCode&quot;)。 选择此值。

![选择](./images/user-guide/select_region_att.png)

接下来，选择一个运算符。

![区域运算符](./images/user-guide/region_operators.png)

最后，在&#x200B;**[!UICONTROL Enter Field Value]**&#x200B;下拉列表中键入国家/地区代码。

>[!NOTE]
>
>国家代码长度为两个字符。 在[ISO 3166-1 alpha-2](https://datahub.io/core/country-list)中可找到完整的列表。

![地区](./images/user-guide/region-based.png)

### 培训窗口{#training-window}

为确保您获得尽可能最准确的模型，使用代表您业务的历史数据来培训您的模型非常重要。 默认情况下，模型使用2个季度（6个月）的转化事件数据进行培训。 选择下拉列表以更改默认设置。 您可以选择用1到4/4的数据（3-12个月）进行培训。

>[!NOTE]
>
>较短的培训窗口对最近的趋势更敏感，而较长的培训窗口则创建更可靠的模型，对最近的趋势则不那么敏感。

![培训窗口](./images/user-guide/training_window.png)

选择培训窗口后，单击右上角的&#x200B;**[!UICONTROL Finish]**。 为数据处理留出一些时间。 完成后，将显示一个快显对话框，确认实例设置已完成。 单击&#x200B;**[!UICONTROL Ok]**&#x200B;可重定向到&#x200B;**[!UICONTROL Service instances]**&#x200B;页面，您可以在该页面查看您的服务实例。

![设置完成](./images/user-guide/instance_setup_complete.png)

## 后续步骤

通过遵循本教程，您已成功地在Attribution AI中创建了服务实例。 实例完成评分（最多允许24小时）后，您就可以[发现Attribution AI洞察](./discover-insights.md)。 此外，如果您希望下载评分结果，请访问[下载分数](./download-scores.md)文档。

## 其他资源

以下视频概述了用于在Attribution AI中创建新实例的端对端工作流程。

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
