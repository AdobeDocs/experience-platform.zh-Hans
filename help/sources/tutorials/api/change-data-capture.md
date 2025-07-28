---
title: 在API中为源连接启用更改数据捕获
description: 了解如何在API中为源连接启用更改数据捕获
source-git-commit: d8b4557424e1f29dfdd8893932aef914226dd60d
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# 在API中为源连接启用更改数据捕获

Adobe Experience Platform源中的变更数据捕获是一项可用于在源系统和目标系统之间保持实时数据同步的功能。

目前，Experience Platform支持&#x200B;**增量数据副本**，这将确保源系统中新建或更新后的记录定期复制到摄取的数据集。 此进程依赖于&#x200B;**时间戳列**（如`LastModified`）的使用来跟踪更改并仅捕获&#x200B;**新插入或更新数据**。 但是，此方法不会考虑已删除的记录，这可能会导致一段时间内的数据不一致。

使用变更数据捕获，给定流捕获并应用所有变更，包括插入、更新和删除。 同样，Experience Platform数据集与源系统保持完全同步。

您可以对以下源使用变更数据捕获：

## [!DNL Amazon S3]

确保您打算摄取到Experience Platform的`_change_request_type`文件中存在[!DNL Amazon S3]。 此外，必须确保文件中包含以下有效值：

* `u`：用于插入和更新
* `d`：用于删除。

如果您的文件中不存在`_change_request_type`，则将使用默认值`u`。

请阅读以下文档，以了解如何为[!DNL Amazon S3]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Amazon S3] 基本连接](../api/create/cloud-storage/s3.md)。
* [为云存储创建源连接](../api/collect/cloud-storage.md#create-a-source-connection)。

## [!DNL Azure Blob]

确保您打算摄取到Experience Platform的`_change_request_type`文件中存在[!DNL Azure Blob]。 此外，必须确保文件中包含以下有效值：

* `u`：用于插入和更新
* `d`：用于删除。

如果您的文件中不存在`_change_request_type`，则将使用默认值`u`。

请阅读以下文档，以了解如何为[!DNL Azure Blob]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Azure Blob] 基本连接](../api/create/cloud-storage/blob.md)。
* [为云存储创建源连接](../api/collect/cloud-storage.md#create-a-source-connection)。

## [!DNL Azure Databricks]

必须在&#x200B;**表中启用**&#x200B;更改数据馈送[!DNL Azure Databricks]，以便在源连接中使用更改数据捕获。

使用以下命令在[!DNL Azure Databricks]中显式启用更改数据馈送选项

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

## [!DNL Data Landing Zone]

必须在&#x200B;**表中启用**&#x200B;更改数据馈送[!DNL Data Landing Zone]，以便在源连接中使用更改数据捕获。

使用以下命令在[!DNL Data Landing Zone]中显式启用更改数据馈送选项。

请阅读以下文档，以了解如何为[!DNL Data Landing Zone]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Data Landing Zone] 基本连接](../api/create/cloud-storage/data-landing-zone.md)。
* [为云存储创建源连接](../api/collect/cloud-storage.md#create-a-source-connection)。

## [!DNL Google BigQuery]

要在[!DNL Google BigQuery]源连接中使用变更数据捕获，请执行以下操作： 导航到[!DNL Google BigQuery]控制台中的[!DNL Google Cloud]页面，并将`enable_change_history`设置为`TRUE`。 此属性启用数据表的更改历史记录。

有关详细信息，请阅读[ [!DNL GoogleSQL]中](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#table_option_list)数据定义语言语句的指南。

请阅读以下文档，以了解如何为[!DNL Google BigQuery]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Google BigQuery] 基本连接](../api/create/databases/bigquery.md)。
* [为数据库](../api/collect/database-nosql.md#create-a-source-connection)创建源连接。

## [!DNL Google Cloud Storage]

确保您打算摄取到Experience Platform的`_change_request_type`文件中存在[!DNL Google Cloud Storage]。 此外，必须确保文件中包含以下有效值：

* `u`：用于插入和更新
* `d`：用于删除。

如果您的文件中不存在`_change_request_type`，则将使用默认值`u`。

请阅读以下文档，以了解如何为[!DNL Google Cloud Storage]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Google Cloud Storage] 基本连接](../api/create/cloud-storage/google.md)。
* [为云存储创建源连接](../api/collect/cloud-storage.md#create-a-source-connection)。


## [!DNL SFTP]

确保您打算摄取到Experience Platform的`_change_request_type`文件中存在[!DNL SFTP]。 此外，必须确保文件中包含以下有效值：

* `u`：用于插入和更新
* `d`：用于删除。

如果您的文件中不存在`_change_request_type`，则将使用默认值`u`。

请阅读以下文档，以了解如何为[!DNL SFTP]源连接启用更改数据捕获的步骤：

* [创建 [!DNL SFTP] 基本连接](../api/create/cloud-storage/sftp.md)。
* [为云存储创建源连接](../api/collect/cloud-storage.md#create-a-source-connection)。


## [!DNL Snowflake]

必须在&#x200B;**表中启用**&#x200B;更改跟踪[!DNL Snowflake]，以便在源连接中使用更改数据捕获。

在[!DNL Snowflake]中，通过使用`ALTER TABLE`并将`CHANGE_TRACKING`设置为`TRUE`来启用更改跟踪。

```sql
ALTER TABLE mytable SET CHANGE_TRACKING = TRUE
```

有关详细信息，请阅读有关使用changes子句[[!DNL Snowflake] 的](https://docs.snowflake.com/en/sql-reference/constructs/changes#usage-notes)指南。

请阅读以下文档，以了解如何为[!DNL Snowflake]源连接启用更改数据捕获的步骤：

* [创建 [!DNL Snowflake] 基本连接](../api/create/databases/snowflake.md)。
* [为数据库](../api/collect/database-nosql.md#create-a-source-connection)创建源连接。

