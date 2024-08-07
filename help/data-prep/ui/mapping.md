---
keywords: Experience Platform；主页；热门主题；映射csv；映射csv文件；将csv文件映射到xdm；将csv映射到xdm；ui指南；映射器；映射；数据准备；数据准备；准备数据；
title: 数据准备UI指南
description: 本文档提供了有关如何在Platform UI中使用数据准备功能将CSV文件映射到XDM架构的说明。
exl-id: fafa4aca-fb64-47ff-a97d-c18e58ae4dae
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 0%

---

# 数据准备UI指南

本文档提供了有关如何在Adobe Experience Platform用户界面中使用数据准备功能将CSV文件映射到XDM架构的说明。

## 快速入门

本教程需要您实际了解以下平台组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../xdm/home.md)： Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [身份服务](../../identity-service/home.md)：通过跨设备和系统桥接身份，更好地了解个人客户及其行为。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [源](../../sources/home.md)：Experience Platform允许从各种源摄取数据，同时允许您使用Platform服务来构建、标记和增强传入数据。

## 数据流详细信息

>[!TIP]
>
>您可以通过从源目录中选择任意源来访问数据流详细信息。 有关详细信息，请参阅[源概述](../../sources/home.md)。

在将CSV数据映射到XDM架构之前，必须首先建立数据流的详细信息。

[!UICONTROL 数据流详细信息]页面允许您选择是将CSV数据摄取到现有目标数据集，还是新目标数据集。 现有数据集附带预建的目标架构可将您的数据映射到，而新数据集要求您选择现有架构或创建新架构以将您的数据映射到。

### 使用现有目标数据集

要将CSV数据摄取到现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**。 您可以使用[!UICONTROL 高级搜索]选项或通过滚动下拉菜单中的现有数据集列表来检索现有数据集。

选择数据集后，为数据流提供名称和可选描述。

在此过程中，您还可以启用[!UICONTROL 错误诊断]和[!UICONTROL 部分摄取]。 [!UICONTROL 错误诊断]允许为数据流中发生的任何错误记录生成详细的错误消息，而[!UICONTROL 部分摄取]允许您摄取包含错误的数据，摄取阈值为您手动定义的某个阈值。 有关详细信息，请参阅[部分批次摄取概述](../../ingestion/batch-ingestion/partial.md)。

![现有数据集](../images/ui/mapping/existing-dataset.png)

### 使用新的目标数据集

要将CSV数据摄取到新数据集中，请选择&#x200B;**[!UICONTROL 新数据集]**，然后提供输出数据集名称和可选描述。 接下来，使用[!UICONTROL 高级搜索]选项或通过滚动下拉菜单中的现有架构列表来选择要映射到的架构。

选择架构后，为数据流提供名称和可选描述，然后为数据流应用所需的[!UICONTROL 错误诊断]和[!UICONTROL 部分摄取]设置。 完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![新数据集](../images/ui/mapping/new-dataset.png)

## 选择数据

此时将显示[!UICONTROL 选择数据]步骤，该步骤为您提供了一个用于上载本地文件并预览其结构和内容的界面。 选择&#x200B;**[!UICONTROL 选择文件]**&#x200B;以从本地系统上传CSV文件。 或者，您也可以将要上载的CSV文件拖放到[!UICONTROL 拖放文件]面板。

>[!TIP]
>
>本地文件上传当前仅支持CSV文件。 每个文件的最大文件大小为1 GB。

![choose-files](../images/ui/mapping/choose-files.png)

上传文件后，预览界面会更新以显示文件的内容和结构。

![preview-sample-data](../images/ui/mapping/preview-sample-data.png)

根据您的文件，可以为源数据选择列分隔符，例如制表符、逗号、管道或自定义列分隔符。 选择&#x200B;**[!UICONTROL 分隔符]**&#x200B;下拉箭头，然后从菜单中选择相应的分隔符。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![分隔符](../images/ui/mapping/delimiter.png)

## 映射

**[!UICONTROL 映射]**&#x200B;界面为您提供了一个全面的工具，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

![map-csv-to-xdm](../images/ui/mapping/map-csv-to-xdm.png)

### 了解映射界面 {#mapping-interface}

映射界面包括一个功能板，该功能板提供有关摄取工作流上下文中映射字段的运行状况的信息。 仪表板显示有关映射字段的以下详细信息：

