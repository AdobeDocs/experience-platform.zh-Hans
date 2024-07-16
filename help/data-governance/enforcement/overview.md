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

应用[数据使用标签](../labels/overview.md)并定义[数据使用策略](../policies/overview.md)后，您可以强制实施这些策略以防止构成策略违规的数据操作。

>[!NOTE]
>
>本文档重点介绍数据使用策略的实施。 有关访问控制策略的信息，请参阅[基于属性的访问控制](../../access-control/abac/overview.md)指南。

在Adobe Experience Platform上实施策略有两种方法：自动实施和基于API的实施。

## 自动执行

Experience Platform利用数据谱系、数据分类和策略管理功能来自动评估和显示策略违规。 有关详细信息，请参阅有关[自动策略实施](./auto-enforcement.md)的概述。

## 基于API的实施

[!DNL Policy Service] API提供了一些端点，可让您针对数据集或数据使用标签的任意组合测试营销操作，以检查是否发生了任何违反策略的情况。 根据API响应，您随后可以在体验应用程序中设置协议，以相应地强制实施数据治理策略合规性。

有关如何使用API评估策略的步骤，请参阅有关[基于API的实施](./api-enforcement.md)的教程。
