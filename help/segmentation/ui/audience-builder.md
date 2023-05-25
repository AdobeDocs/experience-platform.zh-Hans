---
keywords: Experience Platform；主页；热门主题；分段服务；分段；分段服务；用户指南；ui指南；受众ui指南；受众生成器；受众；受众；受众ui指南；
solution: Experience Platform
title: Audiences UI指南
description: Adobe Experience Platform UI中的Audience Builder提供了一个丰富的工作区，允许您与配置文件数据元素进行交互。 工作区提供了直观的控件，用于为贵组织构建和编辑受众。
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Audience Builder UI指南

>[!IMPORTANT]
>
>受众生成器当前为测试版，并非对所有用户都可用。 文档和功能可能会发生变化。

Audience Builder提供了一个工作区，通过用来表示不同操作的块来构建和编辑受众。

![Audience Builder UI。](../images/ui/audience-builder/audience-builder.png)

受众组合画布由五种不同类型的块组成： **[[!UICONTROL Audience]](#audience-block)**， **[[!UICONTROL 排除]](#exclude-block)**， **[[!UICONTROL 加入]](#join-block)**， **[[!UICONTROL 排名]](#rank-block)**、和 **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

此 **[!UICONTROL Audience]** 块类型允许您添加要构成新的更大受众的子受众。 默认情况下， **[!UICONTROL Audience]** 块包含在合成画布的顶部。

当您选择 **[!UICONTROL Audience]** 块时，右边栏会显示用于标记受众并将受众添加到块的控件。

![将显示受众块详细信息。](../images/ui/audience-builder/select-audience.png)

选择后 **[!UICONTROL 添加受众]**，则会显示受众列表。 选择要包含的受众，然后 **[!UICONTROL 添加]** 以将其附加到受众块。

![此时将显示受众列表。 您可以通过此对话框选择要添加的受众。](../images/ui/audience-builder/select-audience.png)

现在，当符合以下条件时，您选择的受众将显示在右边栏中： **[!UICONTROL Audience]** 块已选中。 从此处，您可以更改组合受众的合并类型。

![受众的可能合并类型会突出显示。](../images/ui/audience-builder/merge-types.png)

| 合并类型 | 描述 |
| ---------- | ----------- |
| [!UICONTROL Union] | 受众将合并为一个受众。 此操作等同于OR操作。 |
| [!UICONTROL 交集] | 受众将合并在一起，而只有共享的受众 **所有** 正在添加它们。 此操作等同于AND操作。 |
| [!UICONTROL 排除重叠] | 受众将合并在一起，而只有共享的受众 **一个，但不是全部** 正在添加它们。 这将等同于XOR操作。 |

## [!UICONTROL 排除] {#exclude-block}

此 **[!UICONTROL 排除]** 块类型允许您从新的更大受众中排除指定的子受众或属性。

添加 **[!UICONTROL 排除]** 块，选择 **+** 图标，后接 **[!UICONTROL 排除]**.

![已选中“Exclude”（排除）选项。](../images/ui/audience-builder/add-exclude-block.png)

此 **[!UICONTROL 排除]** 块已添加。 选择此块后，右侧边栏中会显示有关排除项的详细信息。 这包括块的标签和排除类型。 您可以排除 [按受众](#exclude-audience) 或 [按属性](#exclude-attribute).

![排除块，突出显示可用的两种不同的排除类型。](../images/ui/audience-builder/exclude.png)

### 按受众排除 {#exclude-audience}

如果按受众排除，则可以通过选择选择要排除的受众 **[!UICONTROL 添加受众]**.

![“添加受众”按钮处于选中状态，通过它可选择要排除的受众。](../images/ui/audience-builder/add-excluded-audience.png)

此时将显示受众列表。 选择 **[!UICONTROL 添加]** 以将要排除的受众添加到排除块。

![此时将显示受众列表。 您可以通过此对话框选择要添加的受众。](../images/ui/audience-builder/select-audience.png)

### 按属性排除 {#exclude-attribute}

如果按属性排除，则可以通过选择 ![过滤器](../images/ui/audience-builder/filter-attribute.png) 中的图标 **[!UICONTROL 排除规则]** 部分。

![属性部分会突出显示，显示从何处选择要排除的属性。](../images/ui/audience-builder/exclude-attribute.png)

此时将显示配置文件属性列表。 选择要排除的属性类型，然后 **[!UICONTROL 选择]** 以将其添加到排除块。

![此时将显示属性列表。](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL 加入] {#join-block}

此 **[!UICONTROL 加入]** 块类型允许您从Adobe Experience Platform尚未处理的数据集添加外部受众。

添加 **[!UICONTROL 加入]** 块，选择 **+** 图标，后接 **[!UICONTROL 加入]**.

![已选中“连接”选项。](../images/ui/audience-builder/add-join-block.png)

当您选择块时，有关联接的详细信息将显示在右边栏中，包括块的标签以及将受众添加到扩充数据集的选项。

![高亮显示连接块，包括有关连接块的详细信息。](../images/ui/audience-builder/join.png)

选择后 **[!UICONTROL 添加受众]**，则会显示受众列表。 选择要包含的受众，然后 **[!UICONTROL 添加]** 以将其添加到连接块。

![此时将显示受众列表。 您可以通过此对话框选择要添加的受众。](../images/ui/audience-builder/select-audience.png)

现在，当符合以下条件时，您选择的受众将显示在右边栏中： **[!UICONTROL 加入]** 块已选中。

![将显示作为加入的一部分添加的受众。](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL 排名] {#rank-block}

此 **[!UICONTROL 排名]** 块类型允许您在发布新受众之前对受众进行排名和排序。

添加 **[!UICONTROL 排名]** 块，选择 **+** 图标，后接 **[!UICONTROL 排名]**.

![已选择排名选项。](../images/ui/audience-builder/add-rank-block.png)

当您选择块时，有关排名的详细信息将显示在右边栏中，包括块的标签、排名依据的属性、排名顺序以及用于限制排名配置文件数量的切换开关。

![突出显示排名块，以及排名块的详细信息。](../images/ui/audience-builder/rank.png)

要选择受众排名所依据的属性，请选择 ![过滤器](../images/ui/audience-builder/filter-attribute.png) 图标。

![过滤器图标会突出显示，显示用于访问配置文件属性选择屏幕的选项。](../images/ui/audience-builder/select-rank-attribute.png)

此时将显示配置文件属性列表。 在此弹出窗口中，您可以选择要按其为受众排名的属性类型。 选择 **[!UICONTROL 选择]** 以将其添加到排名块。 请注意，选定的属性可以 **仅限** 属于类型 `int`.

![此时将显示属性列表。](../images/ui/audience-builder/select-attribute.png)

选择属性后，您可以选择排序依据。 按升序（从最低到最高）或降序（从最高到最低）排列。

此外，您还可以通过启用 **[!UICONTROL 添加配置文件限制]** 切换。 启用此切换后，您可以设置 **[!UICONTROL 包含的配置文件]** 字段。

![添加配置文件限制切换开关会突出显示，用于限制返回的受众数量。](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

此 **[!UICONTROL Split]** 块类型允许您将新受众拆分为各种子受众。 您可以根据百分比或按属性拆分此受众。

添加 **[!UICONTROL Split]** 块，选择 **+** 图标，后接 **[!UICONTROL Split]**.

![已选中“拆分”选项。](../images/ui/audience-builder/add-split-block.png)

### 按百分比拆分 {#split-percentage}

按百分比拆分时，将根据提供的路径数和百分比，随机拆分受众。

例如，您可以有三个路径，每个路径具有不同的用户档案百分比。

![系统将显示按已保存受众数和百分比划分的细分。](../images/ui/audience-builder/percentages.png)

此外，您可以将其中一个拆分受众标记为对照组。

![已启用控制组切换。 这样，您可以将其中一个拆分受众标记为对照组。](../images/ui/audience-builder/control-group.png)

### 按属性拆分 {#split-attribute}

按属性拆分时，将根据提供的属性拆分受众。 要选择作为拆分依据的属性，请选择 **[!UICONTROL Split]** 块，后面跟 ![过滤器](../images/ui/audience-builder/filter-attribute.png) 图标。

![已选择过滤器按钮，显示如何按属性过滤。](../images/ui/audience-builder/select-attribute-split.png)

此时将显示配置文件属性列表。 选择属性类型，然后 **[!UICONTROL 选择]** 以将其添加到拆分块。

![此时将显示属性列表。](../images/ui/audience-builder/select-attribute.png)

选择属性后，您可以通过添加中的值来选择哪些配置文件将属于哪个子受众 **[!UICONTROL 值]** 字段。

![将添加要按其拆分属性的值。](../images/ui/audience-builder/attribute-split-values.png)

此外，您还可以启用 **[!UICONTROL 其他配置文件]** 切换以创建包含所有非选定用户档案的子受众。

![其他配置文件切换开关会突出显示。](../images/ui/audience-builder/attribute-split-other-profiles.png)

## 发布您的受众

构成受众后，您可以通过选择 **[!UICONTROL Publish]**.

![此时会高亮显示“发布”按钮，向您展示如何保存和发布受众。](../images/ui/audience-builder/publish-audience.png)

如果在创建受众时出现任何错误，则会显示警报，让您知道如何解决此问题。

![此时会高亮显示“发布”按钮，向您展示如何保存和发布受众。](../images/ui/audience-builder/audience-alert.png)

## 后续步骤

受众生成器提供了一个丰富的工作流，允许您从不同的块类型创建受众。 要了解有关Segmentation Service UI其他部分的更多信息，请阅读 [分段服务用户指南](./overview.md).
