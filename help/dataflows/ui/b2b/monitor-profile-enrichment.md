---
description: 使用 [!UICONTROL 用户档案扩充] 功能板，了解用户档案扩充作业是否成功运行和完成，并查看基本量度以衡量扩充的有效性。
solution: Experience Platform
title: 监视配置文件扩充作业
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 47a6cc9b77a0591d488d5ebc3929b465e1a6e6d2
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# 在UI中监控配置文件扩充作业 {#monitor-profile-enrichment}

使用 [!UICONTROL 用户档案扩充] 功能板，了解用户档案扩充作业是否成功运行和完成，并查看基本量度以衡量扩充的有效性。

在 [平台UI](https://platform.adobe.com)，选择 **[!UICONTROL 监控]** 从左侧导航访问 [!UICONTROL 监控] 功能板。 在视图选择器中，选择 **B2B流量** 查看特定于 [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  的 [!UICONTROL 监控] 功能板包括来自最新成功运行的基本量度，以及过去长达90天的每日工作状态。

## 相关帐户用户档案扩充(#related-accounts)

的 [!UICONTROL 相关帐户] 功能板显示特定于 [相关帐户](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) 用户档案扩充。

![如何在Experience PlatformUI中访问用户档案扩充作业监控屏幕的直观指示。](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

中的数据 **[!UICONTROL 量度]** 卡片包含来自“相关帐户”作业最新成功运行中的基本量度。

以下量度可用于相关帐户配置文件扩充作业：

| 量度 | 描述 |
| --------- | ---------- |
| **[!UICONTROL 帐户配置文件总数]** | 指示贵组织有权访问的帐户配置文件总数。 |
| **[!UICONTROL 帐户组]** | 指示由相关帐户机器学习作业群集的帐户组数。 |
| **[!UICONTROL 单帐户群组]** | 指示未与其他帐户一起分组的帐户数。 |
| **[!UICONTROL 最大组大小]** | 指示最大相关帐户组的大小。 允许的最大组大小为30。 |
| **[!UICONTROL 中间组大小]** | 指示组织中相关帐户组的中值大小。 |
| **[!UICONTROL 上次成功运行]** | 指示上次成功运行相关帐户作业的日期和时间。 |
| **[!UICONTROL 状态]** | 指示相关帐户作业的状态（成功、失败或处理）。 |
| **[!UICONTROL 消息]** | 指示特定作业运行的错误或警告消息。 |

## 扩充了帐户匹配用户档案 {#lead-to-account-matching}

的 [!UICONTROL 导致帐户匹配] 功能板显示特定于 [导致帐户匹配](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) 用户档案扩充。

![扩充了帐户匹配用户档案](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

以下量度可用于导致帐户匹配配置文件扩充作业：

| 量度 | 描述 |
| --------- | ---------- |
| **[!UICONTROL 有帐户的总人数]** | 指示与帐户关联的总人数。 |
| **[!UICONTROL 帐户总数]** | 指示帐户总数。 |
| **[!UICONTROL 有帐户的现有人员]** | 指示已与来自数据源的帐户关联的人员数量。 |
| **[!UICONTROL 匹配的人]** | 指示与帐户匹配的人员数。 |
| **[!UICONTROL 无与伦比的人]** | 指示与帐户不匹配的人员数。 |
| **[!UICONTROL 上次成功运行]** | 指示上次成功的潜在客户运行帐户匹配作业的日期和时间。 |
| **[!UICONTROL 状态]** | 指示潜在客户与帐户匹配作业的状态（成功、失败或处理）。 |

## UI控件 {#ui-controls}

本节介绍监控界面中的各种用户界面(UI)选项，利用这些选项可筛选页面上显示的量度。

使用箭头图标(![箭头图标](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png))以展开或关闭屏幕顶部的卡，该卡会显示有关用户档案扩充作业的概览信息。

![屏幕录制，其中显示了箭头图标UI控件。](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

使用 **[!UICONTROL 量度和图表]** 切换以关闭显示最新量度的视图。

![可显示量度和图形切换的屏幕记录。](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

使用 **[!UICONTROL 仅显示失败]** 切换以仅显示失败的配置文件扩充作业。

![仅显示“显示失败”切换开关的屏幕录制。](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 后续步骤 {#next-steps}

通过阅读本教程，您现在可以成功监视和了解用于配置文件扩充作业的量度。 有关更多详细信息，请参阅以下文档：

* [Real-time CDP B2B中的相关帐户](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [帐户配置文件UI指南中的“相关帐户”选项卡](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [在实时CDP B2B中实现帐户匹配](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
