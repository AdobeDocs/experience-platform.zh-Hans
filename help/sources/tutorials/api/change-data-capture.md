---
title: 在API中为源连接启用更改数据捕获
description: 了解如何在API中为源连接启用更改数据捕获
exl-id: 362f3811-7d1e-4f16-b45f-ce04f03798aa
source-git-commit: bd28d5be932823b8bf9c98280f97694ff221d76d
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 0%

---

# 在API中为源连接启用更改数据捕获

>[!AVAILABILITY]
>
>连接到VA6数据中心时，在Amazon Web Services (AWS)上运行Adobe Experience Platform时，您现在可以对[!DNL Amazon S3]和[!DNL Data Landing Zone]源使用更改数据捕获。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。

在Adobe Experience Platform源中使用变更数据捕获，使您的源和目标系统近乎实时地保持同步。

Experience Platform当前支持&#x200B;**增量数据副本**，该副本会定期将新创建或更新的记录从源系统传输到摄取的数据集。 此方法依赖于&#x200B;**时间戳列**&#x200B;来跟踪更改，但它不检测删除，这可能会导致数据随时间而出现不一致。

相反，变更数据捕获会近乎实时地捕获并应用插入、更新和删除。 这一全面的更改跟踪确保数据集与源系统保持完全一致，并提供完整的更改历史记录，超出增量拷贝所支持的范围。 但是，删除操作需要特别考虑，因为它们会影响使用目标数据集的所有应用程序。

Experience Platform中的变更数据捕获需要具有&#x200B;**[关系架构](../../../xdm/data-mirror/overview.md)**&#x200B;的[Data Mirror](../../../xdm/schema/relational.md)。 您可以通过两种方式将更改数据提供给Data Mirror：

