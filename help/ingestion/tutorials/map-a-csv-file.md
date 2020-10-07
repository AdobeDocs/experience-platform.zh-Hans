---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: 将CSV文件映射到XDM模式
topic: tutorial
type: Tutorial
description: 本教程介绍如何使用Adobe Experience Platform用户界面将CSV文件映射到XDM模式。
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 1%

---


# 将CSV文件映射到XDM模式

要将CSV数据引入 [!DNL Adobe Experience Platform]其中，必须将数据映射 [!DNL Experience Data Model] 到(XDM)模式。 本教程介绍如何使用用户界面将CSV文件映射到 [!DNL Platform] XDM模式。

此外，本教程的附录还提供了有关使用映射函数的更 [多信息](#mapping-functions)。

## 入门指南

本教程需要对以下组件有一个有效的了解 [!DNL Platform]:

- [[!DNL体验数据模型（XDM系统）]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。
- [[!DNL批量摄取]](../batch-ingestion/overview.md):从用户提供的 [!DNL Platform] 数据文件中摄取数据的方法。

本教程还要求您已创建数据集以将CSV数据引入。 有关在UI中创建数据集的步骤，请参阅数 [据摄取教程](./ingest-batch-data.md)。

## 选择目标

登录到 [[!DNLAdobe Experience Platform]](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏中选]** 择工作流 **[!UICONTROL ，以访问工作流工]** 作区。

从工作流 **[!UICONTROL 屏幕]** ，选择数 **[!UICONTROL 据摄取部分下的]** “将CSV映射 **[!UICONTROL 到XDM模式]** ”，然后选 ****&#x200B;择启动。

![](../images/tutorials/map-a-csv-file/workflows.png)

将显 **[!UICONTROL 示将CSV映射到XDM模式]** ，从目标步骤 **[!UICONTROL 开始]** 。 选择要收录到的入站数据的数据集。 您可以使用现有数据集或创建新数据集。

**使用现有数据集**

要将CSV数据引入现有数据集，请选择“使 **[!UICONTROL 用现有数据集]**”。 您可以使用搜索函数或通过滚动面板中现有数据集的列表来检索现有数据集。

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

要将CSV数据引入新数据集，请选择 **[!UICONTROL 创建新数据集]** ，并在提供的字段中输入数据集的名称和说明。 通过使用搜索函数或滚动模式提供的列表来选择模式。 选择 **[!UICONTROL 下一]** 步以继续。

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 添加数据

将出 **[!UICONTROL 现添加数]** 据步骤。 将CSV文件拖放到提供的空间中，或选择“选 **[!UICONTROL 择文件]** ”以手动输入CSV文件。

![](../images/tutorials/map-a-csv-file/add-data.png)

上载 **[!UICONTROL 文件后]** ，将显示“示例数据”部分，其中显示前十行数据。 确认数据已按预期上传后，选择“下 **[!UICONTROL 一步]**”。

![](../images/tutorials/map-a-csv-file/sample-data.png)

## 将CSV字段映射到XDM模式字段

将出 **[!UICONTROL 现]** “映射”步骤。 CSV文件的列列列在源字段 **[!UICONTROL 下]**，其对应的XDM模式字段列在 **[!UICONTROL 目标字段下]**。 未选择的目标字段以红色列出。 您可以使用筛选器字段选项缩小可用源字段的列表。

>[!TIP]
>
>[!DNL Platform] 根据您选择的目标模式或数据集，为自动映射字段提供智能建议。 您可以手动调整映射规则以适合您的用例。

要将CSV列映射到XDM字段，请选择该列的相应模式字段旁的目标图标。

![](../images/tutorials/map-a-csv-file/mapping.png)

将出 **[!UICONTROL 现“选择模式]** ”字段窗口。 在此，您可以导航XDM模式的结构，并找到要将CSV列映射到的字段。 单击XDM字段以将其选中，然后单击“ **[!UICONTROL 选择]**”。

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

完成其余未映射源字段的步骤后，“映射”屏 **[!UICONTROL 幕将重新显示]** ，选定的XDM字段现在显示在“ **[!UICONTROL 目标”字段下]**。

![](../images/tutorials/map-a-csv-file/field-mapped.png)

在映射字段时，您还可以包含根据输入源字段计算值的函数。 有关详细 [信息](#mapping-functions) ，请参阅附录中的映射函数部分。

### 添加计算字段

计算字段允许根据输入模式中的属性创建值。 然后，可将这些值分配给目标模式中的属性，并提供名称和说明以便更轻松地引用。

选择“添 **[!UICONTROL 加计算字段]** ”按钮以继续。

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

将出 **[!UICONTROL 现“创建计算字段]** ”面板。 左对话框包含计算字段中支持的字段、函数和运算符。 选择一个选项卡以开始向表达式编辑器添加函数、字段或运算符。

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 选项卡 | 描述 |
| --------- | ----------- |
| 字段 | “字段”选项卡列表源模式中可用的字段和属性。 |
| 函数 | 函数选项卡列表可用于转换数据的函数。 |
| 运算符 | “运算符”选项卡列表可用于转换数据的运算符。 |

您可以使用中心的表达式编辑器手动添加字段、函数和运算符。 选择要开始创建表达式的编辑器。

![](../images/tutorials/map-a-csv-file/expression-editor.png)

选择 **[!UICONTROL 保存]** ，以继续。

映射屏幕将随新创建的源字段重新显示。 应用相应的目标字段并选 **[!UICONTROL 择]** “完成”以完成映射。

![](../images/tutorials/map-a-csv-file/new-field.png)

## 监视数据流

映射和创建CSV文件后，您可以监视通过它摄取的数据。 有关监视数据流的详细信息，请参阅有关监视流数据 [流的教程](../../ingestion/quality/monitor-data-flows.md)。

## 使用映射函数

要使用函数，请在“源字段”下 **[!UICONTROL 键入该函数]** ，并输入相应的语法和输入。

例如，要连接城市和国家／地区CSV字段并将它们分配到城市XDM字段，请将源字段设置为 `concat(city, ", ", county)`。

![](../images/tutorials/map-a-csv-file/mapping-function.png)

要了解有关将列映射到XDM字段的更多信息，请阅读有关使 [用数据准备（映射器）功能的指南](../../data-prep/functions.md)。

## 后续步骤

通过遵循本教程，您已成功将平面CSV文件映射到XDM模式并将其引入 [!DNL Platform]。 此数据现在可供下游服务 [!DNL Platform] 使用，如 [!DNL Real-time Customer Profile]。 有关详细信息， [请参阅[!DNL实时客户用户档案]](../../profile/home.md) 的概述。
