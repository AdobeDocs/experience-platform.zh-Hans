---
title: 查询服务中的匿名块
description: 匿名块是Adobe Experience Platform查询服务支持的SQL语法，它允许您高效地执行一系列查询
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 查询服务中的匿名块

Adobe Experience Platform查询服务支持匿名块。 匿名块功能允许您链接一个或多个按顺序执行的SQL语句。 它们还允许使用例外处理选项。

匿名块特征是执行一系列操作或查询的有效方法。 块中的查询链可以另存为模板，并计划以特定时间或间隔运行。 这些查询可用于写入和附加数据以创建新数据集，通常用于具有依赖关系的地方。

>[!IMPORTANT]
>
>使用匿名块计划查询当前只能通过 [!DNL Query Service] API。 请参阅相关文档 [有关通过API计划查询的完整说明](../api/scheduled-queries.md).

该表提供了块主要部分的划分信息：执行和异常处理。 截面由关键字定义 `BEGIN`， `END`、和 `EXCEPTION`.

| 部分 | 描述 |
|---|---|
| 执行 | 可执行部分以关键字开头 `BEGIN` 并以关键词结尾 `END`. 任何包含在 `BEGIN` 和 `END` 关键字将按顺序执行，并确保在顺序中的上一个查询完成之前不执行后续查询。 |
| 异常处理 | 可选的异常处理部分以关键字开头 `EXCEPTION`. 它包含当执行部分中的任何SQL语句失败时捕获和处理异常的代码。 如果有任何查询失败，则整个块将停止。 |

值得注意的是，块是可执行语句，因此可以嵌套在其他块中。

>[!NOTE]
>
> 强烈建议在较小的数据集上测试您的查询，并确保它们按预期工作。 如果查询有语法错误，则将引发异常并中止整个块。 一旦确认了查询的完整性，您就可以开始将它们链接起来。 这可确保在块投入使用之前该块按预期工作。

## 示例匿名块查询

以下查询显示链接SQL语句的示例。 请参阅 [查询服务中的SQL语法](../sql/syntax.md) 文档，以了解有关使用的任何SQL语法的详细信息。

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

在以下示例中， `SET` 保留结果 `SELECT` 在指定的局部变量中查询。 变量的作用域为匿名块。

快照ID存储为局部变量(`@current_sid`)。 然后，在下一个查询中使用它来返回来自同一数据集/表的基于SNAPSHOT的结果。

数据库快照是SQL Server数据库的只读静态视图。 了解更多信息 [有关snapshot子句的信息](../sql/syntax.md#SNAPSHOT-clause) 请参阅SQL语法文档。

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## 后续步骤

通过阅读本文档，您现在对匿名块及其结构方式有了清楚的了解。 [有关查询执行的详细信息](../best-practices/writing-queries.md)，请阅读查询服务中的查询执行指南。

您还应阅读 [如何将匿名块用于增量负载设计模式](./incremental-load.md) 以提高查询效率。