* **[手动更改跟踪](#file-based-sources)**：在数据集中包含未原生生成更改数据捕获记录的源的`_change_request_type`列
* **[本机变更数据捕获导出](#database-sources)**：使用直接从源系统导出的变更数据捕获记录

这两种方法都要求使用关系架构的Data Mirror保持关系并强制实施唯一性。

## 带关系架构的Data Mirror

>[!AVAILABILITY]
>
>Data Mirror和关系架构可供Adobe Journey Optimizer **协调的营销活动**&#x200B;许可证持有人使用。 根据您的许可证和功能启用，它们也可用作Customer Journey Analytics用户的&#x200B;**有限版本**。 请联系您的Adobe代表以获取访问权限。

>[!NOTE]
>
>**协调的营销活动用户**：使用本文档中介绍的Data Mirror功能处理保持引用完整性的客户数据。 即使您的源不使用变更数据捕获格式，Data Mirror也支持关系功能，例如主键实施、记录级别更新插入和架构关系。 这些功能可确保跨连接的数据集进行一致且可靠的数据建模。

Data Mirror使用关系架构来扩展变更数据捕获和启用高级数据库同步功能。 有关Data Mirror的概述，请参阅[Data Mirror概述](../../../xdm/data-mirror/overview.md)。

关系架构扩展了Experience Platform以强制实施主键唯一性、跟踪行级更改和定义架构级关系。 使用变更数据捕获，它们直接在数据湖中应用插入、更新和删除，从而减少了对提取、转换、加载(ETL)或手动协调的需要。

有关详细信息，请参阅[关系架构概述](../../../xdm/schema/relational.md)。

### 变更数据捕获的关系架构要求

在将关系模式用于变更数据捕获之前，请配置以下标识符：

* 用主键唯一地标识每个记录。
* 使用版本标识符按顺序应用更新。
* 对于时间序列架构，请添加时间戳标识符。

### 控制列处理 {#control-column-handling}

使用`_change_request_type`列指定每个行的处理方式：

* `u` — upsert（如果列不存在，则为默认值）
* `d` — 删除

此列仅在引入期间进行评估，不会存储或映射到XDM字段。

### 工作流 {#workflow}

要启用关系模式的变更数据捕获，请执行以下操作：

1. 创建关系架构。
2. 添加所需的描述符：
   * [主键描述符](../../../xdm/api/descriptors.md#primary-key-descriptor)
   * [版本描述符](../../../xdm/api/descriptors.md#version-descriptor)
   * [时间戳描述符](../../../xdm/api/descriptors.md#timestamp-descriptor) （仅限时间序列）
3. 从架构创建数据集并启用变更数据捕获。
4. 仅用于基于文件的摄取：如果需要显式指定删除操作，请将`_change_request_type`列添加到源文件中。 CDC导出配置会自动为数据库源处理此操作。
5. 完成源连接设置以启用摄取。

>[!NOTE]
>
>仅当您想要显式控制行级更改行为时，基于文件的源(Amazon S3、Azure Blob、Google Cloud Storage、SFTP)才需要`_change_request_type`列。 对于具有本机CDC功能的数据库源，更改操作通过CDC导出配置自动处理。 默认情况下，基于文件的摄取假定使用更新插入操作 — 只有在要在文件上载中指定删除操作时才需要添加此列。

>[!IMPORTANT]
>
>**需要数据删除计划**。 在实施变更数据捕获之前，所有使用关系模式的应用程序都必须了解删除后果。 规划删除操作将如何影响相关数据集、合规性要求和下游流程。 有关指导，请参阅[数据卫生注意事项](../../../hygiene/ui/record-delete.md#relational-record-delete)。

## 为基于文件的源提供更改数据 {#file-based-sources}

>[!IMPORTANT]
>
>基于文件的变更数据捕获要求使用具有关系架构的Data Mirror。 在执行以下文件格式设置步骤之前，请确保您已完成本文档前面所述的[Data Mirror设置工作流](#workflow)。 以下步骤描述了如何格式化数据文件，以包含Data Mirror将处理的更改跟踪信息。

对于基于文件的源（[!DNL Amazon S3]、[!DNL Azure Blob]、[!DNL Google Cloud Storage]和[!DNL SFTP]），请在文件中包含`_change_request_type`列。

使用上面`_change_request_type`控件列处理[部分中定义的](#control-column-handling)值。

>[!IMPORTANT]
>
>仅对于&#x200B;**基于文件的源**，某些应用程序可能需要包含`_change_request_type` (upsert)或`u` (delete)的`d`列来验证更改跟踪功能。 例如，Adobe Journey Optimizer的&#x200B;**协调营销活动**&#x200B;功能需要此列启用“协调营销活动”切换功能，并允许为定位选择数据集。 特定于应用程序的验证要求可能有所不同。

请按照下面特定于源的步骤执行操作。

### 云存储源 {#cloud-storage-sources}

按照以下步骤为云存储源启用更改数据捕获：

1. 为源创建基本连接：

   | 来源 | 基本连接指南 |
   |---|---|
   | [!DNL Amazon S3] | [创建 [!DNL Amazon S3] 基本连接](../api/create/cloud-storage/s3.md) |
   | [!DNL Azure Blob] | [创建 [!DNL Azure Blob] 基本连接](../api/create/cloud-storage/blob.md) |
   | [!DNL Google Cloud Storage] | [创建 [!DNL Google Cloud Storage] 基本连接](../api/create/cloud-storage/google.md) |
   | [!DNL SFTP] | [创建 [!DNL SFTP] 基本连接](../api/create/cloud-storage/sftp.md) |

2. [为云存储创建源连接](../api/collect/cloud-storage.md#create-a-source-connection)。

所有云存储源都使用上面`_change_request_type`基于文件的源[部分中描述的相同](#file-based-sources)列格式。

## 数据库源 {#database-sources}

### [!DNL Azure Databricks]

若要通过[!DNL Azure Databricks]使用变更数据捕获，您必须在源表中启用&#x200B;**变更数据馈送**，并在Experience Platform中通过relational schema配置Data Mirror。

使用以下命令在表上启用更改数据馈送：

**新表**

要将更改数据馈送应用到新表，必须在`delta.enableChangeDataFeed`命令中将表属性`TRUE`设置为`CREATE TABLE`。

```sql
CREATE TABLE student (id INT, name STRING, age INT) TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**现有表**

要将更改数据馈送应用于现有表，必须在`delta.enableChangeDataFeed`命令中将表属性`TRUE`设置为`ALTER TABLE`。

```sql
ALTER TABLE myDeltaTable SET TBLPROPERTIES (delta.enableChangeDataFeed = true)
```

**所有新表**

要将更改数据馈送应用于所有新表，必须将默认属性设置为`TRUE`。

```sql
set spark.databricks.delta.properties.defaults.enableChangeDataFeed = true;
```

有关详细信息，请阅读有关启用更改数据馈送[[!DNL Azure Databricks] 的](https://docs.databricks.com/aws/en/delta/delta-change-data-feed#enable-change-data-feed)指南。

请阅读以下文档，以了解如何为[!DNL Azure Databricks]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Azure Databricks] 基本连接](../api/create/databases/databricks.md)。
* [为数据库](../api/collect/database-nosql.md#create-a-source-connection)创建源连接。

### [!DNL Data Landing Zone]

若要通过[!DNL Data Landing Zone]使用变更数据捕获，您必须在源表中启用&#x200B;**变更数据馈送**，并在Experience Platform中通过relational schema配置Data Mirror。

请阅读以下文档，以了解如何为[!DNL Data Landing Zone]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Data Landing Zone] 基本连接](../api/create/cloud-storage/data-landing-zone.md)。
* [为云存储创建源连接](../api/collect/cloud-storage.md#create-a-source-connection)。

### [!DNL Google BigQuery]

要对[!DNL Google BigQuery]使用变更数据捕获，您必须在源表中启用变更历史记录，并在Experience Platform中用“关系架构”配置Data Mirror。

要在[!DNL Google BigQuery]源连接中启用更改历史记录，请在[!DNL Google BigQuery]控制台中导航到您的[!DNL Google Cloud]页面，并将`enable_change_history`设置为`TRUE`。 此属性启用数据表的更改历史记录。

有关详细信息，请阅读[&#x200B; [!DNL GoogleSQL]中](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list)数据定义语言语句的指南。

请阅读以下文档，以了解如何为[!DNL Google BigQuery]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Google BigQuery] 基本连接](../api/create/databases/bigquery.md)。
* [为数据库](../api/collect/database-nosql.md#create-a-source-connection)创建源连接。

### [!DNL Snowflake]

若要将变更数据捕获与[!DNL Snowflake]一起使用，您必须在源表中启用&#x200B;**变更跟踪**，并在Experience Platform中使用relational schema配置Data Mirror。

在[!DNL Snowflake]中，通过使用`ALTER TABLE`并将`CHANGE_TRACKING`设置为`TRUE`来启用更改跟踪。

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

有关详细信息，请阅读有关使用changes子句[[!DNL Snowflake] 的](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes)指南。

请阅读以下文档，以了解如何为[!DNL Snowflake]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Snowflake] 基本连接](../api/create/databases/snowflake.md)。
* [为数据库](../api/collect/database-nosql.md#create-a-source-connection)创建源连接。
