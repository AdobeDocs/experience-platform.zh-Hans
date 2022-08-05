---
keywords: Experience Platform；主页；热门主题；映射CSV；映射CSV文件；将CSV文件映射到XDM；将CSV映射到XDM;UI指南；映射；数据准备；数据准备；准备数据；
title: 数据准备UI指南
description: 本文档提供了有关如何在Platform UI中使用数据准备函数将CSV文件映射到XDM架构的说明。
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: d0f5d1f55101ce15934289d4fcfd1f70c1b63fc7
workflow-type: tm+mt
source-wordcount: '1845'
ht-degree: 1%

---

# 数据准备UI指南

本文档提供了有关如何在Adobe Experience Platform用户界面中使用数据准备函数将CSV文件映射到XDM架构的说明。

## 快速入门

本教程需要对以下平台组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../xdm/home.md):Platform用来组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [Identity Service](../../identity-service/home.md):通过跨设备和系统桥接身份，更好地了解各个客户及其行为。
* [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [源](../../sources/home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。

## 数据流详细信息

>[!TIP]
>
>您可以通过从源目录中选择任何源来访问数据流详细信息。 有关更多信息，请参阅 [源概述](../../sources/home.md).

在将CSV数据映射到XDM架构之前，必须先建立数据流的详细信息。

的 [!UICONTROL 数据流详细信息] 页面允许您选择是要将CSV数据摄取到现有目标数据集还是新目标数据集。 现有数据集附带一个将您的数据映射到的预建目标架构，而新数据集要求您选择现有架构或创建新架构，以将您的数据映射到。

### 使用现有目标数据集

要将CSV数据摄取到现有数据集，请选择 **[!UICONTROL 现有数据集]**. 您可以使用 [!UICONTROL 高级搜索] 选项，或者通过在下拉菜单中滚动浏览现有数据集列表来配置。

选择数据集后，为数据流提供名称和可选描述。

在此过程中，您还可以启用 [!UICONTROL 错误诊断] 和 [!UICONTROL 部分摄取]. [!UICONTROL 错误诊断] 为数据流中发生的任何错误记录启用详细的错误消息生成，而 [!UICONTROL 部分摄取] 允许您摄取包含错误的数据，最多可达您手动定义的特定阈值。 请参阅 [部分批量摄取概述](../../ingestion/batch-ingestion/partial.md) 以了解更多信息。

![现有数据集](../images/ui/mapping/existing-dataset.png)

### 使用新的目标数据集

要将CSV数据摄取到新数据集，请选择 **[!UICONTROL 新数据集]** 然后，提供输出数据集名称和可选描述。 接下来，使用 [!UICONTROL 高级搜索] 选项或通过滚动下拉菜单中的现有架构列表来迁移。

选择架构后，为数据流提供名称和可选描述，然后应用 [!UICONTROL 错误诊断] 和 [!UICONTROL 部分摄取] 数据流所需的设置。 完成后，选择 **[!UICONTROL 下一个]**.

![新数据集](../images/ui/mapping/new-dataset.png)

## 选择数据

的 [!UICONTROL 选择数据] 步骤，为您提供一个界面来上载本地文件并预览其结构和内容。 选择 **[!UICONTROL 选择文件]** 从本地系统上传CSV文件。 或者，您也可以将要上传的CSV文件拖放到 [!UICONTROL 拖放文件] 的上界。

>[!TIP]
>
>本地文件上传当前仅支持CSV文件。 每个文件的最大文件大小为1 GB。

![选择文件](../images/ui/mapping/choose-files.png)

上传文件后，预览界面会随之更新，以显示文件的内容和结构。

![preview-sample-data](../images/ui/mapping/preview-sample-data.png)

根据您的文件，您可以为源数据选择列分隔符，如制表符、逗号、管道分隔符或自定义列分隔符。 选择 **[!UICONTROL 分隔符]** 下拉箭头，然后从菜单中选择相应的分隔符。

完成后，选择 **[!UICONTROL 下一个]**.

![分隔符](../images/ui/mapping/delimiter.png)

## 映射

的 **[!UICONTROL 映射]** 界面为您提供了一个全面的工具，用于将源模式中的源字段映射到目标模式中相应的目标XDM字段。

![将csv-to xdm](../images/ui/mapping/map-csv-to-xdm.png)

### 了解映射界面

映射界面包括一个功能板，用于提供有关摄取工作流上下文中映射字段运行状况的信息。 功能板显示有关映射字段的以下详细信息：

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL 映射的字段] | 显示已映射到目标XDM字段的源字段总数，而不考虑错误。 |
| [!UICONTROL 必填字段] | 显示必填映射字段的数量。 |
| [!UICONTROL 标识字段] | 显示定义为标识的映射字段总数。 这些映射字段由指纹图标表示。 |
| [!UICONTROL 错误] | 显示错误映射字段的数量。 |

![顶部面板](../images/ui/mapping/top-panel.png)

映射界面还提供了一个选项面板，您可以从中进行选择，以便更好地进行交互或在映射字段中进行筛选。

![第二面板](../images/ui/mapping/second-panel.png)

要搜索特定映射集，请选择 **[!UICONTROL 搜索源字段]** 并输入要隔离的源数据的名称。

![搜索](../images/ui/mapping/search.png)

选择 **[!UICONTROL 所有源字段]** 可查看包含筛选选项的下拉菜单，以便更好地缩小映射界面的视图范围。

筛选选项包括：

| 源字段 | 描述 |
| --- | --- |
| [!UICONTROL 所有源字段] | 此选项显示源架构的所有源字段。 默认情况下，会显示此选项。 |
| [!UICONTROL 必填字段] | 此选项过滤源架构以仅显示完成映射所需的字段。 |
| [!UICONTROL 标识字段] | 此选项过滤源架构，以仅显示标记为“身份”的字段。 |
| [!UICONTROL 映射的字段] | 此选项过滤源架构以仅显示已映射的字段。 |
| [!UICONTROL 未映射的字段] | 此选项过滤源架构以仅显示尚未映射的字段。 |
| [!UICONTROL 包含推荐的字段] | 此选项过滤源架构以仅显示包含映射推荐的字段。 |

选择 **[!UICONTROL 有错误的字段]** 以查看所有存在错误的映射字段。

![filter](../images/ui/mapping/filter.png)

此时会显示错误映射字段的孤立视图，允许您通过智能映射推荐或手动映射树来解决错误。

![带错误的字段](../images/ui/mapping/fields-with-errors.png)

### 添加新字段类型

您可以通过选择 **[!UICONTROL 新字段类型]**.

#### 新建映射字段

要添加新映射字段，请选择 **[!UICONTROL 新字段类型]** 然后选择 **[!UICONTROL 添加新字段]** 下拉菜单中。

![add-new-field](../images/ui/mapping/add-new-field.png)

接下来，从显示的源架构树中选择要添加的源字段，然后选择 **[!UICONTROL 选择]**.

![select-new-field](../images/ui/mapping/select-new-field.png)

映射界面会随您选择的源字段和空目标字段一起更新。 选择 **[!UICONTROL 映射目标字段]** 开始将新源字段映射到相应的目标XDM字段。

![map-target-field](../images/ui/mapping/map-target-field.png)

此时会显示一个交互式目标架构树，允许您手动遍历目标架构，并为源字段查找相应的目标XDM字段。

![手动映射](../images/ui/mapping/manual-mapping.png)

完成后，选择架构图标以关闭目标架构界面。

![模式树](../images/ui/mapping/schema-tree.png)

#### 计算字段 {#calculated-fields}

计算量度字段允许根据输入架构中的属性创建值。 然后，可以将这些值分配给目标架构中的属性，并提供名称和说明，以便更便于引用。 计算字段的最大长度为4096个字符。

要创建计算字段，请选择 **[!UICONTROL 新字段类型]** 然后选择 **[!UICONTROL 添加计算字段]**

![add-calculated-field](../images/ui/mapping/add-calculated-field.png)

的 **[!UICONTROL 创建计算字段]** 中。 左侧对话框包含计算字段中支持的字段、函数和运算符。 选择一个选项卡以开始向表达式编辑器添加函数、字段或运算符。

| 选项卡 | 描述 |
| --- | ----------- |
| [!UICONTROL 函数] | 函数选项卡列出了可用于转换数据的函数。 要进一步了解可在计算字段中使用的函数，请阅读 [使用数据准备（映射器）函数](../functions.md). |
| [!UICONTROL 字段] | 字段选项卡列出了源架构中可用的字段和属性。 |
| [!UICONTROL 运算符] | 运算符选项卡列出了可用于转换数据的运算符。 |

![选项卡](../images/ui/mapping/tabs.png)

您可以使用中心的表达式编辑器手动添加字段、函数和运算符。 选择编辑器以开始创建表达式。 完成后，选择 **[!UICONTROL 保存]** 以继续。

![create-calculated-field](../images/ui/mapping/create-calculated-field.png)

### 导入映射 {#import}

您可以重复使用现有数据流的映射，以缩短数据摄取的手动配置时间并限制错误。 选择 **[!UICONTROL 导入映射]** 以重复使用现有映射。

![导入映射](../images/ui/mapping/import-mapping.png)

的 [!UICONTROL 导入映射] 窗口，为您提供要从中选择的数据流列表。

选择预览图标以预览所选数据流的映射。

![列表映射](../images/ui/mapping/list-mapping.png)

利用预览窗口，可在导入到数据流之前检查现有映射。 验证映射后，您可以选择 **[!UICONTROL 返回]** 返回数据流列表并检查另一组映射，或者您可以选择 **[!UICONTROL 选择]** 以继续。

![预览映射](../images/ui/mapping/preview-mapping.png)

或者，您也可以从数据流窗口列表中选择要导入的映射。 选择包含要导入的映射的数据流，然后选择 **[!UICONTROL 选择]** 以继续。

![选择映射](../images/ui/mapping/select-mapping.png)

界面会随您导入的映射一起更新。

>[!NOTE]
>
>您建立或ML映射推荐的任何现有映射集将替换为您从现有数据流导入的映射。

![映射导入](../images/ui/mapping/mapping-imported.png)

选择 **[!UICONTROL 预览数据]** 查看从选定数据集映射最多100行示例数据的结果。

![预览数据](../images/ui/mapping/preview-data.png)

在预览期间，标识列将作为第一个字段按优先级排列，因为它是验证映射结果时必需的关键信息。 完成后，选择 **[!UICONTROL 关闭]**.

![预览 — 屏幕](../images/ui/mapping/preview-screen.png)

要删除所有映射字段，请选择 **[!UICONTROL 清除所有映射]**.

![全部清除](../images/ui/mapping/clear-all.png)

### 使用映射界面

Platform会根据您选择的目标架构或数据集，自动为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例，或修复任何复制的映射字段以清除任何错误。

![映射接口](../images/ui/mapping/mapping-interface.png)

在要调整的目标字段中选择灯泡图标。

![mapping-recc](../images/ui/mapping/mapping-recc.png)

的 [!UICONTROL 映射推荐] 出现弹出面板，其中显示了可映射到特定源字段的推荐目标字段列表。 默认情况下，将自动应用第一个推荐。

有时，源架构有多个推荐可用。 发生这种情况时，映射卡会显示最突出的推荐，后跟一个图标，其中包含可用的其他推荐数量。 选择灯泡图标将显示其他推荐的列表。 您可以选中要映射到的推荐旁边的复选框，以选择其中一个替代推荐。

从此处，您可以更改选定的目标字段以修复错误或与用例匹配。

或者，您也可以选择 **[!UICONTROL 手动选择]** 以手动使用交互式目标架构映射树。

![recc-panel](../images/ui/mapping/recc-panel.png)

目标架构映射界面显示在与映射字段相同的视图中，允许您在同一屏幕中修改映射对。 选择适合您的用例或修复错误的目标字段。

![select-target-field](../images/ui/mapping/select-target-field.png)

完成后，选择 **[!UICONTROL 完成]** 以继续。

![完成](../images/ui/mapping/finish.png)

## 后续步骤

通过阅读本文档，您已使用Platform UI中的映射界面成功将CSV文件映射到目标XDM架构。 有关更多信息，请参阅以下文档：

* [数据准备概述](../home.md)
* [源概述](../../sources/home.md)
* [在UI中监视源数据流](../../dataflows/ui/monitor-sources.md)
