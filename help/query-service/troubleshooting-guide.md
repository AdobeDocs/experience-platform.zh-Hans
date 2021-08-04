---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；故障诊断指南；FAQ；故障诊断；
solution: Experience Platform
title: 查询服务疑难解答指南
topic-legacy: troubleshooting
description: 本文档包含有关您遇到的常见错误代码以及可能原因的信息。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 2b118228473a5f07ab7e2c744b799f33a4c44c98
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 6%

---

# [!DNL Query Service] 疑难解答指南

本文档提供了有关查询服务的常见问题解答，并提供了使用查询服务时常见错误代码的列表。 有关Adobe Experience Platform中与其他服务相关的问题和疑难解答，请参阅[Experience Platform疑难解答指南](../landing/troubleshooting.md)。

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

### 如何过滤我的时间序列数据？

使用时间序列数据进行查询时，应尽可能使用时间戳筛选器以进行更准确的分析。

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

不能使用通配符从行中获取所有数据，因为查询服务应当被视为&#x200B;**colum-store**，而不是传统的基于行的存储系统。

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
| **28000** | 启动 — 身份验证 | 授权类型无效 | 授权类型无效。 必须为`AuthenticationCleartextPassword`。 |
| **42P12** | 启动 — 身份验证 | 未找到表 | 未找到要使用的表 |
| **42601** | 查询 | 语法错误 | 命令或语法错误无效 |
| **42P01** | 查询 | 未找到表 | 在查询中指定的表未找到 |
| **42P07** | 查询 | 表存在 | 已存在同名表（创建表） |
| **53400** | 查询 | LIMIT超出最大值 | 用户指定的LIMIT子句大于100,000 |
| **53400** | 查询 | 语句超时 | 提交的实时声明最多需要10分钟 |
| **58000** | 查询 | 系统错误 | 内部系统故障 |
| **0A000** | 查询/命令 | 不受支持 | 查询/命令中的特性/功能不受支持 |
| **42501** | 拖放表查询 | 删除查询服务未创建的表 | 正在删除的表不是由查询服务使用`CREATE TABLE`语句创建的 |
| **42501** | 拖放表查询 | 表未由经过身份验证的用户创建 | 正在删除的表不是由当前已登录的用户创建的 |
| **42P01** | 拖放表查询 | 未找到表 | 未找到查询中指定的表 |
| **42P12** | 拖放表查询 | 未找到`dbName`的表：请检查`dbName` | 在当前数据库中未找到表 |
