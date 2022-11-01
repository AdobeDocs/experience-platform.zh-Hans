---
title: 使用AI生成的Recommendations（测试版）将CSV文件映射到XDM模式
description: 本教程介绍如何使用AI生成的推荐将CSV文件映射到XDM模式。
source-git-commit: d6f858af8bc44be74b1aaf12b973fb6818c1b2a5
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# 使用AI生成的推荐（测试版）将CSV文件映射到XDM模式

>[!IMPORTANT]
>
>此功能当前处于测试阶段，您的组织可能还无法访问此功能。 文档和功能可能会发生更改。
>
>有关Platform中通常可用的CSV映射功能的信息，请参阅 [将CSV文件映射到现有架构](./existing-schema.md).

要将CSV数据摄取到 [!DNL Adobe Experience Platform]，则数据必须映射到 [!DNL Experience Data Model] (XDM)架构。 您可以选择映射到 [现有模式](./existing-schema.md)，但是如果您不确切知道要使用哪个架构或架构的结构方式，则可以在Platform UI中使用基于机器学习(ML)模型的动态推荐。

## 快速入门

本教程需要对的以下组件有一定的了解 [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。
   * 您至少必须了解 [XDM中的行为](../../../xdm/home.md#data-behaviors)，以便您能够决定是否将数据映射到 [!UICONTROL 用户档案] 类（记录行为）或 [!UICONTROL ExperienceEvent] 类（时间序列行为）。
* [批量摄取](../../batch-ingestion/overview.md):方法 [!DNL Platform] 从用户提供的数据文件中摄取数据。
* [Adobe Experience Platform数据准备](../../batch-ingestion/overview.md):一组功能，允许您映射和转换摄取的数据以符合XDM模式。 有关 [数据准备函数](../../../data-prep/functions.md) 与架构映射特别相关。

## 提供数据流详细信息

在Experience PlatformUI中，选择 **[!UICONTROL 源]** 中。 在 **[!UICONTROL 目录]** ，导航到 **[!UICONTROL 本地系统]** 类别。 在 **[!UICONTROL 本地文件上传]**，选择 **[!UICONTROL 添加数据]**.

![的 [!UICONTROL 源] 平台UI中的目录， [!UICONTROL 添加数据] 在 [!UICONTROL 本地文件上传] 被选中](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

的 **[!UICONTROL 映射CSV XDM架构]** 此时会显示工作流，从 **[!UICONTROL 数据流详细信息]** 中。

选择 **[!UICONTROL 使用ML推荐创建新架构]**，导致显示新控件。 为要映射的CSV数据选择相应的类([!UICONTROL 用户档案] 或 [!UICONTROL ExperienceEvent])。 您可以选择使用下拉菜单为您的业务选择相关行业，或者如果提供的类别不适用于您，则将其留空。 如果贵组织在 [企业对企业(B2B)](../../../xdm/tutorials/relationship-b2b.md) 模型，选择 **[!UICONTROL B2B数据]** 复选框。

![的 [!UICONTROL 数据流详细信息] 步骤，并选择ML推荐选项。 [!UICONTROL 用户档案] 已为类和选择 [!UICONTROL 电信] 为行业选择](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

在此，为将通过CSV数据创建的架构提供名称，并为将包含在该架构下摄取的数据的输出数据集提供名称。

在继续之前，您可以选择为数据流配置以下其他功能：

| 输入名称 | 描述 |
| --- | --- |
| [!UICONTROL 描述] | 数据流的描述。 |
| [!UICONTROL 错误诊断] | 启用后，将为新摄取的批次生成错误消息，这些批次在获取中的相应批次时可查看 [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL 部分摄取] | 启用后，将在指定的错误阈值内摄取新批量数据的有效记录。 利用此阈值，可在整个批处理失败之前配置可接受错误的百分比。 |
| [!UICONTROL 数据流详细信息] | 为将CSV数据导入平台的数据流提供名称和可选描述。 启动此工作流时，会自动为数据流分配默认名称。 更改名称是可选操作。 |
| [!UICONTROL 警报] | 从 [产品内警报](../../../observability/alerts/overview.md) 数据流启动后要接收的与其状态有关的信息。 |

{style=&quot;table-layout:auto&quot;}

配置完数据流后，选择 **[!UICONTROL 下一个]**.

![的 [!UICONTROL 数据流详细信息] 部分已完成](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## 选择数据

在 **[!UICONTROL 选择数据]** 步骤中，使用左列上传CSV文件。 您可以选择 **[!UICONTROL 选择文件]** 要打开文件资源管理器对话框以从中选择文件，或者可以直接将文件拖放到列上。

![的 [!UICONTROL 选择文件] 按钮和拖放区域(在 [!UICONTROL 选择数据] 步骤](../../images/tutorials/map-csv-recommendations/upload-files.png)

上传文件后，会显示一个示例数据部分，其中显示了接收数据的前十行，以便您能够验证其上传是否正确。 选择 **[!UICONTROL 下一个]** 继续。

![工作区中填充了示例数据行](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## 配置架构映射

运行ML模型以根据数据流配置和上传的CSV文件生成新架构。 该过程完成后， [!UICONTROL 映射] 步骤填充以显示每个字段的映射，同时显示生成的架构结构的完全可导航视图。

![的 [!UICONTROL 映射] 步骤，显示映射的所有CSV字段以及生成的架构结构](../../images/tutorials/map-csv-recommendations/schema-generated.png)

从此处，您可以选择 [编辑字段映射](#edit-mappings) 或 [更改与其关联的字段组](#edit-schema) 根据你的需要。 满足后，选择 **[!UICONTROL 完成]** 完成映射并启动您之前配置的数据流。 将CSV数据摄取到系统中，并根据生成的架构结构填充数据集，以便下游Platform服务使用。

![的 [!UICONTROL 完成] 按钮，完成CSV映射过程](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### 编辑字段映射 {#edit-mappings}

使用字段映射预览可编辑现有映射或完全删除现有映射。 有关如何在UI中管理映射集的更多信息，请参阅 [用于数据准备映射的UI指南](../../../data-prep/ui/mapping.md#mapping-interface).

### 编辑字段组 {#edit-field-groups}

CSV字段会使用ML模型自动映射到现有的XDM字段组。 如果要更改任何特定CSV字段的字段组，请选择 **[!UICONTROL 编辑]** 架构树旁边。

![的 [!UICONTROL 编辑] “架构树”旁边的按钮](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

此时会显示一个对话框，用于编辑映射中任何字段的显示名称、数据类型和字段组。 选择编辑图标(![“编辑”图标](../../images/tutorials/map-csv-recommendations/edit-icon.png))，以在选择 **[!UICONTROL 应用]**.

![要更改的源字段的推荐字段组](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

调整源字段的架构推荐后，请选择 **[!UICONTROL 保存]** 以应用更改。

## 后续步骤

本指南介绍了如何使用AI生成的推荐将CSV文件映射到XDM架构，从而允许您通过批量摄取将数据引入平台。

有关将CSV文件映射到现有架构的步骤，请参阅 [现有架构映射工作流](./existing-schema.md). 有关通过预建的源连接将数据实时流式传输到平台的信息，请参阅 [源概述](../../../sources/home.md).
