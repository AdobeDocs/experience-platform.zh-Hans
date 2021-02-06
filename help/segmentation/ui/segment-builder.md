---
keywords: Experience Platform；主题；热门主题；分段服务；分段服务；用户指南；ui指南；分段ui指南；段构建器；段构建器；
solution: Experience Platform
title: 区段生成器UI指南
topic: ui guide
description: 'Adobe Experience PlatformUI中的区段生成器提供丰富的工作区，允许您与用户档案数据元素交互。 工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。 '
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 0%

---


# [!DNL Segment Builder] UI指南

[!DNL Segment Builder] 提供丰富的工作区，允许您与数据元 [!DNL Profile] 素交互。工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。

![](../images/ui/segment-builder/segment-builder.png)

## 段定义构建块

段定义的基本构件是属性和事件。 此外，现有受众中包含的属性和事件也可用作新定义的组件。

您可以在[!DNL Segment Builder]工作区左侧的&#x200B;**[!UICONTROL 字段]**&#x200B;部分看到这些构件块。 **[!UICONTROL 字]** 段包含每个主要构件块的选项卡：“[!UICONTROL 属性]”、“[!UICONTROL 事件]”和“[!UICONTROL 受众]”。

![](../images/ui/segment-builder/segment-fields.png)

### 属性

**[!UICONTROL 属性]**&#x200B;选项卡允许您浏览属于[!DNL XDM Individual Profile]类的[!DNL Profile]属性。 每个文件夹都可以展开以显示其他属性，其中每个属性都是一个拼贴，可拖动到工作区中心的规则构建器画布上。 本指南后面将详细讨论[规则构建器画布](#rule-builder-canvas)。

![](../images/ui/segment-builder/attributes.png)

### 事件

**[!UICONTROL 事件]**&#x200B;选项卡允许您根据使用[!DNL XDM ExperienceEvent]数据元素进行的事件或操作创建受众。 您还可以在&#x200B;**[!UICONTROL 事件类型]**&#x200B;选项卡上找到事件，这些事件是常用的集合，使您能够更快地创建区段。

除了能够浏览[!DNL ExperienceEvent]元素外，还可以搜索事件类型。 事件类型使用与[!DNL ExperienceEvents]相同的编码逻辑，无需您搜索[!DNL XDM ExperienceEvent]类以寻找正确的事件。 例如，使用搜索栏搜索“购物车”将返回事件类型“[!UICONTROL AddCart]”和“[!UICONTROL RemoveCart]”，这两个操作是构建区段定义时最常用的操作。

