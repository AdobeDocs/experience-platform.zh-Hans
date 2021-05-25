---
keywords: Experience Platform；主页；热门主题；分段服务；分段；分段服务；用户指南；UI指南；分段UI指南；区段生成器；区段生成器；
solution: Experience Platform
title: 区段生成器UI指南
topic-legacy: ui guide
description: Adobe Experience Platform UI中的区段生成器提供了一个丰富的工作区，允许您与配置文件数据元素进行交互。 工作区提供了用于构建和编辑规则的直观控件，例如用于表示数据属性的拖放图块。
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 11e8acc3da7f7540421b5c7f3d91658c571fdb6f
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 0%

---

# [!DNL Segment Builder] UI指南

[!DNL Segment Builder] 提供了丰富的工作区，可让您与数据元 [!DNL Profile] 素交互。工作区提供了用于构建和编辑规则的直观控件，例如用于表示数据属性的拖放图块。

![](../images/ui/segment-builder/segment-builder.png)

## 区段定义构建基块

区段定义的基本构建块是属性和事件。 此外，现有受众中包含的属性和事件也可用作新定义的组件。

您可以在[!DNL Segment Builder]工作区左侧的&#x200B;**[!UICONTROL 字段]**&#x200B;部分中看到这些构建基块。 **** 字段包含每个主要构建基块的选项卡：“[!UICONTROL 属性]”、“[!UICONTROL 事件]”和“[!UICONTROL 受众]”。

![](../images/ui/segment-builder/segment-fields.png)

### 属性

**[!UICONTROL 属性]**&#x200B;选项卡允许您浏览属于[!DNL XDM Individual Profile]类的[!DNL Profile]属性。 每个文件夹都可以展开以显示其他属性，其中每个属性都是一个拼贴，可拖动到工作区中心的规则生成器画布上。 本指南后面将详细讨论[规则生成器画布](#rule-builder-canvas)。

![](../images/ui/segment-builder/attributes.png)

### 事件

通过&#x200B;**[!UICONTROL 事件]**&#x200B;选项卡，可以根据使用[!DNL XDM ExperienceEvent]数据元素执行的事件或操作创建受众。 您还可以在&#x200B;**[!UICONTROL 事件]**&#x200B;选项卡上找到事件类型，该选项卡是常用事件的集合，可让您更快地创建区段。

除了能够浏览[!DNL ExperienceEvent]元素之外，您还可以搜索事件类型。 事件类型使用与[!DNL ExperienceEvents]相同的编码逻辑，无需您在[!DNL XDM ExperienceEvent]类中搜索以查找正确的事件。 例如，使用搜索栏搜索“cart”会返回事件类型“[!UICONTROL AddCart]”和“[!UICONTROL RemoveCart]”，这两个事件类型是构建区段定义时最常用的购物车操作。

