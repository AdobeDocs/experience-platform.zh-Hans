---
solution: Experience Platform
title: 区段定义类
description: 了解Experience Data Model (XDM)中的“区段定义”类。
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!UICONTROL 区段定义]类

“[!UICONTROL 区段定义]”是一个标准体验数据模型(XDM)类，可捕获区段定义的详细信息。 类包括必填字段（例如受众的ID和名称）以及其他可选属性。 如果要将外部系统的区段定义引入Adobe Experience Platform，应使用此类。

>[!NOTE]
>
>此类只应用于捕获有关区段定义本身的信息。 若要在配置文件数据中捕获受众成员资格信息，您应使用[!UICONTROL XDM个人配置文件]架构中的[区段成员资格详细信息字段组](../field-groups/profile/segmentation.md)。

![](../images/classes/segment-definition.png)

| 属性 | 描述 |
| --- | --- |
| `_repo` | 包含以下[!UICONTROL 日期时间]字段的对象： <ul><li>`createDate`：在数据存储中创建资源的日期和时间，如首次摄取数据的时间。</li><li>`modifyDate`：上次修改资源的日期和时间。</li></ul> |
| `_id` | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会向其提供显式值。 但是，如果您愿意，仍然可以选择提供自己的唯一ID值。<br><br>请务必注意，此字段&#x200B;**不表示与个人相关的身份**，而是表示数据本身的记录。 与人员相关的身份数据应委托给[身份字段](../schema/composition.md#identity)。 |
| `createdByBatchID` | 导致创建记录的摄取批次的ID。 |
| `description` | 区段定义的描述。 |
| `identityMap` | 一个映射字段，其中包含受众应用于的个人的一组命名空间身份。 有关其用例的更多信息，请参阅[架构组合基础知识](../schema/composition.md#identityMap)中关于标识映射的部分。 |
| `modifiedByBatchID` | 导致更新记录的上次摄取批次的ID。 |
| `repositoryCreatedBy` | 创建记录的用户的ID。 |
| `repositoryLastModifiedBy` | 上次修改记录的用户的ID。 |
| `segmentName` | **（必需）**&#x200B;区段定义的名称。 |
| `segmentStatus` | 来自外部系统的受众的状态。 接受以下值： <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 区段定义的最新版本号。 |

{style="table-layout:auto"}
