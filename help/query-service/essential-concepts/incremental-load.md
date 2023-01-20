---
title: 查询服务中的增量加载
description: 增量加载功能使用匿名块和快照功能，为将数据从数据湖移动到data warehouse提供近乎实时的解决方案，同时忽略匹配的数据。
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 查询服务中的增量加载

增量加载设计模式是用于管理数据的解决方案。 该模式仅处理自上次加载执行以来创建或修改的数据集中的信息。

增量加载使用Adobe Experience Platform查询服务提供的各种功能，如匿名块和快照。 此设计模式提高了处理效率，因为已跳过源中处理的任何数据。 它可用于流数据处理和批处理数据处理。

本文档提供了构建用于增量处理的设计模式的一系列说明。 这些步骤可用作模板，以创建您自己的增量数据加载查询。

## 快速入门

本文档中的SQL示例要求您了解匿名块和快照功能。 建议您阅读 [示例匿名块查询](./anonymous-block.md) 文档和 [快照子句](../sql/syntax.md#snapshot-clause) 文档。

有关本指南中使用的任何术语的指导，请参阅 [SQL语法指南](../sql/syntax.md).

## 增量加载数据

以下步骤演示如何使用快照和匿名块功能创建和以增量方式加载数据。 设计模式可用作您自己的查询序列的模板。

1创建 `checkpoint_log` 表来跟踪用于成功处理数据的最新快照。 跟踪表(`checkpoint_log` 在本例中)必须首先初始化为 `null` 以逐步处理数据集。

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

2在 `checkpoint_log` 表格，其中包含需要增量处理的数据集的一个空记录。 `DIM_TABLE_ABC` 是以下示例中要处理的数据集。 在第一次加工时 `DIM_TABLE_ABC`, `last_snapshot_id` 初始化为 `null`. 这样，您就可以在第一次处理整个数据集，之后以递增方式处理。

```SQL
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
       cast(NULL AS string) last_snapshot_id,
       CURRENT_TIMESTAMP process_timestamp;
```

3接下来，初始化 `DIM_TABLE_ABC_Incremental` 包含处理输出 `DIM_TABLE_ABC`. 在 **必需** 如步骤1至4中所述，下面SQL示例的执行部分按顺序执行，以逐步处理数据。

1. 设置 `from_snapshot_id` 指示处理从何处开始。 的 `from_snapshot_id` 中，从 `checkpoint_log` 表 `DIM_TABLE_ABC`. 在初始运行时，快照ID将为 `null` 这意味着将处理整个数据集。
2. 设置 `to_snapshot_id` 作为源表(`DIM_TABLE_ABC`)。 在此示例中，从源表的元数据表中查询此数据。
3. 使用 `CREATE` 关键词创建 `DIM_TABLE_ABC_Incremenal` 作为目标表。 目标表保留源数据集(`DIM_TABLE_ABC`)。 这允许从源表处理的数据介于 `from_snapshot_id` 和 `to_snapshot_id`，以逐步附加到目标表。
4. 更新 `checkpoint_log` 表格 `to_snapshot_id` 对于 `DIM_TABLE_ABC` 已成功处理。
5. 如果对匿名块的任何按顺序执行的查询失败，则 **可选** 执行异常部分。 这会返回错误并结束该过程。

>[!NOTE]
>
>的 `history_meta('source table name')` 是一种用于获取数据集中可用快照的访问权限的简便方法。

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

4使用下面匿名块示例中的增量数据加载逻辑，以允许以常规频率处理来自源数据集（自最新时间戳以来）的任何新数据并将其附加到目标表。 在本例中，数据更改为 `DIM_TABLE_ABC` 将进行处理并附加到 `DIM_TABLE_ABC_incremental`.

>[!NOTE]
>
> `_ID` 是 `DIM_TABLE_ABC_Incremental` 和 `SELECT history_meta('DIM_TABLE_ABC')`.

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

此逻辑可应用于任何表以执行增量加载。

## 过期的快照

>[!IMPORTANT]
>
>快照元数据在 **二** 天。 过期的快照会使上述脚本的逻辑失效。

要解决快照ID过期的问题，请在匿名块的开头插入以下命令。 以下代码行将覆盖 `@from_snapshot_id` 最早可用 `snapshot_id` 元数据中。

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

通过阅读本文档，您应该更好地了解如何使用匿名块和快照功能来执行增量加载，并可以将此逻辑应用于您自己的特定查询。 有关查询执行的一般指导，请阅读 [查询服务中查询执行指南](../best-practices/writing-queries.md).
