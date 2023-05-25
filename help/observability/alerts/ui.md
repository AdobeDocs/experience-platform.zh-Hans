---
keywords: Experience Platform；主页；热门主题；日期范围
title: 警报UI指南
description: 了解如何在Experience Platform用户界面中管理警报。
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: ed18ecea98497e0c20d44617436a013bf83b69d2
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 警报UI指南

Adobe Experience Platform用户界面允许您根据Adobe Experience Platform可观察性分析显示的指标查看已接收警报的历史记录。 UI还允许您查看、启用、禁用和订阅可用的警报规则。

>[!NOTE]
>
>有关Experience Platform中警报的介绍，请参阅 [警报概述](./overview.md).

要开始配置，请选择 **[!UICONTROL 警报]** 左侧导航栏中。

![](../images/alerts/ui/workspace.png)

## 管理警报规则

此 **[!UICONTROL 浏览]** 选项卡列出了可能触发警报的可用规则。

![](../images/alerts/ui/rules.png)

从列表中选择规则可在右边栏中查看其说明及其配置参数，包括阈值和严重性。

![](../images/alerts/ui/rule-details.png)

选择省略号(**...**)，此时下拉菜单会显示用于启用或禁用警报（取决于警报的当前状态），以及订阅或取消订阅警报的电子邮件通知的控件。

![](../images/alerts/ui/disable-subscribe.png)

## 启用电子邮件警报

警报通知可以直接发送到您的电子邮件。

选择铃铛图标(![铃铛图标](../images/alerts/ui/bell-icon.png))，用于显示通知和公告。 在显示的下拉菜单中，选择齿轮图标(![齿轮图标](../images/alerts/ui/cog-icon.png))以访问“Experience Cloud首选项”页面。

![](../images/alerts/ui/edit-preferences.png)

此 **个人资料** 选项卡中显示。 选择 **[!UICONTROL 通知]** 以访问电子邮件警报首选项。

![](../images/alerts/ui/profile.png)

滚动到 **电子邮件** 部分，然后选择 **[!UICONTROL 即时通知]**

![](../images/alerts/ui/notifications.png)

现在，您订阅的任何警报都将发送到连接到您的Adobe ID帐户的电子邮件地址。

## 查看警报历史记录

此 **[!UICONTROL 历史记录]** 选项卡显示贵组织收到警报的历史记录，包括触发警报、触发日期和解决日期（如果适用）的规则。

![](../images/alerts/ui/history.png)

选择一个列出的警报，右侧边栏中会显示更多详细信息，包括触发警报的事件的简短摘要。

![](../images/alerts/ui/history-details.png)

## 后续步骤

本文档概述了如何在Platform UI中查看和管理警报。 请参阅概述，位于 [可观察性洞察](../home.md) 以了解有关服务功能的详细信息。