| 属性 | 描述 |
| --- | --- |
| [!UICONTROL 映射的字段] | 显示已映射到目标XDM字段的源字段总数，无论是否存在错误。 |
| [!UICONTROL 必填字段] | 显示所需映射字段的数量。 |
| [!UICONTROL 标识字段] | 显示定义为标识的映射字段总数。 这些映射字段由指纹图标表示。 |
| [!UICONTROL 个错误] | 显示错误映射字段的数量。 |

![顶部面板](../images/ui/mapping/top-panel.png)

映射界面还提供了选项面板，您可以从中选择以更好地在映射字段中进行交互或过滤。

![秒面板](../images/ui/mapping/second-panel.png)

要搜索特定的映射集，请选择&#x200B;**[!UICONTROL 搜索源字段]**&#x200B;并输入要隔离的源数据的名称。

![搜索](../images/ui/mapping/search.png)

选择&#x200B;**[!UICONTROL 所有源字段]**&#x200B;可查看包含筛选选项的下拉菜单，以更好地缩小映射界面的视图。

筛选选项包括：

| Source字段 | 描述 |
| --- | --- |
| [!UICONTROL 所有源字段] | 此选项显示源架构的所有源字段。 默认显示此选项。 |
| [!UICONTROL 必填字段] | 此选项筛选源架构以仅显示完成映射所需的字段。 |
| [!UICONTROL 标识字段] | 此选项筛选源架构以仅显示标记为标识的字段。 |
| [!UICONTROL 映射的字段] | 此选项筛选源架构以仅显示已映射的字段。 |
| [!UICONTROL 未映射的字段] | 此选项筛选源架构以仅显示尚未映射的字段。 |
| 带有推荐的[!UICONTROL 字段] | 此选项筛选源架构以仅显示包含映射推荐的字段。 |

选择&#x200B;**[!UICONTROL 有错误的字段]**&#x200B;以查看所有有错误的映射字段。

![筛选器](../images/ui/mapping/filter.png)

将出现错误映射字段的隔离视图，允许您通过智能映射建议或手动映射树解决错误。

![个有错误的字段](../images/ui/mapping/fields-with-errors.png)

### 添加新字段类型

您可以通过选择&#x200B;**[!UICONTROL 新字段类型]**&#x200B;来添加新的映射字段或计算字段。

#### 新建映射字段

要添加新映射字段，请选择&#x200B;**[!UICONTROL 新字段类型]**，然后从出现的下拉菜单中选择&#x200B;**[!UICONTROL 添加新字段]**。

![add-new-field](../images/ui/mapping/add-new-field.png)

接下来，从显示的源架构树中选择要添加的源字段，然后选择&#x200B;**[!UICONTROL 选择]**。

![select-new-field](../images/ui/mapping/select-new-field.png)

映射界面将使用您选择的源字段和空的目标字段进行更新。 选择&#x200B;**[!UICONTROL 映射目标字段]**&#x200B;以开始将新的源字段映射到其相应的目标XDM字段。

![map-target-field](../images/ui/mapping/map-target-field.png)

此时会显示交互式目标架构树，允许您手动遍历目标架构并找到适用于源字段的相应目标XDM字段。

![手动映射](../images/ui/mapping/manual-mapping.png)

完成后，选择架构图标以关闭目标架构界面。

![架构树](../images/ui/mapping/schema-tree.png)

#### 计算字段 {#calculated-fields}

计算字段允许根据输入架构中的属性创建值。 然后，可以将这些值分配给目标架构中的属性，并提供名称和描述以便更轻松地引用。 计算字段的最大长度为4096个字符。

要创建计算字段，请选择&#x200B;**[!UICONTROL 新字段类型]**，然后选择&#x200B;**[!UICONTROL 添加计算字段]**

![添加计算字段](../images/ui/mapping/add-calculated-field.png)

此时将显示&#x200B;**[!UICONTROL 创建计算字段]**&#x200B;面板。 左侧对话框包含计算字段中支持的字段、函数和运算符。 选择其中一个选项卡，开始向表达式编辑器添加函数、字段或运算符。

