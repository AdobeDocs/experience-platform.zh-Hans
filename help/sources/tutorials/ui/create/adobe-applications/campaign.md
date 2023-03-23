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

本教程提供了创建源连接以将Adobe Campaign Managed Cloud Services数据导入Adobe Experience Platform的步骤。

## 快速入门

本指南需要对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [沙箱](../../../../../sandboxes/home.md):Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 将Adobe Campaign Managed Cloud Services连接到平台

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以为其创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 您还可以使用搜索栏来缩小显示的源范围。

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

的 [!UICONTROL 选择数据] 步骤，为您提供用于配置 [!UICONTROL Adobe Campaign实例], [!UICONTROL 目标映射]和 [!UICONTROL 架构名称].

| 属性 | 描述 |
| --- | --- |
| Adobe Campaign实例 | 您使用的Adobe Campaign环境实例的名称。 |
| 目标映射 | Campaign用于投放消息的技术对象，其中包含发送投放所需的所有技术设置。 |
| 架构名称 | 您将引入Platform的架构实体的名称。 相关选项包括“投放日志”和“跟踪日志”。 |

![一个界面，您可以在其中配置Adobe Campaign实例、目标映射和架构名称。](../../../../images/tutorials/create/campaign/select-data.png)

为Campaign实例、目标映射和架构名称提供值后，屏幕会随之更新，以显示架构预览以及示例数据集。 完成后，选择 **[!UICONTROL 下一个]**.

![架构层次结构的预览以及数据集的示例](../../../../images/tutorials/create/campaign/preview.png)

### 使用现有数据集

的 [!UICONTROL 数据流详细信息] 页面允许您选择是要使用现有数据集，还是要为数据流配置新数据集。

要使用现有数据集，请选择 **[!UICONTROL 现有数据集]**. 您可以使用 [!UICONTROL 高级搜索] 选项，或者通过在下拉菜单中滚动浏览现有数据集列表来配置。

选择数据集后，为数据流提供名称和可选描述。

![显示现有数据集选项的界面。](../../../../images/tutorials/create/campaign/existing-dataset.png)

### 使用新数据集

要使用新数据集，请选择 **[!UICONTROL 新数据集]** 然后，提供输出数据集名称和可选描述。 接下来，使用 [!UICONTROL 高级搜索] 选项或通过滚动下拉菜单中的现有架构列表来迁移。 完成后，选择 **[!UICONTROL 下一个]**.

![显示新数据集选项的界面。](../../../../images/tutorials/create/campaign/new-dataset.png)

### 启用警报

您可以启用警报以接收有关数据流状态的通知。 从列表中选择警报，以订阅和接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅源警报](../../alerts.md).

完成向数据流提供详细信息后，选择 **[!UICONTROL 下一个]**.

![可为数据流启用的不同警报类型选项。](../../../../images/tutorials/create/campaign/alerts.png)

### 将数据字段映射到XDM架构

的 [!UICONTROL 映射] 此时会显示步骤，为您提供一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关使用映射器界面和计算字段的完整步骤，请参阅 [数据准备UI指南](../../../../../data-prep/ui/mapping.md).

>[!IMPORTANT]
>
>在将源字段映射到目标XDM字段时，必须确保将指定的主标识字段映射到相应的目标XDM字段。

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![映射树，其中有四个源数据字段被映射到其相应的XDM架构字段。](../../../../images/tutorials/create/campaign/mapping.png)

### 查看数据流

的 **[!UICONTROL 审阅]** 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。

审核数据流后，选择 **[!UICONTROL 完成]** 并为创建数据流留出一些时间。

![显示连接和数据集信息的审核页面。](../../../../images/tutorials/create/campaign/review.png)

### 监控数据集活动

创建数据流后，您可以监控通过其摄取的数据，以查看有关摄取速率以及成功和失败批次的信息。

要开始查看数据集活动，请选择 **[!UICONTROL 数据流]** 的子目录。

![选择了数据流标题选项卡的源目录页面。](../../../../images/tutorials/create/campaign/dataflows.png)

接下来，从显示的数据流列表中选择目标数据集。

![选定了Adobe Campaign投放日志目标数据集的现有数据流列表。](../../../../images/tutorials/create/campaign/target-dataset.png)

此时会显示数据集活动页面。 在此处，您可以看到有关数据流性能的信息，包括摄取率、成功批次和失败批次。

本页还为您提供了一个界面，用于更新数据流的元数据描述、启用部分摄取和错误诊断，以及向数据集添加新数据。

![一个界面，其中包含表示选定数据集的摄取率的图形。](../../../../images/tutorials/create/campaign/dataset-activity.png)

## 后续步骤

通过阅读本教程，您已成功创建了一个数据流，以将Campaign v8投放日志和跟踪日志数据引入平台。 传入数据现在可由下游Platform服务使用，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-Time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)
