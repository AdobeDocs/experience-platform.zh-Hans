---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建查询
topic: queries
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# 创建查询

Adobe Experience Platform [!DNL Query Service] 能够针对中的数据集运行SQL查询 [!DNL Data Lake][!DNL Experience Platform]。 当您使用SQL与数据湖中的数据集交互时，必须了解自动管理某些方面， [!DNL Query Service] 如为数据湖中的每个数据集创建SQL安全表名 [!DNL Data Lake]。 在处理层次数据时，还需考虑 [!DNL Data Lake]一些事项，包括发现数据集所基于的模式，以及确保在层次模型中选择正确的字段。

以下文档将帮助您更好地了解内部的核心概念 [!DNL Query Service]:

- [数据集与表和模式](./datasets-and-tables.md)
- [编写查询的一般指导](./writing-queries.md)
- [ExperienceEvent查询](./experience-event-queries.md)
- [加入数据集](./joining-datasets.md)
- [重复数据消除](./deduplication.md)