可以通过在搜索栏中键入其名称来搜索任何类型的组件，该名称使用[Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 输入整个单词后，搜索结果开始填充。 例如，要根据XDM字段`ExperienceEvent.commerce.productViews`构建规则，请开始在搜索字段中键入“产品视图”。 键入“product”一词后，搜索结果开始显示。 每个结果都包括它所属的对象层次结构。

>[!NOTE]
>
>您的组织定义的自定义模式字段可能需要24小时才能显示，并可用于构建规则。

然后，您可以轻松地将[!DNL ExperienceEvents]和“[!UICONTROL 事件类型]”拖放到您的区段定义中。

![](../images/ui/segment-builder/events-eventTypes.png)

默认情况下，只显示模式存储中已填充的数据字段。 这包括“[!UICONTROL 事件类型]”。 如果“[!UICONTROL 事件类型]”列表不可见，或者您只能选择“[!UICONTROL 任何]”作为“[!UICONTROL 事件类型]”，请选择“字段&#x200B;**[!UICONTROL a9/>”旁的**&#x200B;齿轮图标&#x200B;**，然后选择**[!UICONTROL &#x200B;在&#x200B;**[!UICONTROL 可用字段]**&#x200B;下显示完整的XDM模式&#x200B;]**。]**&#x200B;再次选择&#x200B;**齿轮图标**&#x200B;以返回到&#x200B;**[!UICONTROL 字段]**&#x200B;选项卡，您现在应能视图多个“[!UICONTROL 事件类型]”和模式字段，而不管它们是否包含数据。

![](../images/ui/segment-builder/show-populated.png)

### 受众

**[!UICONTROL 受众]**&#x200B;选项卡列表从外部源(如Adobe Audience Manager)导入的所有受众，以及在[!DNL Experience Platform]中创建的受众。

在&#x200B;**[!UICONTROL 受众]**&#x200B;选项卡上，您可以将所有可用源作为一组文件夹查看。 当您选择文件夹时，可以看到可用的子文件夹和受众。 此外，您还可以选择文件夹图标（如最右侧图像所示）以视图文件夹结构（复选标记表示您当前所在的文件夹），并通过选择树中某个文件夹的名称轻松导航回文件夹。

您可以将鼠标悬ⓘ停在受众旁边以视图受众的相关信息，包括其ID、描述和文件夹层次结构，以便找到受众。

![](../images/ui/segment-builder/audience-folder-structure.png)

您还可以使用搜索栏搜索受众，该搜索栏使用[Lucene的搜索语法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)。 在&#x200B;**[!UICONTROL 受众]**&#x200B;选项卡上，选择顶级文件夹会显示搜索栏，允许您在该文件夹中搜索。 只有输入完整单词后，搜索结果才会开始填充。 例如，要查找名为`Online Shoppers`的受众，请在搜索栏中开始键入“Online”。 在完整键入“在线”一词后，将显示包含“在线”一词的搜索结果。

## 规则构建器画布{#rule-builder-canvas}

区段定义是用于描述目标受众的关键特征或行为的规则集合。 这些规则是使用位于[!DNL Segment Builder]中心的规则生成器画布创建的。

要向区段定义添加新规则，请从&#x200B;**[!UICONTROL 字段]**&#x200B;选项卡中拖动一个拼贴并将其放到规则生成器画布上。 然后，将根据要添加的数据类型向您显示上下文特定选项。 可用数据类型包括：字符串、日期、[!DNL ExperienceEvents]、&quot;[!UICONTROL 事件类型]&quot;和受众。

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>对Adobe Experience Platform的最新更改更新了事件之间`OR`和`AND`逻辑运算符的使用。 这些更新不会影响现有区段。 但是，对现有区段和新区段创建的所有后续更新都将受到这些更改的影响。 请阅读[时间常量更新](./segment-refactoring.md)以了解更多信息。

### 添加受众

您可以将&#x200B;**[!UICONTROL 受众]**&#x200B;选项卡中的受众拖放到规则生成器画布上，以在新区段定义中引用受众成员身份。 这允许您将受众成员资格作为属性加入或排除到新区段规则中。

对于使用[!DNL Segment Builder]创建的[!DNL Platform]受众，您可以选择将受众转换为在该受众的段定义中使用的规则集。 此转换会生成规则逻辑的副本，然后可以修改该副本，而不会影响原始段定义。 在将区段定义转换为规则逻辑之前，请确保已保存对区段定义的任何最近更改。

>[!NOTE]
>
>从外部源添加受众时，只引用受众成员身份。 无法将受众转换为规则，因此在新区段定义中无法修改用于创建原始受众的规则。

![](../images/ui/segment-builder/add-audience-to-segment.png)

如果在将受众转换为规则时发生任何冲突，[!DNL Segment Builder]将尝试保留现有选项，使其能力达到最佳。

### 代码视图

或者，也可以视图在[!DNL Segment Builder]中创建的规则的基于代码的版本。 在规则构建器画布中创建规则后，您可以选择&#x200B;**[!UICONTROL 代码视图]**&#x200B;来将您的区段视为PQL。

![](../images/ui/segment-builder/code-view.png)

代码视图提供一个按钮，允许您复制段值以在API调用中使用。 要获取区段的最新版本，请确保您已将最新更改保存到区段。

![](../images/ui/segment-builder/copy-code.png)

## 容器

区段规则将按其列出的顺序进行评估。 容器允许通过使用嵌套查询来控制执行顺序。

在将至少一个拼贴添加到规则构建器画布后，您可以开始添加容器。 要创建新容器，请选择磁贴右上角的省略号(...)，然后选择&#x200B;**[!UICONTROL 添加容器]**。

![](../images/ui/segment-builder/add-container.png)

新容器显示为第一个容器的子项，但您可以通过拖动和移动容器来调整层次。 容器的默认行为是“[!UICONTROL 包括]”提供的属性、事件或受众。 通过选择磁贴左上角的&#x200B;**[!UICONTROL Include]**&#x200B;并选择“[!UICONTROL Exclude]”，可以将规则设置为与容器条件匹配的“[!UICONTROL Exclude]”用户档案。

也可以通过选择子容器上的“取消换行容器”，提取子容器并内嵌到父容器。 选择子容器右上角的省略号(...)以访问此选项。

![](../images/ui/segment-builder/include-exclude.png)

选择&#x200B;**[!UICONTROL 取消容器]**&#x200B;后，将删除子容器并内联显示条件。

>[!NOTE]
>
>展开容器时，请注意逻辑继续满足所需的段定义。

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## 合并策略

[!DNL Experience Platform] 使您能够将来自多个来源的数据整合在一起，并将其合并，以便了解每个客户的完整视图。合并策略是[!DNL Platform]用来确定数据的优先级以及将哪些数据合并以创建用户档案的规则。

您可以选择与此受众的营销目的匹配的合并策略，或使用[!DNL Platform]提供的默认合并策略。 您可以创建组织特有的多个合并策略，包括创建您自己的默认合并策略。 有关为组织创建合并策略的分步说明，请参阅有关使用UI](../../profile/ui/merge-policies.md)使用合并策略的教程。[

要为段定义选择合并策略，请在&#x200B;**[!UICONTROL 字段]**&#x200B;选项卡上选择齿轮图标，然后使用&#x200B;**[!UICONTROL 合并策略]**&#x200B;下拉菜单选择要使用的合并策略。

![](../images/ui/segment-builder/merge-policy-selector.png)

## 区段属性

在构建区段定义时，工作区右侧的&#x200B;**[!UICONTROL 区段属性]**&#x200B;部分会显示所生成区段的大小估计值，允许您在构建受众本身之前根据需要调整区段定义。

在&#x200B;**[!UICONTROL 区段属性]**&#x200B;部分，您还可以指定有关区段定义的重要信息，包括其名称和说明。 区段定义名称用于在组织定义的区段中识别您的区段，因此应具有描述性、简明性和唯一性。

在继续构建区段定义时，您可以通过选择&#x200B;**[!UICONTROL 视图预览]**&#x200B;来视图受众的分页用户档案。

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>受众估计是使用当天样本数据的样本大小生成的。 如果您的用户档案存储中少于100万个实体，则使用完整的数据集；100万至2000万个单位使用100万个单位；超过2000万个单位，占全部单位的5%。 有关生成段估计的详细信息，请参阅段创建教程的[估计生成部分](../tutorials/create-a-segment.md#estimate-and-preview-an-audience)。

## 后续步骤和其他资源{#next-steps}

区段生成器提供丰富的工作流，允许您从[!DNL Real-time Customer Profile]数据中隔离可销售受众。 阅读本指南后，您现在应能够：

- 使用属性、事件和现有受众的组合作为构件块创建区段定义。
- 使用规则构建器画布和容器控制段规则的执行顺序。
- 视图对未来受众的估计，使您能够根据需要调整细分定义。
- 为计划分段启用所有段定义。
- 为流分段启用指定的段定义。

要进一步了解[!DNL Segmentation Service]，请继续阅读文档，并通过观看以下视频补充您的学习。 要进一步了解[!DNL Segmentation Service] UI的其他部分，请阅读[[!DNL Segmentation Service] 用户指南](./overview.md)

>[!WARNING]
>
> 以下视频中显示的[!DNL Platform] UI已过期。 有关最新的UI屏幕截图和功能，请参阅上面的文档。

**创建区段：**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**创建动态区段：**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)