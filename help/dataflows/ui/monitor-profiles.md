---
keywords: Experience Platform；主页；热门主题；监控配置文件；监控数据流；数据流；配置文件；实时客户配置文件；
description: 实时客户配置文件允许您通过组合来自多个渠道的数据（包括在线、离线、CRM和第三方）来查看每个客户的整体视图。 本教程提供了有关如何使用Experience Platform用户界面使用配置文件监视数据流的说明。
title: 在UI中监控用户档案的数据流
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1d60afdf486642398a2d31302db339eb9cb45130
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 6%

---

# 在UI中监控用户档案的数据流

实时客户配置文件允许您通过组合来自多个渠道的数据（包括在线、离线、CRM和第三方）来查看每个客户的整体视图。 用户档案允许您将客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

监视仪表板在配置文件中为数据活动提供可视化表示形式，包括数据配置文件的状态。 本教程介绍了如何使用Experience Platform用户界面使用监视仪表板监视数据配置文件，从而允许您跟踪配置文件处理的状态。

## 快速入门 {#getting-started}

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

- [数据流](../home.md)：数据流是跨Experience Platform移动数据的数据作业的表示形式。 数据流在不同服务之间配置，帮助将数据从源连接器移动到目标数据集、[!DNL Identity]和[!DNL Profile]以及[!DNL Destinations]。
   - [数据流运行](../../sources/notifications.md)：数据流运行是基于所选数据流的频率配置的周期性计划作业。
