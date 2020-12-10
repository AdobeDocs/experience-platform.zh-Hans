---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: 将CSV文件映射到XDM模式
topic: tutorial
type: Tutorial
description: 本教程介绍如何使用Adobe Experience Platform用户界面将CSV文件映射到XDM模式。
translation-type: tm+mt
source-git-commit: c19360450d7b1f11063683b796774a04f3dbe16c
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---


# 将CSV文件映射到XDM模式

要将CSV数据引入 [!DNL Adobe Experience Platform]其中，必须将数据映射 [!DNL Experience Data Model] 到(XDM)模式。 本教程介绍如何使用用户界面将CSV文件映射到 [!DNL Platform] XDM模式。

此外，本教程的附录还提供了有关使用映射函数的更 [多信息](#mapping-functions)。

## 入门指南

本教程需要对以下组件有一个有效的了解 [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md):从用户提供的 [!DNL Platform] 数据文件中摄取数据的方法。

本教程还要求您已创建数据集以将CSV数据引入。 有关在UI中创建数据集的步骤，请参阅数 [据摄取教程](./ingest-batch-data.md)。

## 选择目标

登录，然 [[!DNL Adobe Experience Platform]](https://platform.adobe.com) 后从左侧导 **[!UICONTROL 航栏]** 中选择工作流 **[!UICONTROL ，以访问工作流]** 工作区。

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

将出 **[!UICONTROL 现]** “映射”步骤。 CSV文件的列列列在源字段 **[!UICONTROL 下]**，其对应的XDM模式字段列在 **[!UICONTROL 目标字段下]**。

[!DNL Platform] 自动根据您选择的目标模式或数据集为自动映射字段提供智能建议。 您可以手动调整映射规则以适合您的用例。

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

要接受所有自动生成的映射值，请选中标有“接受所[!UICONTROL 有目标字段]”的复选框。

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

有时，源模式有多个推荐可用。 出现这种情况时，映射卡会显示最突出的推荐，后跟一个蓝色圆圈，其中包含可用的其他推荐数。 选择灯泡图标将显示其他推荐的列表。 您可以通过选中要映射到的推荐旁的复选框，选择其中一个替代推荐。

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

或者，您也可以选择手动将源模式映射到目标模式。 将鼠标悬停在要映射的源模式上，然后选择加号图标。

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

将显 **[!UICONTROL 示“将源映射到目标”字段]** ，弹出窗口。 在此处，您可以选择要映射的字段，然后选择保 **[!UICONTROL 存]** ，以添加新映射。

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

如果要删除其中一个映射，请将鼠标悬停在该映射上，然后选择减号图标。

### 添加计算字段

计算字段允许根据输入模式中的属性创建值。 然后，可将这些值分配给目标模式中的属性，并提供名称和说明以便更轻松地引用。

选择“添 **[!UICONTROL 加计算字段]** ”按钮以继续。

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

将出 **[!UICONTROL 现“创建计算字段]** ”面板。 左对话框包含计算字段中支持的字段、函数和运算符。 选择一个选项卡以开始向表达式编辑器添加函数、字段或运算符。

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 选项卡 | 描述 |
| --------- | ----------- |
| 字段 | “字段”选项卡列表源模式中可用的字段和属性。 |
| 函数 | 函数选项卡列表可用于转换数据的函数。 要进一步了解可在计算字段中使用的功能，请阅读有关使用数据准 [备（映射器）功能的指南](../../data-prep/functions.md)。 |
| 运算符 | “运算符”选项卡列表可用于转换数据的运算符。 |

您可以使用中心的表达式编辑器手动添加字段、函数和运算符。 选择要开始创建表达式的编辑器。

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

选择 **[!UICONTROL 保存]** ，以继续。

映射屏幕将随新创建的源字段重新显示。 应用相应的目标字段并选 **[!UICONTROL 择]** “完成”以完成映射。

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## 监控数据获取

映射和创建CSV文件后，您可以监视通过它摄取的数据。 有关监视数据摄取的详细信息，请参阅监视数据 [摄取的教程](../../ingestion/quality/monitor-data-ingestion.md)。

## 后续步骤

通过遵循本教程，您已成功将平面CSV文件映射到XDM模式并将其引入 [!DNL Platform]。 此数据现在可供下游服务 [!DNL Platform] 使用，如 [!DNL Real-time Customer Profile]。 See the overview for [[!DNL Real-time Customer Profile]](../../profile/home.md) for more information.
