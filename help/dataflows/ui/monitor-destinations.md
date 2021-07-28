---
keywords: Experience Platform；主页；热门主题；监视帐户；监视数据流；数据流；目标
description: 利用目标，可从Adobe Experience Platform向无数外部合作伙伴激活数据。 本教程提供了有关如何使用Experience Platform用户界面监控目标数据流的说明。
solution: Experience Platform
title: 在UI中监控目标的数据流
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 96855ec4e42e7adb17dc36a734561f63f926693b
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 0%

---

# 在UI中监控目标的数据流

利用目标，可从Adobe Experience Platform向无数外部合作伙伴激活数据。 Platform通过提供数据流的透明度，使跟踪数据到目标的流程变得更加轻松。

监控仪表板可直观地表示数据流的历程，包括数据被激活到的目标。 本教程提供了有关如何直接在目标工作区中监控数据流或使用监控功能板通过Experience Platform用户界面监控目标的数据流的说明。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [数据流](../home.md):数据流是跨平台移动数据的数据作业的表示形式。数据流是跨不同的服务配置的，有助于将数据从源连接器移动到目标数据集，移动到[!DNL Identity]和[!DNL Profile]，以及[!DNL Destinations]。
   - [数据流运行](../../sources/notifications.md):数据流运行是基于所选数据流的频率配置的定期计划作业。
