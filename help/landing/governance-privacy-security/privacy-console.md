---
title: 隐私控制台概述
description: 了解如何在Adobe Experience Platform UI中监控与隐私相关的工作流。
feature: Privacy
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 4%

---

# 隐私控制台概述

Adobe Experience Platform UI中的[!UICONTROL 隐私控制台]选项卡提供了有关您在Experience Platform中与隐私相关的操作的仪表板视图，包括数据卫生工作单、来自Privacy Service的数据主体请求以及Experience Platform用户活动的审核日志。

要访问仪表板，请在左侧导航中选择&#x200B;**[!UICONTROL 隐私控制台]**。

![图像显示在Experience Platform UI的左侧导航中选择[!UICONTROL 隐私控制台]](../images/governance-privacy-security/privacy-console/left-nav.png)

在此处，您可以查看控制台提供的可用[监视小组件](#widgets)，或者探索有关Experience Platform隐私功能的若干[用例指南](#use-case-guides)之一。

## 小组件

[!UICONTROL 隐私控制台]提供了多个小组件来帮助监视您的隐私操作。

![图像显示在Experience Platform UI的左侧导航中选择[!UICONTROL 隐私控制台]](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>根据贵组织已购买的SKU，下面提到的某些小组件可能无法使用。

每个小组件的功能说明如下：

| 构件名称 | 描述 |
| --- | --- |
| 数据卫生工单状态 | 显示所选时间范围内[数据卫生](../../hygiene/home.md)下的记录删除进程状态。 使用下拉菜单更改过去7天、14天和30天之间的时间范围。 |
| 最近的数据卫生工单 | 显示系统正在处理的最新[数据卫生](../../hygiene/home.md)工作单。 使用下拉菜单在最近创建的工作单和最近更新的工作单之间切换。 |
| 最常见的操作 | 显示[审核日志](./audit-logs/overview.md)在所选时间范围内捕获的Experience Platform上最常见的操作。 使用下拉菜单更改过去7天、14天和30天之间的时间范围。 |
| 大多数活动用户 | 显示在所选时间范围内[审核日志](./audit-logs/overview.md)捕获的组织中最活跃的Experience Platform用户。 使用下拉菜单更改过去7天、14天和30天之间的时间范围。 |
| 数据主体请求 | 显示[Privacy Service](../../privacy-service/home.md)在给定日期内提交和完成的数据主体请求数。 |

{style="table-layout:auto"}

## 用例指南

控制台提供了多个产品内指南，向您介绍Experience Platform中的常见隐私工作流程，包括有关如何设置基本实施的简要说明。

![图像显示在Experience Platform UI的左侧导航中选择[!UICONTROL 隐私控制台]](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## 后续步骤

有关与隐私用例相关的各种Experience Platform服务的更多信息，请参阅以下文档：

* [基于属性的访问控制](../../access-control/abac/overview.md)
* [审核日志](./audit-logs/overview.md)
* [数据治理](../../data-governance/home.md)
* [数据安全机制](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
