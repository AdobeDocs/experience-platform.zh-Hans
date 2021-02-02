---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；数据模型；ui；工作区；关系；字段；
solution: Experience Platform
title: 在UI中定义关系字段
description: 了解如何在Experience Platform用户界面中定义关系字段。
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# 在UI中定义关系字段

在体验数据模型(XDM)中，[合并模式](../../schema/composition.md#union)是属于同一类的所有模式的统一视图，同时为[实时客户用户档案](../../../profile/home.md)启用了该。 合并模式被用户档案所利用，以便根据不同的体验数据构建客户的完整表示。

在某些情况下，您可能正在接收不一定是用户档案一部分但仍与用户档案相关的数据。 此类数据的示例是客户“最喜爱的酒店”字段。 由于某人喜爱的酒店属性不是该人自己的属性，因此最好使用基于自定义类别而不是[!DNL XDM Individual Profile]的单独模式来表示该酒店。

由于合并模式只基于共享同一类的模式，因此只启用“酒店”模式在用户档案中使用，就不会包含[!DNL XDM Individual Profile]的字段合并模式。 相反，您必须定义“酒店”与属于该模式的其他合并之间的关系。 这涉及在引用目标模式主标识的源模式中定义&#x200B;**关系字段**。

有关在Adobe Experience PlatformUI中定义两个模式之间关系的详细步骤，请参阅[关系UI教程](../../tutorials/relationship-ui.md)。