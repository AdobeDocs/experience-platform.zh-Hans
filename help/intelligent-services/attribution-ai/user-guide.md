---
keywords: Experience Platform；用户指南；归因人工智能；热门主题；区域
feature: Attribution AI
title: Attribution AI UI指南
description: 本文档用作在Intelligent Services用户界面中与Attribution AI交互的指南。
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2451'
ht-degree: 0%

---

# 归因人工智能UI指南

Attribution AI作为Intelligent Services的一部分，是一种多渠道的算法归因服务，它计算客户交互对指定结果的影响和增量影响。 借助归因人工智能，营销人员可以通过了解客户旅程各个阶段每个客户互动的影响来衡量和优化营销和广告支出。

本文档用作在Intelligent Services用户界面中与Attribution AI交互的指南。

## 创建模型

在[!DNL Adobe Experience Platform] UI的左侧导航中选择&#x200B;**[!UICONTROL 服务]**。 **[!UICONTROL 服务]**&#x200B;浏览器出现，并显示可用的Adobe智能服务。 在归因人工智能的容器中，选择&#x200B;**[!UICONTROL 打开]**。

![正在访问您的模型](./images/user-guide/open_Attribution_ai.png)

此时将显示“归因人工智能服务”页面。 此页面列出归因人工智能的服务模型并显示它们的相关信息，包括模型的名称、转化事件、模型的运行频率以及上次更新的状态。

您可以在&#x200B;**[!UICONTROL 创建模型]**&#x200B;容器的右下角找到&#x200B;**[!UICONTROL 已评分的转化事件总数]**&#x200B;个量度。 此量度跟踪归因人工智能在当前日历年计分的转化事件总数，包括所有沙盒环境和任何已删除的服务模型。

总转化次数![](./images/user-guide/total_conversions.png)

通过使用UI右侧的控件，可以编辑、克隆和删除服务模型。 若要显示这些控件，请从现有&#x200B;**[!UICONTROL 服务模型]**&#x200B;中选择一个模型。 这些控件包含以下信息：

- **[!UICONTROL 编辑]**：选择&#x200B;**[!UICONTROL 编辑]**&#x200B;允许您修改现有的服务模型。 您可以编辑模型的名称、描述、状态、评分频率以及其他得分数据集列。
- **[!UICONTROL 克隆]**：选择&#x200B;**[!UICONTROL 克隆]**&#x200B;将复制所选的服务模型。 然后，您可以修改工作流以进行细微调整，并将其重命名为新模型。
- **[!UICONTROL 删除]**：您可以删除包含任何历史运行的服务模型。 相应的输出数据集将从Experience Platform中删除。 但是，同步到实时客户档案的分数不会被删除。
- **[!UICONTROL 数据源]**：正在使用的数据集的链接。 如果归因人工智能使用多个数据集，则显示“多个”，后面跟着数据集数。 选择超链接后，将显示数据集预览弹出框。
- **[!UICONTROL 上次运行详细信息]**：仅当运行失败时才会显示此信息。 此处显示有关运行失败原因的信息，如错误代码。

![侧窗格](./images/user-guide/multiple-datasets-pane.png)

- **[!UICONTROL 转化事件]**：针对此模型配置的转化事件的快速概述。
- **[!UICONTROL 回顾时间范围]**：您定义的时间范围，用于指示包含转换事件接触点之前的天数。
- **[!UICONTROL 接触点]**：您在创建此模型时定义的所有接触点的列表。

![](./images/user-guide/side_panel_2.png)

选择&#x200B;**[!UICONTROL 创建模型]**&#x200B;以开始。

![创建模型](./images/user-guide/landing_page.png)

接下来，将显示Attribution AI设置页面，您可以在其中提供服务模型的名称和可选描述。

![命名模型](./images/user-guide/naming_instance.png)

## 选择数据 {#select-data}

<!-- https://www.adobe.com/go/aai-select-data -->

通过设计，归因人工智能可以使用Adobe Analytics、体验事件和消费者体验事件数据来计算归因分数。 在选择数据集时，仅列出与归因人工智能兼容的数据集。 要选择一个数据集，请选择数据集名称旁边的(**+**)符号，或选中该复选框以一次添加多个数据集。 您还可以使用搜索选项快速查找感兴趣的数据集。

选择您要使用的数据集后，选择&#x200B;**[!UICONTROL 添加]**&#x200B;按钮以将数据集添加到数据集预览窗格。

