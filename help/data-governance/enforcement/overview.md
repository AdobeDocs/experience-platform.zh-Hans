---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 策略实施概述
topic: enforcement
translation-type: tm+mt
source-git-commit: d1659bbdd40cf1e598713f1fe1a6eeae8e8249cc

---


# 策略实施概述

一旦数据使用标签被应用到平台数据集，并且为针对这些标签的营销操作定义了数据使用策略，“数据管理”功能就允许您实施这些策略并防止构成违反策略的数据操作。

平台上的数据管理功能提供了两种策略实施方法：基于 **API的强制实施****和自动实施**。

## 基于API的实施

策略服务API提供了端点，允许您针对数据集或数据使用标签的任意组合测试营销操作，以检查是否发生了任何策略违规。 然后，根据API响应，您可以在体验应用程序中设置协议以相应地强制执行数据使用策略的合规性。

有关如何使用API [评估策略](api-enforcement.md) ，请参阅策略实施教程。

## 自动执行

构建在Experience Platform之上的某些应用程序（如实时客户数据平台）可自动执行数据使用策略。 每个应用程序都保留自己的方法来显示违反策略的情况并提供解决问题的步骤。

有关自动数据使用策略实施的更多信息，请查阅您所使用的基于平台的应用程序的文档。 有关实时CDP中自动执行策略的信息，请参阅实 [时CDP数据管理概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。