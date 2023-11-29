---
title: 查询服务中的增量加载
description: 增量加载功能同时使用匿名块和快照功能，为在忽略匹配数据的同时将数据从数据湖移动到数据仓库提供了近乎实时的解决方案。
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 查询服务中的增量加载

增量式负载设计模式是一种用于管理数据的解决方案。 该模式仅处理自上次加载执行以来创建或修改的数据集中的信息。

增量加载使用Adobe Experience Platform查询服务提供的各种功能，例如匿名块和快照。 此设计模式提高了处理效率，因为已跳过从源处理的任何数据。 它可以用于流数据处理和批量数据处理。

本文档提供了一系列说明，说明如何构建用于增量处理的设计模式。 这些步骤可用作创建自己的增量数据加载查询的模板。

## 快速入门

本文档中的SQL示例要求您了解匿名块和快照功能。 建议您阅读 [示例匿名块查询](./anonymous-block.md) 文档以及 [snapshot子句](../sql/syntax.md#snapshot-clause) 文档。

有关本指南中所用术语的指导，请参阅 [SQL语法指南](../sql/syntax.md).

## 增量加载数据

以下步骤演示了如何使用快照和匿名块功能创建和增量加载数据。 设计模式可用作您自己的查询序列的模板。

1. 创建 `checkpoint_log` 用于跟踪最近用于成功处理数据的快照的表。 跟踪表(`checkpoint_log` 在此示例中)必须首先初始化为 `null` 以逐步处理数据集。

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

1. 填充 `checkpoint_log` 对于需要增量处理的数据集，有一个空记录的表。 `DIM_TABLE_ABC` 是以下示例中要处理的数据集。 在首次处理时 `DIM_TABLE_ABC`， `last_snapshot_id` 初始化为 `null`. 这样，您就可以在第一次处理整个数据集时，并在其后逐步处理整个数据集。

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. 接下来，初始化 `DIM_TABLE_ABC_Incremental` 以包含已处理的输出 `DIM_TABLE_ABC`. 中的匿名块 **必填** 以下SQL示例的执行部分（如步骤1到4中所述）按顺序执行，以增量方式处理数据。

   1. 设置 `from_snapshot_id` 指示处理从何处开始。 此 `from_snapshot_id` 在本例中，是从 `checkpoint_log` 用于的表 `DIM_TABLE_ABC`. 初次运行时，快照ID将为 `null` 这意味着将处理整个数据集。
   1. 设置 `to_snapshot_id` 作为源表的当前快照ID (`DIM_TABLE_ABC`)。 在本例中，这是从源表的元数据表中查询的。
   1. 使用 `CREATE` 要创建的关键字 `DIM_TABLE_ABC_Incremenal` 作为目标表。 目标表会保留源数据集中已处理的数据(`DIM_TABLE_ABC`)。 这允许源表中的已处理数据，介于 `from_snapshot_id` 和 `to_snapshot_id`，以增量方式附加到目标表中。
   1. 更新 `checkpoint_log` 带有以下内容的表 `to_snapshot_id` 对于源数据， `DIM_TABLE_ABC` 已成功处理。
   1. 如果匿名块的任何顺序执行的查询失败， **可选** 异常部分已执行。 这将返回错误并结束进程。

   >[!NOTE]
   >
   >此 `history_meta('source table name')` 是一种用于获取对数据集中可用快照的访问权限的简便方法。

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

1. 在下面的匿名块示例中使用增量数据加载逻辑，以允许定期处理源数据集中的任何新数据（自最近的时间戳以来）并将其附加到目标表中。 在本例中，数据将更改为 `DIM_TABLE_ABC` 将被处理并附加到 `DIM_TABLE_ABC_incremental`.

   >[!NOTE]
   >
   > `_ID` 是两者中的主键 `DIM_TABLE_ABC_Incremental` 和 `SELECT history_meta('DIM_TABLE_ABC')`.

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

>[!IMPORTANT]
>
>快照元数据过期时间 **二** 天。 过期的快照会使上面提供的脚本的逻辑失效。

要解决快照ID过期的问题，请在匿名块的开头插入以下命令。 以下代码行将覆盖 `@from_snapshot_id` 包含最早可用的 `snapshot_id` 来自元数据。

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

通过阅读本文档，您应该更好地了解如何使用匿名块和快照功能执行增量加载，并且可以将此逻辑应用于您自己的特定查询。 有关查询执行的一般指导，请阅读 [查询服务中的查询执行指南](../best-practices/writing-queries.md).
