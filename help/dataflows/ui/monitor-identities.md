---
keywords: Experience Platform；主页；热门主题；监视器身份；监视数据流；数据流；身份；
description: Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而全面了解客户及其行为。 本教程提供了有关如何使用Experience Platform用户界面通过标识监控数据流的说明。
title: 在UI中监控身份的数据流
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 8%

---

# 在UI中监控标识的数据流

Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而全面了解客户及其行为。

监控仪表板可直观地显示数据在身份内的活动，包括数据的身份状态。 本教程提供了有关如何使用监控仪表板通过Experience Platform用户界面监控数据身份的说明，从而允许您跟踪身份处理的状态。

## 快速入门 {#getting-started}

- [数据流](../home.md):数据流是跨平台移动数据的数据作业的表示形式。 数据流是跨不同的服务进行配置的，有助于将数据从源连接器移动到目标数据集，并 [!DNL Identity] 和 [!DNL Profile]和 [!DNL Destinations].
   - [数据流运行](../../sources/notifications.md):数据流运行是基于所选数据流的频率配置的定期计划作业。
- [Identity Service](../../identity-service/home.md):通过跨设备和系统桥接身份，更好地了解各个客户及其行为。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

## 监控身份仪表板 {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="标识处理"
>abstract="标识处理视图包含有关提取到标识服务的记录的信息，包括添加的标识数量、创建的图表数量和更新的图表数量。查看量度定义指南以了解有关量度和图表的更多信息。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="数据流运行详细信息"
>abstract="数据流运行详细信息页面显示有关标识数据流运行的更多信息，包括其组织 ID 和数据流运行 ID。"

访问 **[!UICONTROL 标识]** 功能板，选择 **[!UICONTROL 监控]** 中。 在 **[!UICONTROL 监控]** 页面，选择 **[!UICONTROL 标识]** 卡。

![身份卡。 显示了有关已接收记录数、已摄取记录数和成功率的信息。](../assets/ui/monitor-identities/focus-card.png)

主 **[!UICONTROL 标识]** 功能板， **[!UICONTROL 标识]** 卡片显示有关已接收记录总数、已摄取记录数以及记录摄取成功率的信息。

功能板本身包含有关身份处理的量度。 默认情况下，功能板将显示贵组织过去24小时来源的身份处理详细信息。

![身份功能板。 显示有关每个源接收的记录数的信息。](../assets/ui/monitor-identities/sources.png)

的 [!UICONTROL 身份处理] 页面包含有关摄取到的记录的信息 [!DNL Identity Service]，包括添加的标识数、创建的图表和更新的图表。

以下量度可用于此功能板视图：

| 身份量度 | 描述 |
| ---------------- | ----------- |
| **[!UICONTROL 已接收的记录]** | 从数据湖接收的记录数。 |
| **[!UICONTROL 失败的记录]** | 由于数据中的错误而未摄取到平台中的记录数。 |
| **[!UICONTROL 跳过的记录数]** | 已摄取但未被摄取的记录数 [!DNL Identity Service] 因为记录行中只有一个标识符。 |
| **[!UICONTROL 已提取的记录]** | 摄取到的记录数 [!DNL Identity Service]. |
| **[!UICONTROL 添加了身份]** | 添加到的新标识符净数 [!DNL Identity Service]. |
| **[!UICONTROL 创建的图形]** | 在中创建的新身份图的净数量 [!DNL Identity Service]. |
| **[!UICONTROL 更新的图表]** | 使用新边缘更新的现有身份图的数量。 |
| **[!UICONTROL 失败的数据流总数]** | 失败的数据流运行数。 |

您可以选择过滤器图标 ![“过滤器”图标](../assets/ui/monitor-identities/filter.png) ，以查看该选定源数据流的身份处理信息。

![过滤器图标会突出显示。 选择此图标可查看所选源的数据流。](../assets/ui/monitor-identities/sources-filter.png)

或者，您也可以选择 **[!UICONTROL 数据流]** 在切换开关上，查看贵组织过去24小时数据流的身份处理详细信息。

