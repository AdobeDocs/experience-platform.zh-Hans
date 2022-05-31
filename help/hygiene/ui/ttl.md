---
title: 管理数据集TTL
description: 了解如何在Adobe Experience Platform UI中为数据集计划生存时间(TTL)。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 22da9e39e168d9a995c7c134733aa7a1b3587749
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# 管理数据集TTL

>[!IMPORTANT]
>
>Adobe Experience Platform中的Adobe卫生功能目前仅适用于已购买Data Shield for Healthcare的组织。

的 [[!UICONTROL 数据卫生] 工作区](./overview.md) 在Adobe Experience Platform UI中，您可以计划数据集的生存时间(TTL)。

本文档介绍如何在平台UI中计划和管理数据集TTL。

## 计划TTL

要创建新请求，请选择 **[!UICONTROL 创建请求]** 的页面。

![显示 [!UICONTROL 创建请求] 按钮](../images/ui/ttl/create-request-button.png)

<!-- The request creation dialog appears. Under the **[!UICONTROL Action]** section, select **[!UICONTROL Dataset]** to update the available controls for TTL scheduling-->

### 选择日期和数据集

将出现请求创建对话框。 在 **[!UICONTROL 操作]** 部分，选择您希望删除数据集的日期。 您可以手动输入日期(格式为 `mm/dd/yyyy`)或选择日历图标(![日历图标的图像](../images/ui/ttl/calendar-icon.png))从对话框中选择日期。

![显示为TTL设置过期日期的图像](../images/ui/ttl/select-date.png)

下一个，下 **[!UICONTROL 数据集详细信息]**，选择数据库图标(![数据库图标的图像](../images/ui/ttl/database-icon.png))打开数据集选择对话框。 从列表中选择要将TTL应用到的数据集，然后选择 **[!UICONTROL 完成]**.

![显示正在选择的数据集的图像](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>只显示属于当前沙盒的数据集。

### 提交请求

选择数据集和TTL日期后，请选择 **[!UICONTROL 提交]**.

![显示 [!UICONTROL 提交] 按钮](../images/ui/ttl/submit.png)

系统将要求您确认删除数据集的日期。 选择 **[!UICONTROL 提交]** 继续。

提交请求后，将创建工作单，并显示在 [!UICONTROL 数据卫生] 工作区。 在此处，您可以在处理请求时监控工作单的状态。

## 编辑或取消TTL

要编辑或取消TTL，请选择 **[!UICONTROL 数据集]** ，然后从列表中选择TTL。

在TTL的详细信息页面上，右边栏显示用于编辑或取消计划删除的控件。

## 后续步骤

本文档介绍了如何在Experience PlatformUI中计划数据集TTL。 要了解如何使用数据卫生API计划数据集TTL，请参阅 [数据集TTL端点指南](../api/ttl.md).
