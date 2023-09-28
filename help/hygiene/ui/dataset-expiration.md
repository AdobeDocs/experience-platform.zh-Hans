---
title: 管理数据集过期时间
description: 了解如何在Adobe Experience Platform UI中计划数据集过期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 7931c8fe4a1ca5d255a80e7e6b0deb976d53c3de
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 16%

---

# 管理数据集过期时间 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="删除多余或到期的客户记录和数据集"
>abstract="<h2>描述</h2><p>要管理与监管合规无关的 Experience Platform 数据的生命周期，可删除使用者记录并安排数据集的到期日期。要创建或管理数据主体请求，请参阅“尊重数据主体隐私请求”用例块。</p>"

此 [[!UICONTROL 数据生命周期] 工作区](./overview.md) 在Adobe Experience Platform UI中，您可以安排数据集的过期时间。 当数据集达到其到期日期时，数据湖、Identity Service和Real-time Customer Profile会开始单独的进程，以从各自的服务中删除数据集的内容。 从所有这三项服务中删除数据后，到期将被标记为完成。

>[!WARNING]
>
>如果数据集设置为过期，则必须手动更改任何可能正在将数据摄取到该数据集的数据流，以便下游工作流不会受到负面影响。

本文档介绍如何在Platform UI中计划和管理数据集过期时间。

>[!NOTE]
>
>数据集到期当前不会从Adobe Experience Platform Edge Network删除数据。 但是，数据集设置为过期后，数据不可能保留在Edge Network中。 这是因为数据集过期的14天服务许可协议与14天期限重合，在这14天期限内，数据在被丢弃之前会存在于边缘网络内。

## 计划数据集过期 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="说明"
>abstract="<ul><li>选择 <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=zh-Hans">数据生命周期</a> 在左侧导航中，然后选择 <b>创建请求</b>.</li><li>如果要删除记录：</li>   <li>选择<b>记录</b>。</li>   <li>选择要从中删除记录的特定数据集，或选择从所有数据集中删除记录的选项。</li>   <li>提供要删除其记录的使用者的身份。选择<b>添加身份</b>以一次提供一个身份，或改为选择<b>选择文件</b>以上传包含多个身份的 JSON 文件。</li>   <li>如果需要，请选择<b>模板</b>以查看该 JSON 文件的预期格式。</li><li>如果要<a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=zh-Hans#schedule-dataset-expiration">安排数据集的到期日期</a>，请参阅说明文档。</li></ul>"

要创建请求，请选择 **[!UICONTROL 创建请求]** 从工作区的主页开始。

>[!IMPORTANT]
>
您最多可以有20个同时计划的数据集过期时间。 这意味着您可以随时计划删除20个数据集。 对于这些过期时间或过期年份没有限制。 例如，如果您计划了20个数据集过期时间，并且有一个数据集将于明天删除，则在删除该数据集之前，您无法再设置任何过期时间。

![此 [!UICONTROL 数据生命周期] 工作区，使用 [!UICONTROL 创建请求] 突出显示。](../images/ui/ttl/create-request-button.png)

此时将显示请求创建工作流。 在 [!UICONTROL 请求的操作] 部分，选择 **[!UICONTROL 删除数据集]** 更新数据集到期计划的控制项。

![使用创建请求的工作流 [!UICONTROL 删除数据集] 选项突出显示。](../images/ui/ttl/dataset-selected.png)

### 选择日期和数据集 {#select-date-and-dataset}

在 **[!UICONTROL 请求的操作]** 部分，选择要按其删除数据集的日期。 您可以手动输入日期(格式为 `mm/dd/yyyy`)或选择日历图标(![日历图标。](../images/ui/ttl/calendar-icon.png))，以从对话框中选择日期。

![为数据集选择并突出显示过期日期的日历对话框。](../images/ui/ttl/select-date.png)

下一个，在 **[!UICONTROL 数据集详细信息]**，选择数据库图标(![数据库图标。](../images/ui/ttl/database-icon.png))以打开数据集选择对话框。 从列表中选择一个要应用到期的数据集，然后选择 **[!UICONTROL 完成]**.

![此 [!UICONTROL 选择数据集] 对话框中选择了一个数据集并 [!UICONTROL 完成] 突出显示。](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
仅显示属于当前沙盒的数据集。

### 提交请求 {#submit-request}

此 [!UICONTROL 数据集详细信息] 将填充部分以包含选定数据集的主标识和架构。 下 **[!UICONTROL 请求设置]**，为请求输入名称和可选描述，然后输入 **[!UICONTROL 提交]**.

![使用已完成的数据集过期请求 [!UICONTROL 请求设置] 和 [!UICONTROL 提交] 按钮突出显示。](../images/ui/ttl/submit.png)

A [!UICONTROL 确认请求] 出现对话框。 系统会要求您确认数据集名称和删除该数据集的日期。 选择 **[!UICONTROL 提交]** 以继续。

提交请求后，系统将创建一个工作单，该工作单将显示在 [!UICONTROL 数据生命周期] 工作区。 从此处，您可以监控工作单处理请求时的状态。

>[!NOTE]
>
请参阅概述部分，了解有关 [时间线和透明度](../home.md#dataset-expiration-transparency) 以了解有关执行数据集过期后如何处理这些过期的详细信息。

## 编辑或取消数据集过期 {#edit-or-cancel}

要编辑或取消数据集过期，请选择 **[!UICONTROL 数据集]** 在工作区的主页上，并从列表中选择数据集过期。

在数据集到期的详细信息页面上，右边栏显示用于编辑或取消计划删除的控件。

## 后续步骤

本文档介绍了如何在Experience PlatformUI中安排数据集过期时间。 有关如何在UI中执行其他数据最小化任务的信息，请参阅 [数据生命周期UI概述](./overview.md).

要了解如何使用数据卫生API计划数据集过期时间，请参阅 [数据集到期端点指南](../api/dataset-expiration.md).
