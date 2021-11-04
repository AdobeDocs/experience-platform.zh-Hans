---
keywords: Experience Platform；主页；热门主题；策略执行；自动执行；基于API的执行；数据管理
solution: Experience Platform
title: 策略实施概述
topic-legacy: guide
description: 在将数据使用情况标签应用于Adobe Experience Platform数据集并为针对这些标签的营销操作定义了数据使用策略后，“数据管理”功能允许您实施这些策略并防止构成违反策略的数据操作。 平台上的“数据管理”功能提供了两种策略实施方法：基于API的实施和自动执行。
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 策略实施概述

将数据使用情况标签应用于数据集并为针对这些标签的营销操作定义数据使用策略后，Adobe Experience Platform数据管理功能允许您实施这些策略并阻止构成违反策略的数据操作。

数据管理功能提供了两种策略执行方法，具体方法为 [!DNL Platform]:基于API的强制和自动强制。

## 基于API的执行

的 [!DNL Policy Service] API提供了端点，允许您针对数据集或数据使用标签的任意组合测试营销操作，以检查是否发生任何策略违规。 然后，您可以根据API响应，在体验应用程序中设置协议，以适当强制执行数据使用策略合规性。

请参阅 [基于API的执行](./api-enforcement.md) 以了解有关如何使用API评估策略的步骤。

## 自动执行

Experience Platform利用数据谱系、数据分类和策略管理功能自动评估和显示策略违规。 请参阅 [自动策略执行](./auto-enforcement.md) 以了解更多信息。
