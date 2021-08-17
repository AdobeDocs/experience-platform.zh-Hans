---
keywords: 目标；目标详细信息页面；目标详细信息页面
title: 查看目标详细信息
description: '单个目标的详细信息页面提供了目标详细信息的概述。 目标详细信息包括目标名称、ID、映射到目标的区段，以及用于编辑激活以及启用和禁用数据流的控件。 '
seo-description: 单个目标的详细信息页面提供了目标详细信息的概述。 目标详细信息包括目标名称、ID、映射到目标的区段，以及用于编辑激活以及启用和禁用数据流的控件。
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---

# 查看目标详细信息

## 概述 {#overview}

在Adobe Experience Platform用户界面中，您可以查看和监视目标的属性和活动。 这些详细信息包括目标的名称和ID、用于激活或禁用目标的控件，等等。 批处理目标的详细信息还包括激活的配置文件记录的量度和数据流运行历史记录。

>[!NOTE]
>
>目标详细信息页面是[!DNL Platform] [!DNL UI]中[!UICONTROL 目标]工作区的一部分。 有关更多信息，请参阅[[!UICONTROL 目标]工作区概述](./destinations-workspace.md) 。

## 查看目标详细信息 {#view-details}

请按照以下步骤查看有关现有目标的更多详细信息。

1. 登录到[Experience PlatformUI](https://platform.adobe.com/)并从左侧导航栏中选择&#x200B;**[!UICONTROL 目标]**。 从顶部标题中选择&#x200B;**[!UICONTROL Browse]**&#x200B;以查看现有目标。

   ![浏览目标](../assets/ui/details-page/browse-destinations.png)

1. 选择左上角的过滤器图标![过滤器图标](../assets/ui/details-page/filter.png)以启动排序面板。 排序面板提供了所有目标的列表。 您可以从列表中选择多个目标，以查看与选定目标关联的已过滤数据流选项。

   ![筛选目标](../assets/ui/details-page/filter-destinations.png)

1. 选择要查看的目标名称。

   ![选择目标](../assets/ui/details-page/destination-select.png)

1. 此时会显示目标的详细信息页面，其中显示了其可用控件。 如果您查看批处理目标的详细信息，则还会显示监控功能板。

   ![目标详细信息](../assets/ui/details-page/destination-details.png)

## 右边栏

右边栏显示有关选定目标的基本信息。

![右边栏](../assets/ui/details-page/right-sidebar.png)

下表涵盖右边栏提供的控件和详细信息：

| 右边栏项目 | 描述 |
| --- | --- |
| [!UICONTROL 激活] | 选择此控件可编辑映射到目标的区段。 有关更多信息，请参阅以下指南：[激活受众数据以划分流目标](./activate-segment-streaming-destinations.md)、[激活受众数据以批量处理基于配置文件的目标](./activate-batch-profile-destinations.md)，以及[激活受众数据以流式处理基于配置文件的目标](./activate-streaming-profile-destinations.md)。 |
| [!UICONTROL 删除] | 允许您删除此数据流并取消映射之前激活的区段（如果有）。 |
| [!UICONTROL 目标名称] | 可以编辑此字段以更新目标的名称。 |
| [!UICONTROL 描述] | 可以编辑此字段，以更新目标或向目标添加可选描述。 |
| [!UICONTROL 目标] | 表示受众被发送到的目标平台。 有关更多信息，请参阅[目标目录](../catalog/overview.md)。 |
| [!UICONTROL 状态] | 指示目标是启用还是禁用。 |
| [!UICONTROL 营销操作] | 指示用于此目标以进行数据管理的营销操作（用例）。 |
| [!UICONTROL 类别] | 指示目标类型。 有关更多信息，请参阅[目标目录](../catalog/overview.md)。 |
| [!UICONTROL 连接类型] | 指示将受众发送到目标的表单。 可能的值包括[!UICONTROL Cookie]和[!UICONTROL 基于配置文件的]。 |
| [!UICONTROL 频度] | 指示将受众发送到目标的频率。 可能的值包括[!UICONTROL 流]和[!UICONTROL 批]。 |
| [!UICONTROL 身份] | 表示目标接受的身份命名空间，如`GAID`、`IDFA`或`email`。 有关已接受的身份命名空间的更多信息，请参阅[身份命名空间概述](../../identity-service/namespaces.md)。 |
| [!UICONTROL 创建者] | 指示创建此目标的用户。 |
| [!UICONTROL 已创建] | 指示创建此目标时的UTC日期时间。 |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL 启用]/ 禁用切换

您可以使用&#x200B;**[!UICONTROL Enabled]/[!UICONTROL Disabled]**&#x200B;切换开关，开始和暂停向目标的所有数据导出。

![启用禁用切换](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL 数据流运行]

[!UICONTROL 数据流运行]选项卡提供数据流运行到批处理目标的量度数据。 有关详细信息，请参阅[监视数据流](monitor-dataflows.md)。

## [!UICONTROL 激活数据] {#activation-data}

[!UICONTROL 激活数据]选项卡显示已映射到目标的区段列表，包括其开始日期和结束日期（如果适用）。 要查看特定区段的详细信息，请从列表中选择其名称。

![激活数据](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>有关浏览区段详细信息页面的详细信息，请参阅[分段UI概述](../../segmentation/ui/overview.md#segment-details)。
