---
title: 使用人工智能生成的Recommendations将CSV文件映射到XDM架构
description: 本教程介绍如何使用人工智能生成的推荐将CSV文件映射到XDM架构。
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: 6632086641004c2b788a28cbc47ac6d8bd4eace3
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 2%

---

# 使用人工智能生成的推荐将CSV文件映射到XDM架构

>[!NOTE]
>
>有关Platform中一般可用的CSV映射功能的信息，请参阅上的文档 [将CSV文件映射到现有架构](./existing-schema.md).

为了将CSV数据摄取到 [!DNL Adobe Experience Platform]，数据必须映射到 [!DNL Experience Data Model] (XDM)架构。 您可以选择映射到 [现有架构](./existing-schema.md)但是，如果您不知道确切要使用哪个架构或者应如何构建该架构，则可以在Platform UI中使用基于机器学习(ML)模型的动态推荐。

## 快速入门

本教程需要对以下组件有一定的了解 [!DNL Platform]：

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md)：[!DNL Platform] 用于组织客户体验数据的标准化框架。
   * 至少，您必须了解 [XDM中的行为](../../../xdm/home.md#data-behaviors)，以便您决定是否将数据映射到 [!UICONTROL 个人资料] 类（记录行为）或 [!UICONTROL ExperienceEvent] 类（时间序列行为）。
* [批量摄取](../../batch-ingestion/overview.md)：用于执行操作的方法 [!DNL Platform] 从用户提供的数据文件中摄取数据。
* [Adobe Experience Platform数据准备](../../batch-ingestion/overview.md)：一套功能，可映射和转换摄取的数据以符合XDM架构。 相关文档 [数据准备功能](../../../data-prep/functions.md) 专门与架构映射相关。

## 提供数据流详细信息

在Experience PlatformUI中，选择 **[!UICONTROL 源]** 在左侧导航中。 在 **[!UICONTROL 目录]** 查看，导航到 **[!UICONTROL 本地系统]** 类别。 下 **[!UICONTROL 本地文件上传]**，选择 **[!UICONTROL 添加数据]**.

![此 [!UICONTROL 源] Platform UI中的目录，使用 [!UICONTROL 添加数据] 下 [!UICONTROL 本地文件上传] 被选中了。](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

此 **[!UICONTROL 映射CSV XDM架构]** 此时会显示工作流，从 **[!UICONTROL 数据流详细信息]** 步骤。

选择 **[!UICONTROL 使用ML推荐创建新架构]**，从而导致显示新控件。 为要映射的CSV数据选择适当的类([!UICONTROL 个人资料] 或 [!UICONTROL ExperienceEvent])。 您可以选择使用下拉菜单为您的企业选择相关的行业，如果提供的类别不适用于您，则将其留空。 如果贵组织使用 [B2B](../../../xdm/tutorials/relationship-b2b.md) 模型，选择 **[!UICONTROL B2B数据]** 复选框。

![此 [!UICONTROL 数据流详细信息] 选择ML推荐选项的步骤。 [!UICONTROL 个人资料] 已为类选择并且 [!UICONTROL 电信] 为行业选择](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

在此处，为将从CSV数据创建的架构提供名称，并为将包含在该架构下摄取的数据的输出数据集提供名称。

您可以选择在继续之前为数据流配置以下附加功能：

| 输入名称 | 描述 |
| --- | --- |
| [!UICONTROL 描述] | 数据流的描述。 |
| [!UICONTROL 错误诊断] | 启用后，将为新摄取的批次生成错误消息，在获取中的相应批次时可以查看这些错误消息 [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL 部分摄取] | 启用后，将在指定的错误阈值内摄取新批次数据的有效记录。 利用此阈值，可配置在整个批处理失败之前可接受的错误百分比。 |
| [!UICONTROL 数据流详细信息] | 为将CSV数据导入Platform的数据流提供名称和可选描述。 启动此工作流时，会自动为数据流分配默认名称。 更改名称是可选的。 |
| [!UICONTROL 警报] | 从列表中选择 [产品内警报](../../../observability/alerts/overview.md) 启动数据流后您想要接收的有关数据流状态的信息。 |

{style="table-layout:auto"}

配置完数据流后，选择 **[!UICONTROL 下一个]**.

![此 [!UICONTROL 数据流详细信息] 部分已完成。](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## 选择数据

在 **[!UICONTROL 选择数据]** 步骤，使用左列上传CSV文件。 您可以选择 **[!UICONTROL 选择文件]** 打开文件资源管理器对话框以从中选择文件，或者直接将文件拖放到列上。

![此 [!UICONTROL 选择文件] 按钮和拖放区域中突出显示的区域 [!UICONTROL 选择数据] 步骤。](../../images/tutorials/map-csv-recommendations/upload-files.png)

上传文件后，会显示一个示例数据部分，该部分显示收到的数据的前10行，以便您验证是否已正确上传。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![示例数据行填充在工作区中](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## 配置架构映射

运行ML模型可根据数据流配置和上传的CSV文件生成新架构。 当该过程完成时， [!UICONTROL 映射] 步骤将填充，以显示每个单独字段的映射以及所生成架构结构的完全可导航视图。

![此 [!UICONTROL 映射] 步骤，显示映射的所有CSV字段以及生成的架构结构。](../../images/tutorials/map-csv-recommendations/schema-generated.png)

>[!NOTE]
>
>在源到目标字段映射工作流中，您可以根据各种条件筛选架构中的所有字段。 默认行为是显示所有映射的字段。 要更改显示的字段，请选择搜索输入字段旁边的过滤器图标，然后从下拉选项中进行选择。<br> ![CSV到XDM架构创建工作流的映射阶段，其中过滤器图标和下拉菜单突出显示。](../../images/tutorials/map-csv-recommendations/source-field-to-target-mapping-filter.png "CSV到XDM架构创建工作流的映射阶段，其中过滤器图标和下拉菜单突出显示。"){width="100" zoomable="yes"}

从此处，您可以选择 [编辑字段映射](#edit-mappings) 或 [更改与它们关联的字段组](#edit-schema) 根据你的需要。 满意后，选择 **[!UICONTROL 完成]** 完成映射并启动之前配置的数据流。 CSV数据被引入到系统中，并根据生成的架构结构填充数据集，以供下游平台服务使用。

![此 [!UICONTROL 完成] 按钮时，完成CSV映射过程。](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### 编辑字段映射 {#edit-mappings}

使用字段映射预览可编辑现有映射或将其完全删除。 有关如何管理UI中映射集的更多信息，请参阅 [数据准备映射的UI指南](../../../data-prep/ui/mapping.md#mapping-interface).

### 编辑字段组 {#edit-field-groups}

CSV字段使用ML模型自动映射到现有XDM字段组。 如果要更改任何特定CSV字段的字段组，请选择 **[!UICONTROL 编辑]** 在模式树的旁边。

![此 [!UICONTROL 编辑] 选择架构树旁边的按钮。](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

此时将显示一个对话框，允许您编辑映射中任何字段的显示名称、数据类型和字段组。 选择编辑图标(![“编辑”图标](../../images/tutorials/map-csv-recommendations/edit-icon.png))，以编辑其右列的详细信息，然后再选择 **[!UICONTROL 应用]**.

![要更改的源字段的建议字段组。](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

调整完源字段的架构建议后，选择 **[!UICONTROL 保存]** 以应用更改。

## 后续步骤

本指南介绍了如何使用AI生成的推荐将CSV文件映射到XDM架构，从而允许您通过批量摄取将数据引入Platform。

有关将CSV文件映射到现有架构的步骤，请参阅 [现有架构映射工作流](./existing-schema.md). 有关通过预建源连接将数据实时流式传输到Platform的信息，请参阅 [源概述](../../../sources/home.md).
