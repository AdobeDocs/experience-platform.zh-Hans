---
keywords: Experience Platform；主页；热门主题；云存储连接器；云存储
solution: Experience Platform
title: 在UI中为云存储流连接器配置数据流
topic-legacy: overview
type: Tutorial
description: 数据流是从源中检索数据并将其引入平台数据集的计划任务。 本教程提供了使用云存储库连接器配置新数据流的步骤。
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# 在UI中为云存储流连接配置数据流

数据流是从源中检索数据并将其引入[!DNL Platform]数据集的计划任务。 本教程提供了使用云存储库连接器配置新数据流的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成的基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

此外，本教程要求您已经创建了云存储连接器。 在[源连接器概述](../../../../home.md)中，可以找到有关在UI中创建不同云存储连接器的列表教程。

## 选择数据

在创建云存储连接器后，将显示&#x200B;*选择数据*&#x200B;步骤，为您提供一个接口，供您选择要从中流化数据的流。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## 将数据字段映射到XDM模式

将出现&#x200B;**[!UICONTROL Mapping]**&#x200B;步骤，提供一个交互式界面，将源数据映射到[!DNL Platform]数据集。

为要摄取的入站数据选择数据集。 您可以使用现有数据集或创建新数据集。

**使用现有数据集**

要将数据收录到现有数据集中，请选择&#x200B;**[!UICONTROL Use existing dataset]**，然后单击数据集图标。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

出现&#x200B;**[!UICONTROL Select dataset]**&#x200B;对话框。 找到您要使用的数据集，选择它，然后单击&#x200B;**[!UICONTROL Continue]**。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**使用新数据集**

要将数据收录到新数据集中，请选择&#x200B;**[!UICONTROL Create new dataset]**，并在提供的字段中输入数据集的名称和说明。 然后，在下拉列表中选择要使用的模式。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## 命名数据流

将出现&#x200B;**[!UICONTROL Dataflow detail]**&#x200B;步骤，允许您命名新数据流并提供有关新数据流的简短说明。

为数据流提供值，然后单击&#x200B;**[!UICONTROL Next]**。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### 查看数据流

将显示&#x200B;**[!UICONTROL Review]**&#x200B;步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

- **[!UICONTROL Source details]**:显示源类型和有关源的其他相关详细信息。
- **[!UICONTROL Target details]**:显示接收源数据的模式集，包括数据集附带的数据集。

查看数据流后，单击&#x200B;**[!UICONTROL Finish]**&#x200B;并允许一段时间创建数据流。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## 监视和删除数据流

创建云存储数据流后，您可以监视通过它摄取的数据。 有关监视和删除数据流的详细信息，请参阅有关[监视数据流](../../../../../ingestion/quality/monitor-data-ingestion.md)的教程。

## 后续步骤

通过本教程，您成功创建了一个数据流以从外部云存储导入数据，并获得了有关监视数据集的洞察。 现在，下游[!DNL Platform]服务（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用传入数据。 有关更多详细信息，请参阅以下文档:

- [[!DNL Real-time Customer Profile] 概述](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)

## 附录

以下部分提供了有关使用源连接器的其他信息。

### 禁用数据流

创建数据流后，它会立即变为活动状态，并根据给出的计划收集数据。 您可以按照以下说明随时禁用活动数据流。

在&#x200B;**[!UICONTROL Sources]**&#x200B;工作区中，单击&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡。 接下来，单击与要禁用的活动数据流关联的连接名称。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

将显示&#x200B;**[!UICONTROL Source activity]**&#x200B;页。 从列表中选择活动数据流，以在屏幕右侧打开其&#x200B;**[!UICONTROL Properties]**&#x200B;列，该列包含一个&#x200B;**[!UICONTROL Enabled]**&#x200B;切换按钮。 单击切换可禁用数据流。 在禁用数据流后，可以使用相同的切换来重新启用数据流。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### 激活[!DNL Profile]人口的入站数据

来自源连接器的入站数据可用于丰富和填充[!DNL Real-time Customer Profile]数据。 有关填充[!DNL Real-time Customer Profile]数据的详细信息，请参阅关于[用户档案填充](../../profile.md)的教程。
