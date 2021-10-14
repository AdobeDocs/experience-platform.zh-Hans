---
keywords: Experience Platform；用户指南；归因ai；热门主题；区域
feature: Attribution AI
title: Attribution AIUI指南
topic-legacy: User guide
description: 本文档是与Intelligent Services用户界面中的Attribution AI交互的指南。
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 1%

---

# Attribution AIUI指南

Attribution AI，作为智能服务的一部分，是一种多渠道的算法归因服务，用于计算客户交互对特定结果的影响和增量影响。 利用 Attribution AI，营销人员可以通过了解客户旅程各个阶段每个客户互动的影响来衡量和优化营销和广告支出。

本文档是与Intelligent Services用户界面中的Attribution AI交互的指南。

## 创建实例

在[!DNL Adobe Experience Platform] UI的左侧导航中，单击&#x200B;**[!UICONTROL Services]**。 出现&#x200B;**[!UICONTROL Services]**&#x200B;浏览器，并显示可用的Adobe智能服务。 在Attribution AI容器中，单击&#x200B;**[!UICONTROL 打开]**。

![访问您的实例](./images/user-guide/open_Attribution_ai.png)

此时将显示Attribution AI服务页面。 本页列出了Attribution AI的服务实例并显示了有关这些实例的信息，包括实例名称、转化事件、实例运行频率以及上次更新的状态。

您可以在&#x200B;**[!UICONTROL 创建实例]**&#x200B;容器右下方找到打分的&#x200B;]**转化事件总数量度。**[!UICONTROL &#x200B;此量度跟踪当前日历年中由Attribution AI评分的转化事件总数，包括所有沙盒环境和任何已删除的服务实例。

![](./images/user-guide/total_conversions.png)

可以使用UI右侧的控件来编辑、克隆和删除服务实例。 要显示这些控件，请从现有的&#x200B;**[!UICONTROL Service实例]**&#x200B;中选择一个实例。 控件包含以下信息：

- **[!UICONTROL 编辑]**:选择 **** 编辑允许您修改现有服务实例。您可以编辑实例的名称、描述、状态和评分频率。
- **[!UICONTROL 克隆]**:选择 **** 克隆选定的服务实例。然后，您可以修改工作流以进行细微调整，并将其重命名为新实例。
- **[!UICONTROL 删除]**:您可以删除包含任何历史运行的服务实例。
- **[!UICONTROL 数据源]**:指向此实例所使用的数据集的链接。
- **[!UICONTROL 上次运行详细信息]**:仅当运行失败时，才会显示该设置。此处显示了有关运行失败原因（如错误代码）的信息。

![](./images/user-guide/side_panel.png)

- **[!UICONTROL 转化事件]**:为此实例配置的转化事件的快速概述。
- **[!UICONTROL 回顾窗口]**:您定义的时间范围，用于指示转化事件接触点之前包含的天数。
- **[!UICONTROL 接触点]**:创建此实例时定义的所有接触点的列表。

![](./images/user-guide/side_panel_2.png)

选择&#x200B;**[!UICONTROL 创建实例]**&#x200B;以开始。

![创建实例](./images/user-guide/landing_page.png)

接下来，将显示Attribution AI的设置页面，您可以在该页面中提供基本信息，并为实例指定数据集。

![设置页面](./images/user-guide/setup_attribution.png)

### 命名实例

在&#x200B;**[!UICONTROL 基本信息]**&#x200B;下，为服务实例提供名称和可选描述。

![命名实例](./images/user-guide/naming_instance.png)

### 选择数据集

填写基本信息后，单击标有&#x200B;**选择数据集**&#x200B;的下拉列表以选择您的数据集。 数据集用于培训模型并对其生成的后续数据进行评分。 从下拉选择器中选择Attribution AI集时，只会列出与数据兼容并符合体验数据模型(XDM)架构的数据集。 选择数据集后，单击右上角的&#x200B;**Next**&#x200B;以继续进入定义事件页面。

>[!TIP]
>
>Adobe Analytics数据集通过Analytics源连接器受支持。

![设置页面](./images/user-guide/dataset_selector.png)

## 定义事件

有三种不同类型的输入数据用于定义事件：

- **转化事件：** 可确定营销活动（如电子商务订单、店内购买和网站访问）影响的业务目标。
- **回顾窗口：** 提供一个时间范围，指示应包含转化事件接触点之前的天数。
- **接触点：** 收件人、个人或Cookie级别的营销事件，用于评估转化的数字或基于收入的影响。

