---
solution: Experience Platform
title: 区段定义类
topic-legacy: overview
description: 本文档概述了体验数据模型(XDM)中的区段定义类。
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 632ea4e2a94bfcad098a5fc5a5ed8985c0f41e0e
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# [!UICONTROL 区段定] 义类

“[!UICONTROL 区段定义]”是标准体验数据模型(XDM)类，用于捕获区段定义的详细信息。 类包括必需字段，如区段的ID和名称，以及其他可选属性。 如果要将外部系统的区段定义引入Adobe Experience Platform，应使用此类。

>[!NOTE]
>
>此类应仅用于捕获有关区段定义本身的信息。 为了捕获用户档案数据中的区段成员关系信息，您应使用[!UICONTROL XDM个人用户档案]模式中的[区段成员关系详细信息字段组](../field-groups/profile/segmentation.md)。

![](../images/classes/segment-definition.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含以下[!UICONTROL DateTime]字段的对象： <ul><li>`createDate`:在数据存储中创建资源的日期和时间，例如首次摄取数据的时间。</li><li>`modifyDate`:上次修改资源的日期和时间。</li></ul> |
| `_id` | 记录的唯一、由系统生成的字符串标识符。 此字段用于跟踪单个记录的唯一性、防止重复数据并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据获取过程中不提供显式值。但是，您仍可以根据需要选择提供自己的唯一ID值。<br><br>必须指出的是，这一 **领域** 不代表与个人有关的身份，而是数据本身的记录。应将与个人有关的身份数据归入[身份字段](../schema/composition.md#identity)。 |
| `createdByBatchID` | 导致创建记录的所摄取批的ID。 |
| `description` | 区段定义的说明。 |
| `identityMap` | 一个映射字段，其中包含段所应用的个体的一组命名空间标识。 有关模式组合的用例的详细信息，请参阅[基础知识](../schema/composition.md#identityMap)中有关标识映射的部分。 |
| `modifiedByBatchID` | 导致记录更新的上次收录批的ID。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户的ID。 |
| `segmentName` | **（必需）** 区段定义的名称。 |
| `segmentStatus` | 外部系统中区段的状态。 接受以下值： <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 区段定义的最新版本号。 |