- [目标](../../destinations/home.md):目标是与常用应用程序的预建集成，允许从平台无缝激活数据以用于跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例。
- [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 在目标工作区中监控数据流

在Platform UI的&#x200B;**[!UICONTROL 目标]**&#x200B;工作区中，导航到&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡，然后选择要查看的目标名称。

![](../assets/ui/monitor-destinations/select-destination.png)

将显示现有数据流的列表。 本页列出了可查看的数据流，包括有关其目标、用户名、数据流数量和状态的信息。

有关状态的更多信息，请参阅下表：

| 状态 | 描述 |
| ------ | ----------- |
| 已启用 | `Enabled`状态表示数据流处于活动状态，并正在根据提供的计划摄取数据。 |
| 已禁用 | `Disabled`状态表示数据流处于非活动状态，且不会摄取任何数据。 |
| 处理时间 | `Processing`状态表示数据流尚未处于活动状态。 此状态通常会在创建新数据流后立即出现。 |
| 错误 | `Error`状态表示数据流的激活过程已中断。 |

### 为流目标运行数据流

对于流目标， [!UICONTROL 数据流运行]选项卡会针对数据流运行的度量数据提供每小时更新。 标有的最显着的统计数据是关于身份的。

标识表示用户档案的不同方面。 例如，如果某个用户档案同时包含电话号码和电子邮件地址，则该用户档案将具有两个身份。

将显示单个运行及其特定量度的列表，以及以下身份总数：

- **[!UICONTROL 已激活的身份]**:为激活而创建或更新的配置文件身份的总数。
- **[!UICONTROL 排除的身份]**:根据缺少属性和同意违规跳过以进行激活的配置文件标识的总数。
- **[!UICONTROL 身份失败]**:由于错误而未激活到目标的配置文件标识的总数。

![](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

每个数据流运行都显示以下详细信息：

- **[!UICONTROL 数据流运行开始]**:数据流运行开始的时间。
- **[!UICONTROL 处理时间]**:数据流处理所花费的时间。
- **[!UICONTROL 收到的用户档案]**:数据流中接收的用户档案总数。
- **[!UICONTROL 已激活的身份]**:成功激活到选定目标的用户档案标识总数。
- **[!UICONTROL 排除的身份]**:根据缺少属性和同意违规而排除进行激活的配置文件标识总数。
- **[!UICONTROL 标]** 识失败由于错误而未激活到目标的配置文件标识总数。
- **[!UICONTROL 激活率]**:已成功激活或跳过的已接收身份的百分比。以下公式演示了如何计算此值：
   ![](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL 状态]**:表示数据流处于的状态：完成  或 [!UICONTROL 处理]。 Completed表示在一小时内摄取了相应数据流运行的所有标识。 处理意味着数据流运行尚未完成。

要查看特定数据流运行的详细信息，请从列表中选择运行的开始时间。

数据流运行的详细信息页面包含其他信息，如接收的用户档案数、激活的标识数、失败的标识数和排除的标识数。

![](../assets/ui/monitor-destinations/dataflow-details-stream.png)

详细信息页面还显示失败的身份和排除的身份的列表。 将显示失败和排除的身份的信息，包括错误代码、身份计数和描述。 默认情况下，列表会显示失败的标识。 要显示跳过的标识，请选择&#x200B;**[!UICONTROL 已排除的标识]**&#x200B;切换开关。

![](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### 为批处理目标运行数据流

对于批处理目标，[!UICONTROL 数据流运行]选项卡提供有关数据流运行的量度数据。 将显示单个运行及其特定量度的列表，以及以下身份总数：

- **[!UICONTROL 已激活的身份]**:成功激活到选定目标的单个配置文件标识的计数。
- **[!UICONTROL 排除的身份]**:根据缺少属性和同意违规，为选定目标排除用于激活的个人配置文件标识的计数。

![](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

每个数据流运行都显示以下详细信息：

- **[!UICONTROL 数据流运行开始]**:数据流运行开始的时间。
- **[!UICONTROL 处理时间]**:处理数据流运行所花费的时间。
- **[!UICONTROL 收到的用户档案]**:数据流中接收的用户档案总数。此值每60分钟更新一次。
- **[!UICONTROL 已激活的身份]**:成功激活到选定目标的用户档案标识总数。
- **[!UICONTROL 排除的身份]**:根据缺少属性和同意违规而排除进行激活的配置文件标识总数。
- **[!UICONTROL 状态]**:表示数据流处于的状态。这可以是三种状态之一：[!UICONTROL Success]、[!UICONTROL 失败]和[!UICONTROL Processing]。  成功表示数据流处于活动状态，且正在根据其提供的计划摄取数据。 失败，表示由于错误，数据激活已挂起。 处理是指数据流尚未处于活动状态，通常在创建新数据流时会遇到该数据流。

要查看特定数据流运行的详细信息，请从列表中选择运行的开始时间。

>[!NOTE]
>
>根据目标数据流的调度频率生成数据流运行。 将针对应用于区段的每个合并策略运行单独的数据流。

数据流的详细信息页面除了数据流列表中显示的详细信息之外，还显示有关数据流的更多具体信息：

- **[!UICONTROL 数据大小]**:正在摄取的数据流的大小。
- **[!UICONTROL 文件总数]**:数据流中摄取的文件总数。
- **[!UICONTROL 上次更新时间]**:上次更新数据流运行的时间。

![](../assets/ui/monitor-destinations/dataflow-batch.png)

详细信息页面还显示失败的身份和排除的身份的列表。 将显示失败和排除的标识的信息，包括错误代码和描述。 默认情况下，列表会显示失败的标识。 要显示排除的身份，请选择&#x200B;**[!UICONTROL 排除的身份]**&#x200B;切换开关。

![](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## 监控目标功能板 {#monitoring-destinations-dashboard}

要访问[!UICONTROL 监视]功能板，请选择&#x200B;**[!UICONTROL 监视]**（![监视图标](../assets/ui/monitor-destinations/monitoring-icon.png)）
)。 在[!UICONTROL 监视]页面上，选择[!UICONTROL 目标]。 [!UICONTROL 监视]功能板包含有关目标运行作业的量度和信息。

功能板的中心是“激活”面板，其中包含量度和图表，用于显示有关导出到目标的数据激活率的数据。

![](../assets/ui/monitor-destinations/dashboard-graph.png)


默认情况下，显示的数据包含过去24小时的激活率。 选择&#x200B;**[!UICONTROL 最近24小时]**&#x200B;以调整显示的记录的时间范围。 可用选项包括&#x200B;**[!UICONTROL 最近24小时]**、**[!UICONTROL 最近7天]**&#x200B;和&#x200B;**[!UICONTROL 最近30天]**。 或者，您也可以在显示的日历弹出窗口中选择日期。 选择日期后，选择&#x200B;**[!UICONTROL Apply]**&#x200B;以调整显示信息的时间范围。

>[!NOTE]
>
>以下屏幕截图显示了过去30天的激活率，而不是过去24小时的激活率。 您可以通过选择&#x200B;**[!UICONTROL 最近30天]**&#x200B;来调整时间范围。

![](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

默认情况下会显示该图表，您可以禁用该图表以展开下面的目标列表。 选择&#x200B;**[!UICONTROL 量度和图形]**&#x200B;切换开关以禁用图形。

**[!UICONTROL Activation]**&#x200B;面板显示至少包含一个现有帐户的目标列表。 此列表还包含有关以下内容的信息：接收的用户档案、激活的用户档案记录、失败的用户档案记录、跳过的用户档案记录、失败的数据流总数以及这些目标的上次更新日期。

![](../assets/ui/monitor-destinations/dashboard-destinations.png)

您还可以过滤目标列表，以仅显示选定的目标类别。 选择&#x200B;**[!UICONTROL My destinations]**&#x200B;下拉列表，然后选择要筛选的目标类型。

![](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

此外，您还可以在搜索栏中输入目标，以隔离到单个目标。 如果要查看目标的数据流，可以选择其旁边的过滤器![filter](../assets/ui/monitor-destinations/filter.png)以查看其活动数据流的列表。

![](../assets/ui/monitor-destinations/filtered-destinations.png)

如果要查看所有目标中的所有现有数据流，请选择&#x200B;**[!UICONTROL 数据流]**。

将显示数据流列表，按目标分组。 您可以查看特定数据流的其他详细信息，方法是：查找要监视的目标，选择该目标旁边的过滤器![filter](../assets/ui/monitor-destinations/filter.png)，然后选择要获取更多信息的数据流旁边的过滤器![filter](../assets/ui/monitor-destinations/filter.png)。

![](../assets/ui/monitor-destinations/dashboard-dataflows.png)


“数据流运行”页显示有关数据流运行的信息，包括数据流运行开始时间、处理时间、收到的用户档案、激活的身份、排除的身份、身份失败、激活速率和状态。 要查看有关特定数据流运行的更多详细信息，请选择数据流运行开始时间旁边的筛选器![filter](../assets/ui/monitor-destinations/filter.png)。

![](../assets/ui/monitor-destinations/dashboard-dataflows-filter.png)

数据流详细信息页面除了数据流列表中显示的详细信息之外，还显示有关数据流的更多具体信息：

- **[!UICONTROL 数据流运行ID]**:数据流的ID。
- **[!UICONTROL IMS组织ID]**:数据流所属的IMS组织。
- **[!UICONTROL 上次更新时间]**:上次更新数据流运行的时间。

详细信息页面还显示失败的身份和排除的身份的列表。 将显示失败和排除的身份的信息，包括错误代码、身份计数和描述。 默认情况下，列表会显示失败的标识。 要显示跳过的标识，请选择&#x200B;**[!UICONTROL 已排除的标识]**&#x200B;切换开关。

![](../assets/ui/monitor-destinations/identities-excluded.png)

## 后续步骤

通过阅读本指南，您现在知道如何监控批处理和流目标的数据流，包括所有相关信息，如处理时间、激活率和状态。 要了解有关Platform中数据流的更多信息，请阅读[数据流概述](../home.md)。 要了解有关目标的更多信息，请阅读[目标概述](../../destinations/home.md)。