---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: 策略实施概述
topic: enforcement
description: 在将数据使用标签应用于Adobe Experience Platform数据集并为针对这些标签的营销操作定义数据使用策略后，数据管理功能允许您实施这些策略并防止构成违反策略的数据操作。 平台上的数据管理功能提供了两种策略实施方法，即基于API的实施和自动实施。
translation-type: tm+mt
source-git-commit: 2fdab7d984a7368df77110f8ba0e0ba687e96d7e
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 策略实施概述

一旦数据使用标签已应用到数 [!DNL Platform] 据集，并且为针对这些标签的营销操作定义了数据使用策略， [!DNL Data Governance] 这些功能就允许您执行这些策略并防止构成策略违规的数据操作。

功能提供了两种策略执行方 [!DNL Data Governance] 法， [!DNL Platform]分别为 **基于API的强制** 和 **自动强制**。

## 基于API的强制

API提 [!DNL Policy Service] 供了端点，允许您针对数据集或数据使用标签的任意组合测试营销操作，以检查是否发生任何策略违规。 根据API响应，您随后可以在体验应用程序中设置协议以适当强制执行数据使用策略合规性。

有关如何使用 [API评估策略](api-enforcement.md) ，请参阅策略实施教程。

## 自动执行

构建于（如）之上的某些应用 [!DNL Experience Platform] 程序为 [!DNL Real-time Customer Data Platform]数据使用策略提供自动实施。 每个应用程序都保留自己的方法来显示违反策略的情况并提供解决问题的步骤。

有关自动数据使用策略 [!DNL Platform]实施的更多信息，请查阅您所使用的基于应用程序的文档。 有关实时CDP中自动执行策略的信息，请参阅 [实时CDP数据管理概述](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)。