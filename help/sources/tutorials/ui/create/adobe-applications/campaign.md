---
keywords: Experience Platform；主页；热门主题；源；连接器；源连接器；营销活动；营销活动托管服务
title: 使用Platform UI创建Adobe Campaign Managed Cloud Services源连接
description: 了解如何使用Platform UI将Adobe Experience Platform连接到Adobe Campaign Managed Cloud Services。
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 6%

---

# 使用Platform UI创建Adobe Campaign Managed Cloud Services源连接

本教程提供了创建源连接以将Adobe Campaign Managed Cloud Services数据引入到Adobe Experience Platform的步骤。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)：Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [沙盒](../../../../../sandboxes/home.md)：Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 将Adobe Campaign Managed Cloud Services连接到平台

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 您还可以使用搜索栏缩小显示的源范围。

在 **[!UICONTROL Adobe应用程序]** 类别，选择 **[!UICONTROL Adobe Campaign Managed Cloud Services]** 然后选择 **[!UICONTROL 添加数据]**.

![显示Adobe Campaign Managed Cloud Services卡的源目录。](../../../../images/tutorials/create/campaign/catalog.png)

### 选择数据 {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Adobe Campaign 环境实例"
>abstract="要使用的 Adobe Campaign 环境的名称。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="目标映射"
>abstract="目标映射是 Campaign 用于传递消息的技术对象，并包含发送投放内容所需的所有技术设置（地址、电话号码、选择加入指示器、附加标识符...）。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="架构名称"
>abstract="Adobe Campaign 数据库中定义的实体的名称。"
>text="Learn more in documentation"

此 [!UICONTROL 选择数据] 此时会显示步骤，为您提供用于配置 [!UICONTROL Adobe Campaign实例]， [!UICONTROL 目标映射]、和 [!UICONTROL 架构名称].

| 属性 | 描述 |
| --- | --- |
| Adobe Campaign实例 | 您正在使用的Adobe Campaign环境实例的名称。 |
| 目标映射 | Campaign用于投放消息的技术对象，包含投放所需的所有技术设置。 |
| 架构名称 | 您要带到Platform的架构实体的名称。 选项包括投放日志和跟踪日志。 |

![可在其中配置Adobe Campaign实例、目标映射和架构名称的界面。](../../../../images/tutorials/create/campaign/select-data.png)

为Campaign实例、目标映射和架构名称提供值后，屏幕会更新以显示架构预览和示例数据集。 完成后，选择 **[!UICONTROL 下一个]**.

![架构层次结构的预览以及数据集示例](../../../../images/tutorials/create/campaign/preview.png)

### 使用现有数据集

此 [!UICONTROL 数据流详细信息] 页面允许您选择是要使用现有数据集，还是要为数据流配置新数据集。

要使用现有数据集，请选择 **[!UICONTROL 现有数据集]**. 您可以使用检索现有数据集 [!UICONTROL 高级搜索] 选项中进行选择，或者通过滚动下拉菜单中的现有数据集列表来进行选择。

选择数据集后，为数据流提供名称和可选描述。

![显示现有数据集选项的界面。](../../../../images/tutorials/create/campaign/existing-dataset.png)

### 使用新数据集

要使用新数据集，请选择 **[!UICONTROL 新建数据集]** 然后提供输出数据集名称和可选描述。 接下来，使用选择要映射到的架构 [!UICONTROL 高级搜索] 选项中进行选择，或者通过滚动下拉菜单中的现有架构列表来进行选择。 完成后，选择 **[!UICONTROL 下一个]**.

![显示新数据集选项的界面。](../../../../images/tutorials/create/campaign/new-dataset.png)

### 启用警报

您可以启用警报以接收有关数据流状态的通知。 从列表中选择警报以订阅并接收有关数据流状态的通知。 有关警报的更多信息，请参阅以下指南中的 [使用UI订阅源警报](../../alerts.md).

完成向数据流提供详细信息后，选择 **[!UICONTROL 下一个]**.

![可为数据流启用的不同警报类型选择。](../../../../images/tutorials/create/campaign/alerts.png)

### 将数据字段映射到XDM架构

此 [!UICONTROL 映射] 步骤随即显示，为您提供了一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的综合步骤，请参阅 [数据准备UI指南](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>将源字段映射到目标XDM字段时，必须确保将指定的主标识字段映射到其相应的目标XDM字段。

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![具有四个源数据字段的映射树映射到它们对应的XDM架构字段。](../../../../images/tutorials/create/campaign/mapping.png)

### 查看您的数据流

此 **[!UICONTROL 审核]** 步骤，允许您在创建新数据流之前对其进行查看。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括该数据集所遵循的架构。

查看数据流后，选择 **[!UICONTROL 完成]** 并留出一些时间来创建数据流。

![显示连接和数据集信息的审核页面。](../../../../images/tutorials/create/campaign/review.png)

### 监测数据集活动

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率以及成功和失败的批次的信息。

要开始查看数据集活动，请选择 **[!UICONTROL 数据流]** 在源目录中。

![选择了数据流标题选项卡的源目录页。](../../../../images/tutorials/create/campaign/dataflows.png)

接下来，从出现的数据流列表中选择目标数据集。

![已选择Adobe Campaign投放日志目标数据集的现有数据流列表。](../../../../images/tutorials/create/campaign/target-dataset.png)

此时将显示数据集活动页面。 从这里，您可以看到有关数据流性能的信息，包括摄取率、成功的批次和失败的批次。

此页面还为您提供了一个界面，用于更新数据流的元数据描述、启用部分摄取和错误诊断，以及向数据集添加新数据。

![带有图形的界面，表示选定数据集的摄取率。](../../../../images/tutorials/create/campaign/dataset-activity.png)

## 后续步骤

通过学习本教程，您已成功创建了一个数据流，将Campaign v8投放日志和跟踪日志数据引入到Platform。 传入数据现在可供下游平台服务使用，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-Time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)
