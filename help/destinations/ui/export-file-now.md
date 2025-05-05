---
title: 使用Experience Platform UI按需将文件导出到批处理目标
type: Tutorial
description: 了解如何使用Experience Platform UI将按需文件导出到批处理目标。
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: d3bd76f5b36b6a6afcb67fe923eb8e4f3d7a9415
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 9%

---


# 使用Experience Platform UI按需将文件导出到批处理目标

>[!IMPORTANT]
> 
>若要激活数据，您需要&#x200B;**[!UICONTROL 查看目标]**、**[!UICONTROL 激活目标]**、**[!UICONTROL 查看配置文件]**&#x200B;和&#x200B;**[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

## **[!UICONTROL 立即导出文件]**&#x200B;概述 {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="立即导出文件"
>abstract="选择此控件可交付完整文件导出以及任何之前计划的导出。将立即触发文件导出，并获取 Experience Platform 分段运行的最新结果。"

本文介绍如何使用Experience Platform UI将文件按需导出到批处理目标，如[云存储](/help/destinations/catalog/cloud-storage/overview.md)和[电子邮件营销](/help/destinations/catalog/email-marketing/overview.md)目标。

通过&#x200B;**[!UICONTROL 立即导出文件]**&#x200B;控件，可以在不中断先前计划受众的当前导出计划的情况下导出完整文件。 此导出操作在之前计划的导出之外进行，不会更改受众的导出频率。 将立即触发文件导出，并获取 Experience Platform 分段运行的最新结果。

您还可以将Experience Platform API用于此目的。 了解如何通过临时激活API[&#128279;](/help/destinations/api/ad-hoc-activation-api.md)将按需受众激活到批处理目标。

## 先决条件 {#prerequisites}

要将按需文件导出到批处理目标，您必须已成功[连接到目标](./connect-destination.md)。 如果您尚未这样做，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，然后配置要使用的目标。

## 如何按需导出文件 {#how-to-export-files-on-demand}

1. 转到&#x200B;**[!UICONTROL 连接>目标]**，选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡和筛选器符号，以显示到所需批处理目标的现有连接。

   ![突出显示如何进入“浏览”选项卡并筛选现有数据流的图像。](../assets/ui/activate-on-demand/browse-tab.png)

2. 选择所需的目标连接以检查到目标的现有数据流。

   ![图像突出显示筛选的数据流。](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. 选择&#x200B;**[!UICONTROL 激活数据]**&#x200B;选项卡，并选择要按需导出文件的受众，然后选择&#x200B;**[!UICONTROL 立即导出文件]**&#x200B;控件以触发一次性导出，该导出会将每个选定受众的文件传送到批处理目标。

   ![图像突出显示“立即导出文件”按钮。](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. 选择&#x200B;**[!UICONTROL 是]**&#x200B;以确认并触发文件导出。

   ![图像显示“立即导出文件”确认对话框。](../assets/ui/activate-on-demand/confirm-activation.png)

5. 此时会显示确认消息，告知您文件导出已开始。

   ![显示成功临时激活确认的图像。](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. 您还可以切换到&#x200B;**[!UICONTROL 数据流运行]**&#x200B;选项卡，以确认文件导出已启动。

## 注意事项 {#considerations}

使用&#x200B;**[!UICONTROL 立即导出文件]**&#x200B;控件时，请牢记以下注意事项：

* **[!UICONTROL 立即导出文件]**&#x200B;仅适用于批次激活数据流中的计划与当前日期重叠的受众。 这包括计划没有结束日期（导出频率为&#x200B;**[!UICONTROL 次]**）的受众，或者结束日期尚未超过的受众。
* 将受众添加到现有数据流时，至少等待&#x200B;**一小时**，然后再使用&#x200B;**[!UICONTROL 立即导出文件]**&#x200B;控件。
* 如果更改受众的合并策略，或者创建使用新合并策略的受众，请等待24小时，直到使用&#x200B;**[!UICONTROL 立即导出文件]**&#x200B;控件。

## UI错误消息 {#ui-error-messages}

使用&#x200B;**[!UICONTROL 立即导出文件]**&#x200B;控件时，您可能会遇到下面列出的任何错误消息。 请查看表格以了解如何在它们出现时解决它们。

| 错误消息 | 解决方法 |
|---------|----------|
| 已为运行ID为`flow run ID`的订单`dataflow ID`运行受众`segment ID` | 此错误消息表示受众当前正在进行临时激活流程。 等待作业完成，然后再触发激活作业。 |
| 受众`<segment name>`不是此数据流的一部分或超出计划范围！ | 此错误消息表示您选择要激活的受众未映射到数据流，或者为受众设置的激活计划已过期或尚未开始。 检查受众是否确实映射到数据流，并验证受众激活计划是否与当前日期重叠。 |

## 相关信息 {#related-information}

* [使用Experience Platform API按需将受众激活到批处理目标](/help/destinations/api/ad-hoc-activation-api.md)
* [将受众数据激活到批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)
