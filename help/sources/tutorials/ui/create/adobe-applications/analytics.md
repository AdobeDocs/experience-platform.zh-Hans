---
title: 在UI中创建Adobe Analytics Source连接
description: 了解如何在UI中创建Adobe Analytics源连接，将消费者数据接入Adobe Experience Platform。
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2676'
ht-degree: 3%

---

# 在UI中创建Adobe Analytics源连接

本教程提供了在UI中创建Adobe Analytics源连接的步骤，以便将Adobe Analytics报表包数据引入Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
* [实时客户个人资料](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时客户个人资料。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 关键术语

请务必了解本文档中使用的以下关键术语：

* **标准属性**：标准属性是Adobe预定义的任何属性。 它们对所有客户具有相同的含义，并且在[!DNL Analytics]源数据和[!DNL Analytics]架构字段组中可用。
* **自定义属性**：自定义属性是[!DNL Analytics]中自定义变量层次结构中的任何属性。 在Adobe Analytics实施中使用自定义属性将特定信息捕获到报表包中，这些属性的使用因报表包而异。 自定义属性包括eVar、prop和列表。 有关eVar的详细信息，请参阅以下[[!DNL Analytics] 有关转化变量](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html)的文档。
* **自定义字段组中的任何属性**：源自客户创建的字段组的属性都是用户定义的属性，既不是标准属性，也不是自定义属性。
* **友好名称**：友好名称是[!DNL Analytics]实施中自定义变量的人工提供标签。 有关友好名称的详细信息，请参阅以下[[!DNL Analytics] 有关转化变量](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html)的文档。

## 创建与Adobe Analytics的源连接

>[!NOTE]
>
>在生产沙盒中创建Analytics源数据流时，将创建两个数据流：
>
>* 一个数据流，将历史报表包数据回填到13个月的数据湖。 此数据流在回填完成后结束。
>* 将实时数据发送到数据湖和[!DNL Real-Time Customer Profile]的数据流流。 此数据流持续运行。

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 您还可以使用搜索栏缩小显示的源。

在&#x200B;**[!UICONTROL Adobe应用程序]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Adobe Analytics]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/analytics/catalog.png)

### 选择数据

>[!IMPORTANT]
>
>屏幕上列出的报表包可能来自不同的区域。 您有责任了解您的数据限制和义务，以及如何跨地区在Adobe Experience Platform中使用这些数据。 请确保贵公司允许这样做。

**[!UICONTROL Analytics源添加数据]**&#x200B;步骤为您提供一个[!DNL Analytics]报表包数据的列表，以便您创建与的源连接。

报表包是构成[!DNL Analytics]报表基础的数据容器。 一个组织可以有多个报表包，每个报表包中包含不同的数据集。

您可以从任何区域（美国、英国或新加坡）摄取报告包，前提是它们映射到与Experience Platform沙盒实例（正在其中创建源连接）相同的组织。 只能使用单个活动数据流摄取报表包。 已在您使用的沙盒或其他沙盒中摄取不可选的报告包。

可以建立多个绑定内连接，将多个报表包纳入同一沙盒中。 如果报表包具有不同的变量架构（如eVar或事件），则应将它们映射到自定义字段组中的特定字段，并使用[数据准备](../../../../../data-prep/ui/mapping.md)避免数据冲突。 只能将报表包添加到单个沙盒中。

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>只有不存在数据冲突(例如两个含义不同的自定义属性（eVar、列表和prop）)，才能为实时客户资料启用多个报表包的数据。

要创建[!DNL Analytics]源连接，请选择一个报表包，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;!—Analytics报告包一次只能为一个沙盒配置。 要将同一报表包导入其他沙盒，必须通过对其他沙盒的配置删除数据集流并重新实例化。—>

### 映射

>[!IMPORTANT]
>
>数据准备转换可能会增加整个数据流的延迟。 附加的延迟因转换逻辑的复杂性而异。

在将[!DNL Analytics]数据映射到目标XDM架构之前，必须首先选择是使用默认架构还是自定义架构。

默认架构代表您创建新架构，包含[!DNL Adobe Analytics ExperienceEvent Template]字段组。 若要使用默认架构，请选择&#x200B;**[!UICONTROL 默认架构]**。

![default-schema](../../../../images/tutorials/create/analytics/default-schema.png)

使用自定义架构，您可以为[!DNL Analytics]数据选择任何可用的架构，前提是该架构具有[!DNL Adobe Analytics ExperienceEvent Template]字段组。 若要使用自定义架构，请选择&#x200B;**[!UICONTROL 自定义架构]**。

![自定义架构](../../../../images/tutorials/create/analytics/custom-schema.png)

[!UICONTROL 映射]页提供了一个将源字段映射到相应目标架构字段的界面。 在此处，您可以将自定义变量映射到新架构字段组并应用数据准备支持的计算。 选择目标架构以启动映射过程。

>[!TIP]
>
>架构选择菜单中仅显示具有[!DNL Adobe Analytics ExperienceEvent Template]字段组的架构。 忽略其他架构。 如果您的报表包数据没有合适的架构，则必须创建新架构。 有关创建架构的详细步骤，请参阅[在UI中创建和编辑架构指南](../../../../../xdm/ui/resources/schemas.md)。

![select-schema](../../../../images/tutorials/create/analytics/select-schema.png)

[!UICONTROL 映射标准字段]部分显示[!UICONTROL 应用的标准映射]、[!UICONTROL 不匹配的标准映射]和[!UICONTROL 自定义映射]的面板。 有关每个类别的具体信息，请参阅下表：

| 映射标准字段 | 描述 |
| --- | --- |
| [!UICONTROL 已应用标准映射] | 应用的[!UICONTROL 标准映射]面板显示映射属性的总数。 标准映射是指源[!DNL Analytics]数据中的所有属性与[!DNL Analytics]字段组中的相应属性之间的映射集。 它们是预映射的，无法编辑。 |
| [!UICONTROL 不匹配的标准映射] | [!UICONTROL 不匹配的标准映射]面板引用包含友好名称冲突的映射属性数。 如果您重复使用的架构已填充了来自其他报表包的字段描述符集，则会出现这些冲突。 即使存在友好名称冲突，您也可以继续处理[!DNL Analytics]数据流。 |
| [!UICONTROL 自定义映射] | [!UICONTROL 自定义映射]面板显示映射的自定义属性的数量，包括eVar、prop和列表。 自定义映射是指源[!DNL Analytics]数据的自定义属性与选定架构中包含的自定义字段组中的属性之间的映射集。 |

![映射标准字段](../../../../images/tutorials/create/analytics/map-standard-fields.png)

要预览[!DNL Analytics] ExperienceEvent模板架构字段组，请在[!UICONTROL 应用的标准映射]面板中选择&#x200B;**[!UICONTROL 查看]**。

![视图](../../../../images/tutorials/create/analytics/view.png)

[!UICONTROL Adobe Analytics ExperienceEvent模板架构字段组]页面为您提供了一个用于检查架构结构的界面。 完成后，选择&#x200B;**[!UICONTROL 关闭]**。

![字段组预览](../../../../images/tutorials/create/analytics/field-group-preview.png)

Experience Platform会自动检测映射集是否存在任何友好名称冲突。 如果映射集没有冲突，请选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![映射](../../../../images/tutorials/create/analytics/mapping.png)

>[!TIP]
>
>如果源报表包与所选架构之间存在友好名称冲突，您仍可以继续使用[!DNL Analytics]数据流，同时确认不会更改字段描述符。 或者，您可以选择使用一组空白描述符创建新架构。

#### 自定义映射

您可以使用数据准备函数为自定义属性添加新的自定义映射或计算字段。 要添加自定义映射，请选择&#x200B;**[!UICONTROL 自定义]**。

![自定义](../../../../images/tutorials/create/analytics/custom.png)

根据您的需要，您可以选择&#x200B;**[!UICONTROL 添加新映射]**&#x200B;或&#x200B;**[!UICONTROL 添加计算字段]**，然后继续为自定义属性创建自定义映射。 有关如何使用数据准备功能的完整步骤，请参阅[数据准备UI指南](../../../../../data-prep/ui/mapping.md)。

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

## 筛选实时客户轮廓 {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="创建筛选规则"
>abstract="在将数据发送到实时客户轮廓时定义行级和列级筛选规则。使用行级筛选来应用条件并指示要&#x200B;**为轮廓提取包含**&#x200B;的数据。使用列级筛选来选择要&#x200B;**为轮廓提取排除**&#x200B;的数据列。筛选规则不适用于发送到数据湖的数据。"

完成[!DNL Analytics]报表包数据的映射后，您可以应用筛选规则和条件以选择性地将数据包含或排除在摄取到Real-time Customer Profile的数据之外。 仅对[!DNL Analytics]数据提供筛选支持，并且仅在输入[!DNL Profile.]之前筛选数据。所有数据都已摄取到数据湖中。

>[!BEGINSHADEBOX]

**有关为实时客户个人资料准备和筛选Analytics数据的更多信息**

* 您可以将筛选功能用于流向个人资料的数据，但不能用于流向数据湖的数据。
* 可以对实时数据使用筛选，但无法筛选回填数据。
   * [!DNL Analytics]源未将数据回填到配置文件中。
* 如果您在[!DNL Analytics]流的初始设置期间使用数据准备配置，则这些更改也会应用于13个月的自动回填。
   * 但是，不适用于筛选，因为筛选仅保留用于实时数据。
* 数据准备会同时应用于流摄取路径和批量摄取路径。 如果您修改了现有的数据准备配置，则这些更改会应用到流摄取和批量摄取路径中的新传入数据。
   * 但是，任何数据准备配置均不适用于已摄取到Experience Platform中的数据，无论它是流数据还是批量数据。
* Analytics中的标准属性始终会自动映射。 因此，不能将转换应用于标准属性。
   * 但是，您可以筛选掉标准属性，只要Identity Service或配置文件中不需要这些属性。
* 无法使用列级筛选来筛选必填字段和标识字段。
* 虽然您可以过滤掉次要身份，特别是AAID和AACustomID，但无法过滤ECID。
* 发生转换错误时，相应的列将导致NULL。

>[!ENDSHADEBOX]

### 行级筛选

>[!IMPORTANT]
>
>使用行级筛选来应用条件并指示要&#x200B;**为轮廓提取包含**&#x200B;的数据。使用列级筛选选择要&#x200B;**排除以进行配置文件摄取**&#x200B;的数据列。

您可以在行级别和列级别筛选[!DNL Profile]摄取的数据。 行级筛选允许您定义字符串包含、等于、开始或结束于等条件。 您还可以使用行级筛选来使用`AND`和`OR`连接条件，并使用`NOT`否定条件。

要在行级别筛选[!DNL Analytics]数据，请选择&#x200B;**[!UICONTROL 行筛选器]**。

![行筛选器](../../../../images/tutorials/create/analytics/row-filter.png)

使用左边栏在架构层次结构中导航，并选择您选择的架构属性以进一步向下钻取特定架构。

![左边栏](../../../../images/tutorials/create/analytics/left-rail.png)

标识要配置的属性后，选择属性并将其从左边栏拖到筛选面板。

![筛选面板](../../../../images/tutorials/create/analytics/filtering-panel.png)

要配置不同的条件，请选择&#x200B;**[!UICONTROL 等于]**，然后从显示的下拉窗口中选择条件。

可配置条件列表包括：

* [!UICONTROL 等于]
* [!UICONTROL 不等于]
* [!UICONTROL 开头为]
* [!UICONTROL 结尾为]
* [!UICONTROL 结尾不是]
* [!UICONTROL 包含]
* [!UICONTROL 不包含]
* [!UICONTROL 存在]
* [!UICONTROL 不存在]

![条件](../../../../images/tutorials/create/analytics/conditions.png)

接下来，根据所选的属性输入要包括的值。 在以下示例中，选择[!DNL Apple]和[!DNL Google]作为&#x200B;**[!UICONTROL Manufacturer]**&#x200B;属性的一部分进行摄取。

![include-manufacturer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

要进一步指定筛选条件，请从架构中添加其他属性，然后根据该属性添加值。 在以下示例中，添加了&#x200B;**[!UICONTROL Model]**&#x200B;属性，并筛选了诸如[!DNL iPhone 13]和[!DNL Google Pixel 6]之类的模型以进行摄取。

![include-model](../../../../images/tutorials/create/analytics/include-model.png)

要添加新容器，请选择筛选界面右上角的省略号(`...`)，然后选择&#x200B;**[!UICONTROL 添加容器]**。

![添加容器](../../../../images/tutorials/create/analytics/add-container.png)

添加新容器后，选择&#x200B;**[!UICONTROL 包括]**，然后从显示的下拉窗口中选择&#x200B;**[!UICONTROL 排除]**。

![排除](../../../../images/tutorials/create/analytics/exclude.png)

接下来，通过拖动架构属性并添加其要从筛选中排除的相应值来完成相同的过程。 在下面的示例中，[!DNL iPhone 12]、[!DNL iPhone 12 mini]和[!DNL Google Pixel 5]都是从&#x200B;**[!UICONTROL 模型]**&#x200B;属性的排除项中筛选出来的，横向从&#x200B;**[!UICONTROL 屏幕方向]**&#x200B;中排除，型号[!DNL A1633]从&#x200B;**[!UICONTROL 型号]**&#x200B;中排除。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![排除示例](../../../../images/tutorials/create/analytics/exclude-examples.png)

### 列级筛选

从标题中选择&#x200B;**[!UICONTROL 列筛选器]**&#x200B;以应用列级筛选。

![列筛选器](../../../../images/tutorials/create/analytics/column-filter.png)

页面将更新为交互式架构树，在列级别显示架构属性。 在此处，您可以选择要从[!DNL Profile]引入中排除的数据列。 或者，您可以展开列并选择特定的排除属性。

默认情况下，所有[!DNL Analytics]都转至[!DNL Profile]，此进程允许从[!DNL Profile]引入中排除XDM数据的分支。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

已选择![列](../../../../images/tutorials/create/analytics/columns-selected.png)

### 筛选次要身份

使用列筛选器从配置文件摄取中排除辅助身份。 要筛选辅助身份，请选择&#x200B;**[!UICONTROL 列筛选器]**，然后选择&#x200B;**[!UICONTROL _identities]**。

仅当标识被标记为次要标识时，该过滤器才适用。 如果选择了身份，但某个事件到达时带有标记为主ID之一，则不会过滤掉这些身份。

![辅助标识](../../../../images/tutorials/create/analytics/secondary-identities.png)

### 提供数据流详细信息

此时将显示&#x200B;**[!UICONTROL 数据流详细信息]**&#x200B;步骤，您必须在该步骤中为数据流提供名称和可选描述。 完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![数据流详细信息](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 审查

此时将显示[!UICONTROL 审核]步骤，允许您在创建新的Analytics数据流之前对其进行审核。 连接的详细信息按类别分组，包括：

* [!UICONTROL 连接]：显示连接的源平台。
* [!UICONTROL 数据类型]：显示选定的报表包及其对应的报表包ID。

![审核](../../../../images/tutorials/create/analytics/review.png)

## 监测数据流 {#monitor-your-dataflow}

数据流完成后，在源目录中选择&#x200B;**[!UICONTROL 数据流]**&#x200B;以监视数据的活动和状态。

![已选择“数据流”选项卡的源目录。](../../../../images/tutorials/create/analytics/select-dataflows.png)

此时将显示您组织中现有Analytics数据流的列表。 在此处，选择一个目标数据集以查看其相应的摄取活动。

![您组织中现有Adobe Analytics数据流的列表。](../../../../images/tutorials/create/analytics/select-target-dataset.png)

[!UICONTROL 数据集活动]页面提供了有关从Analytics发送到Experience Platform的数据进度的信息。 界面会显示一些量度，例如上个月的总记录数、过去七天摄取的记录数总数以及上个月的数据大小。

源实例化两个数据集流。 一个流表示回填数据，另一个流表示实时数据。 回填数据未配置为摄取到Real-time Customer Profile，而是发送到数据湖，以用于分析和数据科学用例。

有关回填、实时数据及其各自延迟的更多信息，请阅读[Analytics源概述](../../../../connectors/adobe-applications/analytics.md)。

![给定目标数据集的数据集活动页面，用于Adobe Analytics数据。](../../../../images/tutorials/create/analytics/dataset-activity.png)

>[!NOTE]
>
>数据集活动页面不显示有关批次的信息，因为Analytics源连接器完全由Adobe管理。 您可以通过查看所摄取记录的相关量度来监控数据流动。

## 删除您的数据流 {#delete-dataflow}

要删除您的Analytics数据流，请从源工作区的顶部标题中选择&#x200B;**[!UICONTROL 数据流]**。 使用数据流页面查找要删除的Analytics数据流，然后选择它旁边的省略号(`...`)。 接下来，使用下拉菜单并选择&#x200B;**[!UICONTROL 删除]**。

* 删除实时Analytics数据流也将删除其基础数据集。
* 删除回填Analytics数据流不会删除基础数据集，但将停止其相应报表包的回填过程。 如果删除回填数据流，则摄取的数据可能仍会通过数据集查看。

## 后续步骤和其他资源

创建连接后，将自动创建数据流以包含传入数据并使用您选择的架构填充数据集。 此外，还会进行数据回填，并摄取至多13个月的历史数据。 完成初始摄取后，[!DNL Analytics]个数据将由下游Experience Platform服务（如[!DNL Real-Time Customer Profile]和分段服务）使用。 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-Time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 概述](../../../../../query-service/home.md)

以下视频旨在支持您了解如何使用Adobe Analytics Source Connector摄取数据：

>[!WARNING]
>
> 以下视频中显示的[!DNL Experience Platform] UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
