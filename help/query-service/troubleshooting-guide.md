---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；故障排除指南；faq；故障排除；
solution: Experience Platform
title: 查询服务和数据Distiller常见问题解答
description: 本文档包含与查询服务和数据Distiller相关的常见问题和解答。 主题包括：导出数据、第三方工具和PSQL错误。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: f0656fcde077fc6c983a7a2d8dc21d2548fa7605
workflow-type: tm+mt
source-wordcount: '5186'
ht-degree: 0%

---

# 查询服务和数据Distiller常见问题解答

本文档解答了有关查询服务和数据Distiller的常见问题。 它还包含使用“查询”产品进行数据验证或将转换后的数据写回数据湖时常见的错误代码。 有关其他Adobe Experience Platform服务的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

为了阐明Query Service和Data Distiller如何在Adobe Experience Platform中协同工作，下面是两个基本问题。

## 查询服务与数据Distiller之间的关系是什么？

查询服务和数据Distiller是两个截然不同的互补组件，可提供特定的数据查询功能。 查询服务专门为Ad Hoc查询而设计，用于探索、验证和试验摄取的数据，而无需更改数据湖。 相比之下，Data Distiller侧重于通过批量查询来转换和扩充数据，并将结果存储回数据湖以供将来使用。 Data Distiller中的批量查询可以计划、监控和管理，支持仅查询服务无法实现的更深入的数据处理和操作。

查询服务可共同帮助实现快速见解，而数据Distiller支持深入、持久的数据转换。

## 查询服务与数据Distiller之间有何区别？

**查询服务**：用于侧重于数据探索、验证和试验的SQL查询。 输出不会存储在数据湖中，执行时间限制为10分钟。 临时查询适用于轻量级的交互式数据检查和分析。

**数据Distiller**：启用批处理查询，以处理、清理和扩充数据，并将结果存储回数据湖。 这些查询支持更长的执行（最长24小时）和其他功能，如计划、监控和加速报告。 Data Distiller非常适合进行深入的数据操作和计划的数据处理任务。

有关详细信息，请参阅[查询服务打包文档](./packaging.md)。

## 问题类别 {#categories}

下面的常见问题解答列表分为以下类别：

