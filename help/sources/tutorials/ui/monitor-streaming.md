---
keywords: Experience Platform；主页；热门主题；监视帐户；监视数据流；数据流
description: Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了从源工作区监控流数据流的步骤。
title: 在UI中监控流源的数据流
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# 在UI中监控流源的数据流

本教程介绍了使用 [!UICONTROL 源] 工作区。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [数据流](../../../dataflows/home.md):数据流是跨平台移动数据的数据作业的表示形式。 数据流是跨不同的服务进行配置的，有助于将数据从源连接器移动到目标数据集，并 [!DNL Identity] 和 [!DNL Profile]和 [!DNL Destinations].
   * [数据流运行](../../notifications.md):数据流运行是基于所选数据流的频率配置的定期计划作业。
* [源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 监控流源的数据流

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可为其创建帐户的各种源。

要查看流源的现有数据流，请选择 **[!UICONTROL 数据流]** 中。

![目录](../../images/tutorials/monitor-streaming/catalog.png)

的 [!UICONTROL 数据流] 页面包含组织中所有现有数据流的列表，包括有关其源数据、帐户名称和数据流运行状态的信息。

选择要查看的数据流的名称。

![数据流](../../images/tutorials/monitor-streaming/dataflows.png)

下表包含有关数据流运行状态的更多信息：

| 状态 | 描述 |
| ------ | ----------- |
| 已完成 | 的 `Completed` 状态表示在1小时内处理了相应数据流运行的所有记录。 A `Completed` 状态仍可能包含数据流运行中的错误。 |
| 成功 | 的 `Success` 状态表示在1小时内处理了相应数据流运行的所有记录，在数据流运行过程中没有遇到任何错误。 |
| 处理时间 | 的 `Processing` 状态表示数据流尚未处于活动状态。 此状态通常会在创建新数据流后立即出现。 |
| 错误 | 的 `Error` 状态表示数据流的激活过程已中断。 |
| 无运行 | 的 `No runs` 状态表示已创建数据流，但未启动数据流运行。 |

的 [!UICONTROL 数据流活动] 页面会显示有关流数据流的特定信息。 顶部横幅包含在选定日期范围内所有流数据流运行的摄取记录和失败记录的累计数量。

![数据流活动](../../images/tutorials/monitor-streaming/dataflow-activity.png)

默认情况下，显示的数据包含过去七天的摄取率。 选择 **[!UICONTROL 最近7天]** 来调整显示记录的时间范围。

此时会出现日历弹出窗口，为您提供替代摄取时间范围的选项。 您可以配置数据流运行时间范围，以查看从前七天或过去30天开始运行的流量。 或者，您也可以配置交互式日历以设置您选择的自定义时间范围。 完成后，选择 **[!UICONTROL 应用]**.

![日历](../../images/tutorials/monitor-streaming/calendar.png)

页面的下半部分显示有关每个流运行接收、摄取和失败的记录数的信息。 每次流量运行都记录在每小时的窗口中。

![数据流运行](../../images/tutorials/monitor-streaming/dataflow-run.png)

### 数据流运行量度 {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="收到的记录"
>abstract="“已接收记录”量度指示在数据流中接收的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="摄取的记录"
>abstract="“摄取的记录”量度指示摄取到数据湖中的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="记录失败"
>abstract="“记录失败”量度指示由于数据中的错误而未摄取到数据湖的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="带警告的记录"
>abstract="带警告的记录指示使用映射器转换警告摄取的记录的总计数。 所有映射器转换错误都会报告为警告，部分摄取的行将被视为成功，并出现警告"
>text="Learn more in documentation"

每个数据流运行都显示以下详细信息：

* **[!UICONTROL 数据流运行开始]**:数据流运行开始的时间。
* **[!UICONTROL 处理时间]**:数据流处理所花费的时间。
* **[!UICONTROL 收到的记录]**:数据流中从源连接器接收的记录总数。
* **[!UICONTROL 摄取的记录]**:摄取到的记录总数 [!DNL Data Lake].
* **[!UICONTROL 警告记录]**:已摄取警告的记录总数。 所有映射器转换错误都将报告为警告，部分摄取的行将标记为 `success` 警告。 **注意**:仅流源支持摄取带有警告的记录。
* **[!UICONTROL 记录失败]**:未摄取到的记录数 [!DNL Data Lake] 由于数据中的错误。
* **[!UICONTROL 摄取率]**:摄取到的记录的成功率 [!DNL Data Lake]. 此量度适用于 [!UICONTROL 部分摄取] 启用。
* **[!UICONTROL 状态]**:表示数据流处于的状态：e [!UICONTROL 已完成] 或 [!UICONTROL 处理]. [!UICONTROL 已完成] 表示在1小时内处理了相应数据流运行的所有记录。 [!UICONTROL 处理] 表示数据流运行尚未完成。

的 [!UICONTROL 数据流运行概述] 页面包含有关数据流的其他信息，如其相应的数据流运行ID、目标数据集和组织ID。

运行时出现错误的流还包含 [!UICONTROL 数据流运行错误] 面板，显示导致运行失败的特定错误以及失败记录的总计数。

![数据流运行概述](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### 查看带有警告的记录 {#warnings}

[!UICONTROL 带警告的记录] 显示在流运行期间发生映射器转换警告的列表。 部分摄取的行被视为成功，如果发现任何映射器转换错误，则会在行后附加警告。

默认情况下，所有映射器转换错误都被视为警告，除非它们属于以下任何错误：

* 语法错误
* 对不存在的属性的引用
* XDM数据类型不匹配

要查看错误诊断，请选择 **[!UICONTROL 预览错误诊断]**.

![带警告的记录](../../images/tutorials/monitor-streaming/records-with-warnings.png)

的 [!UICONTROL 错误诊断预览] 窗口允许您预览有关数据流运行的最多100个错误和/或警告。 从此处，您还可以使用 [!DNL Data Access] API。

![诊断](../../images/tutorials/monitor-streaming/diagnostics.png)

## 后续步骤

通过阅读本教程，您已成功使用 [!UICONTROL 源] 工作区来监视流数据流并识别导致任何失败数据流的错误。 有关更多信息，请参阅以下文档：

* [源概述](../../home.md)
* [数据流概述](../../../dataflows/home.md)
