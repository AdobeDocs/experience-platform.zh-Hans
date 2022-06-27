---
keywords: 编辑激活，编辑目标，编辑目标
title: 编辑激活数据流
type: Tutorial
description: 按照本文中的步骤，编辑Adobe Experience Platform中的现有激活数据流。
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 编辑激活数据流 {#edit-activation-flows}

在Adobe Experience Platform中，您可以编辑目标的现有激活数据流的各种组件，如导出的区段和配置文件属性、导出频率、激活数据流是启用还是禁用等。

## 编辑数据流 {#edit-dataflows}

请按照以下步骤编辑现有激活数据流：

1. 登录到 [Experience PlatformUI](https://platform.adobe.com/) 选择 **[!UICONTROL 目标]** 中。 选择 **[!UICONTROL 浏览]** 来查看现有目标数据流。

   ![浏览目标](../assets/ui/edit-activation/browse-destinations.png)

2. 选择过滤器图标 ![过滤器图标](../assets/ui/edit-activation/filter.png) 来启动排序面板。 排序面板提供了所有目标的列表。 您可以从列表中选择多个目标，以查看与选定目标关联的已过滤数据流选项。

   ![筛选目标](../assets/ui/edit-activation/filter-destinations.png)

3. 选择要编辑的目标数据流的名称。

   ![选择目标](../assets/ui/edit-activation/destination-select.png)

4. 的 **[!UICONTROL 数据流运行]** 页面，显示其可用控件。 此时，您可以编辑目标数据流的多个组件：

   * 选择 **[!UICONTROL 激活区段]** 用于更改要发送到目标的区段或配置文件属性。 此操作会转到激活工作流，该工作流因目标类型而异。 有关更多信息，请参阅以下指南：
      * [将受众数据激活为区段流目标](./activate-segment-streaming-destinations.md) (例如，Facebook或Twitter);
      * [将受众数据激活到批量基于配置文件的目标](./activate-batch-profile-destinations.md) (例如，Amazon S3或OracleEloqua);
      * [将受众数据激活到基于用户档案的流目标](./activate-streaming-profile-destinations.md) (例如，HTTP API或Amazon Kinesis)。
   * 此外，您还可以编辑目标数据流名称和描述。
   * 您可以使用 **[!UICONTROL 已启用]/[!UICONTROL 已禁用]** 切换以开始和暂停所有数据导出到目标。

   ![目标详细信息](../assets/ui/edit-activation/destination-details.png)

## 后续步骤 {#next-steps}

通过阅读本教程，您已成功使用 **[!UICONTROL 目标]** 工作区来更新现有的目标数据流。

有关目标的更多信息，请参阅 [目标概述](../catalog/overview.md).
