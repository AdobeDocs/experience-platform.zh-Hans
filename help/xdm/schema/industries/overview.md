---
solution: Experience Platform
title: 行业数据模型概述
description: 了解可以使用标准体验数据模型(XDM)组件构建的各种行业垂直应用的标准化数据模型。
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# 行业数据模型概述

Experience Data Model (XDM)允许您创建高度可自定义的架构，以捕获与您的业务相关的关键客户体验数据。 为了帮助简化数据建模过程以符合XDM，Adobe Experience Platform提供了一套通用的标准XDM组件，这些组件捕获了多个行业中常用的概念。

>[!NOTE]
>
>新的标准XDM组件正在不断发布，以最好地满足消费者的需求。 要获取最新组件的列表，您可以 [浏览UI中的现有资源](../../ui/explore.md) 或参阅 [官方XDM存储库](https://github.com/adobe/xdm/tree/master/components) 在GitHub上。

根据您的业务运营所在的行业，某些XDM组件将比其他组件更符合您的需求。 此外，您在XDM架构之间建立的关系将因您的行业而异。

为了帮助您根据特定行业来指导您的数据建模策略，本指南提供了多个受支持行业垂直领域的实体关系图(ERD)的参考。

## 先决条件

要阅读本指南中提到的ERD，您必须对XDM组件如何交互以形成架构以及XDM架构如何在整个Experience Platform中运行有一定的了解。 在继续之前，请确保您已阅读以下概述文档：

* [XDM系统概述](../../home.md)：了解XDM如何在平台生态系统中运行。
* [模式组合基础](../../schema/composition.md)：了解XDM组件（如架构字段组、类和数据类型）如何影响架构的结构以及标识字段的角色。

此外，还建议您查看 [数据建模最佳实践指南](../../schema/best-practices.md) 以获取有关如何将数据映射到XDM的一般准则。

## 行业数据模型勘误表 {#erds}

为以下行业垂直行业提供了紧急需要解决措施：

* [[!UICONTROL 零售业]](./retail.md)
* [[!UICONTROL 金融服务]](./financial.md)
* [[!UICONTROL 医疗保健]](./healthcare.md)
* [[!UICONTROL 电信]](./telecom.md)
* [[!UICONTROL 旅游和酒店业]](./travel-hospitality.md)

## 后续步骤

本文档概述了行业数据模型ERD及其解释方式。 要查看ERD，请从上面的列表中选择一个。
