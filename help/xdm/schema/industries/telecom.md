---
solution: Experience Platform
title: 电信行业数据模型ERD
topic-legacy: overview
description: 查看实体关系图(ERD)，该图描述了电信行业的标准化数据模型，该数据模型与在Adobe Experience Platform中使用的体验数据模型(XDM)兼容。
source-git-commit: 38fa2345cb87e50bd4c8788996f03939fb199cf9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


#  电信行业数据模型ERD

以下实体关系图(ERD)代表电信行业的标准化数据模型。 ERD特意以非标准化方式呈现，并考虑数据如何存储在Adobe Experience Platform中。

>[!NOTE]
>
>如上所述的ERD是一项建议，建议您如何为此行业用例建模数据。 要在Platform中利用此数据模型，您必须自行构建推荐的架构及其关系。 有关更多信息，请参阅UI中有关管理[架构](../../ui/resources/schemas.md)和[关系](../../tutorials/relationship-ui.md)的指南。

请使用以下图例来解释此ERD:

* 中显示的每个实体都基于基础的[体验数据模型(XDM)类](../composition.md#class)。
* 对于给定实体，标有&#x200B;**粗体**&#x200B;的每一行代表字段组或数据类型，其提供的相关字段以未加粗的文本列出。
* 给定实体最重要的字段以红色突出显示。
* 所有可用于标识单个客户的资产都会标记为“identity”，其中一个资产会标记为“主要身份”。
* 实体关系被标记为非依赖关系，因为基于Cookie的事件通常无法确定执行交易的人员或个人。


![](../../images/industries/telecom.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示XDM ExperienceEvent类提供的唯一标识符(`_id`)属性。 有关此值预期内容的更多详细信息，请参阅[XDM ExperienceEvent](../../classes/experienceevent.md)上的参考文档。