![身份功能板。 将显示有关每个数据流接收的标识数的信息。](../assets/ui/monitor-identities/dataflows.png)

以下量度可用于此功能板视图：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL 数据流]** | 数据流的名称。 |
| **[!UICONTROL 数据集]** | 数据流插入到的数据集的名称。 |
| **[!UICONTROL 源名称]** | 数据流所属的源的名称。 |
| **[!UICONTROL 已接收的记录]** | 从数据湖接收的记录数。 |
| **[!UICONTROL 失败的记录]** | 由于数据中的错误而未摄取到平台中的记录数。 |
| **[!UICONTROL 跳过的记录数]** | 已摄取但未被摄取的记录数 [!DNL Identity Service] 因为记录行中只有一个标识符。 |
| **[!UICONTROL 已提取的记录]** | 摄取到的记录数 [!DNL Identity Service]. |
| **[!UICONTROL 记录总数]** | 所有记录（包括失败的记录、跳过的记录、添加的标识和重复的记录）的总计数。 |
| **[!UICONTROL 添加了身份]** | 添加到的新标识符净数 [!DNL Identity Service]. |
| **[!UICONTROL 创建的图形]** | 在中创建的新身份图的净数量 [!DNL Identity Service]. |
| **[!UICONTROL 更新的图表]** | 使用新边缘更新的现有身份图的数量。 |
| **[!UICONTROL 失败的数据流总数]** | 失败的数据流运行数。 |

选择过滤器图标 ![过滤器](../assets/ui/monitor-identities/filter.png) 数据流运行开始时间旁边，查看 [!DNL Identity] 数据流运行。

![过滤器图标会突出显示。 选择此图标可查看有关所选数据流的详细信息。](../assets/ui/monitor-identities/dataflows-filter.png)

的 [!UICONTROL 数据流运行详细信息] 页面显示 [!DNL Identity] 数据流运行，包括其组织ID和数据流运行ID。 此页还显示相应的错误代码和 [!DNL Identity Service]，以防摄取过程中发生任何错误。

![将显示显示所选数据流详细信息的功能板。](../assets/ui/monitor-identities/dataflow-run-details.png)

以下量度可用于此功能板视图：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL 已接收的记录]** | 从数据湖接收的记录数。 |
| **[!UICONTROL 失败的记录]** | 由于数据中的错误而未摄取到平台中的记录数。 |
| **[!UICONTROL 跳过的记录数]** | 已摄取但未被摄取的记录数 [!DNL Identity Service] 因为记录行中只有一个标识符。 |
| **[!UICONTROL 已提取的记录]** | 摄取到的记录数 [!DNL Identity Service]. |
| **[!UICONTROL 添加了身份]** | 添加到的新标识符净数 [!DNL Identity Service]. |
| **[!UICONTROL 创建的图形]** | 在中创建的新身份图的净数量 [!DNL Identity Service]. |
| **[!UICONTROL 更新的图表]** | 使用新边缘更新的现有身份图的数量。 |
| **[!UICONTROL 状态]** | 定义数据流的整体状态。 可能的状态值包括： <ul><li>`Success`:表示数据流处于活动状态，并正在根据提供的计划摄取数据。</li><li>`Failed`:表示数据流的激活过程因错误而中断。 </li><li>`Processing`:表示数据流尚未处于活动状态。 此状态通常会在创建新数据流后立即出现。</li></ul> |
| **[!UICONTROL 数据流运行开始]** | 数据流开始运行的日期和时间。 |
| **[!UICONTROL 上次更新时间]** | 数据流上次更新的日期和时间。 |
| **[!UICONTROL 错误摘要]** | 如果数据流运行失败，则会显示错误代码和数据流运行失败原因的摘要。 |
| **[!UICONTROL 数据流运行ID]** | 数据流运行的ID。 |
| **[!UICONTROL IMS组织ID]** | 数据流运行所属的组织ID。 |

此外，您还可以选择切换以查看失败的记录或跳过的记录。 错误部分包含有关错误代码和失败或排除的记录数的详细信息。
