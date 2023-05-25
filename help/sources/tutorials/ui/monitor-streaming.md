---
keywords: Experience Platform；主页；热门主题；监控帐户；监控数据流；数据流
description: Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了从源工作区监视流数据流的步骤。
title: 在UI中监控流源的数据流
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 10%

---

# 在UI中监控流源的数据流

本教程介绍了使用监控流源的数据流的步骤。 [!UICONTROL 源] 工作区。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [数据流](../../../dataflows/home.md)：数据流是跨平台移动数据的数据作业的表示形式。 数据流在不同的服务之间配置，有助于将数据从源连接器移动到目标数据集，以及 [!DNL Identity] 和 [!DNL Profile]、和 [!DNL Destinations].
   * [数据流运行](../../notifications.md)：数据流运行是基于所选数据流的频率配置的定期计划作业。
* [源](../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

## 监测流源的数据流

在Platform UI中，选择 **[!UICONTROL 源]** 以访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以为其创建帐户的各种源。

要查看流源的现有数据流，请选择 **[!UICONTROL 数据流]** 从顶部标题中。

![目录](../../images/tutorials/monitor-streaming/catalog.png)

此 [!UICONTROL 数据流] 页面包含贵组织中所有现有数据流的列表，其中包括有关其源数据、帐户名称和数据流运行状态的信息。

选择要查看的数据流的名称。

![数据流](../../images/tutorials/monitor-streaming/dataflows.png)

下表包含有关数据流运行状态的更多信息：

| 状态 | 描述 |
| ------ | ----------- |
| 已完成 | 此 `Completed` status表示相应数据流运行的所有记录都在一小时时段内处理。 A `Completed` 状态仍可能包含数据流运行中的错误。 |
| 成功 | 此 `Success` status表示相应数据流运行的所有记录都在一小时时段内进行处理，并且在数据流运行期间没有遇到错误。 |
| 处理时间 | 此 `Processing` 状态表示数据流尚未处于活动状态。 创建新数据流后，通常会立即出现此状态。 |
| 错误 | 此 `Error` 状态表示数据流的激活过程已中断。 |
| 无运行 | 此 `No runs` 状态表示数据流已创建，但未启动数据流运行。 |

此 [!UICONTROL 数据流活动] 页面显示有关流数据流的特定信息。 顶部横幅包含在选定日期范围内所有流数据流运行中摄取和失败记录的累计数量。

![数据流活动](../../images/tutorials/monitor-streaming/dataflow-activity.png)

默认情况下，显示的数据包含过去七天的摄取率。 选择 **[!UICONTROL 最近7天]** 以调整所显示记录的时间范围。

此时会出现一个日历弹出窗口，为您提供替代摄取时间范围的选项。 您可以配置数据流运行时间范围以查看过去7天或过去30天的流运行。 或者，您也可以配置交互式日历，以设置您选择的自定义时间范围。 完成后，选择 **[!UICONTROL 应用]**.

![日历](../../images/tutorials/monitor-streaming/calendar.png)

页面下半部分显示有关每次流运行接收、引入和失败的记录数的信息。 每次流量运行均记录在一个每小时窗口中。

![数据流运行](../../images/tutorials/monitor-streaming/dataflow-run.png)

### 数据流运行指标 {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="已接收的记录"
>abstract="“已接收的记录”量度指示数据流中接收的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="已提取的记录"
>abstract="“已提取的记录”量度指示已提取到数据湖中的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="失败的记录"
>abstract="“失败的记录”量度指示因数据错误而未被提取到数据湖的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="带警告的记录"
>abstract="“带警告的记录”指示带映射器转换警告的已提取记录总数。所有映射器转换错误都报告为警告，部分提取的行被视为成功并显示警告"
>text="Learn more in documentation"

每次单独运行数据流都会显示以下详细信息：

* **[!UICONTROL 数据流运行开始]**：数据流开始运行的时间。
* **[!UICONTROL 处理时间]**：数据流处理所用的时间。
* **[!UICONTROL 已接收的记录]**：数据流中从源连接器接收的记录总数。
* **[!UICONTROL 已摄取记录]**：被摄取到的记录总数 [!DNL Data Lake].
* **[!UICONTROL 有警告的记录]**：已引入警告的记录总数。 所有映射器转换错误均报告为警告，部分引入的行将标记为 `success` 带警告。 **注释**：仅对流源支持摄取有警告的记录。
* **[!UICONTROL 记录失败]**：未摄取到的记录数 [!DNL Data Lake] 因为数据错误。
* **[!UICONTROL 摄取率]**：摄取到的记录的成功率 [!DNL Data Lake]. 此量度适用于 [!UICONTROL 部分摄取] 已启用。
* **[!UICONTROL 状态]**：表示数据流所处的状态： [!UICONTROL 已完成] 或 [!UICONTROL 正在处理]. [!UICONTROL 已完成] 表示相应数据流运行的所有记录都在一小时时段内处理。 [!UICONTROL 正在处理] 表示数据流运行尚未完成。

此 [!UICONTROL 数据流运行概述] 页面包含有关数据流的附加信息，例如其对应的数据流运行ID、目标数据集和组织ID。

有错误的流运行还包含 [!UICONTROL 数据流运行错误] 面板，其中显示导致运行失败的特定错误以及失败的记录总数。

![数据流运行概述](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### 查看有警告的记录 {#warnings}

[!UICONTROL 有警告的记录] 显示在流运行期间发生的映射器转换警告的列表。 部分摄取的行被视为成功，如果发现任何映射器转换错误，则会附加警告。

默认情况下，所有映射器转换错误都被视为警告，除非它们属于以下任一情况：

* 语法错误
* 对不存在属性的引用
* XDM数据类型不匹配

要查看错误诊断，请选择 **[!UICONTROL 预览错误诊断]**.

![records-with-warnings](../../images/tutorials/monitor-streaming/records-with-warnings.png)

此 [!UICONTROL 错误诊断预览] 窗口允许您预览有关数据流运行的最多100个错误和/或警告。 从这里，您还可以使用下载摄取失败清单以了解更多信息。 [!DNL Data Access] API。

![诊断](../../images/tutorials/monitor-streaming/diagnostics.png)

## 后续步骤

按照本教程中的说明，您已成功使用了 [!UICONTROL 源] 工作区，用于监视您的流数据流并识别导致任何失败的数据流的错误。 有关更多信息，请参阅以下文档：

* [源概述](../../home.md)
* [数据流概述](../../../dataflows/home.md)
