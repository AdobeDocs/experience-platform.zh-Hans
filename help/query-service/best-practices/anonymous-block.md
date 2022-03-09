---
title: 查询服务中的匿名块
description: 匿名块是Adobe Experience Platform查询服务支持的SQL语法，它允许您高效执行一系列查询
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 7087991c7a3daad57c5acd92a20c7024a1152c7e
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 查询服务中的匿名块

Adobe Experience Platform查询服务支持匿名块。 匿名块功能允许您链接一个或多个按顺序执行的SQL语句。 它们还允许使用例外处理选项。

匿名块功能是执行一系列操作或查询的一种有效方法。 块内的查询链可以另存为模板，并计划在特定时间或间隔运行。 这些查询可用于写入和附加数据以创建新数据集，通常在具有依赖关系的情况下使用。

该表提供了块主要部分的划分：执行和异常处理。 这些部分由关键词定义 `BEGIN`, `END`和 `EXCEPTION`.

| 部分 | 描述 |
|---|---|
| 执行 | 可执行部分以关键字开头 `BEGIN` 和以关键词结尾 `END`. 包含在 `BEGIN` 和 `END` 关键词将按顺序执行，并确保在完成序列中的上一个查询后才会执行后续查询。 |
| 异常处理 | 可选的例外处理部分以关键字开头 `EXCEPTION`. 它包含在执行部分中的任何SQL语句失败时要捕获和处理异常的代码。 如果任何查询失败，则整个块将停止。 |

值得注意的是，块是可执行语句，因此可以嵌套在其他块中。

>[!NOTE]
>
> 强烈建议在较小的数据集上测试查询，并确保查询能够按预期工作。 如果查询存在语法错误，则将引发异常，并且整个块将被中止。 验证查询的完整性后，您可以开始将查询链接起来。 这可确保在将块投入运行之前，块可按预期工作。

## 匿名块查询示例

以下查询显示了链SQL语句的示例。 请参阅 [查询服务中的SQL语法](../sql/syntax.md) 文档，以了解有关所使用的任何SQL语法的详细信息。

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

在以下示例中， `SET` 会保留 `SELECT` 查询。 变量的范围为匿名块。

快照ID将存储为本地变量(`@current_sid`)。 然后，在下一个查询中使用该数据集，以根据来自同一数据集/表的快照返回结果。

数据库快照是SQL Server数据库的只读静态视图。 更多 [关于快照子句的信息](../sql/syntax.md#SNAPSHOT-clause) 请参阅SQL语法文档。

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## 后续步骤

通过阅读本文档，您现在可以清楚地了解匿名块及其结构。 [有关查询执行的详细信息](./writing-queries.md)，请阅读有关查询服务中查询执行的指南。

您还应该阅读 [如何将匿名块与增量加载设计模式一起使用](./incremental-load.md) 以提高查询效率。
