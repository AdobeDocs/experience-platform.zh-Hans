---
keywords: Experience Platform；数据镜像；关系架构；更改数据捕获；数据库同步；主键；关系
solution: Experience Platform
title: Data Mirror概述
description: 了解Data Mirror如何使用具有强制唯一性、关系和版本控制的关系架构，实现从外部数据库到Adobe Experience Platform的行级更改引入。
badge: 有限发布版
exl-id: bb92c77a-6c7a-47df-885a-794cf55811dd
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 0%

---

# Data Mirror概述

>[!AVAILABILITY]
>
>Data Mirror和关系架构可供Adobe Journey Optimizer **协调的营销活动**&#x200B;许可证持有人使用。 根据您的许可证和功能启用，它们也可用作Customer Journey Analytics用户的&#x200B;**有限版本**。 请联系您的Adobe代表以获取访问权限。

Data Mirror是一项Adobe Experience Platform功能，允许使用关系架构将外部数据库中的行级更改引入数据湖。 它保留数据关系，强制唯一性，并支持版本控制，而无需上游提取、转换、加载(ETL)过程。

使用Data Mirror将外部系统（如[!DNL Snowflake]、[!DNL Databricks]或[!DNL BigQuery]）的插入、更新和删除（可变数据）直接同步到Experience Platform中。 这有助于在将数据导入Platform时保持现有数据库模型结构和数据完整性。

## 功能和优点

Data Mirror提供了以下基本数据库同步功能：

* **主键强制**：确保数据集内的唯一性，并防止在摄取期间出现重复记录。
* **行级更改引入**：支持粒度数据更改，包括带精确控制的更新插入和删除。
* **架构关系**：通过描述符启用数据集之间的外键和主键关系。
* **乱序事件处理**：使用版本和时间戳描述符处理更改事件，即使这些更改事件不按顺序到达也是如此。
* **直接仓库集成**：与支持的云数据仓库连接，以实现近乎实时的更改同步。

使用Data Mirror直接从源系统中摄取更改，强制实施架构完整性，并将数据用于Analytics、Journey Orchestration和合规性工作流。 Data Mirror通过启用现有数据库模型的直接镜像，消除了复杂的上游ETL流程并加快了实施。

在使用Data Mirror实施关系架构时，规划删除和数据卫生要求。 在部署之前，所有应用程序都必须考虑删除操作对相关数据集、合规性工作流和下游进程的影响。

## 先决条件 {#prerequisites}

在开始之前，您应该了解Experience Platform的以下组件，并确认您的环境符合技术和结构要求：

