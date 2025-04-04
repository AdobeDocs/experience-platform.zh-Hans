---
keywords: Experience Platform；主页；热门主题；支付连接器
solution: Experience Platform
title: 在UI中使用支付Source创建数据流
type: Tutorial
description: 数据流是一种计划任务，用于在源中检索数据并将其摄取到Experience Platform数据集。 本教程提供了有关如何使用Experience Platform UI为支付来源创建数据流的步骤。
exl-id: 7355435b-c038-4310-b04a-8ac6b6723b9b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1585'
ht-degree: 1%

---

# 在UI中为支付来源创建数据流

数据流是一种计划任务，用于在源中检索数据并将其摄取到Adobe Experience Platform中的数据集。 本教程提供了有关如何使用Experience Platform UI为支付来源创建数据流的步骤。

>[!NOTE]
>
>* 要创建数据流，您必须已拥有带支付源的经过身份验证的帐户。 在[源概述](../../../home.md#payments)中可找到在UI中创建不同支付源帐户的教程列表。
>* 要让Experience Platform摄取数据，必须将所有基于表的批处理源的时区配置为UTC时区。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [源](../../../home.md)： Experience Platform允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [[!DNL Experience Data Model (XDM)] 系统](../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。
* [[!DNL Data Prep]](../../../../data-prep/home.md)：允许数据工程师映射、转换和验证与Experience Data Model (XDM)之间的数据。

## 添加数据

创建付款源帐户后，将显示&#x200B;**[!UICONTROL 添加数据]**&#x200B;步骤，为您提供一个浏览付款源帐户表层次结构的界面。

* 界面的左半部分是一个浏览器，显示帐户中包含的数据表列表。 该界面还包括一个搜索选项，可让您快速识别要使用的源数据。
* 界面的右半部分是预览面板，允许您预览最多100行数据。

>[!NOTE]
>
>搜索源数据选项适用于除Adobe Analytics、[!DNL Amazon Kinesis]和[!DNL Azure Event Hubs]之外的所有基于表的源。

找到源数据后，请选择该表，然后选择&#x200B;**[!UICONTROL 下一步]**。

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## 提供数据流详细信息

[!UICONTROL 数据流详细信息]页面允许您选择是要使用现有数据集，还是使用新数据集。 在此过程中，您还可以配置[!UICONTROL 配置文件数据集]、[!UICONTROL 错误诊断]、[!UICONTROL 部分摄取]和[!UICONTROL 警报]的设置。

![数据流详细信息](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### 使用现有数据集

要将数据摄取到现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**。 您可以使用[!UICONTROL 高级搜索]选项或通过滚动下拉菜单中的现有数据集列表来检索现有数据集。 选择数据集后，为数据流提供名称和描述。

![现有数据集](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### 使用新数据集

要摄取到新数据集中，请选择&#x200B;**[!UICONTROL 新数据集]**，然后提供输出数据集名称和可选描述。 接下来，使用[!UICONTROL 高级搜索]选项或通过滚动下拉菜单中的现有架构列表来选择要映射到的架构。 选择架构后，为数据流提供名称和描述。

![新数据集](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### 启用[!DNL Profile]和错误诊断

接下来，选择&#x200B;**[!UICONTROL 配置文件数据集]**&#x200B;切换开关以为[!DNL Profile]启用您的数据集。 这允许您创建实体的属性和行为的整体视图。 来自所有已启用[!DNL Profile]的数据集的数据将包含在[!DNL Profile]中，并且更改会在您保存数据流时应用。

[!UICONTROL 错误诊断]允许为数据流中发生的任何错误记录生成详细的错误消息，而[!UICONTROL 部分摄取]允许您摄取包含错误的数据，摄取阈值为您手动定义的某个阈值。 有关详细信息，请参阅[部分批次摄取概述](../../../../ingestion/batch-ingestion/partial.md)。

![配置文件和错误](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### 启用警报

您可以启用警报以接收有关数据流状态的通知。 从列表中选择警报以订阅接收有关数据流状态的通知。 有关警报的详细信息，请参阅[使用UI订阅源警报指南](../alerts.md)。

完成向数据流提供详细信息后，选择&#x200B;**[!UICONTROL 下一步]**。

![警报](../../../images/tutorials/dataflow/table-based/alerts.png)

## 将数据字段映射到XDM架构

此时将显示[!UICONTROL 映射]步骤，该步骤为您提供了一个接口，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Experience Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的全面步骤，请参阅[数据准备UI指南](../../../../data-prep/ui/mapping.md)。

成功映射源数据后，选择&#x200B;**[!UICONTROL 下一步]**。

![映射](../../../images/tutorials/dataflow/table-based/mapping.png)

## 计划摄取运行

此时将显示[!UICONTROL 计划]步骤，允许您配置摄取计划，以使用配置的映射自动摄取选定的源数据。 默认情况下，计划设置为`Once`。 要调整您的摄取频率，请选择&#x200B;**[!UICONTROL 频率]**，然后从下拉菜单中选择一个选项。

>[!TIP]
>
>间隔和回填在一次性摄取期间不可见。

![计划](../../../images/tutorials/dataflow/table-based/scheduling.png)

如果将摄取频率设置为`Minute`、`Hour`、`Day`或`Week`，则必须设置一个间隔，以便在每次摄取之间建立一个设置的时间范围。 例如，摄取频率设置为`Day`，间隔设置为`15`意味着您的数据流计划每15天摄取一次数据。

在此步骤中，您还可以启用&#x200B;**回填**&#x200B;并为增量数据摄取定义列。 回填用于摄取历史数据，而您为增量摄取定义的列允许从现有数据中区分新数据。

有关计划配置的详细信息，请参阅下表。

| 计划配置 | 描述 |
| --- | --- |
| 频度 | 配置频率以指示数据流运行的频率。 您可以将频率设置为： <ul><li>**一次**：将频率设置为`once`以创建一次性引入。 创建一次性摄取数据流时，间隔和回填配置不可用。 默认情况下，调度频率设置为一次。</li><li>**分钟**：将频率设置为`minute`，以计划数据流以每分钟摄取数据。</li><li>**小时**：将频率设置为`hour`，以计划数据流每小时摄取数据。</li><li>**天**：将频率设置为`day`，以计划数据流每天摄取数据。</li><li>**周**：将频率设置为`week`，以计划数据流每周摄取数据。</li></ul> |
| 间隔 | 选择频率后，可以配置间隔设置以建立每次引入之间的时间范围。 例如，如果将频率设置为天并将间隔配置为15，则数据流将每15天运行一次。 不能将间隔设置为零。 每个频率的最小接受间隔值如下：<ul><li>**一次**：不适用</li><li>**分钟**： 15</li><li>**小时**： 1</li><li>**天**： 1</li><li>**周**： 1</li></ul> |
| 开始时间 | 预计运行的时间戳，以UTC时区显示。 |
| 回填 | 回填可确定最初摄取的数据。 如果启用了回填，则指定路径中的所有当前文件将在第一次计划摄取期间摄取。 如果禁用回填，则只摄取在第一次引入运行到开始时间之间加载的文件。 将不会摄取在开始时间之前加载的文件。 |
| 加载增量数据依据 | 一个选项，其中包含一组类型为、日期或时间的源架构字段。 您为&#x200B;**[!UICONTROL 加载增量数据(]**)选择的字段必须具有UTC时区的日期时间值，才能正确加载增量数据。 所有基于表的批处理源均可通过将增量列时间戳值与相应的流运行窗口UTC时间进行比较，然后复制源中的数据（如果在UTC时间窗口内发现任何新数据）来选择增量数据。 |

![回填](../../../images/tutorials/dataflow/table-based/backfill.png)

## 查看您的数据流

将显示&#x200B;**[!UICONTROL 审核]**&#x200B;步骤，允许您在创建新数据流之前对其进行审核。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括数据集所遵循的架构。
* **[!UICONTROL 计划]**：显示摄取计划的活动时段、频率和间隔。

查看数据流后，选择&#x200B;**[!UICONTROL 完成]**，然后等待一些时间来创建数据流。

![审核](../../../images/tutorials/dataflow/table-based/review.png)

## 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的详细信息，请参阅有关UI](../monitor.md)中[监视帐户和数据流的教程。

## 删除您的数据流

您可以删除不再必需的数据流或使用&#x200B;**[!UICONTROL 数据流]**&#x200B;工作区中提供的&#x200B;**[!UICONTROL 删除]**&#x200B;功能错误地创建的数据流。 有关如何删除数据流的详细信息，请参阅有关[在UI中删除数据流](../delete.md)的教程。

## 后续步骤

通过学习本教程，您已成功地创建了一个数据流，以将数据从您的支付来源引入Experience Platform。 下游[!DNL Experience Platform]服务（如[!DNL Real-Time Customer Profile]和[!DNL Data Science Workspace]）现在可以使用传入数据。 有关更多详细信息，请参阅以下文档：

* [[!DNL Real-Time Customer Profile] 概述](../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> 以下视频中显示的Experience Platform UI已过期。 有关最新的UI屏幕截图和功能，请参阅上述文档。
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)