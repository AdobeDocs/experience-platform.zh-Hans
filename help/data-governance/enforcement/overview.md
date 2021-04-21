---
keywords: Experience Platform；主页；热门主题；策略执行；自动执行；基于API的执行；数据管理
solution: Experience Platform
title: 策略实施概述
topic-legacy: guide
description: 在将数据使用标签应用于Adobe Experience Platform数据集并为针对这些标签的营销操作定义数据使用策略后，数据管理功能允许您实施这些策略并防止构成策略违规的数据操作。 平台上的数据管理功能提供了两种策略实施方法、基于API的实施和自动实施。
exl-id: d19d8060-85a1-405c-856d-f59041947a33
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 策略实施概述

在将数据使用标签应用到数据集并为针对这些标签的营销操作定义数据使用策略后，Adobe Experience Platform Data Governance功能允许您实施这些策略并防止构成策略违规的数据操作。

[!DNL Platform]上的[!DNL Data Governance]功能提供了两种策略实施方法：基于API的强制和自动强制。

## 基于API的强制

[!DNL Policy Service] API提供的端点允许您针对数据集或数据使用标签的任意组合测试营销操作，以检查是否发生任何策略违规。 然后，根据API响应，您可以在体验应用程序中设置协议以相应地强制执行数据使用策略合规性。

有关如何使用API评估策略的步骤，请参阅[基于API的强制](./api-enforcement.md)教程。

## 自动强制

Experience Platform利用数据谱系、数据分类和策略管理功能自动评估和查看策略违规。 有关详细信息，请参阅[自动策略实施](./auto-enforcement.md)的概述。
