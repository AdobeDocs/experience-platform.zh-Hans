---
keywords: Experience Platform；主页；热门主题；关系架构；关系架构；架构；架构；xdm；体验数据模型；
solution: Experience Platform
title: 关系架构
description: 了解Adobe Experience Platform中的关系架构，包括功能、必填字段、关系和限制。
badge: 有限发布版
exl-id: 397e5937-b892-4fd3-b90e-29ed9229dc69
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 0%

---

# 关系架构

>[!AVAILABILITY]
>
>Data Mirror和关系架构可供Adobe Journey Optimizer **协调的营销活动**&#x200B;许可证持有人使用。 根据您的许可证和功能启用，它们也可用作Customer Journey Analytics用户的&#x200B;**有限版本**。 请联系您的Adobe代表以获取访问权限。

关系架构提供了一种灵活的受控建模模式，用于在Adobe Experience Platform数据湖中表示结构化数据。 它们支持强制的主键、模式级别的关系和对记录的细粒度控制 — 所有这些都不依赖合并模式或完整关系数据库系统。

>[!IMPORTANT]
>
>数据删除注意事项适用于所有关系架构实施。 使用这些架构的应用程序必须了解删除操作如何影响相关数据集、合规性要求和下游流程。 在实施之前，规划删除方案并审查[数据卫生指导](../../hygiene/ui/record-delete.md#relational-record-delete)。

使用关系架构可以：

* 使用强制的单字段或复合主键确保数据完整性。
* 使用版本控制功能对插入、更新和删除操作启用精确的更改跟踪。
* 定义可重用的架构级别关系以模拟现实世界的实体连接。
* 通过支持多个数据模型，避免跨应用程序复制架构结构。
* 绕过合并架构限制以简化新用户引导，减少架构膨胀，并避免不需要的架构更改。

## 关系架构与标准XDM架构有何不同

Experience Platform中的标准XDM架构遵循以下三种数据行为之一：记录、时间序列或临时。 有关定义和详细信息，请参阅[XDM数据行为](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/home#data-behaviors)。

在传统模型中，记录和时间序列架构参与[联合架构](../api/unions.md)（另请参阅[联合架构UI指南](../../profile/ui/union-schema.md)）。 这些架构会随着共享[字段组](./composition.md#field-group)的更新而自动演变，并且自定义字段必须嵌套在租户命名空间下。 虽然此模型功能强大，但可能会减慢载入速度，生成包含未使用字段的过于复杂的架构，并需要额外的数据映射或转换。 这些因素会增加学习曲线和持续的维护工作。

关系架构删除合并架构依赖项，从而消除共享字段组中的自动更新，并允许直接字段定义，而无需租户命名空间限制。 您可以明确地控制主键、关系和初始架构设计，从而更容易建模数据以满足创建时的需求。

## 关系架构的功能

使用以下功能对数据湖中的结构化数据进行建模，同时保持治理、完整性和互操作性。

* **架构行为支持**：配置方式：
   * **记录行为**：捕获实体（如客户、帐户或营销活动）的当前状态。
   * **时间序列行为**：捕获事件及其发生时间，用于跟踪序列或随时间发生的变化。
* **主键强制**：定义一个主键以唯一地标识每个记录并防止在摄取期间出现重复项。
* **版本控制**：使用&#x200B;**版本标识符**（描述符）确保以正确的顺序应用更新，即使记录不按顺序到达也是如此。
* **关系映射**：在关系架构之间或关系架构与标准架构之间创建一对一或多对一关系。 关系定义存储为描述符，以实现高效联接。
* **简化的演化**：关系架构不参与合并视图，在共享字段组更改时不会更新，从而防止意外的下游更改。
* **灵活的字段定义**：直接添加字段，而无需租户ID命名空间。 关系架构不支持XDM字段组。
* **不依赖合并架构**：提高了查询性能并减少了管理全局架构视图的操作开销。
* **事件时间排序**：对于时间序列架构，请使用&#x200B;**时间戳标识符**&#x200B;按发生时间而不是摄取时间对事件进行排序。

## 必填字段

关系架构需要某些描述符 — 架构定义中的元数据，用于控制关键行为和约束。 在架构定义中添加以下描述符。

### 主键描述符

使用主键描述符确保每个记录都是唯一可识别的。 支持的配置包括：

* **单字段主键**：为每个记录使用一个具有唯一值的字段。
* **复合主键**：使用多个字段形成唯一标识符。 对于时间序列架构，复合密钥必须包含由时间戳描述符标识的时间戳字段。

>[!NOTE]
>
>在UI架构编辑器中，版本描述符和时间戳描述符分别显示为“[!UICONTROL Version identifier]”和“[!UICONTROL Timestamp identifier]”。

**示例（单字段）：**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": "customerId"
}
```

**示例（时间序列复合）**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": ["customerId", "eventTimestamp"]
}
```

### 版本描述符（标识符）

定义版本描述符（标识符）以保持正确的记录状态并确保应用最新的更新。 当多个记录共享同一主键时，具有最高版本值的记录被视为最新记录。

**示例：**

```json
{
  "xdm:descriptor": "xdm:descriptorVersion",
  "xdm:sourceProperty": "lastModified"
}
```

### 时间戳描述符（标识符）

对于时间序列架构，请定义时间戳描述符（标识符）以设置事件时间进行排序。

**示例：**

```json
{
  "xdm:descriptor": "xdm:descriptorTimestamp",
  "xdm:sourceProperty": "eventTimestamp"
}
```

>[!NOTE]
>
>描述符是架构定义元数据的一部分，不会存储在数据行中。

有关在架构编辑器中创建描述符的说明，请参阅[在架构编辑器中创建描述符](../tutorials/relationship-ui.md)。 有关基于API的创建，请参阅[使用API创建描述符](../tutorials/relationship-api.md)。

## 关系支持 {#relationship-support}

关系数据建模是关系架构的主要用途。 应用程序用例甚至可能将这些架构称为“关系架构”。 关系描述符通过链接跨架构的数据集而不在数据行中嵌入外键来启用这些连接。 它们改进了引用完整性，支持可重用的建模模式，并支持跨应用程序的连接查询。

在架构级别创建关系描述符，以便在查询时动态解析。 基数值（1:1，多对一）提供了指导，但在引入期间不强制实施约束，从而支持跨连接的数据集进行灵活的数据建模。

在添加关系描述符之前，请确定适当的类型和目标：

* **一对一** — 源架构中的每个记录最多只对应于目标架构中的一个记录。
* **多对一** — 源架构中的多个记录可能引用目标架构中的相同记录。

>[!NOTE]
>
>可以定义两个关系架构之间的关系或关系架构与标准架构之间的关系。 不支持与临时架构的关系。

**示例：一对一关系**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "accountId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/account",
  "xdm:destinationProperty": "accountId"
}
```

**示例：多对一关系**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "customerId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/customer",
  "xdm:destinationProperty": "customerId"
}
```

有关关系描述符类型和语法的列表，请参阅[描述符API引用](../api/descriptors.md)。要了解如何在实践中应用这些概念，请按照教程[在API中定义关系](../tutorials/relationship-api.md)或[在UI中创建关系](../tutorials/relationship-ui.md)。

>[!NOTE]
>
>由于在架构级别定义关系，请确保在查询中显式连接相关数据集。 使用Data Distiller等工具在查询期间解决这些关系。

>[!IMPORTANT]
>
>关系基数是信息性的，在引入期间不会强制执行。 它仅在查询或分析期间解析关系时应用。 在引入期间，不要依赖基数设置来验证数据。 自行检查并清理数据，并确保您定义的关系规则与您查询或分析数据的方式相匹配。

>[!NOTE]
>
>关系架构可以链接到标准架构，但不能链接到临时架构。

## 数据删除和卫生注意事项 {#data-hygiene-support}

关系架构支持精确删除对所有应用程序和用例具有普遍影响的记录级别。 主键、版本和时间戳描述符为在删除操作期间准确识别记录奠定了基础。

### 普遍删除影响

所有使用关系架构的应用程序都必须考虑：

* **引用完整性**：删除操作可能会影响跨连接数据集的相关记录
* **合规性要求**：某些行业需要特定的删除行为和审核跟踪
* **应用程序行为**：下游系统可能需要正确处理删除事件
* **数据一致性**：相关数据集必须在删除操作期间保持一致性
* **删除计划**：考虑在设计阶段对所有连接的数据集和应用程序产生的下游影响

有关实施指南，请参阅[从基于关系架构的数据集中删除记录](../../hygiene/ui/record-delete.md#relational-record-delete)。

## 限制和注意事项 {#limitations}

在使用关系架构之前，请查看以下限制：

* 关系架构不参与合并架构。
* 架构演化是手动的；当字段组更改时，它们不会自动更新。

>[!IMPORTANT]
>
>在使用架构初始化数据集后，架构演化将受到限制。 事先仔细规划字段名称和类型，因为一旦接收到数据，就无法删除或修改字段。

* 关系仅限于一对一和多对一。
* 可用性取决于您的许可证或功能支持。
* 时间序列架构需要复合主键。
