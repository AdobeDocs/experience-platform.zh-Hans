---
title: 管理数据集过期时间
description: 了解如何在Adobe Experience Platform UI中计划数据集过期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# 管理数据集过期时间 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="描述"
>abstract=""

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买的组织 **AdobeHealth Shield** 或 **Adobe隐私和安全防护**.

此 [[!UICONTROL 数据卫生] 工作区](./overview.md) 在Adobe Experience Platform UI中，您可以安排数据集的过期时间。 当数据集到达其到期日期时，数据湖、Identity Service和Real-time Customer Profile开始单独的进程，以从各自的服务中删除数据集的内容。 从所有三个服务中删除数据后，到期将被标记为完成。

>[!WARNING]
>
>如果数据集设置为过期，则必须手动更改任何可能正在将数据摄取到该数据集的数据流，以便下游工作流不会受到负面影响。

本文档介绍如何在Platform UI中计划和管理数据集过期时间。

## 计划数据集过期 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="说明"
>abstract=""

要创建新请求，请选择 **[!UICONTROL 创建请求]** 从工作区的主页中。

![图像显示 [!UICONTROL 创建请求] 正在选择按钮](../images/ui/ttl/create-request-button.png)

此时将显示请求创建对话框。 在 **[!UICONTROL 请求的操作]** 部分，选择 **[!UICONTROL 删除数据集]** 更新数据集到期计划的可用控件。

![图像显示 [!UICONTROL 创建请求] 正在选择按钮](../images/ui/ttl/dataset-selected.png)

### 选择日期和数据集

此时将显示请求创建对话框。 在 **[!UICONTROL 请求的操作]** 部分，选择要按其删除数据集的日期。 您可以手动输入日期(格式为 `mm/dd/yyyy`)或选择日历图标(![日历图标的图像](../images/ui/ttl/calendar-icon.png))，以从对话框中选择日期。

![显示为数据集设置的到期日期的图像](../images/ui/ttl/select-date.png)

下一个，在下 **[!UICONTROL 数据集详细信息]**，选择数据库图标(![数据库图标的图像](../images/ui/ttl/database-icon.png))以打开数据集选择对话框。 从列表中选择一个要应用到期的数据集，然后选择 **[!UICONTROL 完成]**.

![显示正在选择的数据集的图像](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>仅显示属于当前沙盒的数据集。

### 提交请求

此 [!UICONTROL 数据集详细信息] 部分将填充以包含所选数据集的主标识和架构。 下 **[!UICONTROL 请求设置]**，为请求输入名称和可选描述，后跟一个 **[!UICONTROL 提交]**.

![图像显示 [!UICONTROL 提交] 正在选择按钮](../images/ui/ttl/submit.png)

系统会要求您确认删除数据集的日期。 选择 **[!UICONTROL 提交]** 以继续。

提交请求后，将创建一个工作单，该工作单将显示在 [!UICONTROL 数据卫生] 工作区。 从此处，您可以监控工作单在处理请求时的状态。

>[!NOTE]
>
>请参阅概述部分，了解 [时间轴和透明度](../home.md#dataset-expiration-transparency) 以了解执行数据集过期后如何处理这些过期的详细信息。

## 编辑或取消数据集过期

要编辑或取消数据集过期，请选择 **[!UICONTROL 数据集]** ，并从列表中选择数据集过期时间。

在数据集到期的详细信息页面上，右边栏显示用于编辑或取消计划删除的控件。

## 后续步骤

本文档介绍了如何在Experience PlatformUI中安排数据集过期时间。 有关如何在UI中执行其他数据卫生任务的信息，请参阅 [数据卫生UI概述](./overview.md).

要了解如何使用数据卫生API计划数据集过期，请参阅 [数据集到期端点指南](../api/dataset-expiration.md).
