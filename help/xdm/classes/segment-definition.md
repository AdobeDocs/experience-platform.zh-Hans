---
solution: Experience Platform
title: 区段定义类
description: 本文档概述了体验数据模型(XDM)中的区段定义类。
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# [!UICONTROL 区段定义] 类

&quot;[!UICONTROL 区段定义]“是一个标准的体验数据模型(XDM)类，可捕获区段定义的详细信息。 类包括必填字段（如区段的ID和名称）以及其他可选属性。 如果要将外部系统中的区段定义引入Adobe Experience Platform，则应使用此类。

>[!NOTE]
>
>此类只应用于捕获有关区段定义本身的信息。 要在用户档案数据中捕获区段成员资格信息，您应使用 [区段成员资格详细信息字段组](../field-groups/profile/segmentation.md) 在 [!UICONTROL XDM个人配置文件] 架构。

![](../images/classes/segment-definition.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含以下项的对象 [!UICONTROL DateTime] 字段： <ul><li>`createDate`:在数据存储中创建资源的日期和时间，例如首次摄取数据时。</li><li>`modifyDate`:上次修改资源的日期和时间。</li></ul> |
| `_id` | 记录的唯一、系统生成的字符串标识符。 此字段用于跟踪单个记录的唯一性，防止重复数据，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会为其提供显式值。 但是，如果您愿意，您仍可以选择提供您自己的唯一ID值。<br><br>必须区分此字段 **不** 表示与个人相关的身份，而是数据本身的记录。 与个人有关的身份数据应降级为 [身份字段](../schema/composition.md#identity) 中。 |
| `createdByBatchID` | 导致创建记录的摄取批次的ID。 |
| `description` | 区段定义的描述。 |
| `identityMap` | 一个映射字段，其中包含区段所应用个人的一组命名空间标识。 请参阅 [架构组合基础知识](../schema/composition.md#identityMap) ，以了解其用例的详细信息。 |
| `modifiedByBatchID` | 导致记录更新的上次摄取的批处理的ID。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户ID。 |
| `segmentName` | **（必需）** 区段定义的名称。 |
| `segmentStatus` | 外部系统中区段的状态。 接受以下值： <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 区段定义的最新版本号。 |

{style=&quot;table-layout:auto&quot;}
