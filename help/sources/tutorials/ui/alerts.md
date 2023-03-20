---
keywords: Experience Platform；主页；热门主题；警报
description: 创建数据流时，您可以订阅警报，以接收有关流程运行状态、成功或失败的警报消息。
title: 在UI中订阅上下文关联警报
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: d450dc7b0dc0303c9d33c3e8e003659e3140cf5b
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 1%

---

# 在UI中订阅源数据流警报

Adobe Experience Platform允许您订阅有关Adobe Experience Platform活动的基于事件的警报。 警报可减少或消除轮询 [[!DNL Observability Insights] API](../../../observability/api/overview.md) 为了检查作业是否已完成、是否已到达工作流中的某个里程碑，或是否发生任何错误。

创建数据流时，您可以订阅警报，以接收有关流运行状态、成功或失败的警报消息。

本文档提供了有关如何订阅源数据流的警报消息的步骤。

## 快速入门

本文档要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [可观测性](../../../observability/home.md): [!DNL Observability Insights] 允许您通过使用统计量度和事件通知来监控平台活动。
   * [警报](../../../observability/alerts/overview.md):当您的Platform操作达到一组特定条件（例如，当系统超出阈值时可能出现问题）时，Platform可以向组织中订阅了这些条件的任何用户发送警报消息。

## 在UI中订阅警报 {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="订阅源警报"
>abstract="警报允许您根据源数据流的状态接收通知。 如果数据流已启动、成功、失败或未摄取任何数据，则可以设置警报通知以获取更新。"
>text="Learn more in documentation"

>[!IMPORTANT]
>
>您必须为Platform帐户启用电子邮件的即时通知，才能接收数据流基于电子邮件的警报通知。

您可以在 [!UICONTROL 数据流详细信息] 源工作区中的源工作流步骤。

![数据流详细信息](../../images/tutorials/alerts/dataflow-detail.png)

源数据流的可用警报包括：

| 警报 | 描述 |
| --- | --- |
| 源数据流运行开始 | 当源数据流启动时，此警报会向您发送一条消息。 |
| 源数据流运行成功 | 成功将来自源的数据摄取到平台后，此警报会向您发送一条消息。 |
| 源数据流运行失败 | 如果数据流中发生错误，此警报会向您发送消息。 |
| ~~缺少摄取的源数据流~~ | ~~如果摄取延迟超过七小时且未将数据摄取到平台，则此警报会向您发送消息。~~ <br>**注意：** 您将不再收到警报，因为此警报已弃用。 |

选择要订阅的警报，然后选择 **[!UICONTROL 下一个]** 以检查和完成数据流。

![选择警报](../../images/tutorials/alerts/select-alerts.png)

有关在UI中创建源数据流的详细步骤，请参阅以下指南：

* [Advertising](./dataflow/advertising.md)
* [云存储](./dataflow/batch/cloud-storage.md)
* [CRM](./dataflow/crm.md)
* [数据库](./dataflow/databases.md)
* [电子商务](./dataflow/ecommerce.md)
* [本地文件](./create/local-system/local-file-upload.md)
* [营销自动化](./dataflow/marketing-automation.md)
* [支付](./dataflow/payments.md)
* [协议](./dataflow/protocols.md)

## 接收警报

数据流运行后，您可以通过UI或电子邮件接收警报。

### 在UI中

警报在UI中由Platform UI顶部标题中的通知图标表示。 选择通知图标可查看有关数据流的特定警报消息。

![通知](../../images/tutorials/alerts/notification.png)

此时会出现通知面板，其中显示了您创建的数据流上的状态更新列表。

![警报窗口](../../images/tutorials/alerts/alert-window.png)

您可以将鼠标悬停在警报消息上以将其标记为已读，或者选择时钟图标以设置将来有关数据流状态的提醒。

![提醒我](../../images/tutorials/alerts/remind-me.png)

选择警报消息以查看数据流的特定信息。

![select-alert-message](../../images/tutorials/alerts/select-alert-message.png)

的 [!UICONTROL 数据流运行概述] 页面。 屏幕的上半部分显示有关数据流的概述，包括其属性、相应数据流运行ID和高级错误摘要的信息。

![数据流概述](../../images/tutorials/alerts/dataflow-overview.png)

页面的下半部分显示任何 [!UICONTROL 数据流运行错误] 在数据流运行阶段出现。 从此处，您可以预览错误诊断或使用 [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) 下载错误诊断或与数据流对应的文件清单。

![数据流运行错误](../../images/tutorials/alerts/dataflow-run-error.png)

有关处理数据流错误的更多信息，请参阅 [在UI中监控源数据流](../../../dataflows/ui/monitor-sources.md).

### 通过电子邮件

数据流的警报也通过电子邮件发送给您。 在电子邮件正文中选择数据流名称，以查看有关数据流的更多信息。

![电子邮件](../../images/tutorials/alerts/email.png)

与UI警报类似， [!UICONTROL 数据流运行概述] 页面，为您提供一个界面来调查与数据流关联的任何错误。

![数据流概述](../../images/tutorials/alerts/dataflow-overview.png)

## 订阅和退订警报

您可以订阅更多警报或取消订阅 [!UICONTROL 数据流] 页面。 从列表中找到您创建的数据流，然后选择省略号(`...`)以查看选项的下拉菜单。 接下来，选择 **[!UICONTROL 订阅警报]** 修改数据流的警报设置。

![选项](../../images/tutorials/alerts/options.png)

此时会出现一个弹出窗口，为您提供源警报列表。 选择要订阅或取消订阅的警报。 完成后，选择 **[!UICONTROL 保存]**.

![保存](../../images/tutorials/alerts/save.png)

## 后续步骤

本文档提供了关于如何订阅源数据流的上下文关联警报的分步指南。 有关更多信息，请参阅 [警报UI指南](../../../observability/alerts/ui.md).