可以通过在搜索栏中键入任何类型的组件名称来搜索任何类型的组件，该名称使用[Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 在输入整个词时，搜索结果会开始填充。 例如，要构建基于XDM字段`ExperienceEvent.commerce.productViews`的规则，请开始在搜索字段中键入“产品视图”。 键入“product”一词后，搜索结果即开始显示。 每个结果都包括它所属的对象层次结构。

>[!NOTE]
>
>您的组织定义的自定义架构字段可能需要长达24小时才能显示出来，并可用于构建规则。

然后，您可以轻松地将[!DNL ExperienceEvents]和“[!UICONTROL 事件类型]”拖放到区段定义中。

![](../images/ui/segment-builder/events-eventTypes.png)

默认情况下，仅显示数据存储中填充的架构字段。 这包括“[!UICONTROL 事件类型]”。 如果“[!UICONTROL 事件类型]”列表不可见，或者您只能选择“[!UICONTROL Any]”作为“[!UICONTROL 事件类型]”，请选择&#x200B;**[!UICONTROL Fields]**&#x200B;旁边的&#x200B;**齿轮图标**，然后选择&#x200B;**[!UICONTROL 在**[!UICONTROL &#x200B;可用字段&#x200B;]**下显示完整的XDM架构]**。 再次选择&#x200B;**齿轮图标**&#x200B;以返回到&#x200B;**[!UICONTROL 字段]**&#x200B;选项卡，无论它们是否包含数据，您现在都应该能够查看多个“[!UICONTROL 事件类型]”和架构字段。

![](../images/ui/segment-builder/show-populated.png)

### 受众

**[!UICONTROL 受众]**&#x200B;选项卡列出了从外部源(如Adobe Audience Manager)导入的所有受众，以及在[!DNL Experience Platform]中创建的受众。

在&#x200B;**[!UICONTROL 受众]**&#x200B;选项卡上，您可以将所有可用源视为一组文件夹。 选择文件夹时，可以看到可用的子文件夹和受众。 此外，您还可以选择文件夹图标（如最右侧图像中所示）以查看文件夹结构（复选标记表示您当前所在的文件夹），并通过选择树中文件夹的名称轻松导航回文件夹。

您可以将鼠标悬停在受众旁ⓘ的上方，以查看有关受众的信息，包括受众的ID、描述以及用于查找受众的文件夹层次结构。

![](../images/ui/segment-builder/audience-folder-structure.png)

您还可以使用搜索栏搜索受众，该搜索栏利用[Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 在&#x200B;**[!UICONTROL 受众]**&#x200B;选项卡上，选择顶级文件夹会显示搜索栏，允许您在该文件夹内进行搜索。 只有输入了整个词后，搜索结果才会开始填充。 例如，要查找名为`Online Shoppers`的受众，请开始在搜索栏中键入“Online”。 完整键入“在线”一词后，将显示包含“在线”一词的搜索结果。

## 规则生成器画布{#rule-builder-canvas}

区段定义是用于描述目标受众的关键特征或行为的规则集合。 这些规则是使用规则生成器画布创建的，画布位于[!DNL Segment Builder]的中心。

要向区段定义中添加新规则，请从&#x200B;**[!UICONTROL Fields]**&#x200B;选项卡中拖动图块，并将其拖放到规则生成器画布上。 然后，将根据要添加的数据类型向您显示特定于上下文的选项。 可用数据类型包括：字符串、日期、[!DNL ExperienceEvents]、“[!UICONTROL 事件类型]”和受众。

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>对Adobe Experience Platform的最新更改更新了事件之间`OR`和`AND`逻辑运算符的用法。 这些更新不会影响现有区段。 但是，对现有区段和新区段创建的所有后续更新都将受到这些更改的影响。 请阅读[时间常量更新](./segment-refactoring.md)以获取更多信息。

### 添加受众

您可以将&#x200B;**[!UICONTROL 受众]**&#x200B;选项卡中的受众拖放到规则生成器画布上，以在新区段定义中引用受众成员资格。 这允许您在新区段规则中包含或排除受众成员资格作为属性。

对于使用[!DNL Segment Builder]创建的[!DNL Platform]受众，您可以选择将受众转换为该受众区段定义中使用的规则集。 此转换会生成规则逻辑的副本，随后可以修改该副本，而不会影响原始区段定义。 在将区段定义转换为规则逻辑之前，请确保已保存对区段定义所做的任何最近更改。

>[!NOTE]
>
>从外部源添加受众时，仅引用受众成员资格。 您无法将受众转换为规则，因此在新区段定义中无法修改用于创建原始受众的规则。

![](../images/ui/segment-builder/add-audience-to-segment.png)

如果在将受众转换为规则时发生任何冲突，[!DNL Segment Builder]将尝试尽可能保留现有选项。

### 代码视图

或者，您也可以查看在[!DNL Segment Builder]中创建的基于代码的规则版本。 在规则生成器画布中创建规则后，您可以选择&#x200B;**[!UICONTROL 代码视图]**&#x200B;以将区段显示为PQL。

![](../images/ui/segment-builder/code-view.png)

“代码”视图提供了一个按钮，用于复制要在API调用中使用的区段值。 要获取区段的最新版本，请确保已将最新更改保存到该区段。

![](../images/ui/segment-builder/copy-code.png)

### 聚合函数

[!DNL Segment Builder]中的聚合是对一组XDM属性的计算，该组XDM属性的数据类型是数字（双精度或整数）。 区段生成器中支持的四个聚合函数为SUM、AVERAGE、MIN和MAX。

要创建聚合函数，请从左边栏中选择一个事件，并将其插入到[!UICONTROL Events]容器中。

![](../images/ui/segment-builder/select-event.png)

将事件置于事件容器中后，选择省略号图标(...)，然后选择&#x200B;**[!UICONTROL 聚合]**。

![](../images/ui/segment-builder/add-aggregation.png)

聚合现已添加。 您现在可以选择聚合函数、选择要聚合的属性、相等函数以及值。 对于以下示例，此区段将确定任何购买值总和大于$100（即使每次购买小于$100）的用户档案。

![](../images/ui/segment-builder/filled-aggregation.png)

### 计数函数{#count-functions}

区段生成器中的计数函数用于查找指定的事件并计数完成事件的次数。 区段生成器中支持的计数函数为“至少”、“最多”、“精确”、“介于”和“全部”。

要创建计数函数，请从左边栏中选择一个事件，并将其插入到[!UICONTROL Events]容器中。

![](../images/ui/segment-builder/add-event.png)

将事件置于事件容器中后，选择[!UICONTROL 至少1]按钮。

![](../images/ui/segment-builder/add-count.png)

计数函数现已添加。 您现在可以选择计数函数和函数的值。 以下示例将包括至少单击一次的任何事件。

![](../images/ui/segment-builder/select-count.png)

## 容器

区段规则将按其列出顺序进行评估。 容器允许通过使用嵌套查询来控制执行顺序。

在规则生成器画布中至少添加一个拼贴后，即可开始添加容器。 要创建新容器，请选择图块右上角的省略号(...)，然后选择&#x200B;**[!UICONTROL 添加容器]**。

![](../images/ui/segment-builder/add-container.png)

新容器将作为第一个容器的子容器显示，但您可以通过拖动和移动容器来调整层次结构。 容器的默认行为是“[!UICONTROL Include]”提供的属性、事件或受众。 您可以将规则设置为“[!UICONTROL Exclude]”符合容器条件的配置文件，方法是选择图块左上角的&#x200B;**[!UICONTROL Include]**，然后选择“[!UICONTROL Exclude]”。

也可以通过选择子容器上的“取消包装容器”来提取子容器并将其内联添加到父容器。 选择子容器右上角的省略号(...)以访问此选项。

![](../images/ui/segment-builder/include-exclude.png)

选择&#x200B;**[!UICONTROL 取消包装容器]**&#x200B;后，子容器将被删除，标准将显示为内嵌。

>[!NOTE]
>
>展开容器时，请务必注意逻辑是否继续满足所需的区段定义。

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## 合并策略

[!DNL Experience Platform] 允许您将多个来源的数据合并在一起，以便查看各个客户的完整视图。合并策略是[!DNL Platform]用来确定数据的优先级以及将哪些数据合并以创建用户档案的规则，当将此数据合并在一起时，会使用这些规则。

您可以选择与此受众的营销目的相匹配的合并策略，也可以使用[!DNL Platform]提供的默认合并策略。 您可以创建组织特有的多个合并策略，包括创建您自己的默认合并策略。 有关为组织创建合并策略的分步说明，请首先阅读[合并策略概述](../../profile/merge-policies/overview.md)。

要为区段定义选择合并策略，请在&#x200B;**[!UICONTROL 字段]**&#x200B;选项卡上选择齿轮图标，然后使用&#x200B;**[!UICONTROL 合并策略]**&#x200B;下拉菜单选择要使用的合并策略。

![](../images/ui/segment-builder/merge-policy-selector.png)

## 区段属性

构建区段定义时，工作区右侧的&#x200B;**[!UICONTROL 区段属性]**&#x200B;部分显示结果区段的预估大小，允许您在构建受众本身之前根据需要调整区段定义。

在&#x200B;**[!UICONTROL 区段属性]**&#x200B;部分，您还可以指定有关区段定义的重要信息，包括其名称和描述。 区段定义名称用于在组织定义的区段中标识您的区段，因此应当具有描述性、简洁性和唯一性。

在继续构建区段定义时，您可以通过选择&#x200B;**[!UICONTROL 查看配置文件]**&#x200B;来查看受众的分页预览。

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>受众估计是使用当天样本数据的样本量生成的。 如果您的用户档案存储中的实体少于100万个，则使用完整的数据集；100万至2000万个单位使用100万个单位；超过2000万个单位使用5%的单位。 有关生成区段估计的更多信息，请参阅区段创建教程的[估计生成部分](../tutorials/create-a-segment.md#estimate-and-preview-an-audience)。

## 后续步骤 {#next-steps}

区段生成器提供了一个丰富的工作流程，允许您从[!DNL Real-time Customer Profile]数据中隔离可销售的受众。 阅读本指南后，您现在应该能够：

- 使用属性、事件和现有受众的组合作为构建基块来创建区段定义。
- 使用规则生成器画布和容器来控制区段规则执行的顺序。
- 查看潜在受众的估计值，以便根据需要调整区段定义。
- 为计划分段启用所有区段定义。
- 为流分段启用指定的区段定义。

要了解有关[!DNL Segmentation Service]的更多信息，请继续阅读文档并通过观看相关视频来补充您的学习。 要进一步了解[!DNL Segmentation Service] UI的其他部分，请阅读[[!DNL Segmentation Service] 用户指南](./overview.md)
