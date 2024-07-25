---
keywords: 编辑激活、编辑目标、编辑目标
title: 编辑激活数据流
type: Tutorial
description: 按照本文中的步骤进行操作，以在Adobe Experience Platform中编辑现有的激活数据流。
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 编辑激活数据流 {#edit-activation-flows}

在Adobe Experience Platform中，您可以编辑现有激活数据流到目标的各种组件，如导出的受众和配置文件属性、导出频率、激活数据流是启用还是禁用等等。

## 编辑数据流 {#edit-dataflows}

请按照以下步骤编辑现有的激活数据流：

1. 登录到[Experience PlatformUI](https://platform.adobe.com/)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 目标]**。 从顶部标题中选择&#x200B;**[!UICONTROL 浏览]**&#x200B;以查看现有目标数据流。

   ![浏览目标](../assets/ui/edit-activation/browse-destinations.png)

2. 选择左上角的过滤器图标![过滤器图标](/help/images/icons/filter.png)以启动排序面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的数据流的过滤选择。

   ![筛选目标](../assets/ui/edit-activation/filter-destinations.png)

3. 选择要编辑的目标数据流的名称。

   ![选择目标](../assets/ui/edit-activation/destination-select.png)

4. 此时将显示目标的&#x200B;**[!UICONTROL 数据流运行]**&#x200B;页面，并显示其可用的控件。 此时，您可以编辑目标数据流的多个组件：

   * 在右边栏中选择&#x200B;**[!UICONTROL 激活受众]**&#x200B;以更改要发送到目标的受众或配置文件属性。 此操作会将您转到激活工作流，该工作流因目标类型而异。 有关详细信息，请参阅以下指南：
      * [将受众数据激活到受众流目标](./activate-segment-streaming-destinations.md)(例如，Facebook或Twitter)；
      * [将受众数据激活到基于个人资料的批次目标](./activate-batch-profile-destinations.md)(例如，Amazon S3或Oracle Eloqua)；
      * [将受众数据激活到基于个人资料的流式目标](./activate-streaming-profile-destinations.md)(例如，HTTP API或Amazon Kinesis)。

   * 此外，您还可以编辑目标数据流的名称和描述。
   * 您可以使用&#x200B;**[!UICONTROL 已启用]/[!UICONTROL 已禁用]**&#x200B;切换开关来开始和暂停所有数据导出到目标。

   ![目标详细信息](../assets/ui/edit-activation/destination-details.png)

## 后续步骤 {#next-steps}

通过学习本教程，您已成功使用&#x200B;**[!UICONTROL 目标]**&#x200B;工作区来更新现有的目标数据流。

有关目标的详细信息，请参阅[目标概述](../catalog/overview.md)。
