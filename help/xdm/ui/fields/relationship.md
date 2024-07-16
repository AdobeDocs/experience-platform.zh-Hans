---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；数据模型；ui；工作区；关系；字段；
solution: Experience Platform
title: 在UI中定义关系字段
description: 了解如何在Experience Platform用户界面中定义关系字段。
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 在UI中定义关系字段

在Experience Data Model (XDM)中，[联合架构](../../schema/composition.md#union)是属于已为[实时客户个人资料](../../../profile/home.md)启用的同一类的所有架构的统一视图。 配置文件利用合并架构从不同的体验数据中构建客户的完整表示形式。

在某些情况下，您摄取的数据不一定是用户档案的一部分，但依然与用户档案相关。 此类数据的一个示例是客户的“最喜爱的酒店”字段。 由于个人最喜爱的酒店的属性不是个人自己的属性，因此酒店最好由基于自定义类的单独架构来表示，而不是[!DNL XDM Individual Profile]。

由于合并架构仅基于共享相同类的架构，因此，仅启用“Hotels”架构以在配置文件中使用时，不会包含其针对[!DNL XDM Individual Profile]的字段合并架构。 相反，您必须定义“Hotels”与属于联合的其他架构之间的关系。 这涉及在引用引用架构的主标识的源架构中定义&#x200B;**关系字段**。

有关在Adobe Experience Platform UI中定义两个架构之间关系的详细步骤，请参阅[关系UI教程](../../tutorials/relationship-ui.md)。
