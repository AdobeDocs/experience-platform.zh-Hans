---
title: 管理数据集过期
description: 了解如何在Adobe Experience Platform UI中计划数据集过期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# 管理数据集过期日期 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="删除不需要或过期的客户记录和数据集"
>abstract="<h2>描述</h2><p>要管理与法规遵从性无关的Experience Platform数据的生命周期，您可以删除客户记录并计划数据集的过期日期。 要创建或管理数据主体请求，请参阅“执行数据主体隐私请求”用例块。</p>"

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买的组织 **Adobe医疗保健盾** 或 **Adobe隐私和安全防护**. 这些功能将在不久的将来正式发布。 有关这些服务即将发布的更多信息，请联系您的Adobe服务代表。 但是，您可以立即 [通过删除数据集 [!UICONTROL 数据集] UI](../../catalog/datasets/user-guide.md#delete).

的 [[!UICONTROL 数据卫生] 工作区](./overview.md) 在Adobe Experience Platform UI中，您可以计划数据集的过期日期。 当数据集到期日期时，数据湖、Identity Service和实时客户配置文件会开始各自的流程，以从各自的服务中删除数据集的内容。 从所有这三项服务中删除数据后，过期时间将标记为完成。

>[!WARNING]
>
>如果数据集设置为过期，您必须手动更改任何可能将数据摄取到该数据集的数据流，以便下游工作流不会受到负面影响。

本文档介绍如何在Platform UI中计划和管理数据集过期。

## 计划数据集过期 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="说明"
>abstract="<ul><li>选择 <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html">数据卫生</a> 在左侧导航中，选择 <b>创建请求</b>.</li><li>如果要删除记录：</li>   <li>选择 <b>记录</b>.</li>   <li>选择要从中删除记录的特定数据集，或选择从所有数据集中删除记录的选项。</li>   <li>提供要删除其记录的消费者的身份。 选择 <b>添加标识</b> 一次提供一个标识或选择 <b>选择文件</b> ，以上传身份的JSON文件。</li>   <li>如果需要，请选择 <b>模板</b> 查看JSON文件的预期格式。</li><li>如果需要，请参阅相关文档以获取相关说明 <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html#schedule-dataset-expiration">计划数据集的过期日期</a>.</li></ul>"

要创建新请求，请选择 **[!UICONTROL 创建请求]** 的页面。

![显示 [!UICONTROL 创建请求] 按钮](../images/ui/ttl/create-request-button.png)

将出现请求创建对话框。 在 **[!UICONTROL 请求的操作]** 选择 **[!UICONTROL 删除数据集]** 用于更新数据集过期计划的可用控件。

![显示 [!UICONTROL 创建请求] 按钮](../images/ui/ttl/dataset-selected.png)

### 选择日期和数据集

将出现请求创建对话框。 在 **[!UICONTROL 请求的操作]** 部分，选择您希望删除数据集的日期。 您可以手动输入日期(格式为 `mm/dd/yyyy`)或选择日历图标(![日历图标的图像](../images/ui/ttl/calendar-icon.png))从对话框中选择日期。

![显示数据集已设置过期日期的图像](../images/ui/ttl/select-date.png)

下一个，下 **[!UICONTROL 数据集详细信息]**，选择数据库图标(![数据库图标的图像](../images/ui/ttl/database-icon.png))打开数据集选择对话框。 从列表中选择要将过期时间应用到的数据集，然后选择 **[!UICONTROL 完成]**.

![显示正在选择的数据集的图像](../images/ui/ttl/select-dataset.png)

>[!NOTE]
只显示属于当前沙盒的数据集。

### 提交请求

的 [!UICONTROL 数据集详细信息] 部分中填充了相应内容，以包含选定数据集的主标识和架构。 在 **[!UICONTROL 请求设置]**，为请求输入名称和可选描述，然后输入 **[!UICONTROL 提交]**.

![显示 [!UICONTROL 提交] 按钮](../images/ui/ttl/submit.png)

系统将要求您确认删除数据集的日期。 选择 **[!UICONTROL 提交]** 继续。

提交请求后，将创建工作单，并显示在 [!UICONTROL 数据卫生] 工作区。 在此处，您可以在处理请求时监控工作单的状态。

>[!NOTE]
请参阅 [时间表和透明度](../home.md#dataset-expiration-transparency) 有关执行数据集过期日期后如何处理这些过期日期的详细信息。

## 编辑或取消数据集过期

要编辑或取消数据集过期，请选择 **[!UICONTROL 数据集]** ，然后从列表中选择数据集过期时间。

在数据集过期的详细信息页面上，右边栏会显示用于编辑或取消计划删除的控件。

## 后续步骤

本文档介绍了如何在Experience PlatformUI中计划数据集过期。 有关如何在UI中执行其他数据卫生任务的信息，请参阅 [数据卫生UI概述](./overview.md).

要了解如何使用数据卫生API计划数据集过期，请参阅 [数据集过期端点指南](../api/dataset-expiration.md).
