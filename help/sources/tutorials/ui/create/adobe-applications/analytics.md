---
title: 在UI中创建Adobe Analytics源连接
description: 了解如何在UI中创建Adobe Analytics源连接，将消费者数据接入Adobe Experience Platform。
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '2298'
ht-degree: 6%

---

# 在UI中创建Adobe Analytics源连接

本教程提供了在UI中创建Adobe Analytics源连接的步骤，以便将Adobe Analytics报表包数据引入Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [Experience Data Model (XDM)系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
* [Real-time Customer Profile](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

### 关键术语

请务必了解本文档中使用的以下关键术语：

* **标准属性**：标准属性是Adobe预定义的任何属性。 它们对于所有客户具有相同的含义，并且在 [!DNL Analytics] 源数据和 [!DNL Analytics] 架构字段组。
* **自定义属性**：自定义属性是中自定义变量层次结构中的任何属性 [!DNL Analytics]. 在Adobe Analytics实施中使用自定义属性将特定信息捕获到报表包中，这些属性的使用因报表包而异。 自定义属性包括eVar、prop和列表。 请参阅以下内容 [[!DNL Analytics] 有关转化变量的文档](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 以了解有关eVar的更多信息。
* **自定义字段组中的任何属性**：源自客户创建的字段组的属性都是用户定义的属性，既不是标准属性，也不是自定义属性。
* **友好名称**：友好名称是中由人工提供的自定义变量标签 [!DNL Analytics] 实现。 请参阅以下内容 [[!DNL Analytics] 有关转化变量的文档](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 以了解有关友好名称的详细信息。

## 创建与Adobe Analytics的源连接

>[!NOTE]
>
>在生产沙盒中创建Analytics源数据流时，将创建两个数据流：
>
>* 一个数据流，将历史报表包数据回填到13个月的数据湖。 此数据流在回填完成后结束。
>* 将实时数据发送到数据湖和的数据流 [!DNL Real-Time Customer Profile]. 此数据流持续运行。

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕中显示多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 您还可以使用搜索栏缩小显示的源。

在 **[!UICONTROL Adobe应用程序]** 类别，选择 **[!UICONTROL Adobe Analytics]** 然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/analytics/catalog.png)

### 选择数据

>[!IMPORTANT]
>
>屏幕上列出的报表包可能来自不同的区域。 您有责任了解您的数据限制和义务，以及如何跨地区在Adobe Experience Platform中使用这些数据。 请确保贵公司允许这样做。

此 **[!UICONTROL Analytics源添加数据]** 步骤为您提供以下列表 [!DNL Analytics] 用于创建源连接的报表包数据。

报表包是构成基础的数据容器 [!DNL Analytics] 报表。 一个组织可以有多个报表包，每个报表包中包含不同的数据集。

您可以从任何区域（美国、英国或新加坡）摄取报告包，前提是它们映射到与在中创建源连接的Experience Platform沙盒实例相同的组织。 只能使用单个活动数据流摄取报表包。 已在您使用的沙盒或其他沙盒中摄取不可选的报告包。

可以建立多个绑定内连接，将多个报表包纳入同一沙盒中。 如果报表包具有不同的变量架构（例如eVar或事件），则应将其映射到自定义字段组中的特定字段，并使用避免数据冲突 [数据准备](../../../../../data-prep/ui/mapping.md). 只能将报表包添加到单个沙盒中。

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>只有不存在数据冲突(例如两个含义不同的自定义属性（eVar、列表和prop）)，才能为实时客户资料启用多个报表包的数据。

创建 [!DNL Analytics] 源连接，选择一个报表包，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Analytics报告包一次只能为一个沙盒配置。 要将同一报表包导入其他沙盒，必须通过对其他沙盒的配置删除数据集流并重新实例化。—>

### 映射

>[!IMPORTANT]
>
>数据准备转换可能会增加整个数据流的延迟。 附加的延迟因转换逻辑的复杂性而异。

在映射您的 [!DNL Analytics] 将数据定位到XDM架构，您必须首先选择是使用默认架构还是自定义架构。

默认架构代表您创建新架构，包含 [!DNL Adobe Analytics ExperienceEvent Template] 字段组。 要使用默认架构，请选择 **[!UICONTROL 默认架构]**.

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

使用自定义架构，您可以为您的选择任何可用的架构 [!DNL Analytics] 数据，只要该架构具有 [!DNL Adobe Analytics ExperienceEvent Template] 字段组。 要使用自定义架构，请选择 **[!UICONTROL 自定义架构]**.

![custom-schema](../../../../images/tutorials/create/analytics/custom-schema.png)

此 [!UICONTROL 映射] 页面提供了一个将源字段映射到其相应目标架构字段的界面。 在此处，您可以将自定义变量映射到新架构字段组并应用数据准备支持的计算。 选择目标架构以启动映射过程。

>[!TIP]
>
>仅限具有以下特征的架构： [!DNL Adobe Analytics ExperienceEvent Template] 字段组显示在架构选择菜单中。 忽略其他架构。 如果您的报表包数据没有合适的架构，则必须创建新架构。 有关创建架构的详细步骤，请参阅 [在UI中创建和编辑架构](../../../../../xdm/ui/resources/schemas.md).

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

此 [!UICONTROL 映射标准字段] 部分显示面板 [!UICONTROL 应用的标准映射]， [!UICONTROL 不匹配的标准映射] 和 [!UICONTROL 自定义映射]. 有关每个类别的具体信息，请参阅下表：

| 映射标准字段 | 描述 |
| --- | --- |
| [!UICONTROL 应用的标准映射] | 此 [!UICONTROL 应用的标准映射] 面板显示已映射属性的总数。 标准映射是指源中所有属性之间的映射集 [!DNL Analytics] 中的数据和相应属性 [!DNL Analytics] 字段组。 它们是预映射的，无法编辑。 |
| [!UICONTROL 不匹配的标准映射] | 此 [!UICONTROL 不匹配的标准映射] 面板是指包含友好名称冲突的映射属性的数量。 如果您重复使用的架构已填充了来自其他报表包的字段描述符集，则会出现这些冲突。 您可以继续您的 [!DNL Analytics] 即使存在友好名称冲突的数据流。 |
| [!UICONTROL 自定义映射] | 此 [!UICONTROL 自定义映射] 面板显示映射的自定义属性的数量，包括eVar、prop和列表。 自定义映射是指源中自定义属性之间的映射集 [!DNL Analytics] 所选架构中包含的自定义字段组中的数据和属性。 |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

要预览 [!DNL Analytics] ExperienceEvent模板架构字段组，选择 **[!UICONTROL 视图]** 在 [!UICONTROL 应用的标准映射] 面板。

![view](../../../../images/tutorials/create/analytics/view.png)

此 [!UICONTROL Adobe Analytics ExperienceEvent模板架构字段组] 页面为您提供了一个用于检查架构结构的界面。 完成后，选择 **[!UICONTROL 关闭]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

Platform会自动检测您的映射集是否存在任何友好名称冲突。 如果映射集没有冲突，请选择 **[!UICONTROL 下一个]** 以继续。

![映射](../../../../images/tutorials/create/analytics/mapping.png)

>[!TIP]
>
>如果源报表包与所选架构之间存在友好名称冲突，您仍可以继续使用 [!DNL Analytics] 数据流，确认不会更改字段描述符。 或者，您可以选择使用一组空白描述符创建新架构。

#### 自定义映射

您可以使用数据准备函数为自定义属性添加新的自定义映射或计算字段。 要添加自定义映射，请选择 **[!UICONTROL 自定义]**.

![自定义](../../../../images/tutorials/create/analytics/custom.png)

根据需要，您可以选择以下任一选项 **[!UICONTROL 添加新映射]** 或 **[!UICONTROL 添加计算字段]** ，然后继续为自定义属性创建自定义映射。 有关如何使用数据准备功能的完整步骤，请参阅 [数据准备UI指南](../../../../../data-prep/ui/mapping.md).

以下文档提供了有关了解数据准备、计算字段和映射函数的更多资源：

* [数据准备概述](../../../../../data-prep/home.md)
* [数据准备映射函数](../../../../../data-prep/functions.md)
* [添加计算字段](../../../../../data-prep/ui/mapping.md#calculated-fields)

<!-- 
To use Data Prep functions and add new mapping or calculated fields for custom attributes, select **[!UICONTROL View custom mappings]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

Next, select **[!UICONTROL Add new mapping]**.

Depending on your needs, you can select either **[!UICONTROL Add new mapping]** or **[!UICONTROL Add calculated field]** from the options that appear. 

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

An empty mapping set appears. Select the mapping icon to add a source field.

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

You can use the interface to navigate through the source schema structure and identify the new source field that you want to use. Once you have selected the source field that you want to map, select **[!UICONTROL Select]**.

![select-mapping](../../../../images/tutorials/create/analytics/select-mapping.png)

Next, select the mapping icon under [!UICONTROL Target Field] to map your selected source field to its appropriate target field.

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

Similar to the source schema, you can use the interface to navigate through the target schema structure and select the target field you want to map to. Once you have selected the appropriate target field, select **[!UICONTROL Select]**.

![select-target-mapping](../../../../images/tutorials/create/analytics/select-target-mapping.png)

With your custom mapping set completed, select **[!UICONTROL Next]** to proceed.

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png) -->

### 筛选实时客户个人资料 {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="创建筛选规则"
>abstract="在将数据发送到实时客户配置文件时定义行级和列级筛选规则。使用行级筛选来应用条件并指示要&#x200B;**为配置文件提取包含**&#x200B;的数据。使用列级筛选来选择要&#x200B;**为配置文件提取排除**&#x200B;的数据列。筛选规则不适用于发送到数据湖的数据。"

完成映射后， [!DNL Analytics] 报表包数据之后，您可以应用过滤规则和条件来有选择地将数据包含或排除到实时客户档案的摄取中。 仅支持筛选 [!DNL Analytics] 仅在输入之前过滤数据和数据 [!DNL Profile.] 所有数据都会摄取到数据湖中。

#### 行级筛选

>[!IMPORTANT]
>
>使用行级筛选来应用条件并指示要&#x200B;**为配置文件提取包含**&#x200B;的数据。使用列级筛选来选择要&#x200B;**为配置文件提取排除**&#x200B;的数据列。

您可以筛选以下项的数据 [!DNL Profile] 在行级别和列级别引入。 行级筛选允许您定义字符串包含、等于、开始或结束于等条件。 您还可以使用行级筛选来连接条件，方法是 `AND` 以及 `OR`，并使用否定条件 `NOT`.

要筛选您的 [!DNL Analytics] 行级别的数据，选择 **[!UICONTROL 行筛选器]**.

![row-filter](../../../../images/tutorials/create/analytics/row-filter.png)

使用左边栏在架构层次结构中导航，并选择您选择的架构属性以进一步向下钻取特定架构。

![左边栏](../../../../images/tutorials/create/analytics/left-rail.png)

标识要配置的属性后，选择属性并将其从左边栏拖到筛选面板。

![filtering-panel](../../../../images/tutorials/create/analytics/filtering-panel.png)

要配置不同的条件，请选择 **[!UICONTROL 等于]** 然后从显示的下拉列表中选择一个条件。

可配置条件列表包括：

* [!UICONTROL 等于]
* [!UICONTROL 不等于]
* [!UICONTROL 开头为]
* [!UICONTROL 结束于]
* [!UICONTROL 结尾不为]
* [!UICONTROL 包含]
* [!UICONTROL 不包含]
* [!UICONTROL 存在]
* [!UICONTROL 不存在]

![条件](../../../../images/tutorials/create/analytics/conditions.png)

接下来，根据所选的属性输入要包括的值。 在以下示例中， [!DNL Apple] 和 [!DNL Google] 选择作为的一部分进行摄取 **[!UICONTROL 制造商]** 属性。

![include-manufacturer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

要进一步指定筛选条件，请从架构中添加其他属性，然后根据该属性添加值。 在以下示例中， **[!UICONTROL 模型]** 属性被添加，模型如 [!DNL iPhone 13] 和 [!DNL Google Pixel 6] 将进行筛选以供摄取。

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

要添加新容器，请选择省略号(`...`)图标，然后选择 **[!UICONTROL 添加容器]**.

![add-container](../../../../images/tutorials/create/analytics/add-container.png)

添加新容器后，选择 **[!UICONTROL 包括]** 然后选择 **[!UICONTROL 排除]** 从出现的下拉窗口中。

![排除](../../../../images/tutorials/create/analytics/exclude.png)

接下来，通过拖动架构属性并添加其要从筛选中排除的相应值来完成相同的过程。 在以下示例中， [!DNL iPhone 12]， [!DNL iPhone 12 mini]、和 [!DNL Google Pixel 5] 都是从的排除项中过滤而来的 **[!UICONTROL 模型]** 属性，横向排除在外 **[!UICONTROL 屏幕方向]**&#x200B;和型号 [!DNL A1633] 排除自 **[!UICONTROL 型号]**.

完成后，选择 **[!UICONTROL 下一个]**.

![exclude-examples](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### 列级筛选

选择 **[!UICONTROL 列筛选条件]** 以应用列级筛选。

![column-filter](../../../../images/tutorials/create/analytics/column-filter.png)

页面将更新为交互式架构树，在列级别显示架构属性。 在此处，您可以选择要从中排除的数据列 [!DNL Profile] 摄取。 或者，您可以展开列并选择特定的排除属性。

默认情况下，所有 [!DNL Analytics] 转到 [!DNL Profile] 通过此过程，可以从中排除XDM数据的分支 [!DNL Profile] 摄取。

完成后，选择 **[!UICONTROL 下一个]**.

![列已选择](../../../../images/tutorials/create/analytics/columns-selected.png)

### 提供数据流详细信息

此 **[!UICONTROL 数据流详细信息]** 此时将显示步骤，您必须在该步骤中提供数据流的名称和可选描述。 选择 **[!UICONTROL 下一个]** 完成后。

![数据流详细信息](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 请查看

此 [!UICONTROL 审核] 此时会显示步骤，允许您在创建新的Analytics数据流之前对其进行查看。 连接的详细信息按类别分组，包括：

* [!UICONTROL 连接]：显示连接的源平台。
* [!UICONTROL 数据类型]：显示选定的报表包及其对应的报表包ID。

![审核](../../../../images/tutorials/create/analytics/review.png)

### 监测数据流

创建数据流后，您可以监控通过它摄取的数据。 从 [!UICONTROL 目录] 屏幕，选择 **[!UICONTROL 数据流]** 查看与您的Analytics帐户关联的已建立流的列表。

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

此 **数据流** 屏幕。 在此页面上是一对数据集流，包括有关其名称、源数据、创建时间和状态的信息。

连接器实例化两个数据集流。 一个流表示回填数据，另一个流表示实时数据。 未针对用户档案配置回填数据，但会发送到数据湖，以用于分析和数据科学用例。

有关回填、实时数据及其各自延迟的更多信息，请参阅 [Analytics Data Connector概述](../../../../connectors/adobe-applications/analytics.md).

从列表中选择要查看的数据集流。

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

此 **[!UICONTROL 数据集活动]** 页面。 此页以图形形式显示消息的使用速率。 选择 **[!UICONTROL 数据治理]** 以访问标签设置字段。

![数据集活动](../../../../images/tutorials/create/analytics/dataset-activity.png)

您可以从以下位置查看数据集流的继承标签 [!UICONTROL 数据治理] 屏幕。 有关如何为来自Analytics的数据设置标签的更多信息，请访问 [数据使用标签指南](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

要删除数据流，请转到 [!UICONTROL 数据流] 页面，然后选择省略号(`...`)，然后选择 [!UICONTROL 删除].

![delete](../../../../images/tutorials/create/analytics/delete.png)

## 后续步骤和其他资源

创建连接后，将自动创建数据流以包含传入数据并使用您选择的架构填充数据集。 此外，还会进行数据回填，并摄取至多 13 个月的历史数据。当初始摄取完成时， [!DNL Analytics] 数据并由下游平台服务使用，例如 [!DNL Real-Time Customer Profile] 和分段服务。 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-Time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 概述](../../../../../query-service/home.md)

以下视频旨在支持您了解如何使用Adobe Analytics源连接器摄取数据：

>[!WARNING]
>
> 此 [!DNL Platform] 以下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