| 选项卡 | 描述 |
| --- | ----------- |
| [!UICONTROL 函数] | 函数选项卡列出了可用于转换数据的函数。 若要了解有关可在计算字段中使用的函数的更多信息，请阅读有关[使用数据准备（映射器）函数](../functions.md)的指南。 |
| [!UICONTROL 字段] | 字段选项卡列出了源架构中可用的字段和属性。 |
| [!UICONTROL 操作员] | 运算符选项卡列出了可用于转换数据的运算符。 |

![选项卡](../images/ui/mapping/tabs.png)

您可以使用位于中心的表达式编辑器手动添加字段、函数和运算符。 选择编辑器以开始创建表达式。 完成后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以继续。

![创建计算字段](../images/ui/mapping/create-calculated-field.png)

### 导入映射 {#import}

您可以重用现有数据流的映射，以减少数据摄取的手动配置时间并限制错误。 选择&#x200B;**[!UICONTROL 导入映射]**&#x200B;以重用现有映射。

![导入映射](../images/ui/mapping/import-mapping.png)

出现[!UICONTROL 导入映射]窗口，为您提供可从中进行选择的数据流列表。

选择预览图标以预览所选数据流的映射。

![列表映射](../images/ui/mapping/list-mapping.png)

预览窗口允许您在导入到数据流之前检查现有映射。 验证映射后，可以选择&#x200B;**[!UICONTROL 返回]**&#x200B;以返回到数据流列表并检查另一组映射，也可以选择&#x200B;**[!UICONTROL 选择]**&#x200B;以继续。

![预览映射](../images/ui/mapping/preview-mapping.png)

或者，您可以从数据流窗口列表中选择要导入的映射。 选择包含要导入的映射的数据流，然后选择&#x200B;**[!UICONTROL 选择]**&#x200B;以继续。

![选择 — 映射](../images/ui/mapping/select-mapping.png)

界面会随着您导入的映射而更新。

>[!NOTE]
>
>建立或ML映射建议的任何现有映射集将由从现有数据流导入的映射替换。

![映射已导入](../images/ui/mapping/mapping-imported.png)

选择&#x200B;**[!UICONTROL 预览数据]**&#x200B;以查看所选数据集中最多100行示例数据的映射结果。

![预览数据](../images/ui/mapping/preview-data.png)

在预览期间，标识列被优先指定为第一个字段，因为它是验证映射结果时所需的关键信息。 完成后，选择&#x200B;**[!UICONTROL 关闭]**。

![预览屏幕](../images/ui/mapping/preview-screen.png)

要删除所有映射字段，请选择&#x200B;**[!UICONTROL 清除所有映射]**。

![全部清除](../images/ui/mapping/clear-all.png)

### 使用映射接口

Platform会根据您选择的目标架构或数据集，自动为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例，也可以修复任何重复的映射字段以清除任何错误。

![mapping-interface](../images/ui/mapping/mapping-interface.png)

在要调整的目标字段中选择灯泡图标。

![mapping-recc](../images/ui/mapping/mapping-recc.png)

此时将显示[!UICONTROL 映射推荐]弹出面板，其中显示可映射到特定源字段的推荐目标字段列表。 默认情况下，会自动应用第一个推荐。

有时，源架构有多个推荐可用。 发生这种情况时，映射卡片会显示最显眼的推荐，后面是一个图标，其中包含可用的其他推荐数。 选择灯泡图标将显示其他建议的列表。 通过选中要映射到的推荐旁边的复选框，您可以选择替代推荐之一。

在此处，您可以更改所选目标字段以修复错误或匹配您的用例。

或者，您也可以选择&#x200B;**[!UICONTROL 手动选择]**&#x200B;以手动使用交互式目标架构映射树。

![recc-panel](../images/ui/mapping/recc-panel.png)

目标架构映射界面与映射字段显示在同一视图中，允许您在同一屏幕中修改映射对。 选择适合您的用例的目标字段或修复您的错误。

![select-target-field](../images/ui/mapping/select-target-field.png)

完成后，选择&#x200B;**[!UICONTROL 完成]**&#x200B;以继续。

![完成](../images/ui/mapping/finish.png)

## 后续步骤

通过阅读本文档，您已使用Platform UI中的映射界面成功将CSV文件映射到目标XDM架构。 有关详细信息，请参阅以下文档：

* [数据准备概述](../home.md)
* [源概述](../../sources/home.md)
* [在UI中监视源数据流](../../dataflows/ui/monitor-sources.md)
