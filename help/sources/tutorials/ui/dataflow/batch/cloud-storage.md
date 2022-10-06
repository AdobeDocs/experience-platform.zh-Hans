---
keywords: Experience Platform；主页；热门主题；数据流；数据流
title: 在UI中配置数据流以从云存储源中摄取批量数据
description: 本教程提供了有关如何在UI中配置新数据流以从云存储源摄取批量数据的步骤
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 0910de76d817eea7c7c3cb2b988d81268b3e5812
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 0%

---

# 在UI中配置数据流以从云存储源中摄取批量数据

本教程提供了有关如何配置数据流以将批量数据从云存储源引入Adobe Experience Platform的步骤。

## 快速入门

>[!NOTE]
>
>要创建数据流以从云存储中引入批处理数据，您必须已经具有对经过身份验证的云存储源的访问权限。 如果您没有访问权限，请转到 [源概述](../../../../home.md#cloud-storage) 有关可为其创建帐户的云存储源列表。

本教程需要对Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

### 支持的文件格式

批量数据的云存储源支持以下文件格式进行摄取：

* 分隔符分隔值(DSV):任何单字符值都可用作DSV格式数据文件的分隔符。
* [!DNL JavaScript Object Notation] (JSON):JSON格式的数据文件必须符合XDM。
* [!DNL Apache Parquet]:Parquet格式的数据文件必须符合XDM。
* 压缩文件：JSON和分隔文件可压缩为： `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`和 `tar`.

## 添加数据

创建云存储帐户后， **[!UICONTROL 添加数据]** 此时会显示步骤，其中提供了一个界面，用于浏览云存储文件层次结构并选择要引入平台的文件夹或特定文件。

* 界面的左侧是目录浏览器，显示云存储文件层次结构。
* 界面的右侧部分允许您从兼容的文件夹或文件中预览多达100行的数据。

![](../../../../images/tutorials/dataflow/cloud-batch/select-data.png)

选择根文件夹以访问文件夹层次结构。 从此处，您可以选择单个文件夹以递归摄取该文件夹中的所有文件。 摄取整个文件夹时，必须确保该文件夹中的所有文件共享相同的数据格式和架构。

![](../../../../images/tutorials/dataflow/cloud-batch/folder-directory.png)

选择文件夹后，右侧界面将更新为预览选定文件夹中第一个文件的内容和结构。

![](../../../../images/tutorials/dataflow/cloud-batch/select-folder.png)

在此步骤中，您可以对数据进行多项配置，然后再继续。 首先，选择 **[!UICONTROL 数据格式]** 然后，在显示的下拉面板中为文件选择适当的数据格式。

下表显示了支持的文件类型的相应数据格式：

| 文件类型 | 数据格式 |
| --- | --- |
| CSV | [!UICONTROL 分隔] |
| JSON | [!UICONTROL JSON] |
| 镶木 | [!UICONTROL XDM Parquet] |

![](../../../../images/tutorials/dataflow/cloud-batch/data-format.png)

### 选择列分隔符

配置数据格式后，您可以在摄取分隔文件时设置列分隔符。 选择 **[!UICONTROL 分隔符]** 选项，然后从下拉菜单中选择分隔符。 菜单显示最常用的分隔符选项，包括逗号(`,`)、选项卡(`\t`)和管道(`|`)。

![](../../../../images/tutorials/dataflow/cloud-batch/delimiter.png)

如果您希望使用自定义分隔符，请选择 **[!UICONTROL 自定义]** 并在弹出输入栏中输入您选择的单字符分隔符。

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

### 摄取压缩文件

您还可以通过指定压缩类型来摄取压缩的JSON或分隔文件。

在 [!UICONTROL 选择数据] 步骤，选择要摄取的压缩文件，然后选择其相应的文件类型以及它是否符合XDM。 接下来，选择 **[!UICONTROL 压缩类型]** 然后为源数据选择适当的压缩文件类型。

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

要将特定文件引入平台，请选择一个文件夹，然后选择要摄取的文件。 在此步骤中，您还可以使用文件名旁边的预览图标预览给定文件夹中其他文件的文件内容。

完成后，选择 **[!UICONTROL 下一个]**.

![](../../../../images/tutorials/dataflow/cloud-batch/select-file.png)

## 提供数据流详细信息

的 [!UICONTROL 数据流详细信息] 页面允许您选择是要使用现有数据集还是新数据集。 在此过程中，您还可以配置要摄取到配置文件的数据，并启用如下设置 [!UICONTROL 错误诊断], [!UICONTROL 部分摄取]和 [!UICONTROL 警报].

![](../../../../images/tutorials/dataflow/cloud-batch/dataflow-detail.png)

### 使用现有数据集

要将数据摄取到现有数据集，请选择 **[!UICONTROL 现有数据集]**. 您可以使用 [!UICONTROL 高级搜索] 选项，或者通过在下拉菜单中滚动浏览现有数据集列表来配置。 选择数据集后，请为数据流提供名称和描述。

![](../../../../images/tutorials/dataflow/cloud-batch/existing.png)

### 使用新数据集

要摄取到新数据集，请选择 **[!UICONTROL 新数据集]** 然后，提供输出数据集名称和可选描述。 接下来，使用 [!UICONTROL 高级搜索] 选项或通过滚动下拉菜单中的现有架构列表来迁移。 选择架构后，请为数据流提供名称和描述。

![](../../../../images/tutorials/dataflow/cloud-batch/new.png)

### 启用配置文件和错误诊断

接下来，选择 **[!UICONTROL 配置文件数据集]** 切换为“配置文件”启用数据集。 这允许您创建实体属性和行为的整体视图。 所有启用了配置文件的数据集中的数据都将包含在配置文件中，并且会在保存数据流时应用更改。

[!UICONTROL 错误诊断] 为数据流中发生的任何错误记录启用详细的错误消息生成，而 [!UICONTROL 部分摄取] 允许您摄取包含错误的数据，最多可达您手动定义的特定阈值。 请参阅 [部分批量摄取概述](../../../../../ingestion/batch-ingestion/partial.md) 以了解更多信息。

![](../../../../images/tutorials/dataflow/cloud-batch/ingestion-configs.png)

### 启用警报

您可以启用警报以接收有关数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅源警报](../../alerts.md).

