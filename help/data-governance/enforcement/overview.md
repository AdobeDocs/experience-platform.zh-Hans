---
keywords: Experience Platform；主页；热门主题；策略实施；自动实施；基于API的实施；数据治理
solution: Experience Platform
title: 策略实施概述
description: 了解如何在Adobe Experience Platform上实施数据使用策略。
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 策略实施概述

一次 [数据使用标签](../labels/overview.md) 已应用，并且 [数据使用策略](../policies/overview.md) 定义之后，您可以强制实施这些策略以防止构成策略违规的数据操作。

>[!NOTE]
>
>本文档重点介绍数据使用策略的实施。 有关访问控制策略的信息，请参阅以下指南： [基于属性的访问控制](../../access-control/abac/overview.md).

在Adobe Experience Platform上实施策略有两种方法：自动实施以及基于API的实施。

## 自动执行

Experience Platform利用数据谱系、数据分类和策略管理功能来自动评估和显示策略违规。 请参阅概述，位于 [自动策略执行](./auto-enforcement.md) 了解更多信息。

## 基于API的实施

此 [!DNL Policy Service] API提供了一些端点，可让您根据数据集或数据使用标签的任意组合来测试营销操作，以检查是否发生了任何违反策略的情况。 然后，您可以根据API响应，在体验应用程序中设置协议，以适当强制实施数据治理策略合规性。

请参阅上的教程 [基于API的实施](./api-enforcement.md) 有关如何使用API评估策略的步骤。
