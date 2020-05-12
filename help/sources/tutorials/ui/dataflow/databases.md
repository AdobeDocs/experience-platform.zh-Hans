---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中为数据库连接器配置数据流
topic: overview
translation-type: tm+mt
source-git-commit: 415b59fc3fa20c09372549e92571c1b41006e540
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 0%

---


# 在UI中为数据库连接器配置数据流

数据流是从源中检索数据并将其引入平台数据集的计划任务。 本教程提供使用数据库基础连接器配置新数据流的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [体验数据模型(XDM)系统](../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
- [实时客户用户档案](../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

此外，本教程要求您已创建数据库连接器。 有关在UI中创建不同数据库连接器的一列表教程，请参阅源 [连接器概述](../../../home.md)。

## 选择数据

创建数据库连接器后，将显 *[!UICONTROL 示“选择数据]* ”步骤，为您提供一个交互界面来浏览数据库层次结构。

- 界面的左半部分是浏览器，显示您帐户的数据库列表。
- 界面的右半部分允许您预览最多100行数据。

选择要使用的数据库，然后单击“下 **[!UICONTROL 一步]**”。

![](../../../images/tutorials/dataflow/databases/add-data.png)

## 将数据字段映射到XDM模式

将显 *示“映射* ”步骤，提供一个交互界面，将源数据映射到平台数据集。

选择要收录到的入站数据的数据集。 您可以使用现有数据集或创建新数据集。

### 使用现有数据集

要将数据引入现有数据集，请选择 **[!UICONTROL 现有数据集]**，然后单击数据集图标。

![](../../../images/tutorials/dataflow/databases/existing-dataset.png)

此时将 *[!UICONTROL 显示“选择数据集]* ”对话框。 找到您要使用的数据集，选择它，然后单击“继 **[!UICONTROL 续”]**。

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### 使用新数据集

要将数据引入新数据集，请选 **[!UICONTROL 择新数据集]** ，并在提供的字段中输入数据集的名称和说明。

您可以在“选择模式”搜索栏中键入模式名 **[!UICONTROL 称来附加模式]** 字段。 您还可以选择下拉图标以查看现有列表的模式。 或者，也可以选择“高 **[!UICONTROL 级搜索]** ”以显示现有模式的屏幕，包括其各自的详细信息。

![](../../../images/tutorials/dataflow/databases/new-dataset.png)

出现*[!UICONTROL 选择模式] 对话框。 选择要应用于新数据集的模式，然后单击 **[!UICONTROL 完成]**。

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

根据您的需要，您可以选择直接映射字段，或使用映射器函数转换源数据以导出计算值或计算值。 有关数据映射和映射器功能的详细信息，请参阅将CSV数据 [映射到XDM模式字段的教程](../../../../ingestion/tutorials/map-a-csv-file.md)。

映射源数据后，单击“下 **[!UICONTROL 一步]**”。

![](../../../images/tutorials/dataflow/databases/mapping.png)

## 计划摄取运行

此时 *[!UICONTROL 将显示]* “计划”步骤，允许您配置摄取计划，以使用配置的映射自动摄取所选源数据。 下表概述了用于计划的不同可配置字段：

| 字段 | 描述 |
| --- | --- |
| 频率 | 可选频率包括分钟、小时、天和周。 |
| 间隔 | 一个整数，它为所选频率设置间隔。 |
| 开始时间 | UTC时间戳，将对其进行第一次摄取。 |
| 回填 | 一个布尔值，它确定最初摄取的数据。 如果 *启用* “回填”，则指定路径中的所有当前文件将在第一次预定接收期间被摄取。 如果 *禁用* “回填”，则只会摄取在首次摄取和开始时间之间加 *载的文件* 。 在开始时间之 *前加载的文* 件将不会被摄取。 |
| 增量列 | 具有筛选的源模式字段集类型、日期或时间的选项。 此字段用于区分新数据和现有数据。 增量数据将根据所选列的时间戳被摄取。 |

数据流设计为按计划自动摄取数据。 如果您希望通过此工作流只收录一次，可以将 **[!UICONTROL Frequency]** （频率）配置为“Day”，并为Interval（间隔）应用一个非常大的 **[!UICONTROL 数字]**，如10000或类似。

为计划提供值，然后选择“下 **[!UICONTROL 一步]**”。

![](../../../images/tutorials/dataflow/databases/schedule.png)

## 命名数据流

出现 *[!UICONTROL 数据流详细信]* 息步骤，您必须在其中为数据流提供名称和可选说明。 完成后 **[!UICONTROL 选择]** “下一步”。

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## 查看数据流

此时 *[!UICONTROL 会出现]* “审阅”步骤，允许您在创建新数据流之前对其进行查看。 详细信息按以下类别分组：

- *连接*: 显示源类型、所选源文件的相关路径以及该源文件中的列数。
- *分配数据集和地图字段*: 显示接收源数据的数据集，包括数据集附带的模式。
- *计划*: 显示摄取计划的活动周期、频率和间隔。

查看数据流后，单击 **[!UICONTROL 完成]** ，并允许一段时间创建数据流。

![](../../../images/tutorials/dataflow/databases/review.png)

## 监视数据流

创建数据流后，您可以监视通过它摄取的数据。 有关如何监视数据流的详细信息，请参阅有关帐户和数 [据流的教程](../monitor.md)。

## 后续步骤

通过遵循本教程，您成功创建了一个数据流以从外部数据库导入数据并获得了有关监视数据集的洞察。 现在，下游平台服务(如实时客户用户档案和数据科学工作区)可以使用传入数据。 有关更多详细信息，请参阅以下文档:

- [实时客户用户档案概述](../../../../profile/home.md)
- [数据科学工作区概述](../../../../data-science-workspace/home.md)

## 附录

以下部分提供了有关使用源连接器的其他信息。

### 禁用数据流

创建数据流时，它会立即变为活动状态，并根据给定的计划接收数据。 您可以按照以下说明随时禁用活动数据流。

在“源 *[!UICONTROL ”工作]* 区中，选择“数 **[!UICONTROL 据流]** ”选项卡。 接下来，选择要禁用的数据流。

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

“ *属性* ”列显示在屏幕的右侧，包括“已启用” **[!UICONTROL 切换按]** 钮。 选择切换以禁用数据流。 在禁用数据流后，可以使用相同的切换重新启用数据流。

![](../../../images/tutorials/dataflow/databases/disable.png)

### 为用户档案填充激活入站数据

来自源连接器的入站数据可用于丰富和填充实时客户用户档案数据。 有关填充实际客户用户档案数据的更多信息，请参阅关于用户档案填充 [的教程](../profile.md)。