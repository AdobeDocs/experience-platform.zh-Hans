---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；故障诊断指南；FAQ；故障诊断；
solution: Experience Platform
title: 查询服务疑难解答指南
topic-legacy: troubleshooting
description: 本文档包含与查询服务相关的常见问题和解答。 主题包括、导出数据、第三方工具和PSQL错误。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 08272f72c71f775bcd0cd7fffcd2e4da90af9ccb
workflow-type: tm+mt
source-wordcount: '3781'
ht-degree: 1%

---

# [!DNL Query Service] 疑难解答指南

本文档提供了有关查询服务的常见问题解答，并提供了使用查询服务时常见错误代码的列表。 有关Adobe Experience Platform中其他服务的相关问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

以下常见问题解答列表分为以下几类：

- [General](#general)
- [导出数据](#exporting-data)
- [第三方工具](#third-party-tools)
- [PostgreSQL API错误](#postgresql-api-errors)
- [REST API错误](#rest-api-errors)

## 一般查询服务问题 {#general}

本节包含有关性能、限制和流程的信息。

### 我能否在查询服务编辑器中关闭自动完成功能？

+++回答否。 编辑器当前不支持关闭自动完成功能。
+++

### 在查询中键入内容时，查询编辑器有时速度会变慢？

+++回答一个潜在原因是自动完成功能。 该功能会处理某些元数据命令，这些命令有时会在查询编辑期间减慢编辑器速度。
+++

### 我能否将Postman用于查询服务API?

+++回答是，您可以使用Postman（一个免费的第三方应用程序）可视化所有AdobeAPI服务并与之交互。 观看 [Postman设置指南](https://video.tv.adobe.com/v/28832) 有关如何在Adobe Developer控制台中设置项目并获取所有必要凭据以与Postman一起使用的分步说明。 请参阅 [有关启动、运行和共享Postman集合的指导](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### 通过UI查询返回的最大行数是否存在限制？

+++回答是，查询服务在内部应用50,000行的限制，除非在外部指定明确的限制。 请参阅 [交互式查询执行](./best-practices/writing-queries.md#interactive-query-execution) 以了解更多详细信息。
+++

### 查询生成的输出是否存在数据大小限制？

+++回答否。 数据大小没有限制，但是交互式会话的查询超时限制为10分钟。 如果查询以批量CTAS形式执行，则不适用10分钟超时。 请参阅 [交互式查询执行](./best-practices/writing-queries.md#interactive-query-execution) 以了解更多详细信息。
+++

### 如何绕过SELECT查询中行输出数的限制？

+++回答要绕过输出行限制，请在查询中应用“限制0”。 例如：

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### 如何在10分钟内停止超时查询？

+++回答当查询超时时，建议使用以下一个或多个解决方案。

- [将查询转换为CTAS查询](./sql/syntax.md#create-table-as-select) 并计划运行。 计划运行可以执行以下任一操作 [通过UI](./ui/user-guide.md#scheduled-queries) 或 [API](./api/scheduled-queries.md#create).
- 通过应用附加数据块，对较小的数据块执行查询 [筛选条件](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [执行EXPLAIN命令](./sql/syntax.md#explain) 收集更多细节。
- 查看数据集中数据的统计信息。
- 将查询转换为简化表单，然后使用 [准备报表](./sql/prepared-statements.md).
+++

### 如果同时运行多个查询，是否会对查询服务性能产生任何问题或影响？

+++回答否。 查询服务具有自动缩放功能，可确保并发查询不会对服务性能产生任何显着影响。
+++

### 如何从分层数据集中查找列名称？

+++回答以下步骤描述如何通过用户界面显示数据集的表格视图，包括扁平化表单中的所有嵌套字段和列。

- 登录Experience Platform后，选择 **[!UICONTROL 数据集]** 在UI的左侧导航中导航到 [!UICONTROL 数据集] 功能板。
- 数据集 [!UICONTROL 浏览] 选项卡。 您可以使用搜索栏优化可用选项。 从显示的列表中选择一个数据集。

![Platform UI中的“数据集”功能板，其中突出显示了搜索栏和数据集。](./images/troubleshooting/dataset-selection.png)

- 的 [!UICONTROL 数据集活动] 屏幕。 选择 **[!UICONTROL 预览数据集]** 打开XDM架构对话框以及所选数据集中扁平化数据的表格视图。 有关更多详细信息，请参阅 [预览数据集文档](../catalog/datasets/user-guide.md#preview-a-dataset)

![数据集功能板的“数据集活动”选项卡中突出显示了“预览”数据集。](./images/troubleshooting/dataset-preview.png)

- 从架构中选择任意字段，以在扁平列中显示其内容。 列的名称显示在页面右侧其内容上方。 您应复制此名称以用于查询此数据集。

![扁平化数据的XDM架构和表格视图。 嵌套数据集的列名称在UI中突出显示。](./images/troubleshooting/column-name.png)

有关 [如何使用嵌套数据结构](./best-practices/nested-data-structures.md) 使用查询编辑器或第三方客户端。
+++

### 如何加快对包含数组的数据集的查询？

+++回答要提高包含数组的数据集上的查询性能，您应该 [引爆阵列](https://spark.apache.org/docs/latest/api/sql/index.html#explode) as a [CTAS查询](./sql/syntax.md#create-table-as-select) 在运行时，然后进一步探索它，以寻找改进其处理时间的机会。
+++

### 为什么CTAS查询在仅处理少量行的数小时后仍会进行处理？

+++回答如果查询在非常小的数据集上花费了很长时间，请联系客户支持。

处理过程中查询卡住的原因可能有多种。 要确定确切原因，需要逐个案例进行深入分析。 [联系Adobe客户支持](#customer-support) 这个过程。
+++

### 如何联系Adobe客户支持？ {#customer-support}

+++回答
[Adobe客户支持电话号码的完整列表](https://helpx.adobe.com/ca/contact/phone.html) 可在Adobe帮助页面上找到。 或者，也可以通过完成以下步骤在线找到帮助：

- 导航到 [https://www.adobe.com/](https://www.adobe.com/cn/) 在Web浏览器中。
- 在顶部导航栏的右侧，选择 **[!UICONTROL 登录]**.

![突出显示了登录的Adobe网站。](./images/troubleshooting/adobe-sign-in.png)

- 使用您在Adobe ID许可证中注册的Adobe和密码。
- 选择 **[!UICONTROL 帮助和支持]** 中。

![顶部导航栏下拉菜单中突出显示了“帮助与支持”、“企业支持”和“联系我们”。](./images/troubleshooting/help-and-support.png)

此时会显示包含 [!UICONTROL 帮助和支持] 中。 选择 **[!UICONTROL 联系我们]** 要打开Adobe客户关怀虚拟助理，请选择 **[!UICONTROL 企业支持]** 为大型组织提供专门帮助。
+++

### 如何实施一系列连续的作业，如果上一个作业未成功完成，则不执行后续作业？

+++答案匿名块功能允许您将一个或多个按顺序执行的SQL语句链接起来。 它们还允许使用例外处理选项。

请参阅 [匿名块文档](./best-practices/anonymous-block.md) 以了解更多详细信息。
+++

### 如何在查询服务中实施自定义归因？

+++答案有两种方法可实施自定义归因：

1. 使用现有 [Adobe定义的函数](./sql/adobe-defined-functions.md) 以确定是否满足用例需求。
1. 如果上一个建议不符合您的用例，则应使用 [窗口函数](./sql/adobe-defined-functions.md#window-functions). 窗口函数查看序列中的所有事件。 它们还允许您查看历史数据，并可用于任何组合。
+++

### 我是否可以模板化我的查询以便能够轻松地重复使用它们？

+++回答是，您可以使用预准备语句模板化查询。 准备的语句可以优化性能并避免重复重新解析查询。 请参阅 [准备陈述文档](./sql/prepared-statements.md) 以了解更多详细信息。
+++

### 如何检索查询的错误日志？ {#error-logs}

+++回答要检索特定查询的错误日志，您必须首先使用查询服务API获取查询日志详细信息。 HTTP响应包含调查查询错误所需的查询ID。

使用GET命令检索多个查询。 有关如何对API进行调用的信息，请参阅 [示例API调用文档](./api/queries.md#sample-api-calls).

在响应中，确定要调查的查询，然后使用其发出另一个GET请求 `id` 值。 有关完整说明，请参阅 [按ID文档检索查询](./api/queries.md#retrieve-a-query-by-id).

成功响应会返回HTTP状态200，并包含 `errors` 数组。 为简便起见，缩短了响应。

```json
{
    "isInsertInto": false,
    "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
    "clientId": "8c2455819a624534bb665c43c3759877",
    "state": "SUCCESS",
    "rowCount": 0,
    "errors": [{
      'code': '58000', 
      'message': 'Batch query execution gets : [failed reason ErrorCode: 58000 Batch query execution gets : [Analysis error encountered. Reason: [sessionId: f055dc73-1fbd-4c9c-8645-efa609da0a7b Function [varchar] not defined.]]]', 
      'errorType': 'USER_ERROR'
      }],
    "isCTAS": false,
    "version": 1,
    "id": "343388b0-e0dd-4227-a75b-7fc945ef408a",
}
```

的 [查询服务API参考文档](https://www.adobe.io/experience-platform-apis/references/query-service/) 提供有关所有可用端点的更多信息。
+++

### “验证架构时出错”是什么意思？

+++回答：“验证架构时出错”消息意味着系统无法在架构中找到字段。 您应阅读 [在查询服务中组织数据资产](./best-practices/organize-data-assets.md) 后跟 [创建表作为选择文档](./sql/syntax.md#create-table-as-select).

以下示例演示了CTAS语法和struct数据类型的用法：

```sql
CREATE TABLE table_name WITH (SCHEMA='schema_name')

AS SELECT '1' as _id,

 STRUCT

  ('2021-02-17T15:39:29.0Z' AS taskActualCompletionDate,

    '2020-09-09T21:21:16.0Z' AS taskActualStartDate,

    'Consulting' AS taskdescription,

    '5f6527c10011e09b89666c52d9a8c564' AS taskguide,

    'Stakeholder Consulting Engagement' AS taskname, 

    '2020-09-09T15:00:00.0Z' AS taskPlannedStartDate,

    '2021-02-15T11:00:00.0Z' AS taskPlannedCompletionDate

  ) AS _workfront ;
```

+++

### 如何快速处理每天进入系统的新数据？

+++回答 [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) 子句可用于基于快照ID增量读取表上的数据。 这非常适合与 [增量负载](./best-practices/incremental-load.md) 设计模式，仅处理自上次加载执行以来创建或修改的数据集中的信息。 因此，它提高了处理效率，并可用于流和批量数据处理。
+++

### 为什么配置文件UI中显示的数字与从配置文件导出数据集计算的数字之间存在差异？

+++回答自上次快照起，配置文件仪表板中显示的数字是准确的。 配置文件导出表中生成的数字完全取决于导出查询。 因此，查询符合特定区段资格的用户档案数量是造成此差异的常见原因。

>[!NOTE]
>
>查询包含历史数据，而UI仅显示当前用户档案数据。

+++

### 为什么我的查询返回了空子集，我该怎么办？

+++答案最可能的原因是您的查询范围太窄。 您应该系统地删除 `WHERE` 子句，直到您开始看到一些数据。

您还可以使用小查询确认数据集包含数据，例如：

```sql
SELECT count(1) FROM myTableName
```

+++

### 我可以采样我的数据吗？

+++回答此功能当前正在进行中。 详情请参阅 [发行说明](../release-notes/latest/latest.md) 以及在该功能准备就绪以供发布后，通过Platform UI对话框。
+++

### 查询服务支持哪些帮助程序函数？

+++应答查询服务提供了多个内置SQL帮助程序函数来扩展SQL功能。 有关 [查询服务支持的SQL函数](./sql/spark-sql-functions.md).
+++

### 都是本地的 [!DNL Spark SQL] 函数受支持或用户仅受包装器限制 [!DNL Spark SQL] Adobe提供的函数？

+++答案至今，并非所有开源 [!DNL Spark SQL] 已在数据湖数据上测试了函数。 测试和确认后，它们将被添加到受支持列表。 请参阅 [受支持列表 [!DNL Spark SQL] 函数](./sql/spark-sql-functions.md) 来检查特定函数。
+++

### 用户能否定义自己的用户定义函数(UDF)，以便在其他查询中使用？

+++回答由于数据安全注意事项，不允许自定义UDF。
+++

### 如果计划查询失败，我应该怎么做？

+++回答：首先，检查日志以查找错误的详细信息。 有关 [在日志中查找错误](#error-logs) 提供了有关如何执行此操作的更多信息。

您还应查看相关文档，以获取有关如何执行操作的指导 [UI中的计划查询](./ui/user-guide.md#scheduled-queries) 通过 [API](./api/scheduled-queries.md).

以下是使用 [!DNL Query Editor]. 它们不适用于 [!DNL Query Service] API:<br/>您只能向已创建、保存和运行的查询添加计划。<br/>您 **无法** 向参数化查询添加计划。<br/>计划查询 **无法** 包含匿名块。<br/>您只能计划 **one** 使用UI查询模板。 如果要向查询模板添加其他计划，则需要使用API。 如果已使用API添加计划，则您将无法使用UI添加其他计划。
+++

### “已达到会话限制”错误是什么意思？

+++回答“已达到会话限制”表示已达到您的组织允许的查询服务会话数上限。 请与贵组织的Adobe Experience Platform管理员联系。
+++

### 查询日志如何处理与已删除数据集相关的查询？

+++应答查询服务从不删除查询历史记录。 这意味着任何引用已删除数据集的查询都将因此返回“无有效数据集”。
+++

### 如何仅获取查询的元数据？

+++回答您可以运行返回零行的查询，以仅获取响应中的元数据。 此示例查询仅返回指定表的元数据。

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### 如何快速地在CTAS(Create Table As Select)查询上进行迭代而不对其进行具体化？

+++答案您可以创建临时表格，以便在将查询实质化以供使用之前，快速对查询进行迭代和实验。 您还可以使用临时表来验证查询是否可正常运行。

例如，您可以创建临时表：

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

然后，您可以按如下方式使用临时表：

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

+++

### 如何将时区从UTC时间戳更改为时区？

+++回答Adobe Experience Platform以UTC（协调的通用时间）时间戳格式保留数据。 UTC格式的示例为 `2021-12-22T19:52:05Z`

查询服务支持内置的SQL函数，以将给定时间戳转换为UTC格式和从UTC格式转换为SQL函数。 和 `to_utc_timestamp()` 和 `from_utc_timestamp()` 方法采用两个参数：时间戳和时区。

| 参数 | 描述 |
|-----------|---------------|
| 时间戳 | 时间戳可以采用UTC格式或简单格式写入 `{year-month-day}` 格式。 如果未提供时间，则默认值为给定日期上午的午夜。 |
| 时区 | 时区以 `{continent/city})` 格式。 它必须是 [公域TZ数据库](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### 转换为UTC时间戳

的 `to_utc_timestamp()` 方法解释给定参数并转换它 **到本地时区的时间戳** UTC格式。 例如，韩国首尔的时区是UTC/GMT +9小时。 通过提供仅限日期的时间戳，方法会使用上午的默认值“午夜”。 时间戳和时区将转换为UTC格式，从该区域的时间转换为本地区域的UTC时间戳。

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

查询在用户的本地时间中返回时间戳。 在这种情况下，首尔会提前9小时，前一天下午3点。

```
2021-08-30 15:00:00
```

再举一个示例，如果给定的时间戳是 `2021-07-14 12:40:00.0` 对于 `Asia/Seoul` 时区，返回的UTC时间戳为 `2021-07-14 03:40:00.0`

查询服务UI中提供的控制台输出是一种更易读的格式：

```
8/30/2021, 3:00 PM
```

#### 从UTC时间戳转换

的 `from_utc_timestamp()` 方法解释给定参数 **从本地时区的时间戳** 和以UTC格式提供所需区域的等效时间戳。 在以下示例中，小时为用户本地时区中的下午2:40。 作为变量传递的首尔时区比本地时区提前九小时。

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

查询会为作为参数传递的时区返回UTC格式的时间戳。 结果会比运行查询的时区早九小时。

```
8/31/2021, 11:40 PM
```

### 如何过滤我的时间序列数据？

+++答案使用时间序列数据进行查询时，应尽可能使用时间戳过滤器，以便进行更准确的分析。

>[!NOTE]
>
> 日期字符串 **必须** 格式 `yyyy-mm-ddTHH24:MM:SS`.

使用时间戳过滤器的示例如下所示：

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### 如何正确使用 `CAST` 运算符来转换SQL查询中的时间戳？

+++使用 `CAST` 运算符来转换时间戳，您需要同时包含这两个日期 **和** 时间。

例如，如下所示，缺少时间组件将导致错误：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

正确使用 `CAST` 运算符如下所示：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### 我是否应使用通配符（如*）从数据集获取所有行？

+++回答您不能使用通配符从行中获取所有数据，因为查询服务应当被视为 **柱状存储** 而不是传统的基于行的存储系统。
+++

### 我应该使用 `NOT IN` ?

+++回答 `NOT IN` 运算符通常用于检索未在其他表或SQL语句中找到的行。 此运算符可能会降低性能，如果正在比较的列接受，则可能会返回意外结果 `NOT NULL`，或者您有大量记录。

而不是使用 `NOT IN`，则可以使用 `NOT EXISTS` 或 `LEFT OUTER JOIN`.

例如，如果您创建了以下表：

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

如果您使用 `NOT EXISTS` 运算符，您可以使用 `NOT IN` 运算符：

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

或者，如果您使用 `LEFT OUTER JOIN` 运算符，您可以使用 `NOT IN` 运算符：

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### 我是否可以使用CTAS查询创建数据集，并使用双下划线名称（如UI中显示的名称）？ 例如：`test_table_001`。

+++答案否，这是跨Experience Platform的有意限制，适用于所有Adobe服务，包括查询服务。 可接受具有两个下划线的名称作为架构和数据集名称，但数据集的表名称只能包含一个下划线。
+++

## 导出数据 {#exporting-data}

本节提供有关导出数据和限制的信息。

### 是否在查询处理后从查询服务中提取数据，并将结果保存为CSV文件？ {#export-csv}

+++回答是。 可以从查询服务中提取数据，还可以选择通过SQL命令以CSV格式存储结果。

使用PSQL客户端时，有两种方法可保存查询结果。 您可以使用 `COPY TO` 命令或使用以下格式创建语句：

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[关于使用 `COPY TO` 命令](./sql/syntax.md#copy) 可在SQL语法参考文档中找到。
+++

### 我是否可以提取通过CTAS查询摄取的最终数据集的内容（假设这些数据是较大量的数据，如TB）？

+++回答否。 目前没有可用于提取摄取数据的功能。
+++

### Analytics数据连接器为何不返回数据？

+++答案此问题的一个常见原因是在没有时间过滤器的情况下查询时间序列数据。 例如：

```sql
SELECT * FROM prod_table LIMIT 1;
```

应写成：

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## 第三方工具 {#third-party-tools}

本节包含有关使用第三方工具(如PSQL和Power BI)的信息。

### 是否可以将查询服务连接到第三方工具？

+++回答是，您可以将多个第三方桌面客户端连接到查询服务。 请参阅相关文档 [有关可用客户端以及如何将它们连接到查询服务的完整详细信息](./clients/overview.md).
+++

### 是否有一种方法可以连接一次查询服务，以便与第三方工具一起持续使用？

+++回答是，第三方桌面客户端可以通过一次性设置未过期的凭据连接到查询服务。 未过期的凭据可由授权用户生成，并以JSON文件的形式接收，该文件会自动下载到其本地计算机。 完整 [有关如何创建和下载未过期的凭据的指导](./ui/credentials.md#non-expiring-credentials) 可在文档中找到。
+++

### 为什么我的未过期凭据不起作用？

+++回答未过期凭据的值是 `technicalAccountID` 和 `credential` 从配置JSON文件中获取。 密码值采用以下形式： `{{technicalAccountId}:{credential}}`.
有关如何 [使用凭据连接外部客户端](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### 我可以连接到查询服务编辑器的第三方SQL编辑器是什么类型？

+++回答任何PSQL或 [!DNL Postgres] 符合客户端规范可连接到查询服务编辑器。 请参阅相关文档 [将客户端连接到查询服务](./clients/overview.md) 以获取可用说明列表。
+++

### 是否可以将Power BI工具连接到查询服务？

+++回答是，您可以将Power BI连接到查询服务。 请参阅相关文档 [有关将Power BI桌面应用程序连接到查询服务的说明](./clients/power-bi.md).
+++

### 连接到查询服务时，功能板为何需要较长时间才能加载？

+++答案当系统连接到查询服务时，它会连接到交互式或批处理引擎。 这可能会导致加载时间较长，从而反映已处理的数据。

如果要缩短功能板的响应时间，您应当实施Business Intelligence(BI)服务器作为查询服务和BI工具之间的缓存层。 通常，大多数BI工具都为服务器提供附加服务。

添加缓存服务器层的目的是缓存来自查询服务的数据，并利用这些数据对功能板来加速响应。 这是可能的，因为每天都会在BI服务器中缓存执行查询的结果。 然后，缓存服务器会向具有相同查询的任何用户提供这些结果，以减少延迟。 有关此设置的说明，请参阅您所使用的实用工具或第三方工具的文档。
+++

### 能否使用pgAdmin连接工具访问查询服务？

+++答案否，不支持pgAdmin连接。 A [可用的第三方客户端列表以及如何将它们连接到查询服务的说明](./clients/overview.md) 可在文档中找到。
+++

## PostgreSQL API错误 {#postgresql-api-errors}

下表提供了PSQL错误代码及其可能的原因。

| 错误代码 | 连接状态 | 描述 | 可能的原因 |
|------------|---------------------------|-------------|----------------|
| **08P01** | 不适用 | 不支持的消息类型 | 不支持的消息类型 |
| **2001年2月28日** | 启动 — 身份验证 | 密码无效 | 身份验证令牌无效 |
| **28000** | 启动 — 身份验证 | 授权类型无效 | 授权类型无效。 必须为 `AuthenticationCleartextPassword`. |
| **42P12** | 启动 — 身份验证 | 未找到表 | 未找到要使用的表 |
| **42601** | 查询 | 语法错误 | 命令或语法错误无效 |
| **42P01** | 查询 | 未找到表 | 在查询中指定的表未找到 |
| **42P07** | 查询 | 表存在 | 已存在同名表（创建表） |
| **53400** | 查询 | LIMIT超出最大值 | 用户指定的LIMIT子句大于100,000 |
| **53400** | 查询 | 语句超时 | 提交的实时声明最多需要10分钟 |
| **58000** | 查询 | 系统错误 | 内部系统故障 |
| **0A000** | 查询/命令 | 不支持 | 查询/命令中的特性/功能不受支持 |
| **42501** | 拖放表查询 | 删除查询服务未创建的表 | 正在删除的表不是由查询服务使用 `CREATE TABLE` 语句 |
| **42501** | 拖放表查询 | 表未由经过身份验证的用户创建 | 正在删除的表不是由当前已登录的用户创建的 |
| **42P01** | 拖放表查询 | 未找到表 | 未找到查询中指定的表 |
| **42P12** | 拖放表查询 | 找不到的表 `dbName`:请检查 `dbName` | 在当前数据库中未找到表 |

### 在我的表上使用history_meta()方法时，为什么我收到58000错误代码？

+++回答 `history_meta()` 方法用于从数据集访问快照。 以前，如果要在Azure数据湖存储(ADLS)的空数据集上运行查询，您将收到一个58000错误代码，指出数据集不存在。 下面显示了旧系统错误的示例。

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

发生此错误是因为查询没有返回值。 此行为现已修复，可返回以下消息：

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## REST API错误 {#rest-api-errors}

下表提供了HTTP错误代码及其可能的原因。

| HTTP状态代码 | 描述 | 可能的原因 |
|------------------|-----------------------|----------------------------|
| 400 | 错误请求 | 查询格式错误或非法 |
| 401 | 身份验证失败 | 身份验证令牌无效 |
| 500 | 内部服务器错误 | 内部系统故障 |