- [General](#general)
- [数据蒸馏器](#data-distiller)
- [查询Ui](#queries-ui)
- [数据集示例](#dataset-samples)
- [导出数据](#exporting-data)
- [SQL语法](#sql-syntax) 
- [ITAS查询](#itas-queries)
- [第三方工具](#third-party-tools)
- [PostgreSQL API错误](#postgresql-api-errors)
- [REST API错误](#rest-api-errors)

## 一般查询服务问题 {#general}

本节包含有关性能、限制和流程的信息。

### 我可以在查询服务编辑器中关闭自动完成功能吗？

+++回答
不适用。 编辑器当前不支持关闭自动完成功能。
+++

### 为什么在键入查询时，查询编辑器有时运行缓慢？

+++回答
一个潜在的原因是自动完成功能。 该功能会处理某些元数据命令，这些命令有时在查询编辑过程中会降低编辑器的速度。
+++

### 我可以将[!DNL Postman]用于查询服务API吗？

+++回答
可以，您可以使用[!DNL Postman]（免费的第三方应用程序）可视化所有Adobe API服务并与之交互。 请查看[[!DNL Postman] 设置指南](https://video.tv.adobe.com/v/28832)，了解有关如何在Adobe Developer Console中设置项目以及获取用于[!DNL Postman]的所有必要凭据的分步说明。 请参阅官方文档，了解有关启动、运行和共享[收藏集 [!DNL Postman] 的](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/)指南。
+++

### 通过UI从查询返回的最大行数是否存在限制？

+++回答
是，查询服务在内部应用50,000行的限制，除非在外部指定了显式限制。 有关更多详细信息，请参阅有关[交互式查询执行](./best-practices/writing-queries.md#interactive-query-execution)的指南。
+++

### 我可以使用查询来更新行吗？

+++回答
在批处理查询中，不支持更新数据集内的行。
+++

### 查询结果输出是否存在数据大小限制？

+++回答
不适用。 数据大小没有限制，但交互会话的查询超时限制为10分钟。 如果查询作为批量CTAS执行，则10分钟超时不适用。 有关更多详细信息，请参阅有关[交互式查询执行](./best-practices/writing-queries.md#interactive-query-execution)的指南。
+++

### 如何防止查询在10分钟内超时？

+++回答
如果查询超时，建议使用以下一个或多个解决方案。

- [将查询转换为CTAS查询](./sql/syntax.md#create-table-as-select)并计划运行。 可以通过[通过UI](./ui/user-guide.md#scheduled-queries)或[API](./api/scheduled-queries.md#create)计划运行。
- 通过应用额外的[筛选条件](https://spark.apache.org/docs/latest/api/sql/index.html#filter)，对较小的数据区块执行查询。
- [执行EXPLAIN命令](./sql/syntax.md#explain)以收集更多详细信息。
- 查看数据集内数据的统计信息。
- 将查询转换为简化形式，然后使用[准备好的语句](./sql/prepared-statements.md)重新运行。
+++

### 如果同时运行多个查询，是否存在问题或对Query Service性能的影响？

+++回答
不适用。 查询服务具有自动缩放功能，可确保并发查询不会显着影响服务的性能。
+++

### 是否可以将保留的关键字用作列名？

+++回答
某些保留关键字不能用作列名，如`ORDER`、`GROUP BY`、`WHERE`、`DISTINCT`。 如果要使用这些关键字，则必须对这些列进行转义。
+++

### 如何从分层数据集中查找列名称？

+++回答
以下步骤描述了如何通过UI显示数据集的表格视图，包括拼合表单中的所有嵌套字段和列。

- 登录Experience Platform后，在UI的左侧导航中选择&#x200B;**[!UICONTROL 数据集]**&#x200B;以导航到[!UICONTROL 数据集]仪表板。
- 数据集[!UICONTROL 浏览]选项卡打开。 您可以使用搜索栏来优化可用选项。 从显示的列表中选择数据集。

![Experience Platform UI中的数据集仪表板，带有搜索栏和一个突出显示的数据集。](./images/troubleshooting/dataset-selection.png)

- 将显示[!UICONTROL 数据集活动]屏幕。 选择&#x200B;**[!UICONTROL 预览数据集]**&#x200B;以打开XDM架构的对话框和选定数据集中拼合数据的表格视图。 有关更多详细信息，请参阅[预览数据集文档](../catalog/datasets/user-guide.md#preview-a-dataset)

![突出显示预览数据集的数据集仪表板的数据集活动选项卡。](./images/troubleshooting/dataset-preview.png)

- 从架构中选择任意字段以在拼合列中显示其内容。 列的名称显示在页面右侧其内容的上方。 您应该复制此名称以用于查询此数据集。

![平面化数据的XDM架构和表格视图。 嵌套数据集的列名称在UI中突出显示。](./images/troubleshooting/column-name.png)

请参阅文档，了解有关[如何使用查询编辑器或第三方客户端处理嵌套数据结构](./key-concepts/nested-data-structures.md)的完整指南。
+++

### 如何加快对包含数组的数据集的查询速度？

+++回答
若要提高包含数组的数据集上的查询性能，您应在运行时[将数组](https://spark.apache.org/docs/latest/api/sql/index.html#explode)分解为[CTAS查询](./sql/syntax.md#create-table-as-select)，然后进一步探索以找出改进其处理时间的机会。
+++

### 为什么我的CTAS查询仍在处理只有少量行的许多小时后？

+++回答
如果查询在非常小的数据集上花费了很长时间，请联系客户支持。

查询在处理过程中可能卡住的原因有很多。 要确定确切的原因，需要逐案进行深入分析。 [联系Adobe客户支持](#customer-support)以成为此流程。
+++

### 如何联系Adobe客户支持？ {#customer-support}

+++回答
[Adobe帮助页面上提供了Adobe客户支持电话号码的完整列表](https://helpx.adobe.com/ca/contact/phone.html)。 或者，可通过完成以下步骤在线查找帮助：

- 在Web浏览器中导航到[https://www.adobe.com/](https://www.adobe.com/cn)。
- 选择顶部导航栏右侧的&#x200B;**[!UICONTROL 登录]**。

![登录的Adobe网站突出显示。](./images/troubleshooting/adobe-sign-in.png)

- 使用已在Adobe ID许可证中注册的Adobe和密码。
- 从顶部导航栏中选择&#x200B;**[!UICONTROL 帮助和支持]**。

![顶部导航栏下拉菜单（包含帮助和支持、企业支持和联系我们）突出显示。](./images/troubleshooting/help-and-support.png)

此时会出现一个下拉横幅，其中包含[!UICONTROL 帮助和支持]部分。 选择&#x200B;**[!UICONTROL 联系我们]**&#x200B;以打开Adobe客户关怀虚拟助手，或选择&#x200B;**[!UICONTROL 企业支持]**&#x200B;以获得大型组织的专用帮助。
+++

### 如果上一个作业未成功完成，如何实施一系列连续的作业，而不执行后续作业？

+++回答
匿名块功能允许您链接一个或多个按顺序执行的SQL语句。 它们还允许使用例外处理选项。

有关详细信息，请参阅[匿名块文档](./key-concepts/anonymous-block.md)。
+++

### 如何在查询服务中实施自定义归因？

+++回答
有两种方法可以实施自定义归因：

1. 使用现有[Adobe定义的函数](./sql/adobe-defined-functions.md)的组合来确定是否满足用例需求。
1. 如果前面的建议不满足您的使用案例，则您应使用[窗口函数](./sql/adobe-defined-functions.md#window-functions)的组合。 窗口函数查看一个序列中的所有事件。 还允许您查看历史数据，并且可以任意组合使用。
+++

### 能否将我的查询模板化，以便轻松地重复使用？

+++回答
可以，您可以使用预准备语句将查询模板化。 预准备语句可以优化性能并避免重复地重新解析查询。 有关更多详细信息，请参阅[预准备语句文档](./sql/prepared-statements.md)。
+++

### 如何检索查询的错误日志？ {#error-logs}

+++回答
要检索特定查询的错误日志，您必须首先使用查询服务API获取查询日志详细信息。 HTTP响应包含调查查询错误所需的查询ID。

使用GET命令检索多个查询。 有关如何调用API的信息可在[示例API调用文档](./api/queries.md#sample-api-calls)中找到。

从响应中，确定要调查的查询，并使用其`id`值提出另一个GET请求。 可以在[按ID检索查询](./api/queries.md#retrieve-a-query-by-id)中找到完整说明。

成功的响应返回HTTP状态200并包含`errors`数组。 为简短起见，已缩短答复。

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

[查询服务API参考文档](https://www.adobe.io/experience-platform-apis/references/query-service/)提供了有关所有可用端点的详细信息。
+++

### “验证架构时出错”是什么意思？

+++回答
“验证架构时出错”消息意味着系统无法找到架构中的字段。 您应该阅读[在查询服务中组织数据资产](./best-practices/organize-data-assets.md)的最佳实践文档，然后阅读[创建表作为选择文档](./sql/syntax.md#create-table-as-select)。

以下示例演示了CTAS语法和结构数据类型的使用：

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

+++回答
[`SNAPSHOT`](./sql/syntax.md#snapshot-clause)子句可用于基于快照ID增量读取表上的数据。 这非常适合与[增量加载](./key-concepts/incremental-load.md)设计模式一起使用，该模式仅处理自上次加载执行以来创建或修改的数据集中的信息。 因此，它提高了处理效率，并且可用于流式和批量数据处理。
+++

### 为什么在配置文件UI中显示的数字与通过配置文件导出数据集计算的数字之间存在差异？

+++回答
配置文件操控板中显示的数字自上次快照以来是准确的。 配置文件导出表中生成的数字完全取决于导出查询。 因此，查询符合特定受众资格的用户档案数量是造成这种差异的常见原因。

>[!NOTE]
>
>查询包括历史数据，而UI仅显示当前配置文件数据。

+++

### 为什么我的查询返回了空子集？我应该怎么做？

+++回答
最可能的原因是查询的范围太窄。 在开始看到某些数据之前，您应该系统地删除`WHERE`子句的一个部分。

您还可以使用小型查询来确认您的数据集包含数据，例如：

```sql
SELECT count(1) FROM myTableName
```

+++

### 我可以采样我的数据吗？

+++回答
此功能当前正在进行中。 在功能准备发布后，详细信息将在[发行说明](../release-notes/latest/latest.md)中以及通过Experience Platform UI对话框提供。
+++

### 查询服务支持哪些帮助程序函数？

+++回答
查询服务提供多个内置的SQL帮助程序函数以扩展SQL功能。 有关查询服务[支持的](./sql/spark-sql-functions.md)SQL函数的完整列表，请参阅此文档。
+++

### 是否支持所有本机[!DNL Spark SQL]函数，或者用户是否仅限于Adobe提供的包装器[!DNL Spark SQL]函数？

+++回答
迄今为止，尚未在数据湖数据中测试所有开源[!DNL Spark SQL]函数。 经测试和确认后，它们将被添加到受支持列表中。 请参阅支持的[函数的 [!DNL Spark SQL] 列表](./sql/spark-sql-functions.md)以检查特定函数。
+++

### 用户能否定义自己的用户定义函数(UDF)，以便在其他查询中使用？

+++回答
出于数据安全考虑，不允许使用UDF的自定义定义。
+++

### 如果我的计划查询失败，我应该怎么做？

+++回答
首先，检查日志以了解错误的详细信息。 有关[在日志](#error-logs)中查找错误的常见问题解答部分提供了有关如何执行此操作的更多信息。

您还应该查看文档以了解有关如何在UI[中以及通过](./ui/user-guide.md#scheduled-queries)API[执行](./api/scheduled-queries.md)计划查询的指导。

请注意，使用[!DNL Query Editor]时，您只能向已创建并保存的查询添加计划。 这不适用于[!DNL Query Service] API。
+++

### “已达到会话限制”错误是什么意思？

+++回答
“已达到会话限制”表示已达到组织允许的最大查询服务会话数。 请联系贵组织的Adobe Experience Platform管理员。
+++

### 查询日志如何处理与已删除的数据集相关的查询？

+++回答
查询服务从不删除查询历史记录。 这意味着任何引用已删除数据集的查询都会因此返回“无有效数据集”。
+++

### 如何仅获取查询的元数据？

+++回答
您可以运行返回零行的查询，以仅获取响应中的元数据。 此示例查询仅返回指定表的元数据。

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### 如何快速迭代CTAS（创建表作为选择）查询而不将其实体化？

+++回答
您可以创建临时表，以便在具体化查询以供使用之前对其进行快速迭代和试验。 还可以使用临时表来验证查询是否有效。

例如，您可以创建一个临时表：

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

然后可以使用临时表，如下所示：

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

### 如何更改与UTC时间戳之间的时区？

+++回答
Adobe Experience Platform以UTC（协调世界时）时间戳格式保留数据。 UTC格式的示例为`2021-12-22T19:52:05Z`

查询服务支持内置SQL函数，以将给定时间戳转换为UTC格式或从UTC格式转换给定时间戳。 `to_utc_timestamp()`和`from_utc_timestamp()`方法都采用两个参数：时间戳和时区。

| 参数 | 描述 |
|-----------|---------------|
| 时间戳 | 时间戳可以采用UTC格式或简单的`{year-month-day}`格式写入。 如果未提供时间，则默认值为给定日期的凌晨的午夜。 |
| 时区 | 时区以`{continent/city})`格式写入。 它必须是在[公共域TZ数据库](https://data.iana.org/time-zones/tz-link.html#tzdb)中找到的可识别时区代码之一。 |

#### 转换为UTC时间戳

`to_utc_timestamp()`方法解释给定参数并将其&#x200B;**以UTC格式转换为本地时区**&#x200B;的时间戳。 例如，韩国首尔的时区是UTC/GMT +9小时。 通过提供仅用于日期的时间戳，该方法使用上午午夜的默认值。 时间戳和时区会转换为UTC格式，从该区域的时间转换为您本地区域的UTC时间戳。

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

查询会返回以用户的本地时间表示的时间戳。 在这个例子中，前一天下午3点，首尔提前了9个小时。

```
2021-08-30 15:00:00
```

作为另一个示例，如果给定时间戳为`2021-07-14 12:40:00.0`时区的`Asia/Seoul`，则返回的UTC时间戳为`2021-07-14 03:40:00.0`

查询服务UI中提供的控制台输出是更易于用户识别的格式：

```
8/30/2021, 3:00 PM
```

#### 从UTC时间戳转换

`from_utc_timestamp()`方法从本地时区&#x200B;**的时间戳中解释给定参数**，并以UTC格式提供所需区域的等效时间戳。 在下面的示例中，小时是用户本地时区的2:40PM。 作为变量传递的首尔时区比当地时区早九小时。

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

查询会返回作为参数传递的时区的时间戳（UTC格式）。 结果比运行查询的时区早九小时。

```
8/31/2021, 11:40 PM
```

### 如何过滤时间序列数据？

+++回答
在查询时序数据时，应尽可能使用时间戳过滤器以实现更准确的分析。

>[!NOTE]
>
> 日期字符串&#x200B;**必须**&#x200B;的格式为`yyyy-mm-ddTHH24:MM:SS`。

下面显示了使用时间戳过滤器的示例：

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### 如何正确使用`CAST`运算符在SQL查询中转换我的时间戳？

+++回答
使用`CAST`运算符转换时间戳时，需要同时包含日期&#x200B;**和**&#x200B;时间。

例如，缺少时间组件（如下所示）将导致错误：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

`CAST`运算符的正确用法如下所示：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### 是否应使用通配符（如*）获取数据集中的所有行？

+++回答
无法使用通配符获取行中的所有数据，因为查询服务应被视为&#x200B;**列存储**，而不是传统的基于行的存储系统。
+++

### 是否应在SQL查询中使用`NOT IN`？

+++回答
`NOT IN`运算符通常用于检索在另一个表或SQL语句中找不到的行。 此运算符可能会降低性能，如果进行比较的列接受`NOT NULL`，或者您有大量记录，则可能会返回意外结果。

您可以使用`NOT IN`或`NOT EXISTS`，而不是使用`LEFT OUTER JOIN`。

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

如果您使用`NOT EXISTS`运算符，则可以使用以下查询使用`NOT IN`运算符进行复制：

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

或者，如果您使用`LEFT OUTER JOIN`运算符，则可以使用以下查询使用`NOT IN`运算符进行复制：

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### 我是否可以使用CTAS查询创建一个具有双下划线名称（与UI中显示的名称类似）的数据集？ 例如： `test_table_001`。

+++回答
不是，这是跨Experience Platform的有意限制，适用于所有Adobe服务，包括查询服务。 带有两个下划线的名称可以作为架构和数据集名称，但数据集的表名称只能包含单个下划线。
+++

### 一次可以运行多少个并发查询？

+++回答
由于批处理查询作为后端作业运行，因此不存在查询并发限制。 但是，有一个查询超时限制设置为24小时。
+++

### 是否有活动仪表板，您可以在其中查看查询活动和状态？

+++回答
有监控和警报功能来检查查询活动和状态。 有关详细信息，请参阅[查询服务审核日志集成](./data-governance/audit-log-guide.md)和[查询日志](./ui/overview.md#log)文档。
+++

### 是否可以回滚更新？ 例如，如果在将数据写回Experience Platform时发生了错误或某些计算需要重新配置，应如何处理这种情况？

+++回答
目前，我们不支持以这种方式进行回滚或更新。
+++

### 如何在Adobe Experience Platform中优化查询？

+++回答
系统没有索引，因为它不是数据库，但它具有绑定到数据存储的其他优化。 以下选项可用于调整查询：

- 基于时间系列数据的过滤器。
- 已针对结构数据类型优化向下推送。
- 优化了阵列和映射数据类型的成本和内存下推功能。
- 使用快照进行增量处理。
- 持久数据格式。
+++

### 登录是否可以限制为查询服务的某些方面，或者它是“完全或无”解决方案？

+++回答
查询服务是一个“全有或无”的解决方案。 无法提供部分访问权限。
+++

### 我可以限制查询服务可以使用的数据吗？还是它只是访问整个Adobe Experience Platform数据湖？

+++回答
可以，您可以将查询限制为具有只读访问权限的数据集。
+++

### 还有其他哪些选项来限制查询服务可以访问的数据？

+++回答
限制访问的方法有三种。 具体如下：

- 使用SELECT only语句并赋予数据集只读访问权限。 此外，分配管理查询权限。
- 使用SELECT/INSERT/CREATE语句并赋予数据集写入权限。 此外，分配查询管理权限。
- 使用具有上述建议的集成帐户，并分配查询集成权限。

+++

### 查询服务返回数据后，Experience Platform是否可以运行任何检查来确保未返回任何受保护数据？

- 查询服务支持基于属性的访问控制。 您可以在列/叶级别和/或结构级别限制对数据的访问。 请参阅文档，了解有关基于属性的访问控制的更多信息。

### 我可以为与第三方客户端的连接指定SSL模式吗？ 例如，我可以对Power BI使用“verify-full”吗？

+++回答
支持SSL模式。 请参阅[SSL模式文档](./clients/ssl-modes.md)，了解可用不同SSL模式的划分以及它们提供的保护级别。
+++

### 我们是否对来自Power BI客户端的所有连接使用TLS 1.2来查询服务？

+++回答
是的。 传输中的数据始终符合HTTPS标准。 当前支持的版本为TLS1.2。
+++

### 在端口80上建立的连接是否仍使用https？

+++回答
是的，在端口80上建立的连接仍使用SSL。 您也可以使用端口5432。
+++

### 我是否可以控制对特定连接的特定数据集和列的访问？ 这是如何配置的？

+++回答
是，如果进行了配置，将强制执行基于属性的访问控制。 有关详细信息，请参阅[基于属性的访问控制概述](../access-control/abac/overview.md)。
+++

### 查询服务是否支持“INSERT OVERWRITE INTO”命令？

+++回答
否，查询服务不支持“INSERT OVERWRITE INTO”命令。
+++

### 许可证使用情况仪表板上的使用情况数据多久更新一次数据Distiller计算小时数？

+++回答
Data Distiller计算机小时的许可证使用情况仪表板每天更新四次，每六小时更新一次。
+++

### 我是否可以在没有Data Distiller访问权限的情况下使用CREATE VIEW命令？

+++回答
可以，您可以使用不具有Data Distiller访问权限的`CREATE VIEW`命令。 此命令提供数据的逻辑视图，但不会将其写回数据湖。
+++

### 能否在DbVisualizer中使用匿名块？

+++回答
是的。 但是，某些第三方客户端（如DbVisualizer）在SQL块之前和之后可能需要单独的标识符来指示脚本的一部分应作为单个语句处理。 可在[匿名块文档](./key-concepts/anonymous-block.md)或[官方的DbVisualizer文档](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsinganSQLDialect)中找到更多详细信息。
+++

## 数据蒸馏器 {#data-distiller}

### 如何跟踪Data Distiller的许可证使用情况？可在何处查看此信息？

+++回答\
用于跟踪批次查询使用情况的主要量度是计算小时。 您可以通过[许可证使用情况仪表板](../dashboards/guides/license-usage.md)访问此信息和当前使用情况。
+++

### 什么是计算小时？

+++回答\
计算小时数是衡量在执行批量查询时，查询服务引擎读取、处理数据并将其写回数据湖所花费的时间。
+++

### 如何测量计算小时数？

+++回答\
计算小时数是在所有授权的沙盒中累计测量的。
+++

### 即使连续运行同一查询，为什么有时会注意到计算小时使用量存在差异？

+++回答\
查询的计算小时数可能因多种因素而波动。 其中包括处理的数据量、SQL查询中转换操作的复杂性等。 查询服务会根据每个查询的上述参数缩放聚类，这可能会导致计算小时数存在差异。
+++

### 如果我长时间使用相同数据运行相同的查询，会注意到计算小时数减少吗？ 为什么会出现这种情况？

+++回答\
后端基础架构不断改进，以优化计算小时利用率和处理时间。 因此，随着性能的增强，您可能会注意到随着时间的推移而发生变化。
+++

### Data Distiller在开发沙盒和生产沙盒之间的性能是否存在差异？

+++回答
在开发沙盒和生产沙盒中运行查询时，您可能会获得类似的性能。 两个环境都旨在提供相同级别的处理能力。 但是，根据运行查询时处理的数据量和整体系统活动，可能会出现计算小时数方面的差异。

在Experience Platform UI的[许可证使用情况仪表板](../dashboards/guides/license-usage.md)中跟踪您的计算小时使用情况。
+++

## 查询Ui

### 尝试连接到查询服务时，“创建查询”卡住“正在初始化连接……”。 如何修复此问题？

+++回答
如果“创建查询”卡在“正在初始化连接……”上，则可能是连接或会话问题。 如果您使用的是Experience Platform UI，请刷新浏览器并重试。
+++

## 数据集示例

### 是否可以在系统数据集中创建示例？

+++回答
不适用。 系统数据集的写入权限受到限制，因此无法创建示例。
+++

## 导出数据 {#exporting-data}

本节提供有关导出数据和限制的信息。

### 是否有办法在查询处理后从查询服务中提取数据，并将结果保存在CSV文件中？ {#export-csv}

+++回答
是的。 数据可以从查询服务中提取，并且还可以选择通过SQL命令以CSV格式存储结果。

使用PSQL客户端时，有两种方式可保存查询结果。 您可以使用`COPY TO`命令或使用以下格式创建语句：

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[有关使用`COPY TO`命令的指导](./sql/syntax.md#copy)可以在SQL语法参考文档中找到。
+++

### 我是否可以提取通过CTAS查询摄取的最终数据集的内容（假设这些是大量数据，例如TB）？

+++回答
不适用。 当前没有可用于提取已摄取数据的功能。
+++

### 为什么Analytics Data Connector不返回数据？

+++回答
此问题的常见原因是查询时间序列数据时没有时间过滤器。 例如：

```sql
SELECT * FROM prod_table LIMIT 1;
```

应写为：

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## SQL语法

### Data Distiller或查询服务是否支持MERGE INTO？

+++回答
Data Distiller或查询服务不支持MERGE INTO SQL构造。
+++

## ITAS查询 {#itas-queries}

### 什么是ITAS查询？

+++回答
INSERT INTO查询称为ITAS查询。 请注意，CREATE TABLE查询称为CTAS查询。
+++

### 查询服务是否支持更新和删除操作？

+++回答
否，查询服务不支持更新或删除操作。 它仅支持使用ITAS的仅附加操作。
+++

## 第三方工具 {#third-party-tools}

本节包含有关使用PSQL和Power BI等第三方工具的信息。

### 是否可以将查询服务连接到第三方工具？

+++回答
可以，您可以将多个第三方桌面客户端连接到查询服务。 请参阅文档，了解[有关可用客户端以及如何将它们连接到查询服务](./clients/overview.md)的完整详细信息。
+++

### 是否有办法连接一次查询服务以与第三方工具一起连续使用？

+++回答
可以，可以通过一次性设置不过期凭据将第三方桌面客户端连接到查询服务。 未过期的凭据可由授权用户生成，并在自动下载到其本地计算机的JSON文件中接收。 在文档中可找到有关如何创建和下载未过期凭据[的完整](./ui/credentials.md#non-expiring-credentials)指南。
+++

### 为什么我的未过期凭据不起作用？

+++回答
未过期凭据的值是来自`technicalAccountID`的拼接参数以及来自配置JSON文件的`credential`的拼接参数。 密码值采用以下形式： `{{technicalAccountId}:{credential}}`。
请参阅文档以了解有关如何[使用凭据](./ui/credentials.md#using-credentials-to-connect-to-external-clients)连接到外部客户端的详细信息。
+++

### 对于未过期的凭据密码的特殊字符是否有任何限制？

+++回答
是的。 为未过期的凭据设置密码时，必须至少包含一个数字、一个小写字母、一个大写字母和一个特殊字符。 不支持美元符号($)。 请改用特殊字符，如！、@、#、^或&amp;。
+++

### 哪种第三方SQL编辑器可以连接到查询服务编辑器？

+++回答
任何与PSQL或[!DNL Postgres]客户端兼容的第三方SQL编辑器都可以连接到查询服务编辑器。 有关可用说明的列表，请参阅有关[将客户端连接到查询服务](./clients/overview.md)的文档。
+++

### 能否将Power BI工具连接到查询服务？

+++回答
是，您可以将Power BI连接到查询服务。 有关将Power BI桌面应用程序连接到查询服务[的说明，请参阅文档](./clients/power-bi.md)。
+++

### 连接到查询服务时，为何需要很长时间才能加载功能板？

+++回答
当系统连接到查询服务时，它会连接到交互式或批处理引擎。 这可能会导致加载时间较长以反映处理过的数据。

如果要缩短功能板的响应时间，应实施Business Intelligence (BI)服务器作为查询服务和BI工具之间的缓存层。 通常，大多数BI工具都为服务器提供了附加服务。

添加缓存服务器层的目的是缓存来自查询服务的数据，并利用该缓存服务让仪表板加快响应。 这是可能的，因为执行的查询的结果每天都会缓存在BI服务器中。 然后，缓存服务器会为具有相同查询的任何用户提供这些结果，以减少延迟。 有关此类设置的说明，请参阅您所使用的实用程序或第三方工具的文档。
+++

### 是否可以使用pgAdmin连接工具访问查询服务？

+++回答
否，不支持pgAdmin连接。 在文档中可以找到[可用第三方客户端列表以及如何将它们连接到查询服务](./clients/overview.md)的说明。
+++

## PostgreSQL API错误 {#postgresql-api-errors}

下表提供了PSQL错误代码及其可能的原因。

| 错误代码 | 连接状态 | 描述 | 可能的原因 |
|------------|---------------------------|-------------|----------------|
| **08P01** | 不适用 | 不支持的消息类型 | 不支持的消息类型 |
| **28P01** | 启动 — 身份验证 | 密码无效 | 身份验证令牌无效 |
| **28000** | 启动 — 身份验证 | 授权类型无效 | 授权类型无效。 必须为`AuthenticationCleartextPassword`。 |
| **42P12** | 启动 — 身份验证 | 未找到表 | 未找到要使用的表 |
| **42601** | 查询 | 语法错误 | 无效命令或语法错误 |
| **42P01** | 查询 | 未找到表 | 找不到查询中指定的表 |
| **42P07** | 查询 | 表存在 | 具有相同名称的表已存在(CREATE TABLE) |
| **53400** | 查询 | 限制超出最大值 | 用户指定了高于100,000的LIMIT子句 |
| **53400** | 查询 | 语句超时 | 提交实时语句所花费的时间超过了10分钟的最大值 |
| **58000** | 查询 | 系统错误 | 内部系统故障 |
| **0A000** | 查询/命令 | 不受支持 | 不支持查询/命令中的特性/功能 |
| **42501** | DROP TABLE查询 | 正在删除不是由查询服务创建的表 | 查询服务未使用`CREATE TABLE`语句创建要删除的表 |
| **42501** | DROP TABLE查询 | 表不是由经过身份验证的用户创建的 | 当前正在删除的表不是由当前登录的用户创建的 |
| **42P01** | DROP TABLE查询 | 未找到表 | 找不到查询中指定的表 |
| **42P12** | DROP TABLE查询 | 找不到`dbName`的表：请检查`dbName` | 在当前数据库中未找到表 |

### 为什么在表上使用history_meta()方法时会收到58000错误代码？

+++回答
`history_meta()`方法用于访问数据集中的快照。 以前，如果您对Azure Data Lake Storage (ADLS)中的空数据集运行查询，您将收到一个58000错误代码，指出该数据集不存在。 下面显示了旧系统错误的示例。

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

出现此错误是因为查询没有返回值。 此行为现已修复为返回以下消息：

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## REST API错误 {#rest-api-errors}

下表提供了HTTP错误代码及其可能的原因。

| HTTP状态代码 | 描述 | 可能的原因 |
|------------------|-----------------------|----------------------------|
| 400 | 请求无效 | 查询格式不正确或非法 |
| 401 | 身份验证失败 | 身份验证令牌无效 |
| 500 | 内部服务器错误 | 内部系统故障 |
