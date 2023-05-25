---
title: 隐私控制台概述
description: 了解如何在Adobe Experience Platform UI中监控与隐私相关的工作流。
source-git-commit: 1fac36a0fd767add92283cd256d8bcea783ecf3b
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 3%

---

# 隐私控制台概述

此 [!UICONTROL 隐私控制台] 选项卡Adobe Experience Platform UI提供了在Platform中与隐私相关的操作的仪表板视图，包括数据卫生工作单、Privacy Service中的数据主体请求以及Platform用户活动的审核日志。

要访问仪表板，请选择 **[!UICONTROL 隐私控制台]** 左侧导航栏中。

![图像显示 [!UICONTROL 隐私控制台] 在Platform UI的左侧导航中被选择](../images/governance-privacy-security/privacy-console/left-nav.png)

在此处，您可以查看可用的 [监控构件](#widgets) 控制台提供的，或者您可以探索以下几种之一 [用例指南](#use-case-guides) 平台隐私功能的信息。

## 小组件

[!UICONTROL 隐私控制台] 提供了多个小组件来帮助监控您的隐私操作。

![图像显示 [!UICONTROL 隐私控制台] 在Platform UI的左侧导航中被选择](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>根据贵组织购买的SKU，下面提到的某些构件可能不可用。

每个小组件的功能说明如下：

| 构件名称 | 描述 |
| --- | --- |
| 数据卫生工单状态 | 显示记录删除流程的状态 [数据卫生](../../hygiene/home.md) 所选时间范围的。 使用下拉菜单更改过去7天、14天和30天之间的时间范围。 |
| 最近的数据卫生工单 | 显示最近的 [数据卫生](../../hygiene/home.md) 系统正在处理的工作单。 使用下拉菜单可在最近创建的工作单和最近更新的工作单之间切换。 |
| 最常见的操作 | 显示Platform上由捕获的最常见操作 [审核日志](./audit-logs/overview.md) 所选时间范围的。 使用下拉菜单更改过去7天、14天和30天之间的时间范围。 |
| 最活跃的用户 | 显示组织中由捕获的最活跃的Platform用户 [审核日志](./audit-logs/overview.md) 所选时间范围的。 使用下拉菜单更改过去7天、14天和30天之间的时间范围。 |
| 数据主体请求 | 显示提交和完成的数据主体请求数 [Privacy Service](../../privacy-service/home.md) 在给定的日期内。 |

{style="table-layout:auto"}

## 用例指南

该控制台提供了多个产品内指南，向您介绍Platform中的常见隐私工作流程，包括有关如何设置基本实施的简要说明。

![图像显示 [!UICONTROL 隐私控制台] 在Platform UI的左侧导航中被选择](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## 后续步骤

有关与隐私用例相关的各种Platform服务的更多信息，请参阅以下文档：

* [基于属性的访问控制](../../access-control/abac/overview.md)
* [审核日志](./audit-logs/overview.md)
* [数据治理](../../data-governance/home.md)
* [数据安全机制](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
