---
title: 隐私控制台概述
description: 了解如何在Adobe Experience Platform UI中监控与隐私相关的工作流。
source-git-commit: 4fa1b826d033ace6536af920b070e8eebbbf401c
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 3%

---

# 隐私控制台概述

的 [!UICONTROL 隐私控制台] 选项卡Adobe Experience Platform UI提供了Platform中与隐私相关操作的功能板视图，包括数据卫生工作单、Privacy Service中的数据主体请求以及Platform用户活动的审核日志。

要访问功能板，请选择 **[!UICONTROL 隐私控制台]** 中。

![图像显示 [!UICONTROL 隐私控制台] 在Platform UI的左侧导航中进行选择](../images/governance-privacy-security/privacy-console/left-nav.png)

从此处，您可以查看可用的 [监控小组件](#widgets) 提供，或者您可以浏览以下任意一个 [用例指南](#use-case-guides) 的隐私功能。

## 小组件

[!UICONTROL 隐私控制台] 提供了多个小组件来帮助监视您的隐私操作。

![图像显示 [!UICONTROL 隐私控制台] 在Platform UI的左侧导航中进行选择](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>根据贵组织购买的SKU，可能无法使用下面提到的某些小组件。

每个小组件的功能说明如下：

| 小组件名称 | 描述 |
| --- | --- |
| 数据卫生工作单状态 | 显示下方消费者删除流程的状态 [数据卫生](../../hygiene/home.md) 的值。 使用下拉菜单更改过去7天、14天和30天之间的时间范围。 |
| 最近的数据卫生工作单 | 显示最近 [数据卫生](../../hygiene/home.md) 系统正在处理的工作单。 使用下拉菜单可在最近创建的工作单和最近更新的工作单之间切换。 |
| 最常执行的操作 | 显示平台上最常执行的操作，由 [审核日志](./audit-logs/overview.md) 的值。 使用下拉菜单更改过去7天、14天和30天之间的时间范围。 |
| 最活跃的用户 | 显示组织内最活跃的Platform用户，其捕获者 [审核日志](./audit-logs/overview.md) 的值。 使用下拉菜单更改过去7天、14天和30天之间的时间范围。 |
| 数据主体请求 | 显示提交和完成的数据主体请求数 [Privacy Service](../../privacy-service/home.md) 一天。 |

{style=&quot;table-layout:auto&quot;}

## 用例指南

该控制台提供了一些产品内指南，向您介绍Platform中常见的隐私工作流程，包括有关如何设置基本实施的简要说明。

![图像显示 [!UICONTROL 隐私控制台] 在Platform UI的左侧导航中进行选择](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## 后续步骤

有关与隐私用例相关的各种平台服务的更多信息，请参阅以下文档：

* [基于属性的访问控制](../../access-control/abac/overview.md)
* [审核日志](./audit-logs/overview.md)
* [数据管理](../../data-governance/home.md)
* [数据卫生](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