- [实时客户个人资料](../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时客户个人资料。
- [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 监控轮廓仪表板 {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="轮廓处理"
>abstract="轮廓处理视图包含有关提取到轮廓服务的记录的信息，包括创建的轮廓片段数、更新的轮廓片段数以及轮廓片段总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="数据流运行详细信息"
>abstract="数据流运行详细信息页面显示有关轮廓数据流运行的更多信息，包括其组织 ID 和数据流运行 ID。"

要访问&#x200B;**[!UICONTROL Profiles]**&#x200B;仪表板，请在左侧导航中选择&#x200B;**[!UICONTROL Monitoring]**。 在&#x200B;**[!UICONTROL Monitoring]**&#x200B;页面上，选择&#x200B;**[!UICONTROL Profiles]**&#x200B;信息卡。

![配置文件卡。 显示有关接收的记录数、创建和更新的配置文件片段数以及成功率的信息。](../assets/ui/monitor-profiles/focus-card.png)

在主&#x200B;**[!UICONTROL Profiles]**&#x200B;仪表板上，**[!UICONTROL Profiles]**&#x200B;卡片显示有关接收的记录总数、创建和更新的配置文件片段的数量，以及创建和更新配置文件片段的成功率的信息。

功能板本身包含有关配置文件处理的量度。 默认情况下，仪表板将显示过去24小时内贵组织来源的个人资料处理详细信息。

![用户档案仪表板。 将显示有关每个源接收的配置文件记录数的信息。](../assets/ui/monitor-profiles/sources.png)

[!UICONTROL Profile processing]页面包含有关摄取到[!DNL Profile]的记录的信息，包括创建的配置文件片段的数量、更新的配置文件片段以及配置文件片段的总数。

以下指标可用于此仪表板视图：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL Source name]** | 源的名称。 |
| **[!UICONTROL Records received]** | 从数据湖接收的记录数。 |
| **[!UICONTROL Records failed]** | 已摄取但因错误未摄取到[!DNL Profile]中的记录数。 |
| **[!UICONTROL Profile fragments created]** | 添加的新[!DNL Profile]净片段的数量。 |
| **[!UICONTROL Profile fragments updated]** | 已更新现有[!DNL Profile]片段的数量。 |
| **[!UICONTROL Total Profile fragments]** | 写入[!DNL Profile]的记录总数，包括所有已更新的现有[!DNL Profile]片段和已创建的新[!DNL Profile]片段。 |
| **[!UICONTROL Total failed dataflows]** | 失败的数据流运行次数。 |

您可以选择源名称旁边的过滤器图标![过滤器图标](/help/images/icons/filter.png)以查看所选源的数据流的配置文件处理信息。

或者，您可以在切换中选择&#x200B;**[!UICONTROL Dataflows]**&#x200B;以查看过去24小时内贵组织数据流的配置文件处理详细信息。

![用户档案仪表板。 将显示有关每个数据流接收的配置文件记录数的信息。](../assets/ui/monitor-profiles/dataflows.png)

以下指标可用于此仪表板视图：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL Dataflow]** | 数据流的名称。 |
| **[!UICONTROL Dataset]** | 数据流正在插入的数据集的名称。 |
| **[!UICONTROL Source name]** | 数据流所属的源的名称。 |
| **[!UICONTROL Data type]** | 从数据集接收的数据类型。 |
| **[!UICONTROL Records received**] | 从数据湖接收的记录数。 |
| **[!UICONTROL Records failed]** | 已摄取但因错误未摄取到[!DNL Profile]中的记录数。 |
| **[!UICONTROL Profile fragments created]** | 添加的新[!DNL Profile]净片段的数量。 |
| **[!UICONTROL Profile fragments updated]** | 已更新的现有[!DNL Profile]片段的数量 |
| **[!UICONTROL Total Profile fragments]** | 写入[!DNL Profile]的记录总数，包括所有已更新的现有[!DNL Profile]片段和已创建的新[!DNL Profile]片段。 |
| **[!UICONTROL Total failed flow runs]** | 失败的数据流运行次数。 |
| **[!UICONTROL Last active]** | 上次运行数据流的时间戳。 |

选择数据流运行开始时间旁边的过滤器图标![过滤器](/help/images/icons/filter.png)以查看有关您的[!DNL Profile]数据流运行的更多信息。

此时会出现一个仪表板，其中显示所有数据流运行。 此仪表板包含有关数据流运行的量度，以及显示成功率、创建的配置文件片段和更新的配置文件片段的图表。

![数据流运行仪表板。 显示有关数据流运行的信息。](../assets/ui/monitor-profiles/dataflow-run.png)

以下指标可用于此仪表板视图：

>[!NOTE]
>
>当数据流运行处于&#x200B;**[!UICONTROL Processing]**&#x200B;状态时，您可以通过查看摄取进程中的检查点状态来查看有关准备情况的信息。
>
>![显示配置文件摄取准备情况气泡。](../assets/ui/monitor-profiles/profile-ingestion-readiness.png){zoomable="yes" width="300"}

| 量度 | 描述 |
| ------ | ----------- |
| **[!UICONTROL Dataflow run start]** | 数据流以UTC时间开始运行的时间。 |
| **[!UICONTROL Data type]** | 数据流接收的数据类型。 |
| **[!UICONTROL Records received]** | 从数据湖接收的记录数。 |
| **[!UICONTROL Records failed]** | 已摄取但因错误未摄取到[!DNL Profile]中的记录数。 |
| **[!UICONTROL Profile fragments created]** | 添加的新[!DNL Profile]净片段的数量。 |
| **[!UICONTROL Profile fragments updated]** | 已更新现有[!DNL Profile]片段的数量。 |
| **[!UICONTROL Total profile fragments]** | 写入[!DNL Profile]的记录总数，包括所有已更新的现有[!DNL Profile]片段和已创建的新[!DNL Profile]片段。 |
| **[!UICONTROL Processing time]** | 数据流运行处理所用的时间。 |
| **[!UICONTROL Status]** | 数据流运行的状态。 可能的值包括[!UICONTROL Success]、[!UICONTROL Failed]、[!UICONTROL Queued]和[!UICONTROL Processing]。 |
| **[!UICONTROL Ready for customer segmentation]** | 显示所摄取的记录是否准备好用于客户细分的状态。 可能的值包括[!UICONTROL Yes]、[!UICONTROL Failed]、[!UICONTROL Queued]和[!UICONTROL Processing]。 即使数据流的&#x200B;**状态**&#x200B;正在处理，如果此字段的值为“是”，则可以在客户细分中使用用户档案。 |
| **[!UICONTROL Ready for lookup]** | 显示已摄取的记录是否可以在Adobe Journey Optimizer查找中使用的状态。  可能的值包括[!UICONTROL Yes]、[!UICONTROL Failed]、[!UICONTROL Queued]和[!UICONTROL Processing]。 即使数据流的&#x200B;**状态**&#x200B;正在处理，如果此字段的值为“是”，则可以在Journey Optimizer查找中使用配置文件。 |

[!UICONTROL Dataflow run details]页面显示有关您的[!DNL Profile]数据流运行的更多信息，包括其组织ID和数据流运行ID。 此页面还会显示由[!DNL Profile]提供的相应错误代码和错误消息（如果在摄取过程中发生任何错误）。

![将显示显示选定数据流详细信息的仪表板。](../assets/ui/monitor-profiles/dataflow-run-details.png)

以下指标可用于此仪表板视图：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL Records received]** | 从数据湖接收的记录数。 |
| **[!UICONTROL Records failed]** | 已摄取但因错误未摄取到[!DNL Profile]中的记录数。 |
| **[!UICONTROL Profile fragments created]** | 添加的新[!DNL Profile]净片段的数量。 |
| **[!UICONTROL Profile fragments updated]** | 已更新现有[!DNL Profile]片段的数量。 |
| **[!UICONTROL Status]** | 定义数据流的整体状态。 可能的状态值包括： <ul><li>`Success`：指示数据流处于活动状态并根据提供的计划摄取数据。</li><li>`Failed`：表示数据流的激活过程因错误而中断。 </li><li>`Processing`：指示数据流尚未处于活动状态。 创建新数据流后，经常会立即出现此状态。</li></ul> |
| **[!UICONTROL Dataflow run start]** | 数据流开始运行的日期和时间。 |
| **[!UICONTROL Last updated]** | 上次更新数据流的日期和时间。 |
| **[!UICONTROL Error summary]** | 如果数据流运行失败，将显示错误代码并总结数据流运行失败的原因。 |
| **[!UICONTROL Dataflow run ID]** | 数据流运行的ID。 |
| **[!UICONTROL IMS org ID]** | 数据流运行所属的组织ID。 |

此外，您可以选择切换以查看失败的记录或跳过的记录。 错误部分包括有关错误代码以及失败或排除的记录数的详细信息。
