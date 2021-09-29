---
keywords: Experience Platform；主页；热门主题；流；云存储连接器；云存储
solution: Experience Platform
title: 在UI中为云存储源创建流数据流
topic-legacy: overview
type: Tutorial
description: 数据流是一项计划任务，用于从源中检索数据并将其摄取到平台数据集。 本教程提供了使用云存储基础连接器配置新数据流的步骤。
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: 4a2d82fd6aec25f2570082ebc54f826251bc0a51
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 在UI中为云存储源创建流数据流

数据流是一项计划任务，用于从源中检索数据并将其摄取到Adobe Experience Platform数据集。 本教程提供了在UI中为云存储源创建流数据流的步骤。

在尝试使用本教程之前，您必须先在云存储帐户与平台之间建立一个经过身份验证的有效连接。 如果您还没有经过身份验证的连接，请参阅以下教程之一，以了解有关验证流云存储帐户的信息：

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

- [数据流](../../../../../dataflows/home.md):数据流是跨平台移动数据的数据作业的表示形式。数据流在不同的服务之间进行配置，从源到[!DNL Identity Service]、到[!DNL Profile]和[!DNL Destinations]。
- [数据准备](../../../../../data-prep/home.md):数据准备允许数据工程师映射、转换和验证来自体验数据模型(XDM)的数据。数据准备在数据摄取流程（包括CSV摄取工作流）中显示为“映射”步骤。
- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

## 添加数据

在创建对流云存储帐户进行身份验证后，将显示&#x200B;**[!UICONTROL 选择数据]**&#x200B;步骤，为您提供一个界面以选择要将哪个数据流引入平台。

- 界面的左侧是一个浏览器，用于查看您帐户中的可用数据流；
- 界面的右侧部分允许您从JSON文件预览多达100行数据。

![界面](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

选择要使用的数据流，然后选择&#x200B;**[!UICONTROL 选择文件]**&#x200B;以上传示例架构。

>[!TIP]
>
>如果您的数据符合XDM标准，则可以跳过上传示例架构，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![选择流](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

上传架构后，预览界面会进行更新，以显示您上传的架构的预览。 预览界面允许您检查文件的内容和结构。 您还可以使用[!UICONTROL 搜索字段]实用程序从架构中访问特定项目。

完成后，选择&#x200B;**[!UICONTROL Next]**。

![模式预览](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## 映射

将显示&#x200B;**[!UICONTROL 映射]**&#x200B;步骤，提供一个接口，用于将源数据映射到Platform数据集。

为要摄取到的入站数据选择数据集。 您可以使用现有数据集，也可以创建新数据集。

### 新数据集

要将数据摄取到新数据集，请选择&#x200B;**[!UICONTROL New dataset]** ，然后在提供的字段中输入数据集的名称和说明。 要添加架构，您可以在&#x200B;**[!UICONTROL 选择架构]**&#x200B;对话框中输入现有架构名称。 或者，您也可以选择&#x200B;**[!UICONTROL 架构高级搜索]**&#x200B;以搜索相应的架构。

![新数据集](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

此时会出现[!UICONTROL 选择架构]窗口，为您提供可供选择的可用架构列表。 从列表中选择一个架构以更新右边栏，以显示特定于您选择的架构的详细信息，包括有关是否为[!DNL Profile]启用该架构的信息。

确定并选择要使用的架构后，选择&#x200B;**[!UICONTROL Done]**。

![选择模式](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

[!UICONTROL Target数据集]页面会更新，并显示您选定的架构，该架构将作为数据集的一部分显示。 在此步骤中，您可以为[!DNL Profile]启用数据集，并创建实体属性和行为的整体视图。 所有已启用数据集的数据都将包含在[!DNL Profile]中，并在保存数据流时应用更改。

切换&#x200B;**[!UICONTROL 配置文件数据集]**&#x200B;按钮，为[!DNL Profile]启用目标数据集。

![新配置文件](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### 现有数据集

要将数据摄取到现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**，然后选择数据集图标。

![现有数据集](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

此时会出现&#x200B;**[!UICONTROL 选择数据集]**&#x200B;对话框，为您提供可供选择的可用数据集列表。 从列表中选择一个数据集以更新右边栏，以显示特定于您选择的数据集的详细信息，包括是否可以为[!DNL Profile]启用该数据集的信息。

识别并选择要使用的数据集后，选择&#x200B;**[!UICONTROL Done]**。

![select-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

选择数据集后，选择[!DNL Profile]切换开关以为[!DNL Profile]启用数据集。

![现有配置文件](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### 映射标准字段

建立数据集和架构后，将显示&#x200B;**[!UICONTROL 映射标准字段]**&#x200B;界面，允许您为数据手动配置映射字段。

>[!TIP]
>
>Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。

根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关映射器函数和计算字段的详细信息，请参阅[数据准备函数指南](../../../../../data-prep/functions.md)或[计算字段指南](../../../../../data-prep/calculated-fields.md)。

映射源数据后，选择&#x200B;**[!UICONTROL Next]**。

![映射](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## 数据流详细信息

出现&#x200B;**[!UICONTROL 数据流详细信息]**&#x200B;步骤，允许您命名并简要描述新数据流。

为数据流提供值，然后选择&#x200B;**[!UICONTROL Next]**。

![数据流详细信息](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### 审阅

此时会出现&#x200B;**[!UICONTROL Review]**&#x200B;步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

- **[!UICONTROL 连接]**:显示您的帐户名称、源类型以及特定于您所使用的流云存储源的其他信息。
- **[!UICONTROL 分配数据集和映射字段]**:显示用于数据流的目标数据集和架构。

审核数据流后，选择&#x200B;**[!UICONTROL 完成]**&#x200B;并为创建数据流留出一些时间。

![审查](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## 监控和删除数据流

创建流云存储数据流后，您可以监控通过它摄取的数据。 有关监控和删除流数据流的更多信息，请参阅[监控流数据流](../../monitor-streaming.md)的教程。

## 后续步骤

在本教程中，您已成功创建了数据流以从云存储源流化数据。 现在，下游Platform服务（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用传入数据。 有关更多详细信息，请参阅以下文档：

- [[!DNL Real-time Customer Profile] 概述](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)