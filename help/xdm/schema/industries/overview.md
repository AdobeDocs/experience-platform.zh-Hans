---
solution: Experience Platform
title: 行业数据模型概述
description: 了解可使用标准体验数据模型(XDM)组件构建的各种行业垂直项目的标准化数据模型。
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# 行业数据模型概述

Experience Data Model (XDM)允许您创建高度可自定义的架构，以捕获与您的业务相关的关键客户体验数据。 为了帮助简化建模数据以符合XDM的过程，Adobe Experience Platform提供了一套通用的标准XDM组件，这些组件捕获了多个行业中常用的概念。

>[!NOTE]
>
>新的标准XDM组件正在不断发布，以最好地满足消费者的需求。 有关最新组件的列表，您可以[浏览UI](../../ui/explore.md)中的现有资源，或参阅GitHub上的[官方XDM存储库](https://github.com/adobe/xdm/tree/master/components)。

根据您的业务运营所在的行业，某些XDM组件与您的需求的相关性会高于其他组件。 此外，您在XDM架构之间建立的关系将因您的行业而异。

为了帮助根据特定行业指导您的数据建模策略，本指南提供了若干受支持的行业垂直领域的实体关系图(ERD)的参考。

## 先决条件

要阅读本指南中参考的ERD，您必须实际了解XDM组件如何交互以形成架构，以及XDM架构如何在Experience Platform整体中运行。 在继续之前，请确保您已阅读以下概述文档：

* [XDM系统概述](../../home.md)：了解XDM如何在Experience Platform生态系统中运行。
* [架构组合的基础知识](../../schema/composition.md)：了解XDM组件（如架构字段组、类和数据类型）如何影响架构的结构以及标识字段的角色。

还建议您查看[数据建模最佳实践指南](../../schema/best-practices.md)，了解有关如何将数据映射到XDM的一般准则。

## 行业数据模型ERD {#erds}

为以下行业垂直领域提供了紧急应变报告：

* [[!UICONTROL 零售]](./retail.md)
* [[!UICONTROL 金融服务]](./financial.md)
* [[!UICONTROL 医疗保健]](./healthcare.md)
* [[!UICONTROL 电信]](./telecom.md)
* [[!UICONTROL 旅游和酒店业]](./travel-hospitality.md)

## 后续步骤

本文档概述了行业数据模型ERD及其解释方式。 要查看ERD，请从上面的列表中选择一个。
