---
title: 查询服务中的匿名块
description: 匿名块是Adobe Experience Platform查询服务支持的SQL语法，它允许您高效地执行一系列查询
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 65eeeb1df1d512c4cd6c67892905a63cc1cc4fc5
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# 查询服务中的匿名块

Adobe Experience Platform查询服务支持匿名块。 匿名块功能允许您链接一个或多个按顺序执行的SQL语句。 它们还允许使用例外处理选项。

匿名块特征是执行一系列操作或查询的有效方法。 块中的查询链可以另存为模板，并计划以特定时间或间隔运行。 这些查询可用于写入和附加数据以创建新数据集，通常用于具有依赖关系的地方。

该表提供了块主要部分的划分信息：执行和异常处理。 这些部分由关键字`BEGIN`、`END`和`EXCEPTION`定义。

| 部分 | 描述 |
|---|---|
| 执行 | 可执行部分以关键字`BEGIN`开头，以关键字`END`结尾。 将按顺序执行`BEGIN`和`END`关键字中包含的任何语句集，并确保在完成顺序中的上一个查询之前，不会执行后续查询。 |
| 异常处理 | 可选的异常处理部分以关键字`EXCEPTION`开头。 它包含当执行部分中的任何SQL语句失败时捕获和处理异常的代码。 如果有任何查询失败，则整个块将停止。 |

值得注意的是，块是可执行语句，因此可以嵌套在其他块中。

>[!NOTE]
>
> 强烈建议在较小的数据集上测试您的查询，并确保它们按预期工作。 如果查询有语法错误，则将引发异常并中止整个块。 一旦确认了查询的完整性，您就可以开始将它们链接起来。 这可确保在块投入使用之前该块按预期工作。

## 示例匿名块查询

以下查询显示链接SQL语句的示例。 有关使用的任何SQL语法的详细信息，请参阅查询服务[&#128279;](../sql/syntax.md)文档中的SQL语法。

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

在以下示例中，`SET`在指定的局部变量中保留`SELECT`查询的结果。 变量的作用域为匿名块。

快照ID存储为局部变量(`@current_sid`)。 然后，在下一个查询中使用它来返回来自同一数据集/表的基于SNAPSHOT的结果。 有关snapshot子句[&#128279;](../sql/syntax.md#SNAPSHOT-clause)的更多信息，请参阅SQL语法文档。

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## 与第三方客户端的匿名阻止 {#third-party-clients}

某些第三方客户端在SQL块之前和之后可能需要单独的标识符，以指示脚本的一部分应作为单个语句处理。 如果您在第三方客户端上使用查询服务时收到错误消息，您应该参阅第三方客户端关于使用SQL块的文档。

例如，**DbVisualizer**&#x200B;要求分隔符必须是行上的唯一文本。 在DbVisualizer中，开始标识符的默认值为`--/`，结束标识符的默认值为`/`。 下面显示了DbVisualizer中的匿名块示例：

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

特别是对于DbVisualizer，UI中还提供了“[!DNL Execute the complete buffer as one SQL statement]”选项。 有关详细信息，请参阅[DbVisualizer文档](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer)。

## 后续步骤

通过阅读本文档，您现在对匿名块及其结构方式有了清楚的了解。 有关写入查询的详细信息，请阅读[查询执行指南](../best-practices/writing-queries.md)。

您还应该阅读[如何将匿名块与增量负载设计模式](./incremental-load.md)结合使用以提高查询效率。