![选择数据集](./images/user-guide/select-datasets.png)

选择数据集旁边的信息图标![信息图标](/help/images/icons/info.png)将打开数据集预览弹出框。

![选择并搜索数据集](./images/user-guide/dataset-preview.png)

数据集预览包含上次更新时间、源架构和前十列的预览等数据。

选择&#x200B;**[!UICONTROL 保存]**&#x200B;以在工作流中移动时保存草稿。 您还可以保存草稿模型配置并转到工作流中的下一步。 在模型配置期间使用&#x200B;**[!UICONTROL 保存并继续]**&#x200B;创建和保存草稿。 利用功能，可创建和保存模型配置的草稿，当必须在配置工作流中定义多个字段时特别有用。

![突出显示了“保存并保存并继续”的数据科学服务归因人工智能选项卡的创建工作流。](./images/user-guide/aai-save-save-&-exit.png)

### 数据集完整性 {#dataset-completeness}

<!-- https://www.adobe.com/go/aai-dataset-completeness -->

在数据集预览中，是数据集完整性百分比值。 此值提供数据集中有多少列为空/空的快速快照。 如果数据集包含大量缺失值，并且这些值是在其他位置捕获的，则强烈建议您包含包含包含缺失值的数据集。

>[!NOTE]
>
>数据集完整性使用Attribution AI的最大训练窗口（一年）计算。 这意味着在显示数据集完整性值时，不会考虑超过一年的数据。

![数据集完整性](./images/user-guide/dataset-completeness.png)

### 选择身份 {#identity}

您现在可以根据标识映射（字段）将多个数据集连接在一起。 您必须选择身份类型（也称为“身份命名空间”）以及该命名空间中的身份值。 如果在同一命名空间下将多个字段指定为架构中的标识，则所有分配的标识值都会显示在由命名空间（如`EMAIL (personalEmail.address)`或`EMAIL (workEmail.address)`）前置的标识下拉列表中。

>[!IMPORTANT]
>
>您选择的每个数据集都必须使用相同的身份类型（命名空间）。 在身份列中，身份类型旁边会显示一个绿色复选标记，指示数据集兼容。 例如，在使用Phone命名空间和`mobilePhone.number`作为标识符时，其余数据集的所有标识符都必须包含并使用Phone命名空间。

要选择标识，请选择位于标识列中的带下划线的值。 此时将显示“选择身份”弹出框。

![选择相同的命名空间](./images/user-guide/aai-identity-map-save-and-exit.png)

如果命名空间中有多个可用身份，请确保为您的用例选择正确的身份字段。 例如，电子邮件命名空间中提供了两个电子邮件身份：一个是工作电子邮件，另一个是个人电子邮件。 根据用例，个人电子邮件更有可能被填写，并且在个人预测中更有用。 这意味着您将选择`EMAIL (personalEmail.address)`作为您的身份。

未选择![数据集键](./images/user-guide/aai-identity-namespace.png)

