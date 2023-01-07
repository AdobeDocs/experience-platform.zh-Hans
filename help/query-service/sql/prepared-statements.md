---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；准备语句；准备；SQL;
solution: Experience Platform
title: 查询服务中准备的语句
description: 在SQL中，已准备语句用于模板类似查询或更新。 Adobe Experience Platform查询服务通过使用参数化查询支持准备的语句。
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 11%

---

# 准备的陈述

在SQL中，预准备语句用于模拟类似查询或更新。 Adobe Experience Platform [!DNL Query Service] 通过使用参数化查询支持已准备的语句。 这可以优化性能，因为您不再需要重复重新解析查询。

## 使用准备的语句

使用准备语句时，支持以下语法：

- [准备](#prepare)
- [执行](#execute)
- [取消分配](#deallocate)

### 准备陈述 {#prepare}

此SQL查询将书写的SELECT查询保存为，其名称为 `PLAN_NAME`. 您可以使用变量，例如 `$1` 代替实际值。 准备好的语句将在当前会话期间保存。 请注意，计划名称为 **not** 区分大小写。

#### SQL格式

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 示例SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 执行准备语句 {#execute}

此SQL查询使用之前创建的准备语句。

#### SQL格式

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 示例SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 取消分配准备的语句 {#deallocate}

此SQL查询用于删除命名的prepared语句。

#### SQL格式

```sql
DEALLOCATE {PLAN_NAME}
```

#### 示例SQL

```sql
DEALLOCATE test;
```

## 使用预准备语句的示例流程

最初，您可以使用SQL查询，如下面的查询：

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

上述SQL查询将返回以下响应：

| id | 名字 | lastname | 出生日期 | 电子邮件 | city | 国家 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亚历山大 | 戴维斯 | 1993-09-15 | example@example.com | 温哥华 | 加拿大 |
| 10001 | 安托万 | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法国 |
| 10002 | 京子 | 樱花 | 1999-11-26 | example3@example.com | 东京 | 日本 |
| 10003 | 林 | 佩特松 | 1982-06-03 | example4@example.com | 斯德哥尔摩 | 瑞典 |
| 10004 | aasir | 怀塔卡 | 1976-12-17 | example5@example.com | 内罗毕 | 肯尼亚 |
| 10005 | 费尔南德 | rios | 2002-07-30 | example6@example.com | 圣地亚哥 | 智利 |

可以使用以下准备语句对此SQL查询进行参数化：

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

现在，可以使用以下调用执行准备的语句：

```sql
EXECUTE getIdRange(10000, 10005);
```

调用此函数时，您将看到与之前完全相同的结果：

| id | 名字 | lastname | 出生日期 | 电子邮件 | city | 国家 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亚历山大 | 戴维斯 | 1993-09-15 | example@example.com | 温哥华 | 加拿大 |
| 10001 | 安托万 | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法国 |
| 10002 | 京子 | 樱花 | 1999-11-26 | example3@example.com | 东京 | 日本 |
| 10003 | 林 | 佩特松 | 1982-06-03 | example4@example.com | 斯德哥尔摩 | 瑞典 |
| 10004 | aasir | 怀塔卡 | 1976-12-17 | example5@example.com | 内罗毕 | 肯尼亚 |
| 10005 | 费尔南德 | rios | 2002-07-30 | example6@example.com | 圣地亚哥 | 智利 |

使用完准备语句后，您可以使用以下调用取消分配该语句：

```sql
DEALLOCATE getIdRange;
```
