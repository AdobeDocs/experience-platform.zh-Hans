---
keywords: Experience Platform；主页；热门主题；API;API;XDM;XDM系统；体验数据模型；数据模型；UI；工作区；关系；字段；
solution: Experience Platform
title: 在UI中定义关系字段
description: 了解如何在Experience Platform用户界面中定义关系字段。
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 在UI中定义关系字段

在Experience Data Model(XDM)中， [合并模式](../../schema/composition.md#union) 是属于同一类且已启用的所有架构的统一视图 [实时客户资料](../../../profile/home.md). 用户档案利用联合架构，从不同的体验数据构建客户的完整表示形式。

在某些情况下，您可能正在摄取不一定是用户档案一部分，但仍与用户档案相关的数据。 此类数据的一个示例是客户“最喜爱的酒店”字段。 由于人员最喜爱的酒店的属性不是人员自身的属性，因此，最好使用基于自定义类的单独模式来表示酒店，而不是 [!DNL XDM Individual Profile].

由于合并架构仅基于共享同一类的架构，因此仅启用“Hotels”架构以在用户档案中使用时，将不会包含其字段合并架构，用于 [!DNL XDM Individual Profile]. 相反，您必须定义“酒店”与属于工会的其他架构之间的关系。 这包括定义 **关系字段** 在引用目标架构的主标识的源架构中。

有关在Adobe Experience Platform UI中定义两个架构之间的关系的详细步骤，请参阅 [关系UI教程](../../tutorials/relationship-ui.md).
