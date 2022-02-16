---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；故障诊断指南；FAQ；故障诊断；
solution: Experience Platform
title: 查询服务疑难解答指南
topic-legacy: troubleshooting
description: 本文档包含有关您遇到的常见错误代码以及可能原因的信息。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 03cd013e35872bcc30c68508d9418cb888d9e260
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 3%

---

# [!DNL Query Service] 疑难解答指南

本文档提供了有关查询服务的常见问题解答，并提供了使用查询服务时常见错误代码的列表。 有关Adobe Experience Platform中其他服务的相关问题和疑难解答，请参阅 [Experience Platform疑难解答指南](../landing/troubleshooting.md).

## 常见问题

以下是有关查询服务的常见问题解答列表。

### 如何仅获取查询的元数据？

要仅获取查询的元数据，您可以运行返回零行的查询，如下所示：

```sql
SELECT * FROM <table> WHERE 1=0
```

此查询仅返回指定表的元数据。

### 如何快速地在CTAS(Create Table as Select)查询上进行迭代而不对其进行具体化？

您可以创建临时表，以在对查询进行实物化以供使用之前，快速对该查询进行迭代和实验。 您还可以使用临时表来验证查询是否可正常运行。

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

### 如何将时区从UTC时间戳更改为时区？

Adobe Experience Platform以UTC（协调通用时间）时间戳格式保留数据。 UTC格式的示例为 `2021-12-22T19:52:05Z`

查询服务支持内置的SQL函数，以将给定时间戳转换为UTC格式和从UTC格式转换为SQL函数。 和 `to_utc_timestamp()` 和 `from_utc_timestamp()` 方法采用两个参数：时间戳和时区。

| 参数 | 描述 |
|---|---|
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

### 从UTC时间戳转换

的 `from_utc_timestamp()` 方法解释给定参数 **从本地时区的时间戳** 和以UTC格式提供所需区域的等效时间戳。 在以下示例中，小时为用户本地时区中的下午2:40。 作为变量传递的首尔时区比本地时区提前九小时。

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

查询会为作为参数传递的时区返回UTC格式的时间戳。 结果会比运行查询的时区早九小时。

```
8/31/2021, 11:40 PM
```

### 如何过滤我的时间序列数据？

使用时间序列数据进行查询时，应尽可能使用时间戳筛选器以进行更准确的分析。

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

### 我是否应使用通配符（如*）从数据集获取所有行？

不能使用通配符从行中获取所有数据，因为查询服务应当被视为 **柱状存储** 而不是传统的基于行的存储系统。

### 我应该使用 `NOT IN` ?

的 `NOT IN` 运算符通常用于检索未在其他表或SQL语句中找到的行。 此运算符可能会降低性能，如果正在比较的列接受，则可能会返回意外结果 `NOT NULL`，或者您有大量记录。

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

### 正确使用的 `OR` 和 `UNION` 运算符？

### 如何正确使用 `CAST` 运算符来转换SQL查询中的时间戳？

使用 `CAST` 运算符来转换时间戳，您需要同时包含这两个日期 **和** 时间。

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

### 如何将查询结果下载为CSV文件？

查询服务不直接提供此功能。 但是，如果 [!DNL PostgreSQL] 用于连接到数据库服务器的客户端具有该功能，可以将SELECT查询的响应写入并下载为CSV文件。 有关此过程的说明，请参阅您所使用的实用工具或第三方工具的文档。

## REST API错误

| HTTP状态代码 | 描述 | 可能的原因 |
| ---------------- | ----------- | --------------- |
| 400 | 错误请求 | 查询格式错误或非法 |
| 401 | 身份验证失败 | 身份验证令牌无效 |
| 500 | 内部服务器错误 | 内部系统故障 |

## PostgreSQL API错误

| 错误代码 | 连接状态 | 描述 | 可能的原因 |
| ---------- | ---------------- | ----------- | -------------- |
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
| **0A000** | 查询/命令 | 不受支持 | 查询/命令中的特性/功能不受支持 |
| **42501** | 拖放表查询 | 删除查询服务未创建的表 | 正在删除的表不是由查询服务使用 `CREATE TABLE` 语句 |
| **42501** | 拖放表查询 | 表未由经过身份验证的用户创建 | 正在删除的表不是由当前已登录的用户创建的 |
| **42P01** | 拖放表查询 | 未找到表 | 未找到查询中指定的表 |
| **42P12** | 拖放表查询 | 找不到的表 `dbName`:请检查 `dbName` | 在当前数据库中未找到表 |
