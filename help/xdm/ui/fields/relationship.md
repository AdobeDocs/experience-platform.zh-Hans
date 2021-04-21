---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；用户界面；工作区；关系；字段；
solution: Experience Platform
title: 在UI中定义关系字段
description: 了解如何在Experience Platform用户界面中定义关系字段。
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 在UI中定义关系字段

在体验模式模型(XDM)中，[合并用户档案](../../schema/composition.md#union)是属于同一类的所有模式的统一视图，这些类同样已启用[实时客户](../../../profile/home.md)。 合并模式由用户档案利用，以便根据不同的体验数据构建客户的完整表示。

在某些情况下，您可能正在摄取的数据不一定是用户档案的一部分，但仍与用户档案相关。 此类数据的示例是客户“喜爱的酒店”字段。 由于某人喜爱的酒店的属性不是此人本身的属性，因此，酒店最好由基于自定义类的单独模式来表示，而不是[!DNL XDM Individual Profile]。

由于合并模式只基于共享同一类的模式，因此，仅启用“Hotels”模式以在用户档案中使用，将不包括其[!DNL XDM Individual Profile]的字段合并模式。 相反，您必须定义“酒店”与属于该合并的其他模式之间的关系。 这涉及在引用目标模式的主要标识的源模式中定义&#x200B;**关系字段**。

有关在Adobe Experience Platform UI中定义两个模式之间关系的详细步骤，请参阅[关系UI教程](../../tutorials/relationship-ui.md)。
