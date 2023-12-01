---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；故障排除指南；faq；故障排除；
solution: Experience Platform
title: 常见问题
description: 本文档包含与查询服务相关的常见问题和解答。 主题包括：导出数据、第三方工具和PSQL错误。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 006b693c71cd45408bccb7c051f367f140260370
workflow-type: tm+mt
source-wordcount: '4450'
ht-degree: 1%

---

# 常见问题解答

本文档提供有关查询服务的常见问题解答，并提供使用查询服务时常见错误代码的列表。 有关Adobe Experience Platform中其他服务的问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

下面的常见问题解答列表分为以下类别：

- [General](#general)
- [导出数据](#exporting-data)
- [第三方工具](#third-party-tools)
- [PostgreSQL API错误](#postgresql-api-errors)
- [REST API错误](#rest-api-errors)

## 一般查询服务问题 {#general}

本节包含有关性能、限制和流程的信息。

### 我可以在查询服务编辑器中关闭自动完成功能吗？

+++答案否。 编辑器当前不支持关闭自动完成功能。
+++

### 为什么在键入查询时，查询编辑器有时运行缓慢？

+++答案一个潜在原因是自动完成功能。 该功能会处理某些元数据命令，这些命令有时在查询编辑过程中会降低编辑器的速度。
+++

### 我可以使用 [!DNL Postman] 查询服务API的？

+++回答是，您可以使用可视化图表并与所有AdobeAPI服务交互 [!DNL Postman] （第三方免费申请）。 观看 [[!DNL Postman] 安装指南](https://video.tv.adobe.com/v/28832) 有关如何在Adobe Developer控制台中设置项目并获取与一起使用的所有必要凭据的分步说明 [!DNL Postman]. 请参阅官方文档 [关于启动、运行和共享的指南 [!DNL Postman] 收藏集](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### 通过UI从查询返回的最大行数是否存在限制？

+++回答是，查询服务在内部应用50,000行的限制，除非在外部指定了明确限制。 请参阅以下指南 [交互式查询执行](./best-practices/writing-queries.md#interactive-query-execution) 以了解更多详细信息。
+++

### 我可以使用查询来更新行吗？

+++答案在批处理查询中，不支持更新数据集中的行。
+++

### 查询结果输出是否存在数据大小限制？

+++答案否。 数据大小没有限制，但交互会话的查询超时限制为10分钟。 如果查询作为批量CTAS执行，则10分钟超时不适用。 请参阅以下指南 [交互式查询执行](./best-practices/writing-queries.md#interactive-query-execution) 以了解更多详细信息。
+++

### 如何绕过对SELECT查询输出行数的限制？

+++答案要绕过输出行限制，请在查询中应用“LIMIT 0”。 例如：

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### 如何防止查询在10分钟内超时？

+++答案如果查询超时，建议使用以下一个或多个解决方案。

- [将查询转换为CTAS查询](./sql/syntax.md#create-table-as-select) 并安排运行。 可以执行以下任一操作来计划运行 [通过UI](./ui/user-guide.md#scheduled-queries) 或 [API](./api/scheduled-queries.md#create).
- 通过应用其他语句在较小的数据块上执行查询 [筛选条件](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [执行EXPLAIN命令](./sql/syntax.md#explain) 以收集更多详细信息。
- 查看数据集内数据的统计信息。
- 将查询转换为简化表单，然后使用以下方式重新运行 [预准备语句](./sql/prepared-statements.md).
+++

### 如果同时运行多个查询，是否存在问题或对Query Service性能的影响？

+++答案否。 查询服务具有自动缩放功能，可确保并发查询不会显着影响服务的性能。
+++

### 是否可以将保留的关键字用作列名？

+++答案某些保留的关键字不能用作列名，例如， `ORDER`， `GROUP BY`， `WHERE`， `DISTINCT`. 如果要使用这些关键字，则必须对这些列进行转义。
+++

### 如何从分层数据集中查找列名称？

+++回答以下步骤描述了如何通过UI显示数据集的表格视图，包括拼合表单中的所有嵌套字段和列。

- 登录Experience Platform后，选择 **[!UICONTROL 数据集]** 在UI的左侧导航中导航到 [!UICONTROL 数据集] 仪表板。
- 数据集 [!UICONTROL 浏览] 选项卡打开。 您可以使用搜索栏来优化可用选项。 从显示的列表中选择数据集。

![Platform UI中的“数据集”功能板，其中搜索栏和数据集突出显示。](./images/troubleshooting/dataset-selection.png)

- 此 [!UICONTROL 数据集活动] 屏幕。 选择 **[!UICONTROL 预览数据集]** 打开XDM架构的对话框以及选定数据集中拼合数据的表格视图。 欲知更多详情，请参阅 [预览数据集文档](../catalog/datasets/user-guide.md#preview-a-dataset)

![突出显示预览数据集的数据集功能板的数据集活动选项卡。](./images/troubleshooting/dataset-preview.png)

- 从架构中选择任意字段以在拼合列中显示其内容。 列的名称显示在页面右侧其内容的上方。 您应该复制此名称以用于查询此数据集。

![平面化数据的XDM架构和表格视图。 嵌套数据集的列名称在UI中突出显示。](./images/troubleshooting/column-name.png)

有关以下内容的完整指导，请参阅文档： [如何使用嵌套数据结构](./key-concepts/nested-data-structures.md) 使用查询编辑器或第三方客户端。
+++

### 如何加快对包含数组的数据集的查询速度？

+++答案要改进对包含数组的数据集的查询性能，您应： [分解阵列](https://spark.apache.org/docs/latest/api/sql/index.html#explode) as a [CTAS查询](./sql/syntax.md#create-table-as-select) 运行时间，然后探索它以进一步改善其处理时间的机会。
+++

### 为什么我的CTAS查询仍在处理只有少量行的许多小时后？

+++答案如果查询在非常小的数据集上花费了很长时间，请联系客户支持。

查询在处理过程中可能卡住的原因有很多。 要确定确切的原因，需要逐案进行深入分析。 [联系Adobe客户支持](#customer-support) 成为这个过程。
+++

### 如何联系Adobe客户支持？ {#customer-support}

+++回答
[Adobe客户支持电话号码的完整列表](https://helpx.adobe.com/ca/contact/phone.html) 可在Adobe帮助页面上找到。 或者，可通过完成以下步骤在线查找帮助：

- 导航到 [https://www.adobe.com/](https://www.adobe.com/cn/) 在您的Web浏览器中。
- 在顶部导航栏的右侧，选择 **[!UICONTROL 登录]**.

![突出显示登录的Adobe网站。](./images/troubleshooting/adobe-sign-in.png)

- 使用已在您的Adobe许可证中注册的Adobe ID和密码。
- 选择 **[!UICONTROL 帮助与支持]** 从顶部导航栏中。

![顶部导航栏下拉菜单（包含帮助和支持、企业支持和联系我们）突出显示。](./images/troubleshooting/help-and-support.png)

此时将显示一个下拉横幅，其中包含 [!UICONTROL 帮助和支持] 部分。 选择 **[!UICONTROL 联系我们]** 打开Adobe客户关怀虚拟助手，或选择 **[!UICONTROL 企业支持]** 为大型组织提供专门帮助。
+++

### 如果上一个作业未成功完成，如何实施一系列连续的作业，而不执行后续作业？

+++回答匿名块功能允许您链接一个或多个按顺序执行的SQL语句。 它们还允许使用例外处理选项。

请参阅 [匿名块文档](./key-concepts/anonymous-block.md) 以了解更多详细信息。
+++

### 如何在查询服务中实施自定义归因？

+++答案实施自定义归因的方法有两种：

1. 使用现有组合 [Adobe定义的函数](./sql/adobe-defined-functions.md) 以确定是否满足用例需求。
1. 如果前面的建议无法满足您的用例，则您应使用以下组合 [窗口函数](./sql/adobe-defined-functions.md#window-functions). 窗口函数查看一个序列中的所有事件。 还允许您查看历史数据，并且可以任意组合使用。
+++

### 能否将我的查询模板化，以便轻松地重复使用？

+++回答是，您可以使用预准备语句将查询模板化。 预准备语句可以优化性能并避免重复地重新解析查询。 请参阅 [预准备语句文档](./sql/prepared-statements.md) 以了解更多详细信息。
+++

### 如何检索查询的错误日志？ {#error-logs}

+++答案要检索特定查询的错误日志，您必须首先使用查询服务API获取查询日志详细信息。 HTTP响应包含调查查询错误所需的查询ID。

使用GET命令检索多个查询。 有关如何调用API的信息，请参阅 [示例API调用文档](./api/queries.md#sample-api-calls).

在响应中，确定要调查的查询，并使用其发出另一个GET请求 `id` 值。 有关完整说明，请参见 [按ID检索查询文档](./api/queries.md#retrieve-a-query-by-id).

成功的响应返回HTTP状态200，并包含 `errors` 数组。 为简短起见，已缩短答复。

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

此 [查询服务API参考文档](https://www.adobe.io/experience-platform-apis/references/query-service/) 提供了有关所有可用端点的更多信息。
+++

### “验证架构时出错”是什么意思？

+++回答“验证架构时出错”消息意味着系统无法找到架构中的字段。 您应该阅读以下内容的最佳实践文档： [在查询服务中组织数据资产](./best-practices/organize-data-assets.md) 后面是 [创建表作为Select文档](./sql/syntax.md#create-table-as-select).

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

+++回答 [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) 子句可用于基于快照ID增量读取表中的数据。 这非常适用于与 [增量加载](./key-concepts/incremental-load.md) 设计模式，仅处理自上次加载执行以来创建或修改的数据集中的信息。 因此，它提高了处理效率，并且可用于流式和批量数据处理。
+++

### 为什么在配置文件UI中显示的数字与通过配置文件导出数据集计算的数字之间存在差异？

+++回答配置文件仪表板中显示的数字自上次快照以来是准确的。 配置文件导出表中生成的数字完全取决于导出查询。 因此，查询符合特定受众资格的用户档案数量是造成这种差异的常见原因。

>[!NOTE]
>
>查询包括历史数据，而UI仅显示当前配置文件数据。

+++

### 为什么我的查询返回了空子集？我应该怎么做？

+++答案最可能的原因是您的查询范围太窄。 您应系统地删除 `WHERE` 子句，直到您开始看到某些数据。

您还可以使用小型查询来确认您的数据集包含数据，例如：

```sql
SELECT count(1) FROM myTableName
```

+++

### 我可以采样我的数据吗？

+++答案此功能当前正在进行中。 详情请见 [发行说明](../release-notes/latest/latest.md) 并在功能准备发布后通过Platform UI对话框发布。
+++

### 查询服务支持哪些帮助程序函数？

+++应答查询服务提供多个内置的SQL帮助程序函数以扩展SQL功能。 请参阅文档，以获取 [查询服务支持的SQL函数](./sql/spark-sql-functions.md).
+++

### 全部为本机 [!DNL Spark SQL] 函数受支持或用户受限于仅包装器 [!DNL Spark SQL] 功能由Adobe提供？

+++尚未回答，并非所有都是开放源代码 [!DNL Spark SQL] 函数已在Data Lake数据上进行了测试。 经测试和确认后，它们将被添加到受支持列表中。 请参阅 [支持的列表 [!DNL Spark SQL] 函数](./sql/spark-sql-functions.md) 以检查特定功能。
+++

### 用户能否定义自己的用户定义函数(UDF)，以便在其他查询中使用？

+++答案出于数据安全考虑，不允许使用UDF的自定义定义。
+++

### 如果我的计划查询失败，我应该怎么做？

+++请先回答，检查日志以了解错误的详细信息。 上的常见问题解答部分 [在日志中查找错误](#error-logs) 提供了有关如何执行此操作的更多信息。

您还应该查看文档以获得有关如何执行的指导 [UI中的计划查询](./ui/user-guide.md#scheduled-queries) 和至 [API](./api/scheduled-queries.md).

请注意，在使用时 [!DNL Query Editor] 您只能向已创建、保存和运行的查询添加计划。 这不适用于 [!DNL Query Service] API。
+++

### “已达到会话限制”错误是什么意思？

+++回答“已达到会话限制”表示已达到组织允许的最大查询服务会话数。 请联系贵组织的Adobe Experience Platform管理员。
+++

### 查询日志如何处理与已删除的数据集相关的查询？

+++应答查询服务从不删除查询历史记录。 这意味着任何引用已删除数据集的查询都会因此返回“无有效数据集”。
+++

### 如何仅获取查询的元数据？

+++回答您可以运行返回零行的查询，以仅获取响应的元数据。 此示例查询仅返回指定表的元数据。

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### 如何快速迭代CTAS（创建表作为选择）查询而不将其实体化？

+++答案您可以创建临时表，以便在具体化查询以供使用之前对其进行快速迭代和试验。 还可以使用临时表来验证查询是否有效。

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

+++回答Adobe Experience Platform会以UTC（协调世界时）时间戳格式保留数据。 UTC格式的一个示例是 `2021-12-22T19:52:05Z`

查询服务支持内置SQL函数，以将给定时间戳转换为UTC格式或从UTC格式转换给定时间戳。 两者都是 `to_utc_timestamp()` 和 `from_utc_timestamp()` 方法采用两个参数：时间戳和时区。

| 参数 | 描述 |
|-----------|---------------|
| 时间戳 | 时间戳可以采用UTC格式或简单格式写入 `{year-month-day}` 格式。 如果未提供时间，则默认值为给定日期的凌晨的午夜。 |
| 时区 | 时区采用 `{continent/city})` 格式。 它必须是中认可的其中一个时区代码 [公共域TZ数据库](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### 转换为UTC时间戳

此 `to_utc_timestamp()` 方法解释给定参数并对其进行转换 **到您的本地时区的时间戳** UTC格式。 例如，韩国首尔的时区是UTC/GMT +9小时。 通过提供仅用于日期的时间戳，该方法使用上午午夜的默认值。 时间戳和时区会转换为UTC格式，从该区域的时间转换为您本地区域的UTC时间戳。

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

查询会返回以用户的本地时间表示的时间戳。 在这个例子中，前一天下午3点，首尔提前了9个小时。

```
2021-08-30 15:00:00
```

作为另一个示例，如果给定的时间戳为 `2021-07-14 12:40:00.0` 对于 `Asia/Seoul` 时区，返回的UTC时间戳将为 `2021-07-14 03:40:00.0`

查询服务UI中提供的控制台输出是更易于用户识别的格式：

```
8/30/2021, 3:00 PM
```

#### 从UTC时间戳转换

此 `from_utc_timestamp()` 方法解释给定的参数 **根据本地时区的时间戳** 和以UTC格式提供所需区域的等效时间戳。 在下面的示例中，小时是用户本地时区的下午2:40。 作为变量传递的首尔时区比当地时区早九小时。

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

查询会返回作为参数传递的时区的时间戳（UTC格式）。 结果比运行查询的时区早九小时。

```
8/31/2021, 11:40 PM
```

### 如何过滤时间序列数据？

+++回答使用时间序列数据进行查询时，应尽可能使用时间戳过滤器进行更准确的分析。

>[!NOTE]
>
> 日期字符串 **必须** 采用格式 `yyyy-mm-ddTHH24:MM:SS`.

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

### 如何正确使用 `CAST` 运算符，以在SQL查询中转换我的时间戳？

+++使用时回答 `CAST` 运算符要转换时间戳，您需要包含这两个日期 **和** 时间。

例如，缺少时间组件（如下所示）将导致错误：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

正确使用的 `CAST` 运算符如下所示：

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### 是否应使用通配符（如*）获取数据集中的所有行？

+++回答您无法使用通配符获取行中的所有数据，因为查询服务应被视为 **柱形存储** 而不是传统的基于行的存储系统。
+++

### 我应该使用 `NOT IN` 在我的SQL查询中？

+++回答 `NOT IN` 运算符通常用于检索在另一个表或SQL语句中找不到的行。 此运算符可能会降低性能，如果进行比较的列接受，则可能会返回意外结果 `NOT NULL`，或者您有大量记录。

不要使用 `NOT IN`，您可以使用以下任一选项 `NOT EXISTS` 或 `LEFT OUTER JOIN`.

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

如果您使用 `NOT EXISTS` 运算符，您可以使用以下对象进行复制 `NOT IN` 运算符：

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

或者，如果您使用 `LEFT OUTER JOIN` 运算符，您可以使用以下对象进行复制 `NOT IN` 运算符：

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### 我是否可以使用CTAS查询创建一个具有双下划线名称（与UI中显示的名称类似）的数据集？ 例如：`test_table_001`。

+++答案否，这是跨Experience Platform的有意限制，适用于所有Adobe服务，包括查询服务。 带有两个下划线的名称可以作为架构和数据集名称，但数据集的表名称只能包含单个下划线。
+++

### 一次可以运行多少个并发查询？

+++答案当批处理查询作为后端作业运行时，查询并发性没有限制。 但是，有一个查询超时限制设置为24小时。
+++

### 是否有活动仪表板，您可以在其中查看查询活动和状态？

+++答案提供监控和警报功能，以检查查询活动和状态。 请参阅 [查询服务审核日志集成](./data-governance/audit-log-guide.md) 和 [查询日志](./ui/overview.md#log) 文档，以了解更多信息。
+++

### 是否可以回滚更新？ 例如，如果在将数据写回Platform时发生了错误或某些计算需要重新配置，应如何处理这种情况？

+++回答目前，我们不支持以这种方式进行回滚或更新。
+++

### 如何在Adobe Experience Platform中优化查询？

+++回答系统没有索引，因为它不是数据库，但它有与数据存储绑定的其他优化功能。 以下选项可用于调整查询：

- 基于时间系列数据的过滤器。
- 已针对结构数据类型优化向下推送。
- 优化了阵列和映射数据类型的成本和内存下推功能。
- 使用快照进行增量处理。
- 持久数据格式。
+++

### 登录是否可以限制为查询服务的某些方面，或者它是“完全或无”解决方案？

+++应答查询服务是一种“要么全部，要么一无所有”的解决方案。 无法提供部分访问权限。
+++

### 我可以限制查询服务可以使用的数据吗？还是它只是访问整个Adobe Experience Platform数据湖？

+++回答是，您可以将查询限制为具有只读访问权限的数据集。
+++

### 还有其他哪些选项来限制查询服务可以访问的数据？

+++回答：限制访问有三种方法。 具体如下：

- 使用SELECT only语句并赋予数据集只读访问权限。 此外，分配管理查询权限。
- 使用SELECT/INSERT/CREATE语句并赋予数据集写入权限。 此外，分配查询管理权限。
- 使用具有上述建议的集成帐户，并分配查询集成权限。

+++

### 查询服务返回数据后，Platform是否能够运行任何检查来确保未返回任何受保护的数据？

- 查询服务支持基于属性的访问控制。 您可以在列/叶级别和/或结构级别限制对数据的访问。 请参阅文档，了解有关基于属性的访问控制的更多信息。

### 我可以为与第三方客户端的连接指定SSL模式吗？ 例如，我可以对Power BI使用“verify-full”吗？

+++回答是，支持SSL模式。 请参阅 [SSL模式文档](./clients/ssl-modes.md) 提供了不同SSL模式的划分以及它们提供的保护级别。
+++

### 我们是否对从Power BI客户端到查询服务的所有连接使用TLS 1.2？

+++回答是。 传输中的数据始终符合HTTPS标准。 当前支持的版本为TLS1.2。
+++

### 在端口80上建立的连接是否仍使用https？

+++回答是，在端口80上建立的连接仍使用SSL。 您也可以使用端口5432。
+++

### 我是否可以控制对特定连接的特定数据集和列的访问？ 这是如何配置的？

+++答案是，如果进行了配置，将强制执行基于属性的访问控制。 请参阅 [基于属性的访问控制概述](../access-control/abac/overview.md) 以了解更多信息。
+++

### 查询服务是否支持“INSERT OVERWRITE INTO”命令？

+++答案否，查询服务不支持“INSERT OVERWRITE INTO”命令。
+++

### 许可证使用情况仪表板上的使用情况数据多久更新一次数据Distiller计算小时数？

+++应答数据Distiller计算机的许可证使用情况仪表板每天更新四次，每六小时更新一次。
+++

### 我是否可以在没有Data Distiller访问权限的情况下使用CREATE VIEW命令？

+++回答是，您可以使用 `CREATE VIEW` 命令而没有访问Data Distiller。 此命令提供数据的逻辑视图，但不会将其写回数据湖。
+++

### 能否在DbVisualizer中使用匿名块？

+++回答是。 但是，某些第三方客户端（如DbVisualizer）在SQL块之前和之后可能需要单独的标识符来指示脚本的一部分应作为单个语句处理。 欲知更多详情，请参阅 [匿名块文档](./key-concepts/anonymous-block.md) 或 [DbVisualizer官方文档](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsinganSQLDialect).
+++

## 导出数据 {#exporting-data}

本节提供有关导出数据和限制的信息。

### 是否有办法在查询处理后从查询服务中提取数据，并将结果保存在CSV文件中？ {#export-csv}

+++回答是。 数据可以从查询服务中提取，并且还可以选择通过SQL命令以CSV格式存储结果。

使用PSQL客户端时，有两种方式可保存查询结果。 您可以使用 `COPY TO` 命令或使用以下格式创建语句：

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[使用指南 `COPY TO` 命令](./sql/syntax.md#copy) 可以在SQL语法参考文档中找到它们。
+++

### 我是否可以提取通过CTAS查询摄取的最终数据集的内容（假设这些是大量数据，例如TB）？

+++答案否。 当前没有可用于提取已摄取数据的功能。
+++

### 为什么Analytics Data Connector不返回数据？

+++答案此问题的一个常见原因是查询不带时间过滤器的时序数据。 例如：

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

## 第三方工具 {#third-party-tools}

本节包含有关使用PSQL和Power BI等第三方工具的信息。

### 是否可以将查询服务连接到第三方工具？

+++回答是，您可以将多个第三方桌面客户端连接到查询服务。 请参阅相关文档 [有关可用客户端以及如何将其连接到查询服务的完整详细信息](./clients/overview.md).
+++

### 是否有办法连接一次查询服务以与第三方工具一起连续使用？

+++回答是，可以通过一次性设置不过期凭据将第三方桌面客户端连接到查询服务。 未过期的凭据可由授权用户生成，并在自动下载到其本地计算机的JSON文件中接收。 完整 [有关如何创建和下载未过期的凭据的指南](./ui/credentials.md#non-expiring-credentials) 可以在文档中找到。
+++

### 为什么我的未过期凭据不起作用？

+++回答未过期的凭据的值是以下凭证中的连接参数： `technicalAccountID` 和 `credential` 取自配置JSON文件。 密码值采用以下形式： `{{technicalAccountId}:{credential}}`.
有关如何执行操作的更多信息，请参阅文档 [使用凭据连接到外部客户端](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### 哪种第三方SQL编辑器可以连接到查询服务编辑器？

+++应答任何是PSQL或的第三方SQL编辑器 [!DNL Postgres] 客户端兼容可以连接到查询服务编辑器。 请参阅相关文档 [将客户端连接到查询服务](./clients/overview.md) 以获取可用说明的列表。
+++

### 能否将Power BI工具连接到查询服务？

+++回答是，您可以将Power BI连接到查询服务。 请参阅相关文档 [有关将Power BI桌面应用程序连接到查询服务的说明](./clients/power-bi.md).
+++

### 连接到查询服务时，为何需要很长时间才能加载功能板？

+++答案当系统连接到查询服务时，它会连接到交互式或批处理引擎。 这可能会导致加载时间较长以反映处理过的数据。

如果要缩短功能板的响应时间，应实施Business Intelligence(BI)服务器作为查询服务和BI工具之间的缓存层。 通常，大多数BI工具都为服务器提供了附加服务。

添加缓存服务器层的目的是缓存来自查询服务的数据，并利用该缓存服务让仪表板加快响应。 这是可能的，因为执行的查询的结果每天都会缓存在BI服务器中。 然后，缓存服务器会为具有相同查询的任何用户提供这些结果，以减少延迟。 有关此类设置的说明，请参阅您所使用的实用程序或第三方工具的文档。
+++

### 是否可以使用pgAdmin连接工具访问查询服务？

+++答案否，不支持pgAdmin连接。 A [可用第三方客户端列表以及如何将其连接到查询服务的说明](./clients/overview.md) 可以在文档中找到。
+++

## PostgreSQL API错误 {#postgresql-api-errors}

下表提供了PSQL错误代码及其可能的原因。

| 错误代码 | 连接状态 | 描述 | 可能的原因 |
|------------|---------------------------|-------------|----------------|
| **08P01** | 不适用 | 不支持的消息类型 | 不支持的消息类型 |
| **28P01** | 启动 — 身份验证 | 密码无效 | 身份验证令牌无效 |
| **28000** | 启动 — 身份验证 | 授权类型无效 | 授权类型无效。 必须是 `AuthenticationCleartextPassword`. |
| **42P12** | 启动 — 身份验证 | 未找到表 | 未找到要使用的表 |
| **42601** | 查询 | 语法错误 | 无效命令或语法错误 |
| **42P01** | 查询 | 未找到表 | 找不到查询中指定的表 |
| **42P07** | 查询 | 表存在 | 具有相同名称的表已存在(CREATE TABLE) |
| **53400** | 查询 | 限制超出最大值 | 用户指定了高于100,000的LIMIT子句 |
| **53400** | 查询 | 语句超时 | 提交实时语句所花费的时间超过了10分钟的最大值 |
| **58000** | 查询 | 系统错误 | 内部系统故障 |
| **0A000** | 查询/命令 | 不支持 | 不支持查询/命令中的特性/功能 |
| **42501** | DROP TABLE查询 | 正在删除不是由查询服务创建的表 | 查询服务未使用创建要删除的表 `CREATE TABLE` 语句 |
| **42501** | DROP TABLE查询 | 表不是由经过身份验证的用户创建的 | 当前正在删除的表不是由当前登录的用户创建的 |
| **42P01** | DROP TABLE查询 | 未找到表 | 找不到查询中指定的表 |
| **42P12** | DROP TABLE查询 | 未找到表 `dbName`：请查看 `dbName` | 在当前数据库中未找到表 |

### 为什么在表上使用history_meta()方法时会收到58000错误代码？

+++回答 `history_meta()` 方法用于访问数据集中的快照。 以前，如果您对Azure Data Lake Storage (ADLS)中的空数据集运行查询，您将收到一个58000错误代码，指出该数据集不存在。 下面显示了旧系统错误的示例。

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
| 400 | 错误请求 | 查询格式不正确或非法 |
| 401 | 身份验证失败 | 身份验证令牌无效 |
| 500 | 内部服务器错误 | 内部系统故障 |
