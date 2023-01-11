---
keywords: Experience Platform；主页；热门主题；同意和首选项；同意；onetrust;OneTrust
solution: Experience Platform
title: 在UI中使用同意和首选项源创建数据流
type: Tutorial
description: 数据流是一项计划任务，用于从源中检索数据并将其摄取到平台数据集。 本教程提供了有关如何使用Platform UI为同意和首选项源创建数据流的步骤。
exl-id: 340b5945-baa1-4f79-88fa-2572606f6083
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# 在UI中使用同意和首选项源创建数据流

数据流是一项计划任务，用于从源中检索数据并将其摄取到Adobe Experience Platform中的数据集。 本教程提供了有关如何使用Platform UI为同意和首选项源创建数据流的步骤。

>[!NOTE]
>
>要创建数据流，您必须已拥有已通过身份验证的帐户 [!DNL OneTrust Integration] 来源。 请参阅 [创建 [!DNL OneTrust Integration] UI中的源连接](../../ui/create/consent-and-preferences/onetrust.md) 以了解更多信息。

## 快速入门

本教程需要对Platform的以下组件有一定的了解：

* [源](../../../home.md):平台允许从各种源摄取数据，同时让您能够使用构建、标记和增强传入数据 [!DNL Platform] 服务。
* [[!DNL Experience Data Model (XDM)] 系统](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [[!DNL Data Prep]](../../../../data-prep/home.md):允许数据工程师映射、转换和验证来自体验数据模型(XDM)的数据。

## 添加数据

在创建您的同意和首选项源帐户后， **[!UICONTROL 添加数据]** 步骤，为您提供一个界面以浏览同意和首选项帐户的表层次结构。

* 界面的左半部分是浏览器，其中显示了帐户中包含的数据表列表。 该界面还包含一个搜索选项，通过该选项，您可以快速识别要使用的源数据。
* 界面的右半部是一个预览面板，允许您预览多达100行数据。

>[!NOTE]
>
>搜索源数据选项适用于所有基于表的源(不包括Adobe Analytics、 [!DNL Amazon Kinesis]和 [!DNL Azure Event Hubs].

找到源数据后，选择表，然后选择 **[!UICONTROL 下一个]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## 提供数据流详细信息

的 [!UICONTROL 数据流详细信息] 页面允许您选择是要使用现有数据集还是新数据集。 在此过程中，您还可以配置 [!UICONTROL 配置文件数据集], [!UICONTROL 错误诊断], [!UICONTROL 部分摄取]和 [!UICONTROL 警报].

![数据流详细信息](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### 使用现有数据集

要将数据摄取到现有数据集，请选择 **[!UICONTROL 现有数据集]**. 您可以使用 [!UICONTROL 高级搜索] 选项，或者通过在下拉菜单中滚动浏览现有数据集列表来配置。 选择数据集后，请为数据流提供名称和描述。

![现有数据集](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### 使用新数据集

要摄取到新数据集，请选择 **[!UICONTROL 新数据集]** 然后，提供输出数据集名称和可选描述。 接下来，使用 [!UICONTROL 高级搜索] 选项或通过滚动下拉菜单中的现有架构列表来迁移。 选择架构后，请为数据流提供名称和描述。

![新数据集](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### 启用 [!DNL Profile] 和错误诊断

接下来，选择 **[!UICONTROL 配置文件数据集]** 切换为启用数据集 [!DNL Profile]. 这允许您创建实体属性和行为的整体视图。 所有数据 [!DNL Profile]-enabled数据集将包含在 [!DNL Profile] 和更改将在您保存数据流时应用。

[!UICONTROL 错误诊断] 为数据流中发生的任何错误记录启用详细的错误消息生成，而 [!UICONTROL 部分摄取] 允许您摄取包含错误的数据，最多可达您手动定义的特定阈值。 请参阅 [部分批量摄取概述](../../../../ingestion/batch-ingestion/partial.md) 以了解更多信息。

![配置文件和错误](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### 启用警报

您可以启用警报以接收有关数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的更多信息，请参阅 [使用UI订阅源警报](../alerts.md).

完成向数据流提供详细信息后，选择 **[!UICONTROL 下一个]**.

![警报](../../../images/tutorials/dataflow/table-based/alerts.png)

## 将数据字段映射到XDM架构

>[!IMPORTANT]
>
>不能将任何动态键对值映射为 [!DNL OneTrust] 到平台，且必须在目标架构中指定这些键，才能在摄取期间映射数据。

的 [!UICONTROL 映射] 此时会显示步骤，为您提供一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关使用映射器界面和计算字段的完整步骤，请参阅 [数据准备UI指南](../../../../data-prep/ui/mapping.md).

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![映射](../../../images/tutorials/dataflow/table-based/mapping.png)

## 计划摄取运行

的 [!UICONTROL 计划] 步骤，允许您配置摄取计划以使用配置的映射自动摄取选定的源数据。 默认情况下，计划设置为 `Once`. 要调整摄取频率，请选择 **[!UICONTROL 频率]** ，然后从下拉菜单中选择一个选项。

>[!TIP]
>
>在一次性摄取期间，间隔和回填不可见。

![调度](../../../images/tutorials/dataflow/table-based/scheduling.png)

如果将摄取频度设置为 `Minute`, `Hour`, `Day`或 `Week`，则必须设置一个间隔，以在每次摄取之间建立一个设置的时间范围。 例如，摄取频度设置为 `Day` 和间隔设置为 `15` 意味着您的数据流计划每15天摄取一次数据。

在此步骤中，您还可以启用 **回填** 并为数据的增量摄取定义一列。 回填用于摄取历史数据，而您为增量摄取定义的列允许将新数据与现有数据区分开。

有关计划配置的更多信息，请参阅下表。

| 字段 | 描述 |
| --- | --- |
| 频度 | 发生摄取的频率。 可选频率包括 `Once`, `Minute`, `Hour`, `Day`和 `Week`. |
| 间隔 | 一个整数，用于设置所选频率的间隔。 间隔的值应为非零整数，并应设置为大于或等于15。 |
| 开始时间 | UTC时间戳，指示何时设置进行第一次摄取。 开始时间必须大于或等于当前UTC时间。 |
| 回填 | 一个布尔值，用于确定最初摄取的数据。 如果启用了回填，则在首次计划摄取期间将摄取指定路径中的所有当前文件。 如果禁用回填，则只会摄取在首次摄取运行到开始时间之间加载的文件。 不会摄取在开始时间之前加载的文件。 |
| 加载增量数据的方式 | 一个选项，其中包含一组类型、日期或时间的筛选源架构字段。 此字段用于区分新数据和现有数据。 将根据选定列的时间戳摄取增量数据。 |

![回填](../../../images/tutorials/dataflow/table-based/backfill.png)

## 查看数据流

的 **[!UICONTROL 审阅]** 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。
* **[!UICONTROL 计划]**:显示摄取计划的活动期、频率和间隔。

审核数据流后，选择 **[!UICONTROL 完成]** 并为创建数据流留出一些时间。

![审查](../../../images/tutorials/dataflow/table-based/review.png)

## 监控数据流

创建数据流后，您可以监控通过其摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监控数据流的更多信息，请参阅 [监控UI中的帐户和数据流](../monitor.md).

## 删除数据流

您可以删除不再需要或使用错误创建的数据流 **[!UICONTROL 删除]** 函数 **[!UICONTROL 数据流]** 工作区。 有关如何删除数据流的更多信息，请参阅 [删除UI中的数据流](../delete.md).

## 后续步骤

通过阅读本教程，您已成功创建了一个数据流，用于将来自您同意和首选项源的数据引入Platform。 现在，下游可以使用传入数据 [!DNL Platform] 诸如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-Time Customer Profile] 概述](../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> 以下视频中显示的平台UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)