完成向数据流提供详细信息后，选择 **[!UICONTROL 下一个]**.

![](../../../../images/tutorials/dataflow/cloud-batch/alerts.png)

## 将数据字段映射到XDM架构

的 [!UICONTROL 映射] 此时会显示步骤，为您提供一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关使用映射器界面和计算字段的完整步骤，请参阅 [数据准备UI指南](../../../../../data-prep/ui/mapping.md).

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![](../../../../images/tutorials/dataflow/cloud-batch/mapping.png)

## 计划摄取运行

>[!IMPORTANT]
>
>强烈建议在使用 [FTP源](../../../../connectors/cloud-storage/ftp.md).

的 [!UICONTROL 计划] 步骤，允许您配置摄取计划以使用配置的映射自动摄取选定的源数据。 默认情况下，计划设置为 `Once`. 要调整摄取频率，请选择 **[!UICONTROL 频率]** ，然后从下拉菜单中选择一个选项。

>[!TIP]
>
>在一次性摄取期间，间隔和回填不可见。

![调度](../../../../images/tutorials/dataflow/cloud-batch/scheduling.png)

如果将摄取频度设置为 `Minute`, `Hour`, `Day`或 `Week`，则必须设置一个间隔，以在每次摄取之间建立一个设置的时间范围。 例如，摄取频度设置为 `Day` 和间隔设置为 `15` 意味着您的数据流计划每15天摄取一次数据。

在此步骤中，您还可以启用 **回填** 并为数据的增量摄取定义一列。 回填用于摄取历史数据，而您为增量摄取定义的列允许将新数据与现有数据区分开。

有关计划配置的更多信息，请参阅下表。

| 字段 | 描述 |
| --- | --- |
| 频度 | 发生摄取的频率。 可选频率包括 `Once`, `Minute`, `Hour`, `Day`和 `Week`. |
| 间隔 | 一个整数，用于设置所选频率的间隔。 间隔的值应为非零整数，并应设置为大于或等于15。 |
| 开始时间 | UTC时间戳，指示何时设置进行第一次摄取。 开始时间必须大于或等于当前UTC时间。 |
| 回填 | 一个布尔值，用于确定最初摄取的数据。 如果启用了回填，则在首次计划摄取期间将摄取指定路径中的所有当前文件。 如果禁用回填，则只会摄取在首次摄取运行到开始时间之间加载的文件。 不会摄取在开始时间之前加载的文件。 |

>[!NOTE]
>
>对于批量摄取，每个后续数据流都会根据文件的源文件选择要摄取的文件 **上次修改时间** 时间戳。 这意味着批处理数据流从源中选择新文件或自上次流程运行以来已修改的文件。 此外，您必须确保在文件上传和计划流运行之间有足够的时间跨度，因为在计划流运行时间之前未完全上传到云存储帐户的文件可能无法提取以用于摄取。

配置完摄取计划后，选择 **[!UICONTROL 下一个]**.

![](../../../../images/tutorials/dataflow/cloud-batch/scheduling-configs.png)

## 查看数据流

的 **[!UICONTROL 审阅]** 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。
* **[!UICONTROL 计划]**:显示摄取计划的活动期、频率和间隔。

审核数据流后，单击 **[!UICONTROL 完成]** 并为创建数据流留出一些时间。

![](../../../../images/tutorials/dataflow/cloud-batch/review.png)


## 后续步骤

通过阅读本教程，您成功创建了一个数据流以从外部云存储中导入数据，并获得了有关监控数据集的洞察信息。 要了解有关创建数据流的更多信息，您可以通过观看以下视频来补充您的学习。 此外，现在下游可以使用传入数据 [!DNL Platform] 诸如 [!DNL Real-time Customer Profile] 和 [!DNL Data Science Workspace]. 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-time Customer Profile]概述](../../../../../profile/home.md)
* [[!DNL Data Science Workspace]概述](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> 的 [!DNL Platform] 以下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## 附录

以下部分提供了有关使用源连接器的其他信息。

## 监控数据流

创建数据流后，您可以监控通过其摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监控数据流的更多信息，请访问 [监控UI中的帐户和数据流](../../monitor.md).

## 更新数据流

要更新数据流计划、映射和常规信息的配置，请访问 [在UI中更新源数据流](../../update-dataflows.md)

## 删除数据流

您可以删除不再需要或使用错误创建的数据流 **[!UICONTROL 删除]** 函数 **[!UICONTROL 数据流]** 工作区。 有关如何删除数据流的更多信息，请访问 [删除UI中的数据流](../../delete.md).