### 定义转化事件 {#define-conversion-events}

要定义转化事件，您需要为事件指定名称，并通过单击&#x200B;**Enter Field Name**&#x200B;下拉菜单选择事件类型。

![是下拉列表](./images/user-guide/conversion_event_2.png)

选择事件后，其右侧会显示一个新的下拉菜单。 第二个下拉列表用于通过使用操作为事件提供更多上下文。 对于此转化事件，使用默认操作&#x200B;*exists*。

>[!NOTE]
>
>在定义事件时， *转化名称*&#x200B;下的字符串会更新。

![无下拉列表](./images/user-guide/conversion_event_1.png)

使用&#x200B;**[!UICONTROL Add event]**&#x200B;和&#x200B;**[!UICONTROL Add Group]**&#x200B;按钮可进一步定义您的转化。 根据您定义的转化，您可能需要使用&#x200B;**[!UICONTROL Add event]**&#x200B;和&#x200B;**[!UICONTROL Add group]**&#x200B;按钮来提供更多上下文。

![添加事件](./images/user-guide/add_event.png)

单击&#x200B;**[!UICONTROL Add event]**&#x200B;会创建其他字段，这些字段可以使用与上面所述相同的方法填写。 这样做会在转换名称下方的字符串定义中添加AND语句。 单击&#x200B;**x**&#x200B;可删除已添加的事件。

![添加事件菜单](./images/user-guide/add_event_result.png)

单击&#x200B;**[!UICONTROL 添加组]**&#x200B;可选择创建与原始字段不同的其他字段。 添加组后，将显示蓝色的&#x200B;*And*&#x200B;按钮。 单击&#x200B;**And**&#x200B;会提供一个选项，可将参数更改为包含“Or”。 “或”用于定义多个成功的转化路径。 “和”扩展了转化路径以包含其他条件。

![使用或](./images/user-guide/and_or.png)

如果需要多次转化，请单击&#x200B;**添加转化**&#x200B;以创建新的转化卡。 您可以重复上述过程以定义多个转化。

![添加转化](./images/user-guide/add_conversion.png)

### 定义回顾窗口 {#lookback-window}

定义完转化后，需要确认回顾窗口。 使用箭头键或单击默认值(56)，指定您希望在转化事件发生前的多少天加入接触点。 接触点在下一步中定义。

![回顾](./images/user-guide/lookback_window.png)

### 定义接触点

