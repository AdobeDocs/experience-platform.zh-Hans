---
title: 使用人工智能生成的Recommendations将CSV文件映射到XDM架构
description: 本教程介绍如何使用AI生成的推荐将CSV文件映射到XDM架构。
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: df6f76be6beba962b1795bd33dc753ef04267734
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# 使用人工智能生成的推荐将CSV文件映射到XDM架构

>[!NOTE]
>
>有关Platform中一般可用的CSV映射功能的信息，请参阅以下文档： [将CSV文件映射到现有架构](./existing-schema.md).

为了将CSV数据摄取到 [!DNL Adobe Experience Platform]，数据必须映射到 [!DNL Experience Data Model] (XDM)架构。 您可以选择映射到 [现有架构](./existing-schema.md)但是，如果您不确定要使用哪个架构或应如何构建该架构，则可以在Platform UI中使用基于机器学习(ML)模型的动态推荐。

## 快速入门

本教程需要对以下组件有一定的了解 [!DNL Platform]：

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。
   * 您至少必须了解 [XDM中的行为](../../../xdm/home.md#data-behaviors)，以便您可以决定是否将数据映射到 [!UICONTROL 个人资料] 类（记录行为）或 [!UICONTROL ExperienceEvent] 类（时间序列行为）。
* [批量摄取](../../batch-ingestion/overview.md)：用于执行此操作的方法 [!DNL Platform] 从用户提供的数据文件中摄取数据。
* [Adobe Experience Platform数据准备](../../batch-ingestion/overview.md)：一套功能，可映射和转换摄取的数据以符合XDM架构。 相关文档 [数据准备函数](../../../data-prep/functions.md) 与架构映射具体相关。

## 提供数据流详细信息

在Experience PlatformUI中，选择 **[!UICONTROL 源]** 左侧导航栏中。 在 **[!UICONTROL 目录]** 查看，导航到 **[!UICONTROL 本地系统]** 类别。 下 **[!UICONTROL 本地文件上传]**，选择 **[!UICONTROL 添加数据]**.

![此 [!UICONTROL 源] Platform UI中的目录，使用 [!UICONTROL 添加数据] 下 [!UICONTROL 本地文件上传] 被选中。](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

此 **[!UICONTROL 映射CSV XDM架构]** 此时将显示工作流，从 **[!UICONTROL 数据流详细信息]** 步骤。

选择 **[!UICONTROL 使用ML推荐创建新架构]**，从而导致显示新控件。 为要映射的CSV数据选择适当的类([!UICONTROL 个人资料] 或 [!UICONTROL ExperienceEvent])。 您可以选择使用下拉菜单为您的企业选择相关的行业，或者如果提供的类别不适用于您，则将其留空。 如果贵组织在 [B2B](../../../xdm/tutorials/relationship-b2b.md) 模型，选择 **[!UICONTROL B2B数据]** 复选框。

![此 [!UICONTROL 数据流详细信息] 选择ML推荐选项的步骤。 [!UICONTROL 个人资料] 已为该类选择和 [!UICONTROL 电信] 为行业选择](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

在此处，为将从CSV数据创建的架构提供一个名称，并为将包含在该架构下摄取的数据的输出数据集提供一个名称。

您可以选择在继续之前为数据流配置以下附加功能：

| 输入名称 | 描述 |
| --- | --- |
| [!UICONTROL 描述] | 数据流的描述。 |
| [!UICONTROL 错误诊断] | 启用后，将为新摄取的批次生成错误消息，在获取中的相应批次时可以查看这些错误消息 [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL 部分摄取] | 启用后，将在指定的错误阈值内摄取新批次数据的有效记录。 利用此阈值，可配置在整个批处理失败之前可接受的错误百分比。 |
| [!UICONTROL 数据流详细信息] | 为将CSV数据导入Platform的数据流提供名称和可选描述。 启动此工作流时，会自动为数据流分配默认名称。 更改名称是可选的。 |
| [!UICONTROL 警报] | 从列表中选择 [产品内警报](../../../observability/alerts/overview.md) 启动数据流后，您希望接收的有关数据流状态的消息。 |

{style="table-layout:auto"}

配置完数据流后，选择 **[!UICONTROL 下一个]**.

![此 [!UICONTROL 数据流详细信息] 部分已完成。](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## 选择数据

在 **[!UICONTROL 选择数据]** 步骤，使用左列上传CSV文件。 您可以选择 **[!UICONTROL 选择文件]** 打开文件资源管理器对话框以从中选择文件，或者将文件直接拖放到列上。

![此 [!UICONTROL 选择文件] 按钮和拖放区域(高亮显示于 [!UICONTROL 选择数据] 步骤。](../../images/tutorials/map-csv-recommendations/upload-files.png)

上传文件后，会显示一个示例数据部分，其中显示收到的数据的前10行，以便您验证是否已正确上传。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![样本数据行填充在工作区中](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## 配置架构映射

运行ML模型可根据数据流配置和上传的CSV文件生成新架构。 当该过程完成时， [!UICONTROL 映射] 步骤将填充以显示每个单独字段的映射，以及生成的架构结构的完全可导航视图。

![此 [!UICONTROL 映射] 步骤，显示映射的所有CSV字段以及生成的架构结构。](../../images/tutorials/map-csv-recommendations/schema-generated.png)

从此处，您可以选择 [编辑字段映射](#edit-mappings) 或 [更改与其关联的字段组](#edit-schema) 根据你的需要。 满意后，选择 **[!UICONTROL 完成]** 完成映射并启动之前配置的数据流。 CSV数据被引入到系统中，并根据生成的架构结构填充数据集，以供下游平台服务使用。

![此 [!UICONTROL 完成] 按钮时，完成CSV映射过程。](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### 编辑字段映射 {#edit-mappings}

使用字段映射预览可编辑现有映射或完全删除现有映射。 有关如何管理UI中映射集的更多信息，请参阅 [用于数据准备映射的UI指南](../../../data-prep/ui/mapping.md#mapping-interface).

### 编辑字段组 {#edit-field-groups}

CSV字段会使用ML模型自动映射到现有XDM字段组。 如果要更改任何特定CSV字段的字段组，请选择 **[!UICONTROL 编辑]** 模式树的旁边。

![此 [!UICONTROL 编辑] 按钮进行标记。](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

此时将显示一个对话框，允许您编辑映射中任何字段的显示名称、数据类型和字段组。 选择编辑图标(![“编辑”图标](../../images/tutorials/map-csv-recommendations/edit-icon.png))来编辑其详细信息，然后再选择 **[!UICONTROL 应用]**.

![要更改的源字段的建议字段组。](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

调整完源字段的架构推荐后，选择 **[!UICONTROL 保存]** 以应用更改。

## 后续步骤

本指南介绍了如何使用AI生成的推荐将CSV文件映射到XDM架构，从而允许您通过批量摄取将数据引入Platform。

有关将CSV文件映射到现有架构的步骤，请参阅 [现有架构映射工作流](./existing-schema.md). 有关通过预建源连接实时将数据流式传输到Platform的信息，请参阅 [源概述](../../../sources/home.md).
