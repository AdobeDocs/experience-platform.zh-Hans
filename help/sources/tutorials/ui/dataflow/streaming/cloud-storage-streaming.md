---
keywords: Experience Platform;home;popular topics;cloud storage connector;cloud storage
solution: Experience Platform
title: 在UI中为云存储流连接器配置数据流
topic: overview
description: 数据流是从源中检索数据并将其引入平台数据集的计划任务。 本教程提供使用云存储库连接器配置新数据流的步骤。
translation-type: tm+mt
source-git-commit: c1b493de7374cbd1c916d90f9382574f831e11e3
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 0%

---


# 在UI中为云存储流连接器配置数据流

数据流是从源中检索数据并将其引入数据集的计划任务 [!DNL Platform] 符。 本教程提供使用云存储库连接器配置新数据流的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

此外，本教程要求您已创建云存储连接器。 有关在UI中创建不同云存储连接器的列表教程，请参阅源连接 [器概述](../../../../home.md)。

## 选择数据

创建云存储连接器后，将显 *示选择* 步骤，为您提供一个界面，供您选择要从哪个流传输数据。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## 将数据字段映射到XDM模式

将显 **[!UICONTROL 示]** “映射”步骤，提供一个交互界面来将源数据映射到数 [!DNL Platform] 据集。

选择要收录到的入站数据的数据集。 您可以使用现有数据集或创建新数据集。

**使用现有数据集**

要将数据引入现有数据集，请选择 **[!UICONTROL 使用现有数据集]**，然后单击数据集图标。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

此时将 **[!UICONTROL 显示“选择数据集]** ”对话框。 找到您要使用的数据集，选择它，然后单击“继 **[!UICONTROL 续”]**。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**使用新数据集**

要将数据引入新数据集，请选 **[!UICONTROL 择创建新数据集]** ，并在提供的字段中输入数据集的名称和说明。 然后，在下拉列表中选择要使用的模式。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## 命名数据流

此时 **[!UICONTROL 会显示]** “数据流详细信息”步骤，允许您命名新数据流并简要描述新数据流。

提供数据流的值，然后单击“下 **[!UICONTROL 一步]**”。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### 查看数据流

此时 **[!UICONTROL 会出现]** “审阅”步骤，允许您在创建新数据流之前对其进行查看。 详细信息按以下类别分组：

- **[!UICONTROL 源详细信息]**:显示源类型和有关源的其他相关详细信息。
- **[!UICONTROL 目标详细信息]**:显示接收源数据的数据集，包括数据集附带的模式。

查看数据流后，单击 **[!UICONTROL 完成]** ，并允许一段时间创建数据流。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## 监视和删除数据流

创建云存储数据流后，您可以监视通过它摄取的数据。 有关监视和删除数据流的详细信息，请参阅有关监视数据流 [的教程](../../../../../ingestion/quality/monitor-data-flows.md)。

## 后续步骤

通过遵循本教程，您已成功创建了从外部云存储导入数据的数据流，并获得了有关监视数据集的洞察。 现在，下游服务（如和）可 [!DNL Platform] 以使用传入 [!DNL Real-time Customer Profile] 数据 [!DNL Data Science Workspace]。 有关更多详细信息，请参阅以下文档:

- [[!DNL Real-time Customer Profile] 概述](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)

## 附录

以下部分提供了有关使用源连接器的其他信息。

### 禁用数据流

创建数据流时，它会立即变为活动状态，并根据给定的计划接收数据。 您可以按照以下说明随时禁用活动数据流。

在“源 **[!UICONTROL ”工作]** 区中，单击“ **[!UICONTROL 浏览]** ”选项卡。 然后，单击与要禁用的活动数据流关联的连接的名称。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

将显 **[!UICONTROL 示“源活动]** ”页面。 从列表中选择活动数据流以在屏 **[!UICONTROL 幕]** 右侧打开其“属性”列，该列包含“已启用 **** ”切换按钮。 单击切换以禁用数据流。 在禁用数据流后，可以使用相同的切换重新启用数据流。

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### 激活入站数据以进行 [!DNL Profile] 填充

来自源连接器的入站数据可用于丰富和填充数 [!DNL Real-time Customer Profile] 据。 有关填充数据的更 [!DNL Real-time Customer Profile] 多信息，请参阅用户档案填 [充教程](../../profile.md)。