* [在Experience Platform UI](../ui/resources/schemas.md)或[API中创建架构](../api/schemas.md)
* [配置云源连接](../../sources/home.md#cloud-storage)
* [应用变更数据捕获概念](../../sources/tutorials/api/change-data-capture.md) （更新插入、删除）
* 区分[标准](../schema/composition.md)和[关系架构](../schema/relational.md)
* [定义与描述符的结构关系](../api/descriptors.md)

### 实施要求

您的Platform实例和源数据必须满足特定要求，Data Mirror才能正常运行。 Data Mirror需要&#x200B;**关系架构**，这些架构是具有强制约束的灵活数据结构。

在所有架构中包括&#x200B;**主键和版本描述符**。 如果您使用的是时间序列架构，则还需要&#x200B;**时间戳描述符**。

外部数据库必须支持变更数据捕获或提供用于标识插入、更新和删除的元数据。 Source数据必须包含&#x200B;**唯一标识符**、单个字段或复合主键以及&#x200B;**版本信息**，以便系统能够以正确的顺序应用更新。

要检测删除，请添加一个`_change_request_type`列，指定每个记录是更新插入还是删除。

## 实施Data Mirror {#implementation-workflow}

与标准摄取方法不同，Data Mirror将您的数据库模型结构保留在Experience Platform数据湖中。 这种数据结构一致性消除了外部预处理的需要。 以下是高级的Data Mirror实施工作流程。 根据团队的工作流程和源系统选择实施方法。

### 定义架构结构

创建具有所需描述符（定义架构行为和约束的元数据）的[关系架构](../schema/relational.md)。 通过UI或直接通过API，选择适合您团队工作流程的方法。

* **UI方法**： [在架构编辑器中创建关系架构](../ui/resources/schemas.md#create-relational-schema)
* **API方法**：[通过架构注册表API创建架构](../api/schemas.md#create-relational-schema)

### 映射关系并定义数据管理

使用关系描述符定义数据集之间的连接。 跨数据集管理关系并保持数据质量。 这些任务可确保一致的联接，并支持符合数据卫生要求。

* **架构关系**： [使用描述符定义数据集之间的关系](../api/descriptors.md)
* **记录卫生**： [管理基于关系架构的数据集的Precision记录删除](../../hygiene/ui/record-delete.md#relational-record-delete)

### 配置源连接

选择基于源系统和用例的摄取方法。 每个选项都支持不同级别的自动化、转换和可扩展性。

* [**配置云源连接**](../../sources/home.md#cloud-storage)
* **SQL引入**：使用Data Distiller写入关系数据集
* [**文件上传**](../ui/resources/schemas.md#upload-ddl-file)：手动上传文件以进行批次或一次性摄取

### 启用变更数据捕获摄取

设置与支持的云数据仓库的变更数据捕获连接。 在保持唯一性并按正确顺序应用更新的同时，摄取行级更改。

* **更改数据捕获**： [在源连接中启用更改数据捕获](../../sources/tutorials/api/change-data-capture.md)

## 常见使用案例 {#use-cases}

请查看下面列出的常见用例，在这些用例中，Data Mirror支持精确的数据同步和关系保留。 每个方案都展示了Data Mirror如何跨Analytics、编排和合规性支持常见的业务需求。

### 关系数据建模

在Data Mirror中使用[关系架构](../schema/relational.md)表示实体，在行级别处理插入、更新和删除，并维护数据源中存在的主键和外键关系。 此方法将关系数据建模原则引入到Experience Platform中，并确保跨数据集的结构一致性。

### 仓库到湖同步

将事件数据、客户交互日志、活动事件和辅助数据从受支持的云数据仓库镜像到Experience Platform中。 这支持促销活动资格、定位精确度和消息排序。 Journey Optimizer和Real-Time CDP B2B依赖此逻辑实现近乎实时的编排逻辑。

### Customer Journey Analytics集成

同步时间序列事件，例如Web点击、产品查看、购买以及呼叫中心或聊天日志等系统中的支持交互。 完整的更改历史记录支持准确的趋势分析和行为分段。 适用于Customer Journey Analytics的Experience Platform Data Mirror使用此项来反映源系统中的更新插入和删除。

### B2B关系建模

保留帐户到联系人、订阅到帐户或联系人到区域等关系。 这些功能支持分段、商机评分、机会跟踪和多渠道协调。 与扁平化关系的标准摄取不同，Data Mirror使用描述符原生维护关系，以实现更准确的建模。

### 订阅管理

通过完整的版本历史记录跟踪事件，如续订、取消、升级、降级和计划更改。 这支持保留活动、流失预测和基于生命周期的分段。 完整历史记录可帮助实现行为洞察和精确定位。

### 数据卫生操作

使用变更数据捕获实现针对法规遵从性（例如，管控行业）和清理工作流的精确记录级删除。 Data Mirror可准确应用删除操作，同时跨连接的数据集保留相关数据。

## 重要注意事项 {#considerations}

查看这些关键注意事项，确保您的实施与支持的模式行为、摄取方法和关系模式保持一致。 正确的规划有助于避免集成问题并确保准确的数据建模。

### 数据删除和卫生要求

所有使用关系架构和Data Mirror的应用程序都必须了解数据删除后果。 关系架构支持精确的记录级别删除，这些删除可能会影响连接数据集中的相关数据。 无论您的特定使用情形如何，这些删除功能都会影响数据完整性、法规遵从性和下游应用程序行为。 在实施之前，查看基于关系架构[的数据集的](../../hygiene/ui/record-delete.md#relational-record-delete)数据卫生要求，并规划删除方案。

### 架构行为选择

关系架构默认为&#x200B;**记录行为**，用于捕获实体状态（客户、帐户等）。 如果您需要&#x200B;**时序行为**&#x200B;才能进行事件跟踪，则必须对其进行显式配置。

### 摄取方法比较

使用此比较表可以选择满足您的数据需求的最佳摄取方法，无论您是需要实时同步、基于SQL的转换还是手动文件上载。

| 摄取方法 | 用例 |
| ----------------------- | -------------------------------------------------------------- |
| **更改数据捕获** | 从支持的云仓库进行实时同步 |
| **数据Distiller** | 基于SQL的摄取和转换工作流 |
| **文件上传** | 在源集成不可用时批量/手动摄取 |

### 关系限制

Data Mirror支持使用描述符的&#x200B;**一对一**&#x200B;和&#x200B;**多对一**&#x200B;关系。 **多对多**&#x200B;关系需要额外的建模，因此不直接支持。

## 后续步骤

查看此概述后，您应该能够确定Data Mirror是否适合您的用例，并了解实施的要求。 要开始使用，请执行以下操作：

1. **数据架构师**&#x200B;应该评估您的数据模型，以确保它支持主键、版本控制和更改跟踪功能。
2. **业务利益相关者**&#x200B;应确认您的许可证包含关系架构支持和所需的Experience Platform版本。
3. **架构设计器**&#x200B;应该规划架构结构，以确定所需的描述符、字段关系和数据治理需求。
4. **实施团队**&#x200B;应根据您的源系统、实时要求和操作工作流选择摄取方法。

有关实施详细信息，请参阅[关系架构文档](../schema/relational.md)。
