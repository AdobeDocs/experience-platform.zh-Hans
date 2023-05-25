---
keywords: Experience Platform；主页；热门主题；映射csv；映射csv文件；将csv文件映射到xdm；将csv映射到xdm；用户界面指南；
solution: Experience Platform
title: 将CSV文件映射到现有XDM架构
type: Tutorial
description: 本教程介绍如何使用Adobe Experience Platform用户界面将CSV文件映射到现有XDM架构。
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# 将CSV文件映射到现有XDM架构

>[!NOTE]
>
>本文档介绍如何将CSV文件映射到现有XDM架构。 有关如何使用AI生成的架构推荐工具（当前为测试版）的信息，请参阅以下文档： [使用机器学习推荐映射CSV文件](./recommendations.md).

为了将CSV数据摄取到 [!DNL Adobe Experience Platform]，数据必须映射到 [!DNL Experience Data Model] (XDM)架构。 本教程介绍如何使用将CSV文件映射到XDM架构 [!DNL Platform] 用户界面。

## 快速入门

本教程需要对以下组件有一定的了解 [!DNL Platform]：

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。
- [批量摄取](../../batch-ingestion/overview.md)：用于执行此操作的方法 [!DNL Platform] 从用户提供的数据文件中摄取数据。
- [Adobe Experience Platform数据准备](../../batch-ingestion/overview.md)：一套功能，可映射和转换摄取的数据以符合XDM架构。 相关文档 [数据准备函数](../../../data-prep/functions.md) 与架构映射特别相关。

此外，本教程还要求您已创建一个数据集以将CSV数据摄取到。 有关在UI中创建数据集的步骤，请参阅 [数据引入教程](../ingest-batch-data.md).

## 选择目标

登录 [[!DNL Adobe Experience Platform]](https://platform.adobe.com) 然后选择 **[!UICONTROL 工作流]** 以访问 **[!UICONTROL 工作流]** 工作区。

从 **[!UICONTROL 工作流]** 屏幕，选择 **[!UICONTROL 将CSV映射到XDM架构]** 在 **[!UICONTROL 数据摄取]** 部分，然后选择 **[!UICONTROL Launch]**.

![](../../images/tutorials/map-a-csv-file/workflows.png)

此 **[!UICONTROL 将CSV映射到XDM架构]** 此时将显示工作流，从 **[!UICONTROL 目标]** 步骤。 选择要引入的集客数据的数据集。 您可以使用现有数据集或创建新数据集。

**使用现有数据集**

要将CSV数据摄取到现有数据集，请选择 **[!UICONTROL 使用现有数据集]**. 您可以使用搜索函数或通过滚动面板中的现有数据集列表来检索现有数据集。

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

要将CSV数据摄取到新数据集，请选择 **[!UICONTROL 创建新数据集]** 并在提供的字段中输入数据集的名称和描述。 使用搜索功能或滚动浏览提供的架构列表来选择架构。 选择 **[!UICONTROL 下一个]** 以继续。

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 添加数据

此 **[!UICONTROL 添加数据]** 步骤。 将CSV文件拖放到提供的空间中，或选择 **[!UICONTROL 选择文件]** 以手动输入CSV文件。

![](../../images/tutorials/map-a-csv-file/add-data.png)

此 **[!UICONTROL 示例数据]** 文件上传后会显示部分，其中显示前十行数据。 确认数据已按预期上传后，选择 **[!UICONTROL 下一个]**.

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## 将CSV字段映射到XDM架构字段

此 **[!UICONTROL 映射]** 步骤。 CSV文件的列列在 **[!UICONTROL 源字段]**，其对应的XDM架构字段列在下 **[!UICONTROL 目标字段]**.

[!DNL Platform] 根据您选择的目标架构或数据集，自动为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

要接受所有自动生成的映射值，请选中标有“[!UICONTROL 接受所有目标字段]“。

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

有时，源架构有多个推荐可用。 发生这种情况时，映射卡片会显示最显眼的建议，其后跟一个蓝色圆圈，其中包含可用的其他建议数量。 选择灯泡图标将显示其他建议的列表。 通过选中要映射到的推荐旁边的复选框，您可以选择替代推荐之一。

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

或者，您可以选择手动将源架构映射到目标架构。 将鼠标悬停在要映射的源架构上，然后选择加号图标。

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

此 **[!UICONTROL 将源映射到目标字段]** 弹出窗口即会出现。 在此处，您可以选择要映射的字段，然后 **[!UICONTROL 保存]** 以添加新映射。

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

如果要删除其中一个映射，请将鼠标悬停在该映射上，然后选择减号图标。

### 添加计算字段 {#add-calculated-field}

计算字段允许根据输入架构中的属性创建值。 然后，可以将这些值分配给目标架构中的属性，并提供名称和描述以便更轻松地引用。

选择 **[!UICONTROL 添加计算字段]** 按钮以继续。

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

此 **[!UICONTROL 创建计算字段]** 面板。 左侧对话框包含计算字段中支持的字段、函数和运算符。 选择其中一个选项卡，开始向表达式编辑器添加函数、字段或运算符。

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 选项卡 | 描述 |
| --------- | ----------- |
| 字段 | 字段选项卡列出了源架构中可用的字段和属性。 |
| 函数 | 函数选项卡列出了可用于转换数据的函数。 要了解有关可在计算字段中使用的函数的更多信息，请阅读以下指南： [使用数据准备（映射器）函数](../../../data-prep/functions.md). |
| 操作员 | 运算符选项卡列出了可用于转换数据的运算符。 |

您可以使用位于中心的表达式编辑器手动添加字段、函数和运算符。 选择编辑器以开始创建表达式。

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

选择 **[!UICONTROL 保存]** 以继续。

此时会重新显示映射屏幕，其中包含新创建的源字段。 应用相应的目标字段并选择 **[!UICONTROL 完成]** 以完成映射。

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## 监测数据提取

在映射和创建CSV文件后，您可以监控通过它摄取的数据。 有关监控数据摄取的更多信息，请参阅关于以下内容的教程： [监测数据摄取](../../../ingestion/quality/monitor-data-ingestion.md).

## 后续步骤

通过阅读本教程，您已成功将平面CSV文件映射到XDM架构并将其摄取到 [!DNL Platform]. 此数据现在可供下游使用 [!DNL Platform] 服务，例如 [!DNL Real-Time Customer Profile]. 请参阅概述，了解 [[!DNL Real-Time Customer Profile]](../../../profile/home.md) 了解更多信息。
