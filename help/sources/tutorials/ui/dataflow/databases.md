---
keywords: Experience Platform；主页；热门主题；数据库连接器
solution: Experience Platform
title: 在UI中为数据库源连接配置数据流
topic: overview
type: Tutorial
description: 数据流是从源中检索数据并将其引入平台数据集的计划任务。 本教程提供使用数据库帐户配置新数据流的步骤。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 0%

---


# 在UI中为数据库连接配置数据流

数据流是从源中检索数据并将其引入平台数据集的计划任务。 本教程提供使用数据库帐户配置新数据流的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

此外，本教程要求您已创建数据库帐户。 在[源连接器概述](../../../home.md)中可找到有关在UI中创建不同数据库连接器的列表教程。

## 选择数据

创建数据库帐户后，将显示&#x200B;**[!UICONTROL 选择数据]**&#x200B;步骤，为您提供一个交互式界面来浏览数据库层次结构。

- 界面的左半部分是浏览器，显示您帐户的数据库列表。
- 界面的右半部分允许您预览最多100行数据。

您可以使用页面顶部的&#x200B;**[!UICONTROL 搜索]**&#x200B;选项快速识别要使用的源数据。

>[!NOTE]
>
>搜索源数据选项适用于所有基于表格的源连接器，不包括分析、分类、事件中心和Kinesis连接器。

找到源数据后，选择目录，然后单击&#x200B;**[!UICONTROL 下一步]**。

![select-data](../../../images/tutorials/dataflow/databases/select-data.png)


## 将数据字段映射到XDM模式

出现&#x200B;*映射*&#x200B;步骤，提供交互式界面以将源数据映射到平台数据集。

选择要收录到的入站数据的数据集。 您可以使用现有数据集或创建新数据集。

### 使用现有数据集

要将数据引入现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**，然后单击数据集图标。

![](../../../images/tutorials/dataflow/databases/existing-dataset.png)

出现&#x200B;**[!UICONTROL 选择数据集]**&#x200B;对话框。 找到您要使用的数据集，选择它，然后单击&#x200B;**[!UICONTROL 继续]**。

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### 使用新数据集

要将数据引入新数据集，请选择&#x200B;**[!UICONTROL New dataset]**，并在提供的字段中输入数据集的名称和说明。

可以在&#x200B;**[!UICONTROL 选择模式]**&#x200B;搜索栏中输入模式名称，附加模式字段。 您还可以选择下拉图标以查看现有列表的模式。 或者，您也可以选择&#x200B;**[!UICONTROL 高级搜索]**&#x200B;访问现有模式的屏幕，包括其各自的详细信息。

在此步骤中，您可以为[!DNL Real-time Customer Profile]启用数据集，并创建实体属性和行为的整体视图。 来自所有已启用数据集的数据将包含在[!DNL Profile]中，并在保存数据流时应用更改。

切换&#x200B;**[!UICONTROL 用户档案数据集]**&#x200B;按钮，为[!DNL Profile]启用目标数据集。

![create-new-dataset](../../../images/tutorials/dataflow/databases/new-dataset.png)

出现&#x200B;**[!UICONTROL 选择模式]**&#x200B;对话框。 选择要应用于新数据集的模式，然后单击&#x200B;**[!UICONTROL 完成]**。

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

根据您的需要，您可以选择直接映射字段，或使用映射器函数转换源数据以导出计算值或计算值。 有关模式映射和映射器功能的详细信息，请参阅有关[将CSV数据映射到XDM字段](../../../../ingestion/tutorials/map-a-csv-file.md)的教程。

>[!TIP]
>
>[!DNL Platform] 根据您选择的目标模式或数据集，为自动映射字段提供智能建议。您可以手动调整映射规则以适合您的用例。

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

选择&#x200B;**[!UICONTROL 预览数据]**&#x200B;可查看所选数据集中最多100行样本数据的映射结果。

在该预览中，标识列作为第一字段进行优先级排序，因为它是验证映射结果时必需的关键信息。

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

映射源数据后，选择&#x200B;**[!UICONTROL 关闭]**。

## 计划摄取运行

出现&#x200B;**[!UICONTROL 计划]**&#x200B;步骤，允许您配置摄取计划，以使用配置的映射自动摄取所选源数据。 下表概述了用于计划的不同可配置字段：

| 字段 | 描述 |
| --- | --- |
| 频度 | 可选频率包括`Once`、`Minute`、`Hour`、`Day`和`Week`。 |
| 间隔 | 一个整数，它为所选频率设置间隔。 |
| 开始时间 | UTC时间戳，指示何时设置第一次摄取。 |
| 回填 | 一个布尔值，它确定最初摄取的数据。 如果启用了&#x200B;**[!UICONTROL 回填]**，则指定路径中的所有当前文件将在第一次预定接收期间被摄取。 如果&#x200B;**[!UICONTROL 回填]**&#x200B;被禁用，则只会摄取在第一次摄取运行和开始时间之间加载的文件。 不会摄取在开始时间之前加载的文件。 |
| 增量列 | 具有筛选的源模式字段集类型、日期或时间的选项。 此字段用于区分新数据和现有数据。 增量数据将根据所选列的时间戳被摄取。 |

