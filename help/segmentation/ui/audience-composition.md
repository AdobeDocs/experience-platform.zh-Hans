---
solution: Experience Platform
title: Audiences UI指南
description: Adobe Experience Platform UI中的受众组合提供了一个丰富的工作区，允许您与配置文件数据元素进行交互。 工作区提供了一些直观的控件，可用于为贵组织构建和编辑受众。
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 56d9d3ec5565960438540ffec867ed528b52eaf1
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 0%

---

# 受众合成UI指南

>[!NOTE]
>
>本指南介绍如何使用受众构成创建受众。 要了解如何使用区段生成器通过区段定义创建受众，请参阅 [区段生成器UI指南](./segment-builder.md).

受众构成提供了一个工作区，通过用来表示不同操作的块来构建和编辑受众。

![受众构成UI。](../images/ui/audience-composition/audience-composition.png)

要更改构成的详细信息（包括标题和描述），请选择 ![滑块](../images/ui/audience-composition/sliders.png) 按钮。

此 **[!UICONTROL 组合属性]** 弹出窗口出现。 您可以在此处插入构图的详细信息，包括标题和描述。

![此时将显示“合成”属性弹出框。](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>如果您愿意 **非** 为您的构图提供一个标题，默认情况下，它具有“构图”的标题，后跟创建日期和时间。

更新合成详细信息后，选择 **[!UICONTROL 保存]** 以确认这些更新。 受众构成画布重新出现。

受众组合画布由四种不同类型的块组成： **[[!UICONTROL 受众]](#audience-block)**， **[[!UICONTROL 排除]](#exclude-block)**， **[[!UICONTROL 排名]](#rank-block)**、和 **[[!UICONTROL Split]](#split-block)**.

## [!UICONTROL 受众] {#audience-block}

此 **[!UICONTROL 受众]** 块类型允许您添加要构成新的较大受众的子受众。 默认情况下， **[!UICONTROL 受众]** 块包含在合成画布的顶部。

当您选择 **[!UICONTROL 受众]** 块时，右边栏会显示用于标记受众、将受众添加到块以及为受众块构建自定义规则的控件。

>[!NOTE]
>
>您可以添加受众 **或** 创建自定义规则。 这两项功能 **无法** 一起使用。

![此时会显示受众块详细信息。](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL 添加受众] {#add-audience}

将受众添加到“受众”块。 选择 **[!UICONTROL 添加受众]**.

![添加受众按钮会突出显示。](../images/ui/audience-composition/add-audience.png)

此时将显示受众列表。 选择要包含的受众，然后 **[!UICONTROL 添加]** 以将其附加到受众块。

![此时将显示受众列表。 您可以通过此对话框选择要添加的受众。](../images/ui/audience-composition/select-audience.png)

现在，当满足以下条件时，您选择的受众将显示在右边栏中： **[!UICONTROL 受众]** 块已选中。 在此处，您可以更改组合受众的合并类型。

![受众的可能合并类型会突出显示。](../images/ui/audience-composition/merge-types.png)

| 合并类型 | 描述 |
| ---------- | ----------- |
| [!UICONTROL Union] | 受众将合并为一个受众。 此操作等同于OR操作。 |
| [!UICONTROL 交集] | 受众将仅与中共享的受众合并 **所有** 正在添加它们。 此操作等同于AND操作。 |
| [!UICONTROL 排除重叠] | 受众将仅与中共享的受众合并 **一个，但不是全部** 正在添加它们。 这相当于XOR操作。 |

### [!UICONTROL 生成规则] {#build-rule}

要将自定义规则添加到“受众”块，请选择 **[!UICONTROL 生成规则]**.

![构建规则按钮突出显示。](../images/ui/audience-composition/build-rule.png)

此时将显示“区段生成器”。 您可以使用区段生成器创建自定义规则，以供受众遵循。 有关使用区段生成器的更多信息，请参阅 [区段生成器指南](./segment-builder.md).

![此时会显示区段生成器UI。](../images/ui/audience-composition/segment-builder.png)

添加自定义规则后，选择 **[!UICONTROL 保存]** 以将规则添加到受众。

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL 排除] {#exclude-block}

此 **[!UICONTROL 排除]** 块类型允许您从新的较大受众中排除指定的子受众或属性。

添加 **[!UICONTROL 排除]** 块，选择 **+** 图标，后接 **[!UICONTROL 排除]**.

![已选中“Exclude（排除）”选项。](../images/ui/audience-composition/add-exclude-block.png)

此 **[!UICONTROL 排除]** 块已添加。 选择此块后，右边栏中会显示有关排除项的详细信息。 这包括块的标签和排除类型。 您可以排除 [按受众](#exclude-audience) 或 [按属性](#exclude-attribute).

![Exclude块，突出显示可用的两种不同的排除类型。](../images/ui/audience-composition/exclude.png)

### 按受众排除 {#exclude-audience}

如果按受众排除，则可以通过选择选择要排除的受众 **[!UICONTROL 添加受众]**.

![此 [!UICONTROL 添加受众] 按钮中选择，以选择要排除的受众。](../images/ui/audience-composition/add-excluded-audience.png)

此时将显示受众列表。 选择 **[!UICONTROL 添加]** 以将要排除的受众添加到排除块。

![此时将显示受众列表。 您可以通过此对话框选择要添加的受众。](../images/ui/audience-composition/select-audience.png)

### 按属性排除 {#exclude-attribute}

如果按属性排除，则可以通过选择 ![筛选](../images/ui/audience-composition/filter-attribute.png) 图标 **[!UICONTROL 排除规则]** 部分。

![属性部分会突出显示，显示从何处选择要排除的属性。](../images/ui/audience-composition/exclude-attribute.png)

此时将显示配置文件属性列表。 选择要排除的属性类型，然后 **[!UICONTROL 选择]** 以将其添加到排除块。

![此时将显示属性列表。](../images/ui/audience-composition/select-attribute-exclude.png)

## [!UICONTROL 扩充] {#enrich-block}

>[!IMPORTANT]
>
>此时，扩充属性可以 **仅限** 用于下游Adobe Journey Optimizer方案。

此 **[!UICONTROL 扩充]** 块类型允许您使用数据集中的其他属性扩充受众。 您可以在个性化用例中使用这些属性。

添加 **[!UICONTROL 扩充]** 块，选择 **+** 图标，后接 **[!UICONTROL 扩充]**.

![此 [!UICONTROL 扩充] 已选中选项。](../images/ui/audience-composition/add-enrich-block.png)

此 **[!UICONTROL 扩充]** 块已添加。 选择此块后，有关扩充的详细信息将显示在右边栏中。 这包括块的标签和扩充数据集。

要选择用于扩充受众的数据集，请选择 ![筛选](../images/ui/audience-composition/filter-attribute.png) 图标。

![筛选器按钮突出显示。 选择此项可引导您找到 [!UICONTROL 选择数据集] 弹出窗口。](../images/ui/audience-composition/enrich-select-dataset.png)

此 **[!UICONTROL 选择数据集]** 弹出窗口出现。 选择要添加以进行扩充的数据集，然后 **[!UICONTROL 选择]** 以添加数据集以进行扩充。

![已选择选定的数据集。](../images/ui/audience-composition/enrich-dataset-selected.png)

>[!IMPORTANT]
>
>选定的数据集 **必须** 符合以下条件：
>
>- 数据集 **必须** 属于记录类型。
>   - 数据集 **无法** 属于事件类型、由系统生成或标记为配置文件。
>- 数据集 **必须** 为1 GB或更小。

此 **[!UICONTROL 扩充条件]** 部分现在显示在右边栏中。 在此部分中，您可以选择 **[!UICONTROL 源连接密钥]** 和 **[!UICONTROL 扩充数据集联接键]**，可让您将扩充数据集与尝试创建的受众链接。

![此 [!UICONTROL 扩充条件] 区域将突出显示。](../images/ui/audience-composition/enrichment-criteria.png)

要选择 **[!UICONTROL 源连接密钥]**，选择 ![筛选](../images/ui/audience-composition/filter-attribute.png) 图标。

![的过滤器图标 [!UICONTROL 源连接密钥] 高亮显示。](../images/ui/audience-composition/enrich-select-source-join-key.png)

此 **[!UICONTROL 选择配置文件属性]** 弹出窗口出现。 选择要用作源连接键的配置文件属性，然后 **[!UICONTROL 选择]** 以选择该属性作为源连接键。

![要用作源连接键的属性会突出显示。](../images/ui/audience-composition/enrich-select-profile-attribute.png)

要选择 **[!UICONTROL 扩充数据集联接键]**，选择 ![筛选](../images/ui/audience-composition/filter-attribute.png) 图标。

![的过滤器图标 [!UICONTROL 扩充数据集联接键] 高亮显示。](../images/ui/audience-composition/enrich-select-enrichment-dataset-join-key.png)

此 **[!UICONTROL 扩充属性]** 弹出窗口出现。 选择要用作扩充数据集联接键的属性，然后 **[!UICONTROL 选择]** 以选择该属性作为扩充数据集联接键。

![将突出显示要用作扩充数据集联接键的属性。](../images/ui/audience-composition/enrich-select-enrichment-dataset-attribute.png)

现在，您已添加两个连接密钥， **[!UICONTROL 扩充属性]** 部分。 您现在可以添加要用于增强受众的属性。 要添加这些属性，请选择 **[!UICONTROL 添加属性]**.

![此 [!UICONTROL 添加属性] 按钮会突出显示。](../images/ui/audience-composition/enrich-select-add-attribute.png)

此 **[!UICONTROL 扩充属性]** 弹出窗口出现。 您可以从数据集中选择属性，以使用扩充受众，然后选择 **[!UICONTROL 选择]** 向受众添加属性。

![要添加的扩充属性会突出显示。](../images/ui/audience-composition/enrich-add-enrichment-attributes.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL 排名] {#rank-block}

此 **[!UICONTROL 排名]** 块类型允许您根据指定属性对配置文件进行排名和排序，并将这些排名配置文件包含在合成中。

添加 **[!UICONTROL 排名]** 块，选择 **+** 图标，后接 **[!UICONTROL 排名]**.

![已选择“排名”选项。](../images/ui/audience-composition/add-rank-block.png)

选择块后，右侧边栏中显示有关排名的详细信息，包括块的标签、要排名的属性、排名顺序以及用于限制要排名的配置文件数量的切换开关。

![突出显示排名块，并突出显示排名块的详细信息。](../images/ui/audience-composition/rank.png)

要选择受众排名所依据的属性，请选择 ![筛选](../images/ui/audience-composition/filter-attribute.png) 图标。

![过滤器图标会高亮显示，其中显示了访问配置文件属性选择屏幕时所要选择的内容。](../images/ui/audience-composition/select-rank-attribute.png)

此时将显示配置文件属性列表。 在此弹出窗口中，您可以选择要按其对受众进行排名的属性类型。 选择 **[!UICONTROL 选择]** 以将其添加到您的排名块。 请注意，所选属性可以 **仅限** 就是数字。

![此时将显示属性列表。](../images/ui/audience-composition/select-attribute-rank.png)

选择属性后，您可以选择排序依据。 这是以升序（从最低到最高）或降序（从最高到最低）顺序显示的。

此外，您还可以通过启用 **[!UICONTROL 添加配置文件限制]** 切换。 启用此切换后，您可以设置 **[!UICONTROL 包含的配置文件]** 字段。

![添加配置文件限制切换开关会突出显示，用于限制返回的受众数量。](../images/ui/audience-composition/add-profile-limit.png)

## [!UICONTROL Split] {#split-block}

此 **[!UICONTROL Split]** 块类型允许您将新受众拆分为各种子受众。 您可以按百分比或属性拆分此受众。

添加 **[!UICONTROL Split]** 块，选择 **+** 图标，后接 **[!UICONTROL Split]**.

![已选中“拆分”选项。](../images/ui/audience-composition/add-split-block.png)

在拆分受众时，您可以按百分比拆分或按属性拆分。

### 按百分比拆分 {#split-percentage}

按百分比拆分时，将根据提供的路径数和百分比随机拆分受众。

例如，您可以有三个路径，每个路径都具有不同的用户档案百分比。

![系统将显示已保存受众数和百分比的细分。](../images/ui/audience-composition/percentages.png)

### 按属性拆分 {#split-attribute}

按属性拆分时，将基于提供的属性拆分受众。 要选择作为拆分依据的属性，请选择 **[!UICONTROL Split]** 块，然后是 ![筛选](../images/ui/audience-composition/filter-attribute.png) 图标。

![已选择过滤器按钮，显示如何按属性过滤。](../images/ui/audience-composition/select-split-attribute.png)

此时将显示配置文件属性列表。 选择属性类型，然后 **[!UICONTROL 选择]** 以将其添加到拆分块。

![此时将显示属性列表。](../images/ui/audience-composition/select-attribute-exclude.png)

选择属性后，您可以通过添加以下范围内的值，选择哪些配置文件将属于哪个子受众 **[!UICONTROL 值]** 字段。

![将添加要按其拆分属性的值。](../images/ui/audience-composition/attribute-split-values.png)

此外，您还可以启用 **[!UICONTROL 其他配置文件]** 切换以创建包含所有未选择的用户档案的子受众。

![“其他配置文件”切换开关会突出显示。](../images/ui/audience-composition/split-other-profiles.png)

## 发布受众

合成受众后，您可以通过选择 **[!UICONTROL Publish]**.

![此时会高亮显示“发布”按钮，向您说明如何保存和发布受众。](../images/ui/audience-composition/publish.png)

如果创建受众时出现任何错误，则会显示一条警报，让您知道如何解决此问题。

![此时会高亮显示“发布”按钮，向您说明如何保存和发布受众。](../images/ui/audience-composition/audience-alert.png)

## 后续步骤

受众构成提供了一个丰富的工作流，允许您从不同的块类型创建受众。 要了解有关Segmentation Service UI其他部分的更多信息，请阅读 [Segmentation Service用户指南](./overview.md).
