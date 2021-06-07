---
solution: Experience Platform
title: 金融服务行业数据模型ERD
topic-legacy: overview
description: 查看实体关系图(ERD)，该图描述银行、金融服务和保险(BFSI)行业的标准化数据模型。 此数据模型与Experience Data Model(XDM)兼容，可在Adobe Experience Platform中使用。
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 88c17992a391b24a76c3e387d3033df4c75a6aa6
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# [!UICONTROL 金融] 服务行业数据模型ERD

以下实体关系图(ERD)代表银行、金融服务和保险(BFSI)行业的标准化数据模型。 ERD特意以非标准化方式呈现，并考虑数据如何存储在Adobe Experience Platform中。

请使用以下图例来解释此ERD:

* 中显示的每个实体都基于基础的[体验数据模型(XDM)类](../composition.md#class)。
* 对于给定实体，标有&#x200B;**粗体**&#x200B;的每一行代表字段组或数据类型，其提供的相关字段以未加粗的文本列出。
* 给定实体最重要的字段以红色突出显示。
* 所有可用于标识单个客户的资产都会标记为“identity”，其中一个资产会标记为“主要身份”。
* 实体关系被标记为非依赖关系，因为基于Cookie的事件通常无法确定执行交易的人员或个人。

![](../../images/industries/financial.png)

>[!NOTE]
>
>体验事件实体包含“_ID”字段，该字段表示XDM ExperienceEvent类提供的唯一标识符(`_id`)属性。 有关此值预期内容的更多详细信息，请参阅[XDM ExperienceEvent](../../classes/experienceevent.md)上的参考文档。