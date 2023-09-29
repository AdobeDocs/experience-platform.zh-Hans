---
keywords: Experience Platform；主页；热门主题；监视器身份；监视器数据流；数据流；身份；
description: Adobe Experience Platform 身份服务通过跨设备和系统桥接身份，使您能够全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。本教程提供了有关如何使用Experience Platform用户界面监视带标识的数据流的说明。
title: 在UI中监控数据流以查找身份
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 14%

---

# 监测UI中标识的数据流

Adobe Experience Platform 身份服务通过跨设备和系统桥接身份，使您能够全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

监视功能板提供了数据在身份中的活动的可视表示形式，包括数据身份的状态。 本教程将介绍如何使用“监视仪表板”通过Experience Platform用户界面监视数据的身份，从而使您能够跟踪身份处理的状态。

## 快速入门 {#getting-started}

- [数据流](../home.md)：数据流表示跨Platform移动数据的数据作业。 数据流在不同的服务之间配置，有助于将数据从源连接器移动到目标数据集，以 [!DNL Identity] 和 [!DNL Profile]、和 [!DNL Destinations].
   - [数据流运行](../../sources/notifications.md)：数据流运行是基于所选数据流的频率配置的定期计划作业。
- [Identity Service](../../identity-service/home.md)：通过跨设备和系统桥接身份，更好地了解个人客户及其行为。
- [沙盒](../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

## 监视身份仪表板 {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="标识处理"
>abstract="标识处理视图包含有关提取到标识服务的记录的信息，包括添加的标识数量、创建的图表数量和更新的图表数量。查看量度定义指南以了解有关量度和图表的更多信息。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="数据流运行详细信息"
>abstract="数据流运行详细信息页面显示有关标识数据流运行的更多信息，包括其组织 ID 和数据流运行 ID。"

要访问 **[!UICONTROL 身份]** 仪表板，选择 **[!UICONTROL 监控]** 在左侧导航中。 一旦在 **[!UICONTROL 监控]** 页面上，选择 **[!UICONTROL 身份]** 卡片。

![身份卡。 其中显示了有关接收的记录数、摄取的记录数和成功率的信息。](../assets/ui/monitor-identities/focus-card.png)

在主页面上 **[!UICONTROL 身份]** 仪表板， **[!UICONTROL 身份]** 卡片可显示有关接收的记录总数、提取的记录数以及记录提取成功率的信息。

仪表板本身包含有关身份处理的量度。 默认情况下，仪表板将显示过去24小时内贵组织源的身份处理详细信息。

![身份仪表板。 显示有关每个源接收的记录数的信息。](../assets/ui/monitor-identities/sources.png)

此 [!UICONTROL 身份处理] 页面包含有关摄取到的记录的信息 [!DNL Identity Service]，包括添加的身份数、创建的图形以及更新的图形。

以下指标可用于此仪表板视图：

| 身份量度 | 描述 |
| ---------------- | ----------- |
| **[!UICONTROL 已接收的记录]** | 从数据湖接收的记录数。 |
| **[!UICONTROL 失败的记录]** | 由于数据错误而未引入到Platform中的记录数。 |
| **[!UICONTROL 跳过的记录数]** | 已摄取但未摄取到的记录数 [!DNL Identity Service] 因为记录行中只有一个标识符。 |
| **[!UICONTROL 已提取的记录]** | 摄取到的记录数 [!DNL Identity Service]. |
| **[!UICONTROL 已添加身份]** | 添加到中的新标识符的净数量 [!DNL Identity Service]. |
| **[!UICONTROL 创建的图]** | 在中创建的净新身份图数 [!DNL Identity Service]. |
| **[!UICONTROL 已更新图]** | 用新边更新的现有标识图的数量。 |
| **[!UICONTROL 失败的数据流总数]** | 失败的数据流运行次数。 |

您可以选择过滤器图标 ![过滤器图标](../assets/ui/monitor-identities/filter.png) 位于源名称旁边，可查看选定源的数据流的身份处理信息。

![过滤器图标会突出显示。 选择此图标可查看所选源的数据流。](../assets/ui/monitor-identities/sources-filter.png)

或者，您可以选择 **[!UICONTROL 数据流]** 打开切换可查看过去24小时内贵组织数据流的身份处理详细信息。

![身份仪表板。 显示有关每个数据流接收的身份数的信息。](../assets/ui/monitor-identities/dataflows.png)

以下指标可用于此仪表板视图：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL 数据流]** | 数据流的名称。 |
| **[!UICONTROL 数据集]** | 数据流正在插入的数据集的名称。 |
| **[!UICONTROL 源名称]** | 数据流所属的源的名称。 |
| **[!UICONTROL 已接收的记录]** | 从数据湖接收的记录数。 |
| **[!UICONTROL 失败的记录]** | 由于数据错误而未引入到Platform中的记录数。 |
| **[!UICONTROL 跳过的记录数]** | 已摄取但未摄取到的记录数 [!DNL Identity Service] 因为记录行中只有一个标识符。 |
| **[!UICONTROL 已提取的记录]** | 摄取到的记录数 [!DNL Identity Service]. |
| **[!UICONTROL 记录总数]** | 所有记录的总数，包括失败的记录、跳过的记录、添加的身份和重复的记录。 |
| **[!UICONTROL 已添加身份]** | 添加到中的新标识符的净数量 [!DNL Identity Service]. |
| **[!UICONTROL 创建的图]** | 在中创建的净新身份图数 [!DNL Identity Service]. |
| **[!UICONTROL 已更新图]** | 用新边更新的现有标识图的数量。 |
| **[!UICONTROL 失败的数据流总数]** | 失败的数据流运行次数。 |

