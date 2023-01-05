---
solution: Experience Platform
title: 行业数据模型概述
topic-legacy: overview
description: 了解各种垂直行业的标准化数据模型，这些数据模型可以使用标准的体验数据模型(XDM)组件构建。
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
source-git-commit: d3f914cb4bcd18980e433c6fd17a663ad0fb5a84
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# 行业数据模型概述

体验数据模型(XDM)允许您创建高度可自定义的架构，以捕获与您的业务相关的关键客户体验数据。 为帮助简化数据建模过程以符合XDM，Adobe Experience Platform提供了一套通用的标准XDM组件，这些组件捕获了多个行业中常用的概念。

>[!NOTE]
>
>新的标准XDM组件正在不断发布，以最符合客户需求。 有关最新组件的列表，您可以 [浏览UI中的现有资源](../../ui/explore.md) 或参阅 [官方XDM存储库](https://github.com/adobe/xdm/tree/master/components) 在GitHub上。

根据您的业务所在的行业，某些XDM组件与您的需求的关系将比其他组件更相关。 此外，您在XDM模式之间建立的关系将因您的行业而异。

为了帮助根据您的特定行业指导您的数据建模策略，本指南为几个受支持的垂直行业提供了实体关系图(ERD)的参考。

## 先决条件

要阅读本指南中引用的ERD，您必须对XDM组件如何交互以形成模式以及XDM模式如何作为一个整体在Experience Platform中运行有一定的了解。 在继续操作之前，请确保您已阅读以下概述文档：

* [XDM系统概述](../../home.md):了解XDM如何在平台生态系统中运行。
* [架构组合的基础知识](../../schema/composition.md):了解XDM组件（如架构字段组、类和数据类型）对架构结构以及身份字段的角色有何贡献。

另外，建议您查看 [数据建模最佳实践指南](../../schema/best-practices.md) ，以了解有关如何将数据映射到XDM的一般准则。

## 行业数据模型ERD {#erds}

ERD针对以下垂直行业提供：

* [[!UICONTROL 零售业]](./retail.md)
* [[!UICONTROL 金融服务]](./financial.md)
* [[!UICONTROL 医疗保健]](./healthcare.md)
* [[!UICONTROL 电信]](./telecom.md)
* [[!UICONTROL 旅游和酒店业]](./travel-hospitality.md)

## 后续步骤

本文档概述了行业数据模型ERD以及如何解释它们。 要查看ERD，请从上面的列表中选择一个。