>[!NOTE]
>
> 如果数据集不存在有效的身份类型（命名空间），则必须使用[架构编辑器](../../xdm/schema/composition.md#identity)设置主身份并将其分配给身份命名空间。 要了解有关命名空间和身份的详细信息，请访问[Identity Service命名空间](../../identity-service/features/namespaces.md)文档。

## 映射媒体渠道和营销活动字段 {#aai-mapping}

<!-- https://www.adobe.com/go/aai-mapping -->

选择并添加完数据集后，将显示&#x200B;**映射**&#x200B;配置步骤。 归因人工智能要求您映射在上一步中选择的每个数据集的媒体渠道字段。 这是因为如果没有数据集之间的媒体渠道映射，则从归因人工智能派生的见解可能无法正常显示，从而导致见解页面难以解释。 尽管只需使用媒体渠道，但强烈建议您映射某些可选字段，例如媒体操作、促销活动名称、促销活动组和促销活动标记。 这样做可以让归因人工智能提供更清晰的洞察和最佳结果。

![映射](./images/user-guide/mapping-save-&-exit.png)

## 定义事件 {#define-events}

<!-- https://www.adobe.com/go/aai-define-events -->

有三种不同类型的输入数据用于定义事件：

- **转化事件：**&#x200B;确定营销活动（如电子商务订单、店内购买和网站访问）影响的业务目标。
- **回顾时间范围：**&#x200B;提供一个时间范围，用于指示应包含转换事件接触点之前的天数。
- **接触点：**&#x200B;收件人、个人和/或Cookie级别的营销事件，用于评估转化的数值或基于收入的影响。

### 定义转化事件 {#define-conversion-events}

要定义转化事件，您需要为事件提供一个名称，并通过从&#x200B;**选择数据集和字段**&#x200B;下拉菜单中选择数据集和字段来选择事件类型。

![是下拉列表](./images/user-guide/define-conversion-events.png)

选择事件后，其右侧将显示一个新的下拉列表。 第二个下拉列表用于通过使用操作为事件提供进一步的上下文。 对于此转换事件，使用默认操作&#x200B;*存在*。

>[!NOTE]
>
>在定义事件时，*转化名称*&#x200B;下的字符串将更新。

![没有下拉列表](./images/user-guide/conversion_event_1.png)

接下来，您可以选择在上一步中通过组合所有输入数据集生成的组合数据集。 或者，您也可以从&#x200B;**选择数据集和字段**&#x200B;下拉菜单中选择基于单个数据集的列。

**[!UICONTROL 添加事件]**&#x200B;和&#x200B;**[!UICONTROL 添加群组]**&#x200B;按钮用于进一步定义您的转化。 根据您定义的转换，您可能需要使用&#x200B;**[!UICONTROL 添加事件]**&#x200B;和&#x200B;**[!UICONTROL 添加组]**&#x200B;按钮来提供进一步的上下文。

![添加事件](./images/user-guide/add_event.png)

选择&#x200B;**[!UICONTROL 添加事件]**&#x200B;将创建附加字段，可使用与上述相同的方法填充这些字段。 这样做会将AND语句添加到转换名称下方的字符串定义中。 选择&#x200B;**x**&#x200B;可删除已添加的事件。

![添加事件菜单](./images/user-guide/add_event_result.png)

选择&#x200B;**[!UICONTROL 添加群组]**&#x200B;可让您选择创建与原始字段不同的其他字段。 添加组后，将显示一个蓝色的&#x200B;*和*&#x200B;按钮。 选择&#x200B;**And**&#x200B;后，可以选择将参数更改为包含“Or”。 “或”用于定义多个成功的转化路径。 “和”扩展了转换路径以包含其他条件。

![使用and或](./images/user-guide/and_or.png)

如果需要多个转换，请选择&#x200B;**添加转换**&#x200B;以创建新的转换卡。 您可以重复上述过程以定义多个转化。

![添加转换](./images/user-guide/add_conversion.png)

### 定义回顾时间范围 {#lookback-window}

定义完转化后，需要确认回顾时间范围。 使用箭头键或选择默认值(56)，指定您希望在转换事件之前的几天包括接触点。 在下一步中定义接触点。

![回顾](./images/user-guide/lookback_window.png)

### 定义接触点

定义接触点的工作流程与[定义转化](#define-conversion-events)的工作流程类似。 最初，您需要为接触点命名，并从&#x200B;*输入字段名称*&#x200B;下拉菜单中选择一个接触点值。 选择后，将显示运算符下拉列表，默认值为“存在”。 选择下拉菜单以显示运算符列表。

![操作员](./images/user-guide/operators.png)

对于此接触点，选择&#x200B;**等于**。

![步骤1](./images/user-guide/touchpoint_step1.png)

选择接触点的运算符后，*输入字段值*&#x200B;将变为可用。 *输入字段值*&#x200B;的下拉值将根据您之前选择的运算符和接触点值填充。 如果下拉列表中未填充某个值，您可以手动在中键入该值。 选择下拉菜单并选择&#x200B;**单击**。

>[!NOTE]
>
>运算符“存在”和“不存在”没有与其关联的字段值。

![接触点下拉列表](./images/user-guide/touchpoint_dropdown.png)

**添加事件**&#x200B;和&#x200B;**添加群组**&#x200B;按钮用于进一步定义您的接触点。 由于接触点周围的性质复杂，对于单个接触点有多个事件和组是很常见的现象。

选中后，**添加事件**&#x200B;允许添加其他字段。 选择&#x200B;**x**&#x200B;可删除已添加的事件。

![添加事件](./images/user-guide/touchpoint_add_event.png)

选择&#x200B;**添加群组**，您可以选择创建与原始字段不同的其他字段。 添加组后，将显示一个蓝色的&#x200B;*和*&#x200B;按钮。 选择&#x200B;**And**&#x200B;以更改参数，新参数“Or”用于定义多个成功路径。 此特定接触点只有一个成功路径，因此不需要“或”。

![接触点概述](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>使用&#x200B;*接触点名称*&#x200B;下的字符串快速了解您的接触点。 请注意，字符串与接触点的名称匹配。

![](./images/user-guide/touchpoint_string.png)

您可以通过选择&#x200B;**添加接触点**&#x200B;并重复上述过程来添加其他接触点。

![添加接触点](./images/user-guide/add_touchpoint.png)

定义完所有必需的接触点后，向上滚动并选择右上角的&#x200B;**下一步**&#x200B;以继续执行最后一步。

![已完成定义](./images/user-guide/define_event_save_and_exit.png)

## 高级培训和评分设置

归因人工智能中的最后一页是用于设置训练和评分的&#x200B;**[!UICONTROL 高级]**&#x200B;页面。

![新页面集选项](./images/user-guide/advanced_settings_set_options.png)

### 安排培训

使用&#x200B;*计划*，您可以选择一周中的哪一天和时间进行评分。

选择&#x200B;*评分频率*&#x200B;下的下拉列表，以在每日、每周和每月评分之间进行选择。 接下来，选择您希望在一周中的哪几天进行评分。 可以选择多天。 再次选择同一天会取消选择它。

![计划培训](./images/user-guide/schedule_training.png)

要更改一天中要计分的时间，请选择时钟图标。 在显示的新叠加图中，输入您希望进行评分的时间。 在叠加图之外选择以将其关闭。

>[!NOTE]
>
>每个评分过程可能需要24小时才能完成。

![时钟图标](./images/user-guide/time_of_day.png)

### 其他得分数据集列（可选）

默认情况下，将为标准架构中的每个服务模型创建一个得分数据集。 您可以选择根据转化事件和接触点配置向评分数据集输出添加其他列。 首先，从输入数据集中选择列，然后您可以通过在汉堡图标上按住鼠标左键来拖放这些列以更改顺序。

![得分数据集列添加](./images/user-guide/Add-score-dataset.png)

### 基于区域的建模（可选） {#region-based-modeling-optional}

您的客户行为可能因国家/地区和地理区域而存在显着差异。 对于全球企业，使用基于国家或地区的模型可以提高归因准确性。 添加的每个区域都将使用该区域的数据创建一个新模型。

要定义新区域，请先选择&#x200B;**[!UICONTROL 添加区域]**。 在显示的容器中，提供区域的名称。 从&#x200B;**[!UICONTROL 输入字段名称]**&#x200B;下拉列表中只填充一个值(“placeContext.geo.countryCode”)。 选择此值。

![选择区域at](./images/user-guide/select_region_att.png)

接下来，选择一个运算符。

![区域运算符](./images/user-guide/region_operators.png)

最后，在&#x200B;**[!UICONTROL 输入字段值]**&#x200B;下拉列表中键入国家/地区代码。

>[!NOTE]
>
>国家/地区代码的长度为两个字符。 可以在此找到[ISO 3166-1 alpha-2](https://datahub.io/core/country-list)的完整列表。

![区域](./images/user-guide/region-based.png)

### 训练窗口期 {#training-window}

为了确保您获得尽可能准确的模型，请务必使用代表您业务的历史数据来训练您的模型。 默认情况下，使用转化事件数据对模型进行两季度（6个月）的培训。 选择下拉菜单以更改默认值。 您可以选择使用一到四个季度（3-12个月）的数据进行培训。

>[!NOTE]
>
>较短的训练窗口期对最近趋势比较敏感，而较长的训练窗口期则创建更稳定的模型，并且对最近趋势不太敏感。

![训练时段](./images/user-guide/training_window.png)

选择培训窗口后，选择右上角的&#x200B;**[!UICONTROL 完成]**。 留出一些时间来处理数据。 完成后，会显示弹出对话框，确认实例设置已完成。 选择&#x200B;**[!UICONTROL 确定]**&#x200B;以重定向到&#x200B;**[!UICONTROL 服务实例]**&#x200B;页面，您可以在其中查看您的服务实例。

![设置完成](./images/user-guide/instance_setup_complete.png)

## 后续步骤

通过阅读本教程，您已在归因人工智能中成功创建了服务实例。 实例完成评分（最长允许24小时）后，您就可以[发现Attribution AI见解](./discover-insights.md)。 此外，如果您希望下载评分结果，请访问[下载得分](./download-scores.md)文档。

## 其他资源

以下视频概述了在归因人工智能中创建新实例的端到端工作流。

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
