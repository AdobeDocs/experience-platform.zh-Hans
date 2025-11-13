---
title: 使用Experience Platform UI按需将文件导出到批处理目标
type: Tutorial
description: 了解如何使用Experience Platform UI将按需文件导出到批处理目标。
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 111f6d5093a0b66a683745b1da8d8909eb17f7eb
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 8%

---


# 使用Experience Platform UI按需将文件导出到批处理目标

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

## **[!UICONTROL Export file now]** 概述 {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="立即导出文件"
>abstract="选择此控件可交付完整文件导出以及任何之前计划的导出。将立即触发文件导出，并获取 Experience Platform 分段运行的最新结果。"

本文介绍如何使用Experience Platform UI将文件按需导出到批处理目标，如[云存储](/help/destinations/catalog/cloud-storage/overview.md)和[电子邮件营销](/help/destinations/catalog/email-marketing/overview.md)目标。

**[!UICONTROL Export file now]**&#x200B;控件允许您在不中断先前计划受众的当前导出计划的情况下导出完整文件。 此导出操作在之前计划的导出之外进行，不会更改受众的导出频率。 将立即触发文件导出，并获取 Experience Platform 分段运行的最新结果。

您还可以将Experience Platform API用于此目的。 了解如何通过临时激活API[将按需受众](/help/destinations/api/ad-hoc-activation-api.md)激活到批处理目标。

## 先决条件 {#prerequisites}

要将按需文件导出到批处理目标，您必须已成功[连接到目标](./connect-destination.md)。 如果您尚未这样做，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，然后配置要使用的目标。

## 如何按需导出文件 {#how-to-export-files-on-demand}

1. 转到&#x200B;**[!UICONTROL Connections > Destinations]**，选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡和筛选器符号以显示与所需批处理目标的现有连接。

   ![突出显示如何进入“浏览”选项卡并筛选现有数据流的图像。](../assets/ui/activate-on-demand/browse-tab.png)

2. 选择所需的目标连接以检查到目标的现有数据流。

   ![图像突出显示筛选的数据流。](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. 选择&#x200B;**[!UICONTROL Activation data]**&#x200B;选项卡并选择要按需导出文件的受众，然后选择&#x200B;**[!UICONTROL Export file now]**&#x200B;控件以触发一次性导出，该导出将把每个选定受众的文件交付到您的批处理目标。

   ![图像突出显示“立即导出文件”按钮。](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. 选择&#x200B;**[!UICONTROL Yes]**&#x200B;以确认并触发文件导出。

   ![图像显示“立即导出文件”确认对话框。](../assets/ui/activate-on-demand/confirm-activation.png)

5. 此时会显示确认消息，告知您文件导出已开始。

   ![显示成功临时激活确认的图像。](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. 您还可以切换到&#x200B;**[!UICONTROL Dataflow runs]**&#x200B;选项卡以确认文件导出已启动。

## 注意事项 {#considerations}

使用&#x200B;**[!UICONTROL Export file now]**&#x200B;控件时，请牢记以下注意事项：

* **[!UICONTROL Export file now]**&#x200B;仅适用于批次激活数据流中的计划与当前日期重叠的受众。 这包括计划没有结束日期（导出频率为&#x200B;**[!UICONTROL Once]**）的受众，或者结束日期尚未超过的受众。
* 将受众添加到现有数据流时，至少等待&#x200B;**1小时**，然后再使用&#x200B;**[!UICONTROL Export file now]**&#x200B;控件。
* 如果更改受众的合并策略，或者创建使用新合并策略的受众，请等待24小时，直到使用&#x200B;**[!UICONTROL Export file now]**&#x200B;控件。
* **[!UICONTROL Export file now]**&#x200B;仅使用计划快照导出中的数据。 它不会从API触发的导出作业中提取数据。 要在API触发的导出作业后导出最新数据，请等待下一次计划导出运行。

## UI错误消息 {#ui-error-messages}

使用&#x200B;**[!UICONTROL Export file now]**&#x200B;控件时，您可能会遇到下面列出的任何错误消息。 请查看表格以了解如何在它们出现时解决它们。

| 错误消息 | 解决方法 |
|---------|----------|
| 已为运行ID为`segment ID`的订单`dataflow ID`运行受众`flow run ID` | 此错误消息表示受众当前正在进行临时激活流程。 等待作业完成，然后再触发激活作业。 |
| 受众`<segment name>`不是此数据流的一部分或超出计划范围！ | 此错误消息表示您选择要激活的受众未映射到数据流，或者为受众设置的激活计划已过期或尚未开始。 检查受众是否确实映射到数据流，并验证受众激活计划是否与当前日期重叠。 |

## 相关信息 {#related-information}

* [使用Experience Platform API按需将受众激活到批处理目标](/help/destinations/api/ad-hoc-activation-api.md)
* [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)
