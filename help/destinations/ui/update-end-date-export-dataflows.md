---
title: 更新数据集导出数据流的结束日期（2025年5月1日前需要操作）
type: Tutorial
hide: true
hidefromtoc: true
description: 了解如何将数据集导出数据流的结束日期更新为2025年5月1日的当前结束日期。
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# 更新数据集导出数据流的结束日期（2025年5月1日前需要操作）

>[!IMPORTANT]
>
>如果您的组织在2024年9月版的Experience Platform之前设置数据集导出数据流，则此页上的措施项适用。

## 发生了什么情况？

Experience Platform](/help/release-notes/latest/latest.md#destinations)的[2024年9月版本引入了为导出数据集数据流设置`endTime`日期的选项。 对于在2024年9月版本&#x200B;*之前创建*&#x200B;的所有数据集导出数据流，Adobe还引入了默认结束日期2025年5月1日。 这些数据流当前显示的消息类似于以下所示的消息。

![需要更新导出数据集数据流的结束日期的UI通知。](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**操作项**：对于其中的任何数据流，您必须在结束日期过期之前手动更新结束日期；否则，您的导出将停止。 使用Experience Platform UI识别哪些数据流将在2025年5月1日停止。

## 为什么会通知我？

您的组织已确定拥有活动数据集导出数据流，结束日期为2025年5月1日。

## 使用UI更新结束日期

使用Experience Platform UI识别结束日期为2025年5月1日的数据流，并将其更新到以后的日期。

### 查找需要更新的数据流

导航到&#x200B;**目标>浏览**，并在&#x200B;**数据类型**&#x200B;列中查找&#x200B;**数据集**，如下所示。 选择所需的数据流以检查它们。

![在“浏览”选项卡中突出显示的数据集导出数据流。](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### 更新数据流的结束日期

要更新数据流的结束日期，请执行以下操作：

1. 在上一步中选择检查的数据流中，选择&#x200B;**导出数据集**。
   ![导出数据集控件在“浏览”选项卡中突出显示。](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. 在工作流中，继续执行&#x200B;**计划**&#x200B;步骤，然后选择&#x200B;**编辑计划**。
   ![编辑计划步骤中突出显示的计划控件。](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. 在2025年5月1日之后选择所需的结束日期，然后选择&#x200B;**保存**。
   ![选择计划步骤中突出显示的结束日期控件。](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. 继续到工作流的结尾并保存您的更新。

有关计划步骤的更多信息，请参阅[导出数据集UI教程](/help/destinations/api/export-datasets.md#scheduling)。

## 使用API更新结束日期

### 查找需要更新的数据流

### 更新数据流的结束日期
