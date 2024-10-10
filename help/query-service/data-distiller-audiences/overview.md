---
title: 使用SQL构建受众
description: 了解如何在Adobe Experience Platform的Data Distiller中使用SQL受众扩展来使用SQL命令创建、管理和发布受众。 本指南涵盖受众生命周期的所有方面，包括创建、更新和删除用户档案，以及使用数据驱动的受众定义来定位基于文件的目标。
source-git-commit: 8b9a46d9dd35a60fc3f3087d5fd3c4dad395b1aa
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 1%

---

# 使用SQL构建受众

本文档介绍如何在Adobe Experience Platform的数据Distiller中使用SQL受众扩展来使用SQL命令创建、管理和发布受众。

使用SQL受众扩展通过数据湖中的数据（包括任何现有的维度实体）构建受众。 通过此扩展，您可以使用SQL直接定义受众区段，从而提供灵活性，而无需在配置文件中使用原始数据。 使用此方法创建的受众会自动在受众工作区中注册，您可以进一步将这些受众定位到基于文件的目标。

![显示SQL受众扩展工作流程的信息图。 这些阶段包括：使用SQL命令通过查询服务构建受众，在平台UI中管理受众，以及在基于文件的目标中激活受众。](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

## Data Distiller中的受众创建生命周期 {#audience-creation-lifecycle}

请按照以下步骤有效管理您的受众。 创建的受众可无缝集成到受众流中，从而允许您从这些基本受众构建区段，并定位基于文件的目标以实现客户定位。 使用以下SQL命令在Adobe Experience Platform中[创建](#create-audience)、[修改](#add-profiles-to-audience)和[删除](#delete-audience)受众。

### 创建受众 {#create-audience}

使用`CREATE AUDIENCE AS SELECT`命令定义新受众。 创建的受众将保存在数据集中，并在Data Distiller下的[!UICONTROL 受众]工作区中注册。

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title']) 
AS (select_query)
```

**参数**

使用以下参数定义SQL受众创建查询：

| 参数 | 描述 |
|--------------------|------------------------------------------------------------------|
| `schema` | 可选。 为查询创建的数据集定义XDM架构。 |
| `table_name` | 表和受众的名称。 |
| `primary_identity` | 指定受众的主标识列。 |
| `identity_namespace` | 标识的命名空间。 |
| `select_query` | 定义受众的SELECT语句。 可在[SELECT查询](../sql/syntax.md#select-queries)部分找到SELECT查询的语法。 |

{style="table-layout:auto"}

**示例：**

以下示例演示了如何构建SQL受众创建查询：

```sql
CREATE Audience aud_test 
WITH (primary_identity=month, identity_namespace=queryService) 
AS SELECT month FROM profile_dim_date LIMIT 5;
```

**限制：**

使用SQL创建受众时，请注意以下限制：

- 主标识列&#x200B;**必须**&#x200B;位于根级别。
- 新批次会覆盖现有数据集；当前不支持追加功能。
- 当前不支持嵌套属性。

### 将配置文件添加到现有受众 {#add-profiles-to-audience}

使用`INSERT INTO`命令将配置文件添加到现有受众。

```sql
INSERT INTO table_name 
SELECT select_query
```

**参数**

下表说明了`INSERT INTO`命令所需的参数：

| 参数 | 描述 |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | 作为create audience命令的一部分创建的表的名称。 |
| `select_query` | SELECT语句。 SELECT查询的语法可以在SELECT查询部分找到。 |

{style="table-layout:auto"}

**示例：**

以下示例演示了如何使用`INSERT INTO`命令将配置文件添加到现有受众：

```sql
INSERT INTO Audience aud_test 
SELECT month FROM profile_dim_date LIMIT 10;
```

### 删除受众（删除受众） {#delete-audience}

使用`DROP AUDIENCE`命令删除现有受众。 如果受众不存在，则除非指定`IF EXISTS`，否则会发生异常。

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**参数**

该表包含`DROP AUDIENCE`命令所需的参数：

| 参数 | 描述 |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | 可选。 如果指定，则在未找到表的情况下，不会引发异常。 |
| `db_name` | 指定用于限定受众数据集的数据组。 |
| `table_name` | 作为create audience命令的一部分创建的表的名称。 |

{style="table-layout:auto"}

**示例：**

以下示例演示了如何使用DROP AUDIENCE命令删除受众：

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### 自动发布受众 {#auto-publish-audiences}

使用SQL扩展创建的受众会自动在受众工作区的Data Distiller下注册。 注册后，这些受众即可进行定位，并可用于基于文件的目标，从而增强您的分段和定位策略。

![Adobe Experience Platform中的Audience工作区，显示Distiller自动发布并可供使用的数据。](../images/data-distiller/sql-audiences/audiences.png)

## 将受众激活到目标 {#activate-audiences}

通过将受众定位到任何基于文件的目标（如[!DNL Amazon S3]、[!DNL SFTP]或[!DNL Azure Blob]）来激活受众。 可以根据需要对丰富的受众属性进行进一步细化和筛选。

![Adobe Experience Platform目标类型的流程图，显示公用和专用/自定义目标，包括批处理选项和流选项。](../images/data-distiller/sql-audiences/destination-types.png)

## 功能说明 {#faqs}

本节介绍有关在Data Distiller中使用SQL创建和管理外部受众的常见问题解答。

+++选择以显示问题和解答

**问题**：

- 是否仅支持为平面数据集创建受众？

+++回答

也支持嵌套的数据集，但受众中只有平面属性可用。

+++

- 创建受众会生成单个数据集还是多个数据集，或者是否因配置而异？

+++回答

受众和数据集之间存在一对一的映射。

+++

- 在受众创建期间创建的数据集是否标记为用户档案？

+++回答

不会，在创建受众期间创建的数据集不会标记为配置文件。

+++

- 是否在数据湖中创建数据集？

+++回答

是，会在数据湖上创建数据集。

+++

- 受众中的属性是否限制为仅用于基于文件的企业批处理目标？ （是或否）

+++回答

是，受众中的属性限制为仅用于基于文件的企业批处理目标。

+++

- 我是否可以创建一个使用数据Distiller受众的受众？

+++回答

能，您可以创建使用数据Distiller受众的受众。

+++

- 这些受众是否会显示在Adobe Journey Optimizer中？ 如果没有，那么在规则生成器中创建一个包含此受众所有成员的新受众时，会发生什么情况？

+++回答

Data Distiller受众当前在Adobe Journey Optimizer中不可用。 您必须在Adobe Journey Optimizer规则生成器中创建新受众，使其在Adobe Journey Optimizer中可用。

+++

- 如何使用不同的计划创建两个Data Distiller受众？ 创建了多少数据集，它们是否标记为配置文件？

+++回答

由于每个受众都有一个基础数据集，因此将创建两个数据集。 但是，这些数据集不会标记为配置文件。 这两个数据集按各自的计划进行管理。

+++

- 如何删除受众？

+++回答

要删除受众，您可以在命令行界面中使用[`DROP AUDIENCE`命令](#delete-audience)或使用[受众工作区快速操作](../../segmentation/ui/audience-portal.md#quick-actions)。 注意：无法删除在下游目标中使用或者在其他受众中是从属的受众。

+++

- 当我将受众发布到配置文件时，它多久才能在区段生成器UI中可用，以及它何时可在目标中可用？

+++回答

配置文件快照导出完成后，即可在受众中查看配置文件。

+++

- Data Distiller受众是外部受众，是否每30天删除一次？

+++回答

是，由于数据Distiller受众是外部受众，因此每30天会删除一次这些受众。

+++

- Data Distiller Audiences是否显示在Audiences清单中？

+++回答

是，Data Distiller Audiences显示在受众清单中，原始名称为“Data Distiller”。

+++

+++

## 后续步骤

在阅读本文档后，您已了解如何在Data Distiller中使用SQL受众扩展，以使用SQL命令有效创建、管理和发布受众。 您现在可以根据独特的业务需求自定义受众定义，并在各种目标中激活这些定义，从而优化营销策略和数据驱动型决策。

接下来，您可以阅读以下文档，以进一步开发和优化您的Platform受众管理策略：

- **浏览受众评估**：了解Adobe Experience Platform中的[受众评估方法](../../segmentation/home.md#evaluate-segments)：用于实时更新的流式分段、用于计划或按需处理的批量分段以及用于在Edge Network上即时评估的边缘分段。
- **与目标集成**：阅读有关如何使用Platform目标UI [按需将文件导出到批处理目标](../../destinations/ui/export-file-now.md)的指南。
- **审核受众性能**：分析您的SQL定义的受众在不同渠道中的执行情况。 使用数据洞察来调整和改进受众定义和定位策略。 请阅读有关[受众分析](../../dashboards/insights/audiences.md)的文档，了解如何在Adobe Real-time Customer Data Platform中访问和调整SQL查询以获取受众分析。 然后，您可以通过自定义受众仪表板创建自己的见解并将原始数据转换为可操作的信息，从而有效地可视化并使用这些见解做出更好的决策。
