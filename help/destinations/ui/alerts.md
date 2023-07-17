---
keywords: Experience Platform；主页；热门主题；警报；目标
description: 您可以在创建数据流时订阅警报，以接收有关流运行的状态、成功或失败的警报消息。
title: 订阅上下文目标警报
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 7%

---

# 订阅上下文目标警报

通过Adobe Experience Platform，可订阅有关Adobe Experience Platform活动的基于事件的警报。 警报减少或无需轮询 [[!DNL Observability Insights] API](../../observability/api/overview.md) 用于检查作业是否已完成、是否已到达工作流中的某个里程碑或者是否已发生任何错误。

在创建数据流以接收有关流运行的状态、成功或失败的警报消息时，您可以订阅警报。

本文档提供了有关如何订阅接收目标数据流的警报消息的步骤。

## 快速入门

本文档要求您对Adobe Experience Platform的以下组件有一定的了解：

* [目标](../home.md)：与目标平台预建集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。
* [可观测性](../../observability/home.md)： [!DNL Observability Insights] 允许您通过使用统计指标和事件通知来监控Platform活动。
   * [警报](../../observability/alerts/overview.md)：当您的Platform操作达到特定条件集时（例如系统违反阈值时出现潜在问题），Platform可以向您组织中订阅了警报消息的任何用户发送警报消息。

## 订阅UI中的警报 {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="订阅目标提醒"
>abstract="提醒可让您接收基于目标数据流状态的通知。您可以设置提醒，以便在数据流已启动、成功、失败或未向目标发送任何数据时获得更新。"
>text="Learn more in documentation"

>[!IMPORTANT]
>
>您必须启用Platform帐户的即时电子邮件通知，才能接收数据流基于电子邮件的警报通知。

您可以在以下期间为数据流启用警报： [!UICONTROL 配置新目标] 的步骤 [目标连接](connect-destination.md) 工作流。

![显示目标警报部分的UI图像。](../assets/ui/alerts/destination-alerts.png)

选择要订阅的警报，然后选择 **[!UICONTROL 下一个]** 以查看并完成您的数据流。

下表介绍了可用于目标数据流的警报。

* 对于流目标，仅 [!DNL Activation Skipped Rate Exceeded] 警报可用。
* 对于基于文件的目标，所有警报都可用。

| 警报 | 描述 |
| --- | --- |
| 目标流运行延迟 | 当目标流运行需要超过150分钟的时间来激活受众时，此警报会通知您。 |
| 目标流运行失败 | 在将受众激活到目标时出现错误时，此警报会通知您。 |
| 目标流运行成功 | 当受众成功激活到目标时，此警报会通知您。 |
| 目标流运行开始 | 此警报会在目标流运行开始激活受众时通知您。 |
| 超出激活跳过率 | 此警报会在激活跳过率超过总激活的1%时通知您。 当标识缺少属性或违反同意时，激活期间会跳过这些标识。 |

## 接收警报 {#receiving-alerts}

目标数据流运行后，您可以通过UI或电子邮件接收警报。

### 在UI中接收警报 {#receiving-alerts-in-ui}

警报在UI中由Platform UI顶部标题中的通知图标表示。 选择通知图标可查看有关数据流的特定警报消息。

![显示Experience Platform中通知图标的UI图像](../assets/ui/alerts/notification.png)

此时将显示通知面板，其中显示您创建的数据流上的状态更新列表。

![显示通知面板的用户界面图像](../assets/ui/alerts/alert-window.png)

您可以将鼠标悬停在警报消息上以将其标记为已读，也可以选择时钟图标以设置未来对数据流状态的提醒。

![显示通知提醒选项的用户界面图像](../assets/ui/alerts/remind-me.png)

选择警报消息可查看有关数据流的特定信息。

![显示如何选择通知的用户界面图像](../assets/ui/alerts/select-alert-message.png)

此 [!UICONTROL 数据流运行详细信息] 页面。 屏幕的上半部分显示数据流的概述，包括有关其属性的信息、对应的数据流运行ID和高级别错误摘要。

![显示数据流运行详细信息页面的UI图像。](../assets/ui/alerts/dataflow-overview.png)

页面下半部显示任何 [!UICONTROL 数据流运行错误] 在数据流运行阶段发生的错误。 在此处，您可以预览错误诊断或使用 [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) 以下载与数据流对应的错误诊断或文件清单。

![显示数据流运行详细信息页面的UI图像，错误部分突出显示。](../assets/ui/alerts/dataflow-run-error.png)

有关处理数据流错误的更多信息，请参阅 [在UI中监控目标数据流](../../dataflows/ui/monitor-destinations.md).

### 通过电子邮件接收警报 {#receiving-alerts-by-email}

数据流警报也通过电子邮件发送给您。 选择电子邮件正文中的数据流名称可查看有关数据流的更多信息。

![警报电子邮件的屏幕截图](../assets/ui/alerts/email.png)

与UI警报类似， [!UICONTROL 数据流运行概述] 页面，为您提供调查与数据流关联的任何错误的界面。

![数据流概述](../assets/ui/alerts/dataflow-overview.png)

## 订阅和取消订阅警报 {#subscribe-and-unsubscribe}

您可以订阅更多警报，也可以取消订阅目标中现有目标数据流的已建立警报 [!UICONTROL 浏览] 页面。

![显示“目标浏览”页面的UI图像](../assets/ui/alerts/destination-list.png)

找到要接收警报的目标连接，然后选择省略号(`...`)，以查看选项的下拉菜单。 接下来，选择 **[!UICONTROL 订阅警报]** 以修改目标数据流的警报设置。

![显示目标选项的用户界面图像](../assets/ui/alerts/destination-alerts-subscribe.png)

此时会出现一个弹出窗口，为您提供目标警报的列表。 选择要订阅的任何警报，或取消选择要取消订阅的警报。 完成后，选择 **[!UICONTROL 保存]**.

![显示目标警报订阅页面的UI图像](../assets/ui/alerts/destination-alerts-list.png)

## 后续步骤 {#next-steps}

本文档提供了有关如何订阅目标数据流的上下文警报的分步指南。 欲了解更多信息，请参见 [警报UI指南](../../observability/alerts/ui.md).
