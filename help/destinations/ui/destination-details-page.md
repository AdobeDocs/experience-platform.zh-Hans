---
keywords: 目标；目标；目标详细信息页；目标详细信息页
title: 视图目标详细信息
description: '单个目标的详细信息页面提供了目标详细信息的概述。 目标详细信息包括目标名称、ID、映射到目标的区段，以及用于编辑激活和启用和禁用数据流的控件。 '
seo-description: 单个目标的详细信息页面提供了目标详细信息的概述。 目标详细信息包括目标名称、ID、映射到目标的区段，以及用于编辑激活和启用和禁用数据流的控件。
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
translation-type: tm+mt
source-git-commit: cc432f7c07f0f82deec653864154016638ec8138
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# 视图目标详细信息

## 概述 {#overview}

在Adobe Experience Platform用户界面中，您可以视图和监视目标的属性和活动。 这些详细信息包括目标的名称和ID、用于激活或禁用目标的控件等。 批处理目标的详细信息还包括激活的用户档案记录的量度和数据流运行的历史记录。

>[!NOTE]
>
>目标详细信息页是[!DNL Platform] [!DNL UI]中[!UICONTROL Destinations]工作区的一部分。 有关详细信息，请参阅[[!UICONTROL Destinations]工作区概述](./destinations-workspace.md)。

## 视图目标详细信息{#view-details}

请按照以下步骤视图有关现有目标的更多详细信息。

1. 登录到[Experience PlatformUI](https://platform.adobe.com/)并从左侧导航栏中选择&#x200B;**[!UICONTROL Destinations]**。 从顶部标题中选择&#x200B;**[!UICONTROL Browse]**&#x200B;以视图现有目标。

   ![浏览目标](../assets/ui/details-page/browse-destinations.png)

1. 选择左上角的过滤器图标![过滤器图标](../assets/ui/details-page/filter.png)以启动排序面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的数据流的筛选选择。

   ![筛选目标](../assets/ui/details-page/filter-destinations.png)

1. 选择要视图的目标的名称。

   ![选择目标](../assets/ui/details-page/destination-select.png)

1. 此时将显示目标的详细信息页面，其中显示了其可用控件。 如果查看批处理目标的详细信息，则还会显示监视仪表板。

   ![目标详细信息](../assets/ui/details-page/destination-details.png)

## 右边栏

右边栏显示有关所选目标的基本信息。

![右栏](../assets/ui/details-page/right-sidebar.png)

下表涵盖右边栏提供的控件和详细信息：

| 右边栏项目 | 描述 |
| --- | --- |
| [!UICONTROL Activate] | 选择此控件可编辑映射到目标的区段。 有关详细信息，请参阅[将区段激活到目标](./activate-destinations.md)的指南。 |
| [!UICONTROL Delete] | 允许您删除此数据流并取消映射先前激活的区段（如果有）。 |
| [!UICONTROL Destination name] | 可以编辑此字段以更新目标的名称。 |
| [!UICONTROL Description] | 可以编辑此字段，以更新或向目标添加可选描述。 |
| [!UICONTROL Destination] | 表示受众被发送到的目标平台。 有关详细信息，请参阅[目标目录](../catalog/overview.md)。 |
| [!UICONTROL Status] | 指示目标是启用还是禁用。 |
| [!UICONTROL Marketing actions] | 指示出于数据管理目的适用于此目标的营销操作（使用案例）。 |
| [!UICONTROL Category] | 指示目标类型。 有关详细信息，请参阅[目标目录](../catalog/overview.md)。 |
| [!UICONTROL Connection type] | 指示将受众发送到目标的表单。 可能的值包括[!UICONTROL Cookie]和[!UICONTROL Profile-based]。 |
| [!UICONTROL Frequency] | 指示受众发送到目标的频率。 可能的值包括[!UICONTROL Streaming]和[!UICONTROL Batch]。 |
| [!UICONTROL Identity] | 表示目标接受的身份命名空间，如`GAID`、`IDFA`或`email`。 有关已接受的标识命名空间的详细信息，请参阅[标识命名空间概述](../../identity-service/namespaces.md)。 |
| [!UICONTROL Created by] | 指示创建此目标的用户。 |
| [!UICONTROL Created] | 指示创建此目标时的UTC日期时间。 |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Enabled]/切[!UICONTROL Disabled] 换

您可以使用&#x200B;**[!UICONTROL Enabled]/[!UICONTROL Disabled]**&#x200B;切换到开始，并暂停所有导出到目标的数据。

![启用禁用切换](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

[!UICONTROL Dataflow runs]选项卡提供数据流上到批处理目标的量度数据。 有关详细信息，请参阅[监视数据流](monitor-dataflows.md)。

## [!UICONTROL Activation data] {#activation-data}

[!UICONTROL Activation data]选项卡显示已映射到目标的区段的列表，包括开始日期和结束日期（如果适用）。 要视图特定区段的详细信息，请从列表中选择其名称。

![激活数据](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>有关浏览区段详细信息页面的详细信息，请参阅[分段UI概述](../../segmentation/ui/overview.md#segment-details)。
