---
keywords: Experience Platform；主页；热门主题；Analytics源连接器；Analytics连接器；Analytics源；Analytics
solution: Experience Platform
title: 在UI中创建Adobe Analytics源连接
type: Tutorial
description: 了解如何在UI中创建Adobe Analytics源连接，以将消费者数据引入Adobe Experience Platform。
exl-id: 5ddbaf63-feaa-44f5-b2f2-2d5ae507f423
source-git-commit: 3530c91cd36e9e2729515827978e6115857f2405
workflow-type: tm+mt
source-wordcount: '2390'
ht-degree: 5%

---

# 在UI中创建Adobe Analytics源连接

本教程提供了在UI中创建Adobe Analytics源连接以将Adobe Analytics报表包数据引入Adobe Experience Platform的步骤。

## 快速入门

本教程需要对Experience Platform的以下组件有一定的了解：

* [Experience Data Model(XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
* [实时客户资料](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 关键术语

请务必了解本文档中使用的以下关键术语：

* **标准属性**:标准属性是指由Adobe预定义的任何属性。 对于所有客户，它们包含相同的含义，并可在 [!DNL Analytics] 源数据和 [!DNL Analytics] 架构字段组。
* **自定义属性**:自定义属性是 [!DNL Analytics]. 自定义属性用于在Adobe Analytics实施中将特定信息捕获到报表包中，并且在报表包和报表包中的使用方式可能有所不同。 自定义属性包括eVar、prop和列表。 请参阅以下内容 [[!DNL Analytics] 转化变量文档](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 以了解有关eVar的更多信息。
* **自定义字段组中的任何属性**:源自客户创建的字段组的属性都由用户定义，因此既不是标准属性，也不是自定义属性。
* **友好名称**:友好名称是人为 [!DNL Analytics] 实施。 请参阅以下内容 [[!DNL Analytics] 转化变量文档](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/conversion-variables/conversion-var-admin.html?lang=en) 有关友好名称的详细信息。

## 创建与Adobe Analytics的源连接

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以为其创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 您还可以使用搜索栏来缩小显示的源范围。

在 **[!UICONTROL Adobe应用程序]** 类别，选择 **[!UICONTROL Adobe Analytics]** 然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/analytics/catalog.png)

### 选择数据

>[!IMPORTANT]
>
>屏幕上列出的报表包可能来自不同地区。 您有责任了解数据的限制和义务，以及如何在Adobe Experience Platform跨区域使用这些数据。 请确保您的公司允许执行此操作。

的 **[!UICONTROL Analytics源添加数据]** 步骤会为您提供 [!DNL Analytics] 用于创建源连接的报表包数据。

报表包是构成 [!DNL Analytics] 报表。 组织可以有多个报表包，每个报表包包含不同的数据集。

您可以从任何区域（美国、英国或新加坡）摄取报表包，前提是这些报表包已映射到与其中创建源连接的Experience Platform沙盒实例相同的组织。 只能使用单个活动数据流摄取报表包。 已摄取无法选择的报表包（位于您使用的沙盒中或位于其他沙盒中）。

可以建立多个绑定连接，以将多个报表包引入同一沙盒。 如果报表包的变量架构不同（如eVar或事件），则应将它们映射到自定义字段组中的特定字段，并避免使用 [数据准备](../../../../../data-prep/ui/mapping.md). 报表包只能添加到单个沙盒。

![](../../../../images/tutorials/create/analytics/report-suite.png)

>[!NOTE]
>
>仅当不存在数据冲突时，才能为实时客户用户档案启用多个报表包中的数据，例如两个具有不同含义的自定义属性（eVar、列表和prop）。

创建 [!DNL Analytics] 源连接，选择报表包，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/analytics/add-data.png)

&lt;! — 可以一次为一个沙盒配置Analytics报表包。 要将同一报表包导入其他沙盒，必须删除数据集流，并通过其他沙盒的配置再次实例化该流。—>

### 映射

>[!IMPORTANT]
>
>数据准备转换可能会为整个数据流添加延迟。 添加的额外延迟因转换逻辑的复杂性而异。

在映射 [!DNL Analytics] 要定位XDM架构的数据，您必须首先选择使用的是默认架构还是自定义架构。

默认架构代表您创建一个新架构，其中包含 [!DNL Adobe Analytics ExperienceEvent Template] 字段组。 要使用默认架构，请选择 **[!UICONTROL 默认架构]**.

![默认模式](../../../../images/tutorials/create/analytics/default-schema.png)

通过自定义架构，您可以为 [!DNL Analytics] 数据，只要该架构具有 [!DNL Adobe Analytics ExperienceEvent Template] 字段组。 要使用自定义架构，请选择 **[!UICONTROL 自定义架构]**.

![自定义模式](../../../../images/tutorials/create/analytics/custom-schema.png)

的 [!UICONTROL 映射] 该页面提供了一个界面，用于将源字段映射到其相应的目标架构字段。 从此处，您可以将自定义变量映射到新架构字段组，并按照数据准备的支持应用计算。 选择目标架构以启动映射过程。

>[!TIP]
>
>仅具有 [!DNL Adobe Analytics ExperienceEvent Template] 字段组显示在架构选择菜单中。 忽略其他架构。 如果报表包数据没有适当的架构，则必须创建新架构。 有关创建架构的详细步骤，请参阅 [在UI中创建和编辑架构](../../../../../xdm/ui/resources/schemas.md).

![选择模式](../../../../images/tutorials/create/analytics/select-schema.png)

的 [!UICONTROL 映射标准字段] 部分显示面板 [!UICONTROL 已应用标准映射], [!UICONTROL 不匹配标准映射] 和 [!UICONTROL 自定义映射]. 有关每个类别的具体信息，请参阅下表：

| 映射标准字段 | 描述 |
| --- | --- |
| [!UICONTROL 已应用标准映射] | 的 [!UICONTROL 已应用标准映射] 面板会显示映射属性的总数。 标准映射是指源中所有属性之间的映射集 [!DNL Analytics] 数据和 [!DNL Analytics] 字段组。 这些是预映射的，无法编辑。 |
| [!UICONTROL 不匹配标准映射] | 的 [!UICONTROL 不匹配标准映射] 面板是指包含友好名称冲突的已映射属性数量。 当您重新使用的架构已从其他报表包中填充了一组字段描述符时，会出现这些冲突。 您可以继续 [!DNL Analytics] 即使存在友好名称冲突的数据流。 |
| [!UICONTROL 自定义映射] | 的 [!UICONTROL 自定义映射] 面板显示映射的自定义属性数量，包括eVar、prop和列表。 自定义映射是指源中自定义属性之间的映射集 [!DNL Analytics] 所选架构中包含的自定义字段组中的数据和属性。 |

![map-standard-fields](../../../../images/tutorials/create/analytics/map-standard-fields.png)

预览 [!DNL Analytics] ExperienceEvent模板架构字段组，选择 **[!UICONTROL 查看]** 在 [!UICONTROL 已应用标准映射] 的上界。

![view](../../../../images/tutorials/create/analytics/view.png)

的 [!UICONTROL Adobe Analytics ExperienceEvent模板架构字段组] 页面为您提供了一个用于检查架构结构的界面。 完成后，选择 **[!UICONTROL 关闭]**.

![field-group-preview](../../../../images/tutorials/create/analytics/field-group-preview.png)

平台会自动检测映射集中是否存在任何友好名称冲突。 如果映射集没有冲突，请选择 **[!UICONTROL 下一个]** 以继续。

![映射](../../../../images/tutorials/create/analytics/mapping.png)

如果源报表包与您选择的架构之间存在友好名称冲突，您仍可以继续 [!DNL Analytics] 数据流，确认字段描述符不会更改。 或者，您也可以选择使用一组空白描述符创建新架构。

选择 **[!UICONTROL 下一个]** 以继续。

![注意](../../../../images/tutorials/create/analytics/caution.png)

#### 自定义映射

要使用数据准备函数并为自定义属性添加新映射或计算字段，请选择 **[!UICONTROL 查看自定义映射]**.

![view-custom-mapping](../../../../images/tutorials/create/analytics/view-custom-mapping.png)

接下来，选择 **[!UICONTROL 添加新映射]**.

根据您的需要，您可以选择 **[!UICONTROL 添加新映射]** 或 **[!UICONTROL 添加计算字段]** 中。

![add-new-mapping](../../../../images/tutorials/create/analytics/add-new-mapping.png)

将出现空映射集。 选择映射图标以添加源字段。

![select-source-field](../../../../images/tutorials/create/analytics/select-source-field.png)

您可以使用界面在源架构结构中导航，并标识要使用的新源字段。 选择要映射的源字段后，选择 **[!UICONTROL 选择]**.

![选择映射](../../../../images/tutorials/create/analytics/select-mapping.png)

接下来，选择下方的映射图标 [!UICONTROL 目标字段] 将您选择的源字段映射到相应的目标字段。

![select-target-field](../../../../images/tutorials/create/analytics/select-target-field.png)

与源架构类似，您可以使用界面在目标架构结构中导航，并选择要映射到的目标字段。 选择相应的目标字段后，选择 **[!UICONTROL 选择]**.

![select-target映射](../../../../images/tutorials/create/analytics/select-target-mapping.png)

完成自定义映射集后，选择 **[!UICONTROL 下一个]** 以继续。

![complete-custom-mapping](../../../../images/tutorials/create/analytics/complete-custom-mapping.png)

以下文档提供了有关了解数据准备、计算字段和映射函数的更多资源：

* [数据准备概述](../../../../../data-prep/home.md)
* [数据准备映射函数](../../../../../data-prep/functions.md)
* [添加计算字段](../../../../../data-prep/ui/mapping.md#calculated-fields)

### 实时客户资料筛选（测试版） {#filtering-for-profile}

>[!CONTEXTUALHELP]
>id="platform_data_prep_analytics_filtering"
>title="创建筛选规则"
>abstract="在将数据发送到实时客户配置文件时定义行级和列级筛选规则。使用行级筛选来应用条件并指示要&#x200B;**为配置文件提取包含**&#x200B;的数据。使用列级筛选来选择要&#x200B;**为配置文件提取排除**&#x200B;的数据列。筛选规则不适用于发送到数据湖的数据。"

>[!IMPORTANT]
>
>支持过滤 [!DNL Analytics] 数据当前为测试版，并非所有用户都能使用。 文档和功能可能会发生变化。

完成 [!DNL Analytics] 报表包数据中，您可以应用过滤规则和条件，以便有选择地将数据从摄取到实时客户资料中或从中排除。 仅对 [!DNL Analytics] 仅在输入之前过滤数据和数据 [!DNL Profile.] 所有数据都会被摄取到数据湖中。

#### 行级过滤

>[!IMPORTANT]
>
>使用行级筛选来应用条件并指示要&#x200B;**为配置文件提取包含**&#x200B;的数据。使用列级筛选来选择要&#x200B;**为配置文件提取排除**&#x200B;的数据列。

您可以过滤数据 [!DNL Profile] 在行级别和列级别摄取。 利用行级筛选，可定义标准，如字符串包含、等于、开始或结束。 您还可以使用行级过滤来连接使用 `AND` 以及 `OR`，使用 `NOT`.

过滤 [!DNL Analytics] 在行级别，选择 **[!UICONTROL 行过滤器]**.

![row-filter](../../../../images/tutorials/create/analytics/row-filter.png)

使用左边栏可在架构层次结构中导航，并选择您选择的架构属性，以进一步深入查看特定架构。

![左边栏](../../../../images/tutorials/create/analytics/left-rail.png)

确定要配置的属性后，选择该属性，然后将其从左边栏拖至筛选面板。

![过滤面板](../../../../images/tutorials/create/analytics/filtering-panel.png)

要配置不同的条件，请选择 **[!UICONTROL 等于]** 然后，从显示的下拉窗口中选择一个条件。

可配置条件列表包括：

* [!UICONTROL 等于]
* [!UICONTROL 不等于]
* [!UICONTROL 开头]
* [!UICONTROL 止于]
* [!UICONTROL 结尾不为]
* [!UICONTROL 包含]
* [!UICONTROL 不包含]
* [!UICONTROL 存在]
* [!UICONTROL 不存在]

![条件](../../../../images/tutorials/create/analytics/conditions.png)

接下来，根据您选择的属性输入要包含的值。 在以下示例中， [!DNL Apple] 和 [!DNL Google] 的 **[!UICONTROL 制造商]** 属性。

![include-manufacturer](../../../../images/tutorials/create/analytics/include-manufacturer.png)

要进一步指定筛选条件，请从架构中添加另一个属性，然后根据该属性添加值。 在以下示例中， **[!UICONTROL 模型]** 属性，并添加模型，例如 [!DNL iPhone 13] 和 [!DNL Google Pixel 6] 会过滤以获取。

![包含模型](../../../../images/tutorials/create/analytics/include-model.png)

要添加新容器，请选择省略号(`...`)，然后选择 **[!UICONTROL 添加容器]**.

![添加容器](../../../../images/tutorials/create/analytics/add-container.png)

添加新容器后，选择 **[!UICONTROL 包括]** 然后选择 **[!UICONTROL 排除]** 从显示的下拉窗口中。

![排除](../../../../images/tutorials/create/analytics/exclude.png)

接下来，通过拖动架构属性并添加要从筛选中排除的相应值，完成同一过程。 在以下示例中， [!DNL iPhone 12], [!DNL iPhone 12 mini]和 [!DNL Google Pixel 5] 全部从排除项中过滤 **[!UICONTROL 模型]** 属性中，横向将从 **[!UICONTROL 屏幕方向]**、和型号 [!DNL A1633] 从 **[!UICONTROL 型号]**.

完成后，选择 **[!UICONTROL 下一个]**.

![exclude-examples](../../../../images/tutorials/create/analytics/exclude-examples.png)

#### 列级过滤

选择 **[!UICONTROL 列过滤器]** 从标题中应用列级过滤。

![列过滤器](../../../../images/tutorials/create/analytics/column-filter.png)

该页面将更新为交互式架构树，在列级别显示您的架构属性。 从此处，您可以选择要从中排除的数据列 [!DNL Profile] 摄取。 或者，您也可以展开列并选择要排除的特定属性。

默认情况下，所有 [!DNL Analytics] 转到 [!DNL Profile] 并且此过程允许将XDM数据的分支从 [!DNL Profile] 摄取。

完成后，选择 **[!UICONTROL 下一个]**.

![列选定](../../../../images/tutorials/create/analytics/columns-selected.png)

### 提供数据流详细信息

的 **[!UICONTROL 数据流详细信息]** 步骤，您必须为数据流提供名称和可选描述。 选择 **[!UICONTROL 下一个]** 完成。

![数据流详细信息](../../../../images/tutorials/create/analytics/dataflow-detail.png)

### 请查看

的 [!UICONTROL 审阅] 步骤，允许您在创建新的Analytics数据流之前查看该数据流。 连接的详细信息按类别分组，包括：

* [!UICONTROL 连接]:显示连接的源平台。
* [!UICONTROL 数据类型]:显示选定的报表包及其相应的报表包ID。

![审查](../../../../images/tutorials/create/analytics/review.png)

### 监控数据流

创建数据流后，您可以监控通过其摄取的数据。 从 [!UICONTROL 目录] 屏幕，选择 **[!UICONTROL 数据流]** 查看与您的Analytics帐户关联的已建流量列表。

![select-dataflows](../../../../images/tutorials/create/analytics/select-dataflows.png)

的 **数据流** 屏幕。 本页是一对数据集流，包括有关其名称、源数据、创建时间和状态的信息。

连接器可实例化两个数据集流。 一个流程表示回填数据，另一个流程用于实时数据。 回填数据未为用户档案配置，而是会发送到数据湖以用于分析和数据科学用例。

有关回填、实时数据及其各自延迟的更多信息，请参阅 [Analytics Data Connector概述](../../../../connectors/adobe-applications/analytics.md).

从列表中选择要查看的数据集流。

![select-target-dataset](../../../../images/tutorials/create/analytics/select-target-dataset.png)

的 **[!UICONTROL 数据集活动]** 页面。 此页面以图表形式显示消息的使用率。 选择 **[!UICONTROL 数据管理]** 来访问标签字段。

![数据集活动](../../../../images/tutorials/create/analytics/dataset-activity.png)

您可以查看 [!UICONTROL 数据管理] 屏幕。 有关如何为来自Analytics的数据设置标签的更多信息，请访问 [数据使用标签指南](../../../../../data-governance/labels/user-guide.md).

![data-gov](../../../../images/tutorials/create/analytics/data-gov.png)

要删除数据流，请转到 [!UICONTROL 数据流] 页面，然后选择省略号(`...`)，然后选择 [!UICONTROL 删除].

![删除](../../../../images/tutorials/create/analytics/delete.png)

## 后续步骤和其他资源

创建连接后，将自动创建数据流以包含传入数据，并使用您选择的架构填充数据集。 此外，还会进行数据回填，并摄取至多 13 个月的历史数据。完成初始摄取后， [!DNL Analytics] 并供下游Platform服务(例如 [!DNL Real-Time Customer Profile] 和Segmentation Service。 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-Time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)
* [[!DNL Query Service] 概述](../../../../../query-service/home.md)

以下视频旨在支持您了解如何使用Adobe Analytics源连接器摄取数据：

>[!WARNING]
>
> 的 [!DNL Platform] 以下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)
