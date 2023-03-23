---
title: （测试版）使用Experience PlatformUI将文件按需导出到批量目标
type: Tutorial
description: 了解如何使用Experience PlatformUI将文件按需导出到批处理目标。
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 8%

---

# （测试版）使用Experience PlatformUI将文件按需导出到批量目标

>[!IMPORTANT]
>
>的 **[!UICONTROL 立即导出文件]** Adobe Experience Platform中的选项当前处于测试阶段。 文档和功能可能会发生更改。
>请联系您的Adobe代表以获取此功能的访问权限。

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

## **[!UICONTROL 立即导出文件]** 概述 {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="立即导出文件"
>abstract="选择此控件可交付完整文件导出以及任何之前计划的导出。将立即触发文件导出，并获取 Experience Platform 分段运行的最新结果。"

本文介绍如何使用Experience PlatformUI将文件按需导出到批处理目标，例如 [云存储](/help/destinations/catalog/cloud-storage/overview.md) 和 [电子邮件营销](/help/destinations/catalog/email-marketing/overview.md) 目标。

的 **[!UICONTROL 立即导出文件]** 利用控制，可导出完整文件，而不会中断先前计划区段的当前导出计划。 此导出操作除了之前计划的导出之外，还不会更改区段的导出频率。 将立即触发文件导出，并获取 Experience Platform 分段运行的最新结果。

您还可以为此目的使用Experience PlatformAPI。 阅读操作说明 [通过临时激活API按需激活受众区段以实现批量目标](/help/destinations/api/ad-hoc-activation-api.md).

## 先决条件 {#prerequisites}

要按需将文件导出到批处理目标，您必须成功 [连接到目标](./connect-destination.md). 如果您尚未执行此操作，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

## 如何按需导出文件 {#how-to-export-files-on-demand}

1. 转到 **[!UICONTROL 连接>目标]**，选择 **[!UICONTROL 浏览]** 选项卡和过滤器符号来显示与所需批处理目标的现有连接。

   ![图像突出显示了如何访问浏览选项卡和筛选现有数据流。](../assets/ui/activate-on-demand/browse-tab.png)

2. 选择所需的目标连接以检查目标的现有数据流。

   ![突出显示过滤的数据流的图像。](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. 选择 **[!UICONTROL 激活数据]** 选项卡上，选择要根据需要导出文件的区段，然后选择 **[!UICONTROL 立即导出文件]** 控件来触发一次性导出，该导出会将文件交付到批处理目标。

   >[!IMPORTANT]
   >
   >UI当前不支持选择多个区段以按需批量导出文件。 使用 [临时激活API](/help/destinations/api/ad-hoc-activation-api.md) 为此。

   ![突出显示“立即导出文件”按钮的图像。](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. 选择 **[!UICONTROL 是]** 以确认并触发文件导出。

   ![显示“立即导出文件”确认对话框的图像。](../assets/ui/activate-on-demand/confirm-activation.png)

5. 此时会显示确认消息，告知您文件导出已开始。

   ![显示确认Ad-Hoc激活成功的图像。](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. 您还可以切换到 **[!UICONTROL 数据流运行]** 选项卡，以确认文件导出已开始。

## 注意事项 {#considerations}

使用 **[!UICONTROL 立即导出文件]** 控制：

* **[!UICONTROL 立即导出文件]** 仅适用于批处理激活数据流中的计划与当前日期重叠的区段。 这包括具有没有结束日期(导出频率为 **[!UICONTROL 一次]**)，或结束日期尚未过去的情况。
* 将区段添加到现有数据流时，请至少等待15分钟，直到使用 **[!UICONTROL 立即导出文件]** 控制。
* 如果更改区段的合并策略，或者创建使用新合并策略的区段，则需等待24小时，直到使用 **[!UICONTROL 立即导出文件]** 控制。

## UI错误消息 {#ui-error-messages}

使用 **[!UICONTROL 立即导出文件]** 控制，您可能会遇到下面列出的任何错误消息。 查看表格，了解在表格显示时如何解决这些问题。

| 错误消息 | 解决方法 |
|---------|----------|
| 已针对区段运行 `segment ID` 订购 `dataflow ID` 使用运行id `flow run ID` | 此错误消息表示当前正在为区段进行临时激活流程。 等待作业完成，然后再次触发激活作业。 |
| 区段 `<segment name>` 不是此数据流的一部分或超出计划范围！ | 此错误消息表示您选择激活的区段未映射到数据流，或者为区段设置的激活计划已过期或尚未启动。 检查区段是否确实映射到数据流，并验证区段激活计划是否与当前日期重叠。 |

## 相关信息 {#related-information}

* [使用Experience PlatformAPI，按需激活受众区段以批量目标](/help/destinations/api/ad-hoc-activation-api.md)
* [激活受众数据以批量配置文件导出目标](/help/destinations/ui/activate-batch-profile-destinations.md)
