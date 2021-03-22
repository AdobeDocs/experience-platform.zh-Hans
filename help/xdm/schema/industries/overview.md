---
solution: Experience Platform
title: 行业数据模型概述
topic: 概述
description: 了解可使用标准体验数据模型(XDM)组件构建的各种行业垂直体系的标准数据模型。
translation-type: tm+mt
source-git-commit: 6a7aebb64a533158f7ab17af0cd28243aeda0eca
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# 行业数据模型概述

体验数据模型(XDM)允许您创建高度可自定义的模式，以捕获与业务相关的关键客户体验数据。 为帮助简化数据建模过程以符合XDM，Adobe Experience Platform提供了一套通用的标准XDM组件，这些组件捕获了在多个行业中常用的概念。

>[!NOTE]
>
>新的标准XDM组件正在不断发布，以最符合消费者需求。 要列表最新的组件，您可以[在UI](../../ui/explore.md)中浏览现有资源，或参阅GitHub上的[官方XDM存储库](https://github.com/adobe/xdm/tree/master/components)。

根据您的业务所处的行业，某些XDM组件与您的需求的相关性会高于其他组件。 此外，您在XDM模式之间建立的关系将因您所在行业的不同而异。

为了帮助指导您根据特定行业制定数据建模战略，本指南为几个受支持的行业纵向提供了实体关系图(ERD)的参考。

## 先决条件

要阅读本指南中引用的ERD，您必须了解XDM组件如何交互以形成模式，以及XDM模式如何在整个Experience Platform中运行。 在继续之前，请确保您已阅读以下概述文档：

* [XDM系统概述](../../home.md):了解XDM如何在平台生态系统中运行。
* [模式合成的基础](../../schema/composition.md):了解XDM组件（如混合、类和数据类型）对模式结构以及身份字段角色的贡献。

还建议您查看[数据建模最佳实践指南](../../schema/best-practices.md)，了解有关如何将数据映射到XDM的一般准则。

## 行业数据模型ERD {#erds}

以下ERD代表的行业垂直模型是有意以去标准化的方式创建的，并考虑数据在平台中的存储方式。

对于给定ERD，中显示的每个实体都基于基础XDM类。 对于给定实体，在&#x200B;**bold**&#x200B;中标记的每行都表示混音或数据类型，其提供的相关字段将以未加粗的文本列出。 给定实体最重要的字段以红色突出显示。

>[!NOTE]
>
>某些实体可能包含“_ID”字段。 这表示平台在摄取事件或用户档案实体时自动为其分配的唯一标识符(`_id`)。 但是，如果需要，您可以选择为此字段使用您自己的唯一ID值。

可用于标识单个客户的所有属性都标记为“identity”，其中一个属性标记为“主要标识”。

实体关系被标记为非依赖关系，因为基于Cookie的事件通常无法确定执行该事务的个人或个人。

ERD针对以下行业垂直体系提供：

* [[!UICONTROL Retail]](./retail.md)
* [[!UICONTROL Financial services]](./financial.md)
* [[!UICONTROL Travel and hospitality]](./travel-hospitality.md)
* [[!UICONTROL Telecommunications]](./telecom.md)

## 后续步骤

本文档概述了行业数据模型ERD以及如何解释它们。 要视图ERD，请从上面的列表中选择一个。