选择过滤器图标 ![筛选](../assets/ui/monitor-identities/filter.png) 在数据流运行开始时间旁边，查看有关 [!DNL Identity] 数据流运行。

![过滤器图标会突出显示。 选择此图标可查看有关所选数据流的详细信息。](../assets/ui/monitor-identities/dataflows-filter.png)

此 [!UICONTROL 数据流运行详细信息] 页面显示有关 [!DNL Identity] 数据流运行，包括其组织ID和数据流运行ID。 此页面还显示提供的相应错误代码和错误消息。 [!DNL Identity Service]时，如果摄取过程中发生任何错误。

![此时会显示一个仪表板，其中显示有关所选数据流的详细信息。](../assets/ui/monitor-identities/dataflow-run-details.png)

以下指标可用于此仪表板视图：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL 已接收的记录]** | 从数据湖接收的记录数。 |
| **[!UICONTROL 失败的记录]** | 由于数据错误而未引入到Platform中的记录数。 |
| **[!UICONTROL 跳过的记录数]** | 已摄取但未摄取到的记录数 [!DNL Identity Service] 因为记录行中只有一个标识符。 |
| **[!UICONTROL 已提取的记录]** | 摄取到的记录数 [!DNL Identity Service]. |
| **[!UICONTROL 已添加身份]** | 添加到中的新标识符的净数量 [!DNL Identity Service]. |
| **[!UICONTROL 创建的图]** | 在中创建的净新身份图数 [!DNL Identity Service]. |
| **[!UICONTROL 已更新图]** | 用新边更新的现有标识图的数量。 |
| **[!UICONTROL 状态]** | 定义数据流的整体状态。 可能的状态值包括： <ul><li>`Success`：指示数据流处于活动状态并根据提供的计划摄取数据。</li><li>`Failed`：指示数据流的激活过程因错误而中断。 </li><li>`Processing`：表示数据流尚未处于活动状态。 创建新数据流后，经常会立即出现此状态。</li></ul> |
| **[!UICONTROL 数据流运行开始]** | 数据流开始运行的日期和时间。 |
| **[!UICONTROL 上次更新时间]** | 上次更新数据流的日期和时间。 |
| **[!UICONTROL 错误摘要]** | 如果数据流运行失败，将显示错误代码并总结数据流运行失败的原因。 |
| **[!UICONTROL 数据流运行ID]** | 数据流运行的ID。 |
| **[!UICONTROL IMS组织ID]** | 数据流运行所属的组织ID。 |

此外，您可以选择切换以查看失败的记录或跳过的记录。 错误部分包括有关错误代码以及失败或排除的记录数的详细信息。