定义接触点的工作流程与定义转化](#define-conversion-events)类似。 [最初，您需要命名接触点，并从&#x200B;*输入字段名称*&#x200B;下拉菜单中选择一个接触点值。 选择后，将显示运算符下拉列表，其默认值为“存在”。 单击下拉菜单以显示运算符列表。

![运算符](./images/user-guide/operators.png)

为此接触点的目的，请选择&#x200B;**等于**。

![步骤1](./images/user-guide/touchpoint_step1.png)

选择接触点的运算符后，将提供&#x200B;*输入字段值*。 根据您之前选择的运算符和接触点值填充&#x200B;*输入字段值*&#x200B;的下拉值。 如果某个值未在下拉菜单中填充，则您可以在中手动键入该值。 单击下拉菜单并选择&#x200B;**CLICK**。

>[!NOTE]
>
>运算符“存在”和“不存在”没有与其关联的字段值。

![接触点下拉列表](./images/user-guide/touchpoint_dropdown.png)

使用&#x200B;*Add event*&#x200B;和&#x200B;*Add Group*&#x200B;按钮可进一步定义您的接触点。 由于接触点周围是复杂的，因此在单个接触点中有多个事件和组并不罕见。

单击&#x200B;**Add event**&#x200B;后，可添加其他字段。 单击&#x200B;**x**&#x200B;可删除已添加的事件。

![添加事件](./images/user-guide/touchpoint_add_event.png)

单击&#x200B;**添加组**&#x200B;可选择创建与原始字段不同的其他字段。 添加组后，将显示蓝色的&#x200B;*And*&#x200B;按钮。 单击&#x200B;**And**&#x200B;以更改参数，新参数“Or”用于定义多个成功路径。 此特定接触点仅具有一个成功路径，因此不需要“或”。

![接触点概述](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>使用&#x200B;*接触点名称*&#x200B;下的字符串可快速查看您的接触点。 请注意，字符串与接触点的名称匹配。

![](./images/user-guide/touchpoint_string.png)

您可以通过单击&#x200B;**添加接触点**&#x200B;并重复上述过程来添加其他接触点。

![添加接触点](./images/user-guide/add_touchpoint.png)

定义完所有必要的接触点后，向上滚动并单击右上角的&#x200B;**Next**&#x200B;以继续执行最后一步。

![完成定义](./images/user-guide/define_event_next.png)

## 高级培训和评分设置

Attribution AI中的最后一页是用于设置培训和评分的&#x200B;**[!UICONTROL Advanced]**&#x200B;页面。

![新页面高级](./images/user-guide/advanced_settings.png)

### 安排培训

使用&#x200B;*计划*，您可以选择要进行评分的一周中的日期和时间。

单击&#x200B;*评分频度*&#x200B;下的下拉菜单，在每日、每周和每月评分之间进行选择。 接下来，选择您希望在一周中的哪几天进行评分。 可以选择多天。 再次单击一天可取消选择它。

![安排培训](./images/user-guide/schedule_training.png)

要更改希望打分的一天时间，请单击时钟图标。 在显示的新叠加图中，输入您希望进行评分的时间。 单击叠加外部以将其关闭。

>[!NOTE]
>
>完成每个评分过程可能最多需要24小时。

![时钟图标](./images/user-guide/time_of_day.png)

### 其他分数数据集列（可选）

默认情况下，会为标准架构中的每个服务实例创建一个分数数据集。 您可以选择根据转化事件和接触点配置向得分数据集输出添加其他列。 首先，从输入数据集中选择列，然后拖放列以更改顺序，方法是将鼠标左键按在汉堡包图标上。

![得分数据集列添加](./images/user-guide/Add-score-dataset.png)

### 基于区域的建模（可选） {#region-based-modeling-optional}

客户的行为可能因国家/地区和地理区域而有显着差异。 对于全球企业，使用基于国家/地区或基于区域的模型可以提高归因准确性。 添加的每个区域都使用该区域的数据创建一个新模型。

要定义新区域，请首先单击&#x200B;**[!UICONTROL Add region]**。 在显示的容器中，提供区域的名称。 从&#x200B;**[!UICONTROL 输入字段名称]**&#x200B;下拉列表中只填充一个值(&quot;placeContext.geo.countryCode&quot;)。 选择此值。

![选择区域](./images/user-guide/select_region_att.png)

接下来，选择一个运算符。

![区域运算符](./images/user-guide/region_operators.png)

最后，在&#x200B;**[!UICONTROL Enter Field Value]**&#x200B;下拉列表中键入国家/地区代码。

>[!NOTE]
>
>国家/地区代码有两个字符长。 可在此处[ISO 3166-1 alpha-2](https://datahub.io/core/country-list)找到完整列表。

![地区](./images/user-guide/region-based.png)

### 培训窗口 {#training-window}

为确保您获得尽可能准确的模型，必须使用代表您业务的历史数据来培训您的模型。 默认情况下，模型会使用2个季度（6个月）的转化事件数据进行培训。 选择下拉菜单以更改默认设置。 您可以选择使用四分之一到四的数据（3-12个月）进行培训。

>[!NOTE]
>
>较短的培训窗口对最近的趋势更敏感，而较长的培训窗口则创建更稳健的模型，对最近的趋势也不那么敏感。

![培训窗口](./images/user-guide/training_window.png)

选择培训窗口后，单击右上角的&#x200B;**[!UICONTROL 完成]**。 允许一些时间处理数据。 完成后，会显示一个弹出对话框，确认实例设置已完成。 单击&#x200B;**[!UICONTROL Ok]**&#x200B;以重定向到&#x200B;**[!UICONTROL Service instances]**&#x200B;页面，您可以在该页面中看到服务实例。

![设置完成](./images/user-guide/instance_setup_complete.png)

## 后续步骤

在本教程之后，您已成功地在Attribution AI中创建了服务实例。 实例完成评分（最多24小时）后，您便可以[发现Attribution AI分析](./discover-insights.md)。 此外，如果您希望下载评分结果，请访问[下载评分](./download-scores.md)文档。

## 其他资源

以下视频概述了用于在Attribution AI中创建新实例的端到端工作流。

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