数据流设计为按计划自动摄取数据。 开始。 然后，设置时间间隔以指定两个流运行之间的周期。 间隔的值应为非零整数，并应设置为大于或等于15。

要设置摄取的开始时间，请调整开始时间框中显示的日期和时间。 或者，也可以选择日历图标以编辑开始时间值。 开始时间必须大于或等于当前UTC时间。

选择&#x200B;**[!UICONTROL 按]**&#x200B;加载增量数据以分配增量列。 此字段区分新数据和现有数据。

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### 设置一次性摄取数据流

要设置一次性摄取，请选择频率下拉箭头，然后选择&#x200B;**[!UICONTROL 一次]**。

>[!TIP]
>
>**[!UICONTROL 在]** 一次 **** 性摄取期间，Interval和Backfillar不可见。

向计划提供适当的值后，选择&#x200B;**[!UICONTROL 下一步]**。

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## 提供数据流详细信息

出现&#x200B;**[!UICONTROL 数据流详细信息]**&#x200B;步骤，允许您命名新数据流并提供有关新数据流的简要说明。

在此过程中，还可以启用&#x200B;**[!UICONTROL 部分摄取]**&#x200B;和&#x200B;**[!UICONTROL 错误诊断]**。 启用&#x200B;**[!UICONTROL 部分摄取]**&#x200B;能够摄取包含错误且达到某个阈值的数据。 启用&#x200B;**[!UICONTROL 部分摄取]**&#x200B;后，拖动&#x200B;**[!UICONTROL 错误阈值%]**&#x200B;拨号以调整批的错误阈值。 或者，也可以通过选择输入框手动调整阈值。 有关详细信息，请参阅[部分批摄取概述](../../../../ingestion/batch-ingestion/partial.md)。
为数据流提供值并选择**[!UICONTROL Next]**。

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## 查看数据流

出现&#x200B;**[!UICONTROL Review]**&#x200B;步骤，允许您在创建新数据流之前对其进行查看。 详细信息按以下类别分组：

- **[!UICONTROL 连接]**:显示源类型、所选源文件的相关路径以及该源文件中的列数。
- **[!UICONTROL 分配数据集和地图字段]**:显示接收源数据的数据集，包括数据集附带的模式。
- **[!UICONTROL 计划]**:显示摄取计划的活动周期、频率和间隔。

查看数据流后，单击&#x200B;**[!UICONTROL 完成]**&#x200B;并允许一段时间创建数据流。

![](../../../images/tutorials/dataflow/databases/review.png)

## 监视数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的详细信息，请参阅有关UI](../monitor.md)中[监视帐户和数据流的教程。

## 删除数据流

您可以删除不再需要的或使用&#x200B;**[!UICONTROL Dataflows]**&#x200B;工作区中可用的&#x200B;**[!UICONTROL Delete]**&#x200B;函数创建错误的数据流。 有关如何删除数据流的详细信息，请参阅有关在UI](../delete.md)中删除数据流的教程。[

## 后续步骤

通过遵循本教程，您成功创建了一个数据流以从外部数据库导入数据并获得了有关监视数据集的洞察。 现在，下游[!DNL Platform]服务（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用传入数据。 有关更多详细信息，请参阅以下文档:

- [[!DNL Real-time Customer Profile] 概述](../../../../profile/home.md)
- [[!DNL Data Science Workspace] 概述](../../../../data-science-workspace/home.md)

## 附录

以下部分提供了有关使用源连接器的其他信息。

### 禁用数据流

创建数据流时，它会立即变为活动状态，并根据给定的计划接收数据。 您可以按照以下说明随时禁用活动数据流。

在&#x200B;**[!UICONTROL 源]**&#x200B;工作区中，选择&#x200B;**[!UICONTROL 数据流]**&#x200B;选项卡。 接下来，选择要禁用的数据流。

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

屏幕的右侧显示&#x200B;**[!UICONTROL 属性]**&#x200B;列，包括&#x200B;**[!UICONTROL 已启用]**&#x200B;切换按钮。 选择切换以禁用数据流。 在禁用数据流后，可以使用相同的切换重新启用数据流。

![](../../../images/tutorials/dataflow/databases/disable.png)

### 为[!DNL Profile]人口激活入站数据

源连接器的入站数据可用于丰富和填充[!DNL Real-time Customer Profile]数据。 有关填充[!DNL Real-time Customer Profile]数据的详细信息，请参阅关于[用户档案填充](../profile.md)的教程。