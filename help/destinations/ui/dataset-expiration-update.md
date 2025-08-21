---
title: 延长在2024年11月之前创建的数据流的数据集导出计划
description: 了解如何延长在2024年11月之前创建且将于2025年9月1日停止工作的数据集导出数据流的导出计划。
type: Tutorial
exl-id: a756886b-3f4b-4427-bd26-817221ba68aa
source-git-commit: 6f8b906729ec31cc0c4847ccd0ae0f89f63a1627
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---

# 延长在2024年11月之前创建的数据流的数据集导出计划

>[!IMPORTANT]
>
>**需要操作**：如果您的组织在2024年11月之前创建了[数据集导出数据流](export-datasets.md)，则这些数据流将于2025年9月1日停止工作。 本指南介绍如何延长要保留的数据流的导出计划，使其超过此日期。

## 概述 {#overview}

在Experience Platform[的](/help/release-notes/2024/september-2024.md#destinations)2024年9月版中，Adobe为2024年9月版之前创建的所有数据集导出数据流引入了默认结束日期&#x200B;**2025年5月1日**。

**对于**&#x200B;在2024年11月之前创建的所有数据集导出数据流，此日期已更新为2025年9月1日&#x200B;****。

除非手动延长过期日期，否则在2024年11月之前创建的数据集导出数据流将停止在2025年9月1日&#x200B;**导出数据**。

如果您需要数据流在&#x200B;**2025年9月1日**&#x200B;之后继续导出数据，则必须按照本指南中的步骤扩展其计划，以访问要向其导出数据集的每个目标。

## 受影响的目标 {#affected-destinations}

您的组织可能具有活动数据集导出数据流，将数据发送到下面列出的目标。 请按照以下部分中的步骤操作，并观看演练视频，以了解如何识别设置为过期的数据集。

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## 视频教程 {#video}

观看以下视频，逐步演示如何使用即将到来的结束日期确定数据集导出，并扩展要保留的数据流的导出计划。

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## 步骤1：识别受影响的数据流 {#identify-dataflows}

在延长数据集导出数据流的导出计划之前，您首先需要确定哪些数据流受即将到来的到期日期影响。 请按照以下步骤查找需要操作的数据流。

1. 在Experience Platform UI中转到&#x200B;**[!UICONTROL 目标]** > **[!UICONTROL 目录]**。
2. 在具有活动数据集导出数据流的目标上选择&#x200B;**[!UICONTROL 激活]**。

   >[!TIP]
   >
   >使用目录左侧的&#x200B;**[!UICONTROL 数据类型]**&#x200B;筛选器按&#x200B;**[!UICONTROL 数据集]**&#x200B;筛选可用的目标。

3. 选择&#x200B;**[!UICONTROL 数据集]**数据类型以仅显示具有数据集导出功能的数据流。
   ![显示如何按数据类型筛选数据流的屏幕截图。](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. 选择&#x200B;**[!UICONTROL 已创建]**&#x200B;列标题并选择&#x200B;**[!UICONTROL 升序排序]**以查看较旧的数据流。
   ![显示如何对数据流进行升序排序的屏幕截图。](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. 确定要保留在2024年11月之前创建的数据流中的哪个。

## 步骤2：访问导出数据集工作流 {#access-workflow}

对于每个要保留的数据流，您需要访问导出数据集工作流以修改计划。

1. 在&#x200B;**[!UICONTROL 名称]**&#x200B;列中选择数据流名称。 这会将您转到&#x200B;**[!UICONTROL 数据流运行]**&#x200B;页面。
2. 在此页面上，选择&#x200B;**[!UICONTROL 导出数据集]**选项。
   ![在数据流运行页面中显示导出数据集选项的屏幕截图。](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. 在&#x200B;**[!UICONTROL 选择数据集]**&#x200B;页面上，选择&#x200B;**[!UICONTROL 下一步]**。 您不需要向数据流添加任何新数据集。
4. 这会将您转到&#x200B;**[!UICONTROL 计划]**页面，您还可以在其中看到通知您数据集导出过期日期的通知。
   ![带有过期通知的数据集导出数据流](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## 第3步：扩展导出计划 {#extend-export-schedule}

现在，您可以修改出口计划，以延长到2025年9月1日之后。

1. 选择&#x200B;**[!UICONTROL 编辑计划]**。
   ![显示“编辑计划”按钮的“计划”步骤屏幕截图。](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. 选择新的导出计划，然后选择&#x200B;**[!UICONTROL 保存]**。
   ![显示计划选项的计划步骤屏幕截图。](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >查看[数据集导出文档](export-datasets.md#scheduling)，获取有关如何配置数据集导出计划的详细指导。

## 如果错过2025年9月1日的最后期限，会发生什么？ {#missed-deadline}

如果您的数据集导出数据流在2025年9月1日到期，并且您未延长其计划，则您有&#x200B;**30天的宽限期**，在此宽限期中，您可以联系Adobe以重新启用数据流，而不会丢失任何数据。 这包括从9月1日到您联系Adobe之日期间未导出的数据。

>[!IMPORTANT]
>
>虽然Adobe提供了此宽限期，但我们强烈建议在2025年9月1日截止日期之前延长您的时间表，以确保数据导出不会出现中断并避免任何可能的服务中断。
