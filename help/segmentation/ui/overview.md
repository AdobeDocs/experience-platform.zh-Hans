---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 区段生成器UI指南
topic: ui guide
translation-type: tm+mt
source-git-commit: 1c9b50f8f71e917b86c34b061df7e2da6fe475a2
workflow-type: tm+mt
source-wordcount: '2766'
ht-degree: 0%

---


# [!UICONTROL 区段生成器] 用户指南

[!DNL Adobe Experience Platform Segmentation Service] 提供RESTful API和用户界面，用于从数据创建区段 [!DNL Real-time Customer Profile] 定义。

## 入门指南

使用细分定义需要了解与细分相关 [!DNL Experience Platform] 的各种服务。 在阅读本用户指南之前，请查阅以下服务的文档：

- [!DNL Segmentation Service](../home.md): 分段服务允许您将与个人( [!DNL Experience Platform] 如客户、潜在客户、用户或组织)相关的存储在其中的数据划分为具有相似特征并将响应类似营销策略的较小组。
- [!DNL Real-time Customer Profile](../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
- [!DNL Identity Service](../../identity-service/home.md): 通过将 [!DNL Real-time Customer Profile] 来自被引入平台的不同数据源的身份连接到平台，可实现此目的。
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): 组织客户体验数 [!DNL Platform] 据的标准化框架。

了解本文档使用的两个关键术语并了解它们之间的区别也很重要：
- **细分定义**: 用于描述目标受众的关键特性或行为的规则集。
- **受众**: 生成的一组符合区段定义条件的用户档案。

## 访问区段定义

要开始使用中的区段定义， [!DNL Adobe Experience Platform]请单击左 **[!UICONTROL 侧导航]** 中的区段。 要查看您的组织的所有区段定义，请单击“浏览 *[!UICONTROL ”选]* 项卡。 此视图列表有关区段定义的信息，包括评估方法、创建日期和上次修改日期。

评估方法可以是流式的，也可以是批量的。 当数据进入系统时，会持续评估流段。 批区段根据一组计划进行评估。

批段会显示附加信息，显示该批的上次评估日期和下一个评估日期。

单 **[!UICONTROL 击右上角]** 的创建区段可打开区段生成器工作区，您可以在此开始创建区段定义。

![](../images/segment-builder/segment-browse.png)

## [!UICONTROL 区段生成器工作区] (Segment Builder)

[!UICONTROL 区段生成器] 提供丰富的工作区，允许您与数据元素 [!DNL Profile] 交互。 工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。

![](../images/segment-builder/segment-builder.png)

## 段定义构建块

段定义的基本构件是属性 **[!UICONTROL 和]****[!UICONTROL 事件]**。 此外，现有事件中包含的属性 **[!UICONTROL 和受众]** ，也可用作新定义的组件。

您可以在Segment Builder工作区左 *侧的* “字段”部分查 [!UICONTROL 看这些构] 件块。 *[!UICONTROL 字段]* 包含每个主要构造块的选项卡： **[!UICONTROL 属性]**、 **[!UICONTROL 事件]**&#x200B;和 **[!UICONTROL 受众]**。

![](../images/segment-builder/segment-fields.png)

### 属性

