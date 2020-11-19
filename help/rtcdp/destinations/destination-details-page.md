---
keywords: destinations;destination;destinations detail page;destinations details page
title: “目标：详细信息”页
seo-title: “目标：详细信息”页
description: '单个目标的详细信息页面提供了目标详细信息的概述，如目标名称、ID、映射到目标的区段，以及用于编辑激活和启用和禁用数据流的控件。 '
seo-description: '单个目标的详细信息页面提供了目标详细信息的概述，如目标名称、ID、映射到目标的区段，以及用于编辑激活和启用和禁用数据流的控件。 '
translation-type: tm+mt
source-git-commit: 0c2acd79492c474ba664ce32d1592969da71f385
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 1%

---


# 目标详细信息页

在Adobe Experience Platform用户界面中，您可以视图和监视目标的属性和活动。 这些详细信息包括目标的名称和ID、用于激活或禁用目标的控件等。 批处理目标的详细信息还包括激活的用户档案记录的度量和数据流运行的历史记录。

>[!NOTE]
>
>目标详细信息页面是平台UI中 [!UICONTROL 的] “目标”工作区的一部分。 有关详细 [[!UICONTROL 信息] ，请参阅目](./destinations-workspace.md) 标工作区概述。

在平台 **[!UICONTROL UI]** 的“目标”工作区中，导航到“浏 **[!UICONTROL 览]** ”选项卡，然后选择要视图的批处理目标的名称。

![](./assets/details-page/select-destination.png)

此时将显示目标的详细信息页面，其中显示其可用控件。 如果您正在查看批处理目标的详细信息，则还会显示监视仪表板。

![](./assets/details-page/details.png)

## 右边栏

右边栏显示有关目标的基本信息。

![](./assets/details-page/right-rail.png)

下表涵盖右边栏提供的控件和详细信息：

| 右边栏项目 | 描述 |
| --- | --- |
| [!UICONTROL 激活] | 选择此控件可编辑映射到目标的区段。 有关更多信息， [请参阅将区段激活到目标](/help/rtcdp/destinations/activate-destinations.md) 的指南。 |
| [!UICONTROL 目标名称] | 可以编辑此字段以更新目标的名称。 |
| [!UICONTROL 描述] | 可以编辑此字段，以更新或向目标添加可选描述。 |
| [!UICONTROL 目标] | 表示受众被发送到的目标平台。 有关详细 [信息](./destinations-catalog.md) ，请参阅目标目录。 |
| [!UICONTROL 状态] | 指示目标是启用还是禁用。 |
| [!UICONTROL 营销操作] | 指明用于此目标的用于数据管理目的的营销操作（使用案例）。 |
| [!UICONTROL 类别] | 指示目标类型。 有关详细 [信息](./destinations-catalog.md) ，请参阅目标目录。 |
| [!UICONTROL 连接类型] | 指示将受众发送到目标的表单。 可能的值[!UICONTROL 包括]“Cookie”[!UICONTROL 和“基于用户档案]”。 |
| [!UICONTROL 频度] | 指示受众发送到目标的频率。 可能的值[!UICONTROL 包括]“流”[!UICONTROL 和]“Batch”。 |
| [!UICONTROL 身份] | 表示目标接受的身份命名空间, `GAID`如 `IDFA`、或 `email`。 有关已接受身份命名空间的更多信息，请参阅 [身份命名空间概述](../../identity-service/namespaces.md)。 |
| [!UICONTROL 创建者] | 指示创建此目标的用户。 |
| [!UICONTROL 已创建] | 指示创建此目标时的UTC日期时间。 |

## [!UICONTROL 启用]/禁[!UICONTROL 用切换]

您可以使用启 **[!UICONTROL 用]/禁用[!UICONTROL 切换到]** 开始，并暂停所有导出到目标的数据。

![](./assets/details-page/enable-disable.png)

## [!UICONTROL 数据流运行]

“数 [!UICONTROL 据流运行] ”选项卡提供数据流运行到批处理目标的度量数据。 将显示单个运行及其特定度量的列表，以及用户档案记录的以下总计：

* **[!UICONTROL 用户档案记录已激活]**:为用户档案创建或更新的激活记录总数。
* **[!UICONTROL 用户档案记录已跳过]**: 根据用户档案退出或缺少属性，为激活跳过的用户档案记录总数。

![](./assets/details-page/dataflow-runs.png)

>[!NOTE]
>
>根据目标数据流的计划频率生成数据流运行。 对应用于段的每个合并策略执行单独的数据流运行。

要视图特定数据流运行的详细信息，请从列表中选择运行的开始时间。 数据流运行的详细信息页面包含其他信息，如已处理数据的大小和错误诊断的详细信息所发生的任何错误的列表。

![](./assets/details-page/dataflow.png)

## [!UICONTROL 区段]

“区 [!UICONTROL 段] ”选项卡显示已映射到目标的区段的列表，包括开始日期和结束日期（如果适用）。 要视图特定区段的详细信息，请从列表中选择其名称。

![](./assets/details-page/segments.png)

>[!NOTE]
>
>有关浏览区段详细信息页面的详细信息，请参阅分 [段UI概述](../../segmentation/ui/overview.md#segment-details)。

## 后续步骤

此文档涵盖目标详细信息页面的功能。 有关在UI中管理目标的详细信息，请参阅目标工作区 [[!UICONTROL 概述]](./destinations-workspace.md)。