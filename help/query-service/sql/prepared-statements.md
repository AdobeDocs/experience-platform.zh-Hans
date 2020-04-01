---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 准备的声明
topic: prepared statements
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 准备的声明

在SQL中，预准备语句用于模拟类似的查询或更新。 Adobe Experience Platform查询服务通过使用参数化查询支持准备的语句。 这可用于优化性能，因为您不再需要反复重新解析查询。

## 使用准备的语句

使用预准备的语句时，支持以下语法：

- [准备](#prepare)
- [执行](#execute)
- [取消分配](#deallocate)

### 准备一份准备好的声明 {#prepare}

此SQL查询将写入的SELECT查询保存为给定的名称 `PLAN_NAME`。 您可以使用变量，如 `$1` 代替实际值。 此准备的语句将在当前会话期间保存。 请注意，计划名称不 **区分大小写** 。

#### SQL格式

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 示例SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 执行准备语句 {#execute}

此SQL查询使用之前创建的预准备语句。

#### SQL格式

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 示例SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 取消分配准备的语句 {#deallocate}

此SQL查询用于删除已命名的prepared语句。

#### SQL格式

```sql
DEALLOCATE {PLAN_NAME}
```

#### 示例SQL

```sql
DEALLOCATE test;
```

## 使用预准备语句的示例流

最初，您可以有一个SQL查询，如下面的一个：

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

上述SQL查询将返回以下响应：

| id | 名字 | lastname | 出生日期 | 电子邮件 | city | 国家 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亚历山大 | 戴维斯 | 1993-09-15 | example@example.com | 温哥华 | 加拿大 |
| 10001 | 安托 | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法国 |
| 10002 | 京子 | 樱花 | 1999-11-26 | example3@example.com | 东京 | 日本 |
| 10003 | linus | 佩特松 | 1982-06-03 | example4@example.com | 斯德哥尔摩 | 瑞典 |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | 内罗毕 | 肯尼亚 |
| 10005 | 费尔南 | rios | 2002-07-30 | example6@example.com | 圣地亚哥 | 智利 |

可以使用以下准备语句参数化此SQL查询:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

现在，可以使用以下调用执行准备的语句：

```sql
EXECUTE getIdRange(10000, 10005);
```

调用它时，您会看到与之前完全相同的结果：

| id | 名字 | lastname | 出生日期 | 电子邮件 | city | 国家 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亚历山大 | 戴维斯 | 1993-09-15 | example@example.com | 温哥华 | 加拿大 |
| 10001 | 安托 | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法国 |
| 10002 | 京子 | 樱花 | 1999-11-26 | example3@example.com | 东京 | 日本 |
| 10003 | linus | 佩特松 | 1982-06-03 | example4@example.com | 斯德哥尔摩 | 瑞典 |
| 10004 | aasir | waithaka | 1976-12-17 | example5@example.com | 内罗毕 | 肯尼亚 |
| 10005 | 费尔南 | rios | 2002-07-30 | example6@example.com | 圣地亚哥 | 智利 |

在使用完准备语句后，可以使用以下调用取消分配它：

```sql
DEALLOCATE getIdRange;
```
