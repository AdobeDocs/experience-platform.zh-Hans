---
title: 查询服务中的增量加载
description: 增量加载功能同时使用匿名块和快照功能，为在忽略匹配数据的同时将数据从数据湖移动到数据仓库提供了近乎实时的解决方案。
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 65eeeb1df1d512c4cd6c67892905a63cc1cc4fc5
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# 查询服务中的增量加载

增量式负载设计模式是一种用于管理数据的解决方案。 该模式仅处理自上次加载执行以来创建或修改的数据集中的信息。

增量加载使用Adobe Experience Platform查询服务提供的各种功能，例如匿名块和快照。 此设计模式提高了处理效率，因为已跳过从源处理的任何数据。 它可以用于流数据处理和批量数据处理。

本文档提供了一系列说明，说明如何构建用于增量处理的设计模式。 这些步骤可用作创建自己的增量数据加载查询的模板。

## 快速入门

本文档中的SQL示例要求您了解匿名块和快照功能。 建议您阅读[示例匿名块查询](./anonymous-block.md)文档以及[快照子句](../sql/syntax.md#snapshot-clause)文档。

有关本指南中使用的任何术语的指导，请参阅[SQL语法指南](../sql/syntax.md)。

## 增量加载数据

以下步骤演示了如何使用快照和匿名块功能创建和增量加载数据。 设计模式可用作您自己的查询序列的模板。

1. 创建`checkpoint_log`表以跟踪用于成功处理数据的最新快照。 跟踪表（`checkpoint_log`，在本例中）必须首先初始化为`null`，以便逐步处理数据集。

   ```SQL
   DROP TABLE IF EXISTS checkpoint_log;
   CREATE TABLE  checkpoint_log AS
   SELECT
      cast(NULL AS string) process_name,
      cast(NULL AS string) process_status,
      cast(NULL AS string) last_snapshot_id,
      cast(NULL AS TIMESTAMP) process_timestamp
      WHERE false;
   ```

1. 为需要增量处理的数据集填充一个空记录的`checkpoint_log`表。 `DIM_TABLE_ABC`是以下示例中要处理的数据集。 在首次处理`DIM_TABLE_ABC`时，`last_snapshot_id`被初始化为`null`。 这样，您就可以在第一次处理整个数据集时，并在其后逐步处理整个数据集。

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. 接下来，初始化`DIM_TABLE_ABC_Incremental`以包含来自`DIM_TABLE_ABC`的已处理输出。 以下SQL示例的&#x200B;**required**&#x200B;执行部分中的匿名块（如步骤1到步骤4中所述）按顺序执行以增量方式处理数据。

   1. 设置`from_snapshot_id`以指示处理从何处开始。 已从`checkpoint_log`表中查询示例中的`from_snapshot_id`以与`DIM_TABLE_ABC`一起使用。 在初始运行时，快照ID将为`null`，这意味着将处理整个数据集。
   1. 将`to_snapshot_id`设置为源表(`DIM_TABLE_ABC`)的当前快照标识。 在本例中，这是从源表的元数据表中查询的。
   1. 使用`CREATE`关键字创建`DIM_TABLE_ABC_Incremenal`作为目标表。 目标表保留源数据集(`DIM_TABLE_ABC`)中已处理的数据。 这允许将来自`from_snapshot_id`到`to_snapshot_id`之间的源表的已处理数据增量附加到目标表。
   1. 使用`to_snapshot_id`更新`checkpoint_log`表，以获取`DIM_TABLE_ABC`已成功处理的源数据。
   1. 如果匿名块的任何按顺序执行的查询失败，则执行&#x200B;**optional**&#x200B;异常部分。 这将返回错误并结束进程。

   >[!NOTE]
   >
   >`history_meta('source table name')`是一种用于获取数据集中可用快照的访问权限的简便方法。

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       CREATE TABLE DIM_TABLE_ABC_Incremental AS
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END 
   $$;
   ```

1. 在下面的匿名块示例中使用增量数据加载逻辑，以允许定期处理源数据集中的任何新数据（自最近的时间戳以来）并将其附加到目标表中。 在此示例中，将处理对`DIM_TABLE_ABC`的数据更改并将其附加到`DIM_TABLE_ABC_incremental`。

   >[!NOTE]
   >
   > `_ID`是`DIM_TABLE_ABC_Incremental`和`SELECT history_meta('DIM_TABLE_ABC')`中的主键。

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       INSERT INTO DIM_TABLE_ABC_Incremental
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END
   $$;
   ```

此逻辑可以应用于任何表以执行增量加载。

## 过期的快照

要解决快照ID过期的问题，请在匿名块的开头插入以下命令。 以下代码行使用元数据中最早可用的`snapshot_id`覆盖`@from_snapshot_id`。

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

整个代码块如下所示：

```SQL
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```

## 后续步骤

通过阅读本文档，您应该更好地了解如何使用匿名块和快照功能执行增量加载，并且可以将此逻辑应用于您自己的特定查询。 有关查询执行的一般指导，请阅读查询服务[&#128279;](../best-practices/writing-queries.md)中查询执行的指南。
