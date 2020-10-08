---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;segmentation service;user guide;ui guide;segmentation ui guide;segment builder;Segment builder;
solution: Experience Platform
title: 分段服务区段生成器用户指南
topic: ui guide
description: '区段生成器提供丰富的工作区，允许您与用户档案数据元素交互。 工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。 '
translation-type: tm+mt
source-git-commit: beacce03136e1620ff57fb549f335d2199bb6001
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 0%

---


# [!DNL Segment Builder] 用户指南

[!DNL Segment Builder] 提供丰富的工作区，允许您与数据元素 [!DNL Profile] 交互。 工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。

![](../images/ui/segment-builder/segment-builder.png)

## 段定义构建块

段定义的基本构件是属性和事件。 此外，现有受众中包含的属性和事件也可用作新定义的组件。

您可以在工作区左侧的 **[!UICONTROL “字段]** ”(Fields)部分查看这些构 [!DNL Segment Builder] 件。 **[!UICONTROL 字段]** 包含每个主要构造块的选项卡：“[!UICONTROL 属性]”、“[!UICONTROL 事件]”和“[!UICONTROL 受众]”。

![](../images/ui/segment-builder/segment-fields.png)

### 属性

“属 **[!UICONTROL 性]** ”选项卡允许您浏览 [!DNL Profile] 属于该类的 [!DNL XDM Individual Profile] 属性。 每个文件夹都可以展开以显示其他属性，其中每个属性都是一个拼贴，可拖动到工作区中心的规则构建器画布上。 本指 [南后面将更](#rule-builder-canvas) 详细地讨论规则构建器画布。

![](../images/ui/segment-builder/attributes.png)

### 事件

事件 **[!UICONTROL 选项卡]** ，允许您根据使用数据元素进行的事件或操作创建 [!DNL XDM ExperienceEvent] 受众。 您还可以在事件类型选 **[!UICONTROL 项卡]** (事件选项卡是常用事件的集合)上查找，以便您更快地创建区段。

除了能够浏览元素外， [!DNL ExperienceEvent] 您还可以搜索事件类型。 事件类型使用与之相同的编 [!DNL ExperienceEvents]码逻辑，无需您在类中搜索 [!DNL XDM ExperienceEvent] 以寻找正确的事件。 例如，使用搜索栏搜索“购物车”会返回事件类型“[!UICONTROL AddCart]”和“[!UICONTROL RemoveCart]”，这两个操作是构建区段定义时最常用的操作。

可以通过在搜索栏中键入组件名称来搜索任何类型的组件，该名称使 [用Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 输入整个单词后，搜索结果开始填充。 例如，要根据XDM字段构建规则，请 `ExperienceEvent.commerce.productViews`在搜索字段中开始键入“产品视图”。 键入“product”一词后，搜索结果开始显示。 每个结果都包括它所属的对象层次结构。

>[!NOTE]
>
>您的组织定义的自定义模式字段可能需要24小时才能显示，并可用于构建规则。

然后，您可以轻松地将 [!DNL ExperienceEvents] 和“[!UICONTROL 事件类型]”拖放到区段定义中。

![](../images/ui/segment-builder/events-eventTypes.png)

默认情况下，只显示模式存储中已填充的数据字段。 这包括“[!UICONTROL 事件类型]”。 如果“事件类型”列表不可见，或者您只能“任何[!UICONTROL ”作为“事件类型]****************”显示，则选择模式Fields下一个，然后选择Drom可用的，选择可用。 再次选 **择齿轮** 图标以返回到“字段 **[!UICONTROL ”选项卡，您现在应能视图多个“]** 事件类型”和模式字段，无论它们是否包含数据。

![](../images/ui/segment-builder/show-populated.png)

### 受众

受众 **[!UICONTROL 标签]** 列表从外部源(如Adobe Audience Manager)导入的所有受众，以及在中创建的受众 [!DNL Experience Platform]。

在“ **[!UICONTROL 受众]** ”选项卡上，您可以将所有可用源作为一组文件夹进行查看。 当您选择文件夹时，可以看到可用的子文件夹和受众。 此外，您还可以选择文件夹图标（如最右侧图像所示）以视图文件夹结构（复选标记表示您当前所在的文件夹），并通过选择树中某个文件夹的名称轻松导航回文件夹。

您可以将鼠标悬ⓘ停在受众旁边以视图受众的相关信息，包括其ID、描述和文件夹层次结构，以便找到受众。

![](../images/ui/segment-builder/audience-folder-structure.png)

您还可以使用搜索栏搜索受众，该搜索栏利 [用Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 在“ **[!UICONTROL 受众]** ”选项卡上，选择顶级文件夹会显示搜索栏，允许您在该文件夹中进行搜索。 只有输入完整单词后，搜索结果才会开始填充。 例如，要查找名为的受众, `Online Shoppers`请在搜索栏中开始键入“在线”。 在完整键入“在线”一词后，将显示包含“在线”一词的搜索结果。

## 规则构建器画布 {#rule-builder-canvas}

区段定义是用于描述目标受众的关键特征或行为的规则集合。 这些规则是使用位于中心的规则生成器画布创建的 [!DNL Segment Builder]。

要向区段定义添加新规则，请从“字段”选项卡中拖 **[!UICONTROL 动拼贴]** ，并将其放到规则构建器画布上。 然后，将根据要添加的数据类型向您显示上下文特定选项。 可用数据类型包括：字符串、日 [!DNL ExperienceEvents]期、“[!UICONTROL 事件类型]”和受众。

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Adobe Experience Platform的最新变化更新了事件和逻辑运 `OR` 算符 `AND` 的使用情况。 这些更新不会影响现有区段。 但是，对现有区段和新区段创建的所有后续更新都将受到这些更改的影响。 请阅读时 [间常量更新](./segment-refactoring.md) ，了解详细信息。

### 添加受众

您可以将受众从受众选项卡拖 **[!UICONTROL 放到]** 规则构建器画布上，以在新的区段定义中引用受众成员身份。 这允许您将受众成员资格作为属性加入或排除到新区段规则中。

对 [!DNL Platform] 于使用创 [!DNL Segment Builder]建的受众，您可以选择将受众转换为在该受众的区段定义中使用的规则集。 此转换会生成规则逻辑的副本，然后可以修改该副本，而不会影响原始段定义。 在将区段定义转换为规则逻辑之前，请确保已保存对区段定义的任何最近更改。

>[!NOTE]
>
>从外部源添加受众时，只引用受众成员身份。 无法将受众转换为规则，因此在新区段定义中无法修改用于创建原始受众的规则。

![](../images/ui/segment-builder/add-audience-to-segment.png)

如果在将受众转换为规则时发生任何冲 [!DNL Segment Builder] 突，将尝试保留现有选项以尽其所能。

### 代码视图

或者，也可以视图在中创建的规则的基于代码的版本 [!DNL Segment Builder]。 在规则构建器画布中创建规则后，您可以选择“代 **[!UICONTROL 码视图]** ”，将区段视为PQL。

![](../images/ui/segment-builder/code-view.png)

代码视图提供一个按钮，允许您复制段值以在API调用中使用。 要获取区段的最新版本，请确保您已将最新更改保存到区段。

![](../images/ui/segment-builder/copy-code.png)

## 容器

区段规则将按其列出的顺序进行评估。 容器允许通过使用嵌套查询来控制执行顺序。

在将至少一个拼贴添加到规则构建器画布后，您可以开始添加容器。 要创建新容器，请选择拼贴右上角的省略号(...)，然后选择添加 **[!UICONTROL 容器]**。

![](../images/ui/segment-builder/add-container.png)

新容器显示为第一个容器的子项，但您可以通过拖动和移动容器来调整层次。 容器的默认行为是“包[!UICONTROL 含]”提供的属性、事件或受众。 通过选择拼贴左上角的“包[!UICONTROL 括]”并选择“排除”，可以将规则设置 **[!UICONTROL 为]** “排除”符合用户档案条件[!UICONTROL 的容器]。

也可以通过选择子容器上的“取消换行容器”，提取子容器并内嵌到父容器。 选择子容器右上角的省略号(...)以访问此选项。

![](../images/ui/segment-builder/include-exclude.png)

选择“取消 **[!UICONTROL 换行容器]** ”后，将删除子容器，并随机显示条件。

>[!NOTE]
>
>展开容器时，请注意逻辑继续满足所需的段定义。

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## 合并策略

[!DNL Experience Platform] 使您能够将来自多个来源的数据整合在一起，并将其合并，以便了解每个客户的完整视图。 将数据整合在一起时，合并策略是 [!DNL Platform] 确定数据的优先级以及将哪些数据合并以创建用户档案的规则。

您可以选择与此受众的营销目的匹配的合并策略，或使用由提供的默认合并策略 [!DNL Platform]。 您可以创建组织特有的多个合并策略，包括创建您自己的默认合并策略。 有关为组织创建合并策略的分步说明，请参阅使用UI [处理合并策略的教程](../../profile/ui/merge-policies.md)。

要为段定义选择合并策略，请在“字段”选项卡上选 **[!UICONTROL 择]** “齿轮”图标，然后使用“ **[!UICONTROL 合并策略]** ”下拉菜单选择要使用的合并策略。

![](../images/ui/segment-builder/merge-policy-selector.png)

## 区段属性

构建区段定义时，工 **[!UICONTROL 作区右侧的]** “区段属性”部分会显示所生成区段的估计大小，允许您在构建受众本身之前根据需要调整区段定义。

在“ **[!UICONTROL 区段属性]** ”部分，您还可以指定有关区段定义的重要信息，包括其名称和说明。 区段定义名称用于在组织定义的区段中识别您的区段，因此应具有描述性、简明性和唯一性。

在继续构建区段定义时，您可以通过选择视图预览来视图受众的分 **[!UICONTROL 页用户档案]**。

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>受众估计是使用当天样本数据的样本大小生成的。 如果您的用户档案存储中少于100万个实体，则使用完整的数据集；100万至2000万个单位使用100万个单位；超过2000万个单位，占全部单位的5%。 有关生成区段估计的更多信息，请参 [阅区段创建教程](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) 的估计生成部分。

## 后续步骤和其他资源 {#next-steps}

区段生成器提供丰富的工作流，允许您从数据中分离可销售的受众 [!DNL Real-time Customer Profile] 信息。 阅读本指南后，您现在应能够：

- 使用属性、事件和现有受众的组合作为构件块创建区段定义。
- 使用规则构建器画布和容器控制段规则的执行顺序。
- 视图对未来受众的估计，使您能够根据需要调整细分定义。
- 为计划分段启用所有段定义。
- 为流分段启用指定的段定义。

要了解更多相 [!DNL Segmentation Service]关信息，请继续阅读文档并通过观看以下视频补充您的学习内容。 要进一步了解UI的其 [!DNL Segmentation Service] 他部分，请阅 [[!DNL Segmentation Service] 读用户指南](./overview.md)

>[!WARNING]
>
> 以 [!DNL Platform] 下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上面的文档。

**创建区段：**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**创建动态区段：**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)