---
title: 自动化数据集过期时间
description: 了解如何在Adobe Experience Platform UI中计划数据集过期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 19%

---

# 自动数据集过期 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="删除多余或到期的客户记录和数据集"
>abstract="<h2>描述</h2><p>要管理与监管合规无关的 Experience Platform 数据的生命周期，可删除使用者记录并计划数据集的过期日期。要创建或管理数据主体请求，请参阅“遵守数据主体隐私请求”用例块。</p>"

Adobe Experience Platform UI中的[[!UICONTROL Data Lifecycle]工作区](./overview.md)允许您计划数据集的过期时间。 当数据集达到其到期日期时，数据湖、Identity Service和Real-time Customer Profile会开始单独的进程，以从各自的服务中删除数据集的内容。 从所有这三项服务中删除数据后，到期将被标记为完成。

>[!WARNING]
>
>如果数据集设置为过期，则必须手动更改任何可能正在将数据摄取到该数据集的数据流，以便下游工作流不会受到负面影响。

本文档介绍如何在Experience Platform UI中计划和自动执行数据集过期操作。

>[!NOTE]
>
>数据集到期当前不会从Adobe Experience Platform Edge Network中删除数据。 但是，在数据集设置为过期后，数据不可能保留在Edge Network中。 这是因为数据集过期的15天服务许可协议与Edge Network中存在数据的14天期限重叠，然后才被丢弃。

高级数据生命周期管理支持通过[数据集到期终结点](../api/dataset-expiration.md)进行数据集删除，以及通过[工作单终结点](../api/workorder.md)使用主标识进行ID删除（行级数据）。 您还可以通过Experience Platform UI管理数据集过期和[记录删除](./record-delete.md)。 有关更多信息，请参阅链接的文档。

>[!NOTE]
>
>数据生命周期不支持批量删除。

## 计划数据集过期 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="说明"
>abstract="<ul><li>在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=zh-Hans#">数据生命周期</a>，然后选择<b>创建请求</b>。</li><li>如果要删除记录：</li>   <li>选择<b>记录</b>。</li>   <li>选择要从中删除记录的特定数据集，或选择从所有数据集中删除记录的选项。</li>   <li>提供要删除其记录的使用者的身份标识。选择<b>添加身份标识</b>以一次提供一个身份标识，或改为选择<b>选择文件</b>以上传包含多个身份标识的 JSON 文件。</li>   <li>如果需要，请选择<b>模板</b>以查看该 JSON 文件的预期格式。</li><li>如果要<a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=zh-Hans#schedule-dataset-expiration">计划数据集的过期日期</a>，请参阅说明文档。</li></ul>"

要创建请求，请从工作区的主页中选择&#x200B;**[!UICONTROL Create request]**。

>[!IMPORTANT]
>
>Real-Time CDP、Adobe Journey Optimizer和Customer Journey Analytics用户有20个挂起的计划数据集到期工作单。 Healthcare Shield和Privacy and Security Shield用户有50个挂起的计划数据集到期工作单。 这意味着您可以随时计划删除20或50个数据集。<br>例如，如果您计划了20个数据集过期时间，并且有一个数据集将在明天删除，则在删除该数据集之前，您无法再设置任何过期时间。

![突出显示带有[!UICONTROL Data Lifecycle]的[!UICONTROL Create request]工作区。](../images/ui/ttl/create-request-button.png)

此时将显示请求创建工作流。 在[!UICONTROL Requested Action]部分下，选择&#x200B;**[!UICONTROL Delete Dataset]**&#x200B;以更新数据集到期计划的控制项。

![突出显示了[!UICONTROL Delete dataset]选项的请求创建工作流。](../images/ui/ttl/dataset-selected.png)

### 选择日期和数据集 {#select-date-and-dataset}

在&#x200B;**[!UICONTROL Requested Action]**&#x200B;部分下，选择要按其删除数据集的日期。 您可以手动输入日期（格式为`mm/dd/yyyy`）或选择日历图标（![日历图标）。](/help/images/icons/calendar.png))以从对话框中选择日期。

![为数据集选择并突出显示过期日期的日历对话框。](../images/ui/ttl/select-date.png)

接下来，在&#x200B;**[!UICONTROL Dataset Details]**&#x200B;下，选择数据库图标（![数据库图标）。](/help/images/icons/database.png))以打开数据集选择对话框。 从列表中选择要应用到期的数据集，然后选择&#x200B;**[!UICONTROL Done]**。

![包含选定数据集并突出显示[!UICONTROL Select dataset]的[!UICONTROL Done]对话框。](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>仅显示属于当前沙盒的数据集。

### 提交请求 {#submit-request}

将填充[!UICONTROL Dataset Details]部分以包含选定数据集的主标识和架构。 在&#x200B;**[!UICONTROL Request settings]**&#x200B;下，输入请求的名称和可选描述，后接&#x200B;**[!UICONTROL Submit]**。

![已完成的突出显示[!UICONTROL Request settings]和[!UICONTROL Submit]按钮的数据集过期请求。](../images/ui/ttl/submit.png)

出现[!UICONTROL Confirm request]对话框。 系统会要求您确认数据集名称和删除该数据集的日期。 选择&#x200B;**[!UICONTROL Submit]**&#x200B;以继续。

提交请求后，将创建一个工作单，该工作单将出现在[!UICONTROL Data Lifecycle]工作区的主选项卡上。 从此处，您可以监控工作单处理请求时的状态。

>[!NOTE]
>
>有关执行数据集过期后如何处理这些过期操作的详细信息，请参阅[时间线和透明度](../home.md#dataset-expiration-transparency)的概述部分。

## 编辑或取消数据集过期 {#edit-or-cancel}

要编辑或取消数据集过期，请在工作区的主页上选择&#x200B;**[!UICONTROL Dataset]**，然后从列表中选择数据集过期。

在数据集到期的详细信息页面上，右边栏显示用于编辑或取消计划删除的控件。

## 后续步骤

本文档介绍了如何在Experience Platform UI中安排数据集过期时间。 有关如何在UI中执行其他数据最小化任务的信息，请参阅[数据生命周期UI概述](./overview.md)。

要了解如何使用数据卫生API计划数据集过期，请参阅[数据集过期端点指南](../api/dataset-expiration.md)。
