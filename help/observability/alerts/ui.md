---
keywords: Experience Platform；主页；热门主题；日期范围
title: 警报UI指南
description: 了解如何在Experience Platform用户界面中管理警报。
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 8d63e9fa4c7eb09ffb90edca612a6e6d44dd18fa
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# 警报UI指南

Adobe Experience Platform用户界面允许您根据Adobe Experience Platform可观察性分析显示的指标查看已接收警报的历史记录。 用户界面还允许您查看、启用、禁用和订阅可用的警报规则。

>[!NOTE]
>
>有关Experience Platform中警报的介绍，请参见 [警报概述](./overview.md).

要开始配置，请选择 **[!UICONTROL 警报]** 在左侧导航中。

![警报页面高亮显示 [!UICONTROL 警报] 在左侧导航中。](../images/alerts/ui/workspace.png)

## 管理警报规则

此 **[!UICONTROL 浏览]** 选项卡列出了可能触发警报的可用规则。

![可用的警报列表显示在 [!UICONTROL 浏览] 选项卡。](../images/alerts/ui/rules.png)

从列表中选择规则以在右边栏中查看其说明及其配置参数，包括阈值和严重性。

![右侧边栏中突出显示的警报规则显示详细信息。](../images/alerts/ui/rule-details.png)

选择省略号(**...**)，则下拉菜单会显示用于启用或禁用警报（取决于警报的当前状态），以及订阅或取消订阅警报的电子邮件通知的控件。

![选定的省略号将显示下拉菜单。](../images/alerts/ui/disable-subscribe.png)

## 管理警报订阅者

>[!NOTE]
>
> 要将警报分配给Adobe用户ID、外部电子邮件地址或电子邮件组列表，您必须是管理员。

此 **[!UICONTROL 浏览]** 选项卡列出了可能触发警报的可用规则。

![中显示的可用警报规则列表 [!UICONTROL 浏览] 选项卡。](../images/alerts/ui/rules.png)

选择省略号(**...**)规则名称旁边的下拉菜单显示控件。 选择 **[!UICONTROL 管理警报订阅者]**.

![选择省略号以显示下拉菜单。 此 [!UICONTROL 管理警报订阅者] 选项会突出显示。](../images/alerts/ui/manage-alert-subscribers.png)

此 [!UICONTROL 管理警报订阅者] 页面。 要向特定用户分配通知，请输入其Adobe用户ID、外部电子邮件地址或电子邮件组列表，然后按Enter键。

>[!NOTE]
>
>要同时将此通知发送给多个用户，请提供用户ID的列表或以逗号分隔的电子邮件地址。

![“管理警报订阅者”页，其中显示了输入的电子邮件地址。](../images/alerts/ui/manage-alert-add-email.png)

电子邮件地址会显示在列出的当前订阅者列表中。 选择&#x200B;**[!UICONTROL 更新]**。

![管理警报订阅者页面突出显示订阅者和 [!UICONTROL 更新].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

您已将用户成功添加到警报通知列表。 提交的用户现在将收到此警报的电子邮件通知，如下图所示。

![收到的警报通知的电子邮件示例。](../images/alerts/ui/manage-alert-subscribers-email.png)

## 启用电子邮件警报

警报通知可以直接发送到您的电子邮件。

选择铃铛图标(![铃铛图标](../images/alerts/ui/bell-icon.png))，用于显示通知和公告。 在显示的下拉列表中，选择齿轮图标(![齿轮图标](../images/alerts/ui/cog-icon.png))以访问“Experience Cloud首选项”页面。

![突出显示铃铛图标和cog图标的警报列表。](../images/alerts/ui/edit-preferences.png)

此 **个人资料** 页面。 选择 **[!UICONTROL 通知]** 以访问电子邮件警报首选项。

![配置文件页面高亮显示 [!UICONTROL 通知] 在左侧导航中。](../images/alerts/ui/profile.png)

滚动到 **电子邮件** 部分，然后选择 **[!UICONTROL 即时通知]**

![电子邮件部分在用户档案页面中突出显示。](../images/alerts/ui/notifications.png)

现在，您订阅的任何警报都将发送到连接到您的Adobe ID帐户的电子邮件地址。

## 查看警报历史记录

此 **[!UICONTROL 历史记录]** 选项卡显示贵组织收到警报的历史记录，包括触发警报、触发日期和解决日期（如果适用）的规则。

![收到的警报列表显示在 [!UICONTROL 历史记录] 选项卡。](../images/alerts/ui/history.png)

选择一个列出的警报，右侧边栏中会显示更多详细信息，包括触发警报的事件的简短摘要。

![右侧边栏中突出显示了详细信息的警报。](../images/alerts/ui/history-details.png)

## 后续步骤

本文档概述了如何在Platform UI中查看和管理警报。 有关更多详细信息，请参阅 [可观察性洞察](../home.md) 以了解有关服务功能的更多信息。