“属 **[!UICONTROL 性]** ”选项卡允许您浏览 [!DNL Profile] 属于该类的 [!DNL XDM Individual Profile] 属性。 每个文件夹都可以展开以显示其他属性，其中每个属性都是一个拼贴，可拖动到工作区中心的规则构建器画布上。 本指 [南后面将更](#rule-builder-canvas) 详细地讨论规则构建器画布。

![](../images/segment-builder/attributes.png)

### 事件

通过 **[!UICONTROL 事件]** 选项卡，您可以根据使用XDM ExperienceEvent数据元素进行的事件或操作创建受众。 您还可以在事件类型选 **[!UICONTROL 项卡]** (事件选项卡是常用事件的集合)上查找，以便您更快地创建区段。

除了能够浏览元素外， [!DNL ExperienceEvent] 您还可以搜索事件类型。 事件类型使用与之相同的编 [!DNL ExperienceEvents]码逻辑，无需您在类中搜索 [!DNL XDM ExperienceEvent] 以寻找正确的事件。 例如，使用搜索栏搜索“购物车”会返回事件类型“[!UICONTROL AddCart]”和“[!UICONTROL RemoveCart]”，这两个操作是构建区段定义时最常用的操作。

可以通过在搜索栏中键入组件名称来搜索任何类型的组件，该名称使 [用Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 输入整个单词后，搜索结果开始填充。 例如，要根据XDM字段构建规则，请 `ExperienceEvent.commerce.productViews`在搜索字段中开始键入“产品视图”。 键入“product”一词后，搜索结果开始显示。 每个结果都包括它所属的对象层次结构。

>[!NOTE]
>
>您的组织定义的自定义模式字段可能需要24小时才能显示，并可用于构建规则。

然后，您可以轻松地将 [!DNL ExperienceEvents] 事件类型 [!UICONTROL 拖放] 到区段定义中。

![](../images/segment-builder/events-eventTypes.png)

默认情况下，只显示模式存储中已填充的数据字段。 这包括 [!UICONTROL 事件类型]。 如果事件类型 [!UICONTROL 列表不可见] ，或者您只能选择“Any[!UICONTROL ”作为事件类型，请单击]Fields旁边的“Any ********”，然后选择Oracle Caliable Digrast可用的模式下的完全XDM。 再次单击齿轮图标以返回到“ *[!UICONTROL 字段]* ”选项卡，您现在应能视图多个 [!UICONTROL 事件类型和] 模式字段，无论它们是否包含数据。

![](../images/segment-builder/show-populated.png)

### 受众

受众 **[!UICONTROL 标签]** 列表从外部源导入的所有受众，如Adobe Audience Manager，以及在中创建的受众 [!DNL Experience Platform]。

在“ [!UICONTROL 受众] ”选项卡上，您可以将所有可用源作为一组文件夹进行查看。 单击到这些文件夹时，可以看到可用的子文件夹和受众。 此外，您还可以单击文件夹图标（如最右侧图像所示）以视图文件夹结构（复选标记表示您当前所在的文件夹），并通过单击树中某个文件夹的名称轻松导航回文件夹。

您可以将鼠标悬ⓘ停在受众旁边以视图受众的相关信息，包括其ID、描述和文件夹层次结构，以便找到受众。

![](../images/segment-builder/audience-folder-structure.png)

您还可以使用搜 [!UICONTROL 索栏] (利用Lucene的搜 [索语法)搜索受众](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 在“ *[!UICONTROL 受众]* ”选项卡上，选择顶级文件夹会显示搜索栏，允许您在该文件夹中进行搜索。 只有输入完整单词后，搜索结果才会开始填充。 例如，要查找名为 [!UICONTROL 的受众] , `Online Shoppers`请在搜索栏中开始键入“在线”。 在完整键入“在线”一词后，将显示包含“在线”一词的搜索结果。

## 规则构建器画布 {#rule-builder-canvas}

区段定义是用于描述目标受众的关键特征或行为的规则集合。 这些规则是使用位于 *[!UICONTROL 区段生成器]*（位于区段生成器）中 [!UICONTROL 心的规则生成器画布创建的]。

要向区段定义添加新规则，请从“字段”选项卡中拖 *[!UICONTROL 动拼贴]* ，并将其放到规则构建器画布上。 然后，将根据要添加的数据类型向您显示上下文特定选项。 可用数据类型包括： 字符串、日期 [!DNL ExperienceEvents]、 [!UICONTROL 事件类型]和 [!UICONTROL 受众]。

![](../images/segment-builder/rule-builder-canvas.png)

### 添加受众

您可以将受众从受众选项卡拖 *[!UICONTROL 放到]* 规则构建器画布上，以在新的区段定义中引用受众成员身份。 这允许您将受众成员资格作为属性加入或排除到新区段规则中。

对于 [!DNL Platform] 使用区 [!UICONTROL 段生成器创建的受众]，您可以选择将受众转换为在该受众的区段定义中使用的规则集。 此转换会生成规则逻辑的副本，然后可以修改该副本，而不会影响原始段定义。 在将区段定义转换为规则逻辑之前，请确保已保存对区段定义的任何最近更改。

>[!NOTE]
>
>从外部源添加受众时，只引用受众成员身份。 无法将受众转换为规则，因此在新区段定义中无法修改用于创建原始受众的规则。

![](../images/segment-builder/add-audience-to-segment.png)

如果将受众转换为规则时发生 [!UICONTROL 任何冲突] ,Segment Builder将尝试保留现有选项，以尽其所能。

### 代码视图

或者，也可以视图在区段生成器中创建的规则的基于代 [!UICONTROL 码的版本]。 在规则构建器画布中创建规则后，您可以选择“代 **[!UICONTROL 码视图]** ”，将区段视为PQL。

![](../images/segment-builder/code-view.png)

代码视图提供一个按钮，允许您复制段值以在API调用中使用。 要获取区段的最新版本，请确保您已将最新更改保存到区段。

![](../images/segment-builder/copy-code.png)

## 容器

区段规则将按其列出的顺序进行评估。 容器允许通过使用嵌套查询来控制执行顺序。

在将至少一个拼贴添加到规则构建器画布后，您可以开始添加容器。 要创建新容器，请单击拼贴右上角的省略号(...)，然后单击添加 **[!UICONTROL 容器]**。

![](../images/segment-builder/add-container.png)

新容器显示为第一个容器的子项，但您可以通过拖动和移动容器来调整层次。 容器的默认行为是“包[!UICONTROL 含]”提供的属性、事件或受众。 您可以通过单击拼贴左上角的“包[!UICONTROL 括]”并选择“排除”，将规则设置为符合 **[!UICONTROL 容器条件的“]** 排除”。

也可以通过单击子容器上的“取消换行容器”，提取子容器并内嵌到父容器。 单击子容器右上角的省略号(...)以访问此选项。

![](../images/segment-builder/include-exclude.png)

单击“取 **[!UICONTROL 消容器]** ”后，将删除子容器并内嵌条件。

>[!NOTE]
>
>展开容器时，请注意逻辑继续满足所需的段定义。

![](../images/segment-builder/unwrapped-container-inline.png)

## 合并策略

[!DNL Experience Platform] 使您能够将来自多个来源的数据整合在一起，并将其合并，以便了解每个客户的完整视图。 将数据整合在一起时，合并策略是 [!DNL Platform] 确定数据的优先级以及将哪些数据合并以创建用户档案的规则。

您可以选择与此受众的营销目的匹配的合并策略，或使用由提供的默认合并策略 [!DNL Platform]。 您可以创建组织特有的多个合并策略，包括创建您自己的默认合并策略。 有关为组织创建合并策略的分步说明，请参阅使用UI [处理合并策略的教程](../../profile/ui/merge-policies.md)。

要为段定义选择合并策略，请单击“字段”选项卡上 *[!UICONTROL 的齿轮]* 图标，然后使用“合并策 *[!UICONTROL 略]”下拉菜单&#x200B;*，以选择要使用的合并策略。

![](../images/segment-builder/merge-policy-selector.png)

## 区段属性

构建区段定义时，工 *[!UICONTROL 作区右侧的]* “区段属性”部分会显示所生成区段的估计大小，允许您在构建受众本身之前根据需要调整区段定义。

在“ *[!UICONTROL 区段属性]* ”部分，您还可以指定有关区段定义的重要信息，包括 *[!UICONTROL 名称]**[!UICONTROL 和说明]*。 区段定义名称用于在组织定义的区段中识别您的区段，因此应具有描述性、简明性和唯一性。

在继续构建区段定义时，您可以通过选择视图预览来视图受众的分 **[!UICONTROL 页用户档案]**。

![](../images/segment-builder/segment-properties.png)

>[!NOTE]
>
>受众估计是使用当天样本数据的样本大小生成的。 如果您的用户档案存储中少于100万个实体，则使用完整的数据集； 100万至2000万个单位使用100万个单位； 超过2000万个单位，占全部单位的5%。 有关生成区段估计的更多信息，请参 [阅区段创建教程](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 的估计生成部分。

## 启用计划分段 {#enable-scheduled-segmentation}

在创建区段定义后，您便可以通过按需或计划（连续）评估来评估这些定义。 评估是指通 [!DNL Real-time Customer Profile] 过细分定义移动数据，以产生相应的受众。 创建受众后，会保存并存储这些数据，以便使用API导出 [!DNL Experience Platform] 它们。

点播评估包括根据需要使用API执行评估和构建受众，而计划评估（也称为“计划分段”）允许您创建循环计划以在特定时间（最多每天一次）评估区段定义。

可以使用UI或API为计划评估启用区段定义。 在UI中，返回至“区段” *[!UICONTROL 中的]* “浏 **[!UICONTROL 览”选]** 项卡 **[!UICONTROL ，然后]**&#x200B;打开“评估所有区段”。 这将导致所有区段都根据您的组织设置的计划进行评估。

>[!NOTE]
>
>对于最多五(5)个合并策略的沙箱，可启用计划评估 [!DNL XDM Individual Profile]。 如果您的组织在单个沙箱环境内 [!DNL XDM Individual Profile] 有五个以上的合并策略，您将无法使用计划的评估。

计划当前只能使用API创建。 有关使用API创建、编辑和使用计划的详细步骤，请按照教程来评估和访问区段结果，特别是使用API进 [行计划评估的部分](../tutorials/evaluate-a-segment.md#scheduled-evaluation)。

![](../images/segment-builder/scheduled-segmentation.png)

## 流细分 {#streaming-segmentation}

>[!NOTE]
>
>为了让流式分段正常工作，客户需要为组织启用计划分段。 有关启用计划分段的详细信息，请参 [阅本用户指南的上一节](#enable-scheduled-segmentation)。

如果查询符合以下任何条件，则将使用流分段自动评估该数据：

| 查询类型 | 详细信息 | 示例 |
| ---------- | ------- | ------- |
| 传入点击 | 任何区段定义，指没有时间限制的单个传入事件。 | ![](../images/segment-builder/incoming-hit.png) |
| 相对时间窗口内的传入点击 | 指过去七天内单个传入事件 **的任何区段定义**。 | ![](../images/segment-builder/relative-hit-success.png) |
| 指用户档案 | 引用单个传入事件（无时间限制）和一个或多个用户档案属性的任何区段定义。 | ![](../images/segment-builder/profile-hit.png) |
| 指相对时间窗口内用户档案的传入点击 | 在过去七天内引用单个传入事件和一个或多个属性 **的任何用户档案定义**。 | ![](../images/segment-builder/profile-relative-success.png) |
| 引用事件的多个用户档案 | 任何引用过去24小时内的多个事件 **并且(可选** )具有一个或多个用户档案属性的定义。 | ![](../images/segment-builder/event-history-success.png) |

下节列表段定义示例，这些示例将 **不启** 用流分段功能。

| 查询类型 | 详细信息 |
| ---------- | ------- | 
| 相对时间窗口内的传入点击 | 如果区段定义引用的事件不 **是** 在最 **近七天的时间段内**。 例如，在过去 **两周内**。 | ![](../images/segment-builder/relative-hit-failure.png) |
| 指相对窗口中的用户档案的传入点击 | 以下选项将不 **支持** 流分段：<ul><li>未在最 **后** 七 **天内到达的事件**。</li><li>包括区段或特征 [!DNL Adobe Audience Manager (AAM)] 的区段定义。</li></ul> | ![](../images/segment-builder/profile-relative-failure.png) |
| 引用事件的多个用户档案 | 以下选项将不 **支持** 流分段：<ul><li>在过去24 **小时** 内 **不发生的事件**。</li><li>包含Adobe Audience Manager(AAM)区段或特征的区段定义。</li></ul> | ![](../images/segment-builder/event-history-failure.png) |
| 多实体查询 | 整体而言，多实体查询不 **受流** 分段支持。 |  |

此外，执行流分段时还会应用一些准则：

| 查询类型 | 准则 |
| ---------- | -------- |
| 单事件查询 | 回顾窗限于 **七天**。 |
| 查询事件历史 | <ul><li>回顾窗限于一 **天**。</li><li>事件之间必 **须存** 在严格的时间排序条件。</li><li>只允许在事件之间进行简单的时间排序（前后）。</li><li>不能否定 **个别事件** 。 但是，整个查询 **可以** 被否定。</li></ul> |

### 监控流细分

创建支持流式播放的区段后，您可以监视该区段的详细信息。

![](../images/segment-builder/monitoring-streaming-segment.png)

具体而言，将显示有关 *[!UICONTROL 合格受众总大小的]* 详细信息。 如果作业在过去24小时内运行，则除了添加的受众的 **[!UICONTROL 折线图外]** ，还会显示作业的受众总大小。 否则，除 **[!UICONTROL 了显示趋势线]** ，还会显示“估计受众大小”。

![](../images/segment-builder/monitoring-streaming-segment-graph.png)

单击“信息气泡”(information bubble)可找到有关上次区段评估的其他信息。

![](../images/segment-builder/info-bubble.png)

### 流分段视频演示

以下视频旨在支持您对流细分的理解。 它展示了一个客户体验示例，然后快速浏览界面中的主要 [!DNL Platform] 功能。

>[!VIDEO](https://video.tv.adobe.com/v/36184?quality=12&learn=on)

## 违反DULE策略

>[!NOTE]
>
>仅当创建已分配到目标的区段时，DULE策略违规才适用。

创建完区段后，将对区段进行分析，以 [!DNL Data Governance] 确保区段内没有违反策略的情况。 有关DULE和策略违规的详细信息，请参阅数 [据使用标签概述](../../data-governance/labels/overview.md)。

![](../images/segment-builder/segment-dule-policy-violations.png)

## 后续步骤和其他资源 {#next-steps}

区段生成器提供丰富的工作流，允许您从数据中分离可销售的受众 [!DNL Real-time Customer Profile] 信息。 阅读本指南后，您现在应能够：

- 使用属性、事件和现有受众的组合作为构件块创建区段定义。
- 使用规则构建器画布和容器控制段规则的执行顺序。
- 视图对未来受众的估计，使您能够根据需要调整细分定义。
- 为计划分段启用所有段定义。
- 为流分段启用指定的段定义。

要了解更多相 [!DNL Segmentation Service]关信息，请继续阅读文档并通过观看以下视频补充您的学习内容。 有关使用API的分步说明， [!DNL Segmentation Service] 请参 [!DNL Segmentation Service] 阅使用API [创建受众段教程](../tutorials/create-a-segment.md) 。

>[!WARNING]
>
> 以 [!DNL Platform] 下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上面的文档。

**创建区段：**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**创建动态区段：**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)
