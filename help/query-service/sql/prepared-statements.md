---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；预准备语句；预准备；sql；
solution: Experience Platform
title: 查询服务中的预准备语句
description: 在SQL中，预准备语句用于模板类似的查询或更新。 Adobe Experience Platform查询服务通过使用参数化查询支持预准备语句。
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 5%

---

# 准备的语句

在SQL中，预准备语句用于模板化类似的查询或更新。 Adobe Experience Platform [!DNL Query Service]通过使用参数化查询支持预准备语句。 这可以优化性能，因为您不再需要重复地重新分析查询。

## 使用预准备语句

使用预准备语句时，支持以下语法：

- [准备](#prepare)
- [执行](#execute)
- [取消分配](#deallocate)

### 准备准备准备的语句 {#prepare}

此SQL查询保存名为`PLAN_NAME`的已写入SELECT查询。 您可以使用变量（如`$1`代替实际值）。 此准备好的语句将在当前会话期间保存。 请注意，计划名称&#x200B;**不区分大小写**。

#### SQL格式

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 示例SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 执行预准备语句 {#execute}

此SQL查询使用以前创建的预准备语句。

#### SQL格式

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 示例SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 取消分配预准备语句 {#deallocate}

此SQL查询用于删除命名的预准备语句。

#### SQL格式

```sql
DEALLOCATE {PLAN_NAME}
```

#### 示例SQL

```sql
DEALLOCATE test;
```

## 使用预准备语句的示例流程

最初，您可以有一个SQL查询，如以下查询：

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

上述SQL查询将返回以下响应：

| ID | 名字 | 姓氏 | 出生日期 | 电子邮件 | 城市 | 国家/地区 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亚历山大 | 戴维斯 | 1993-09-15 | example@example.com | 温哥华 | 加拿大 |
| 10001 | 安东尼 | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法国 |
| 10002 | 恭子 | 樱花 | 1999-11-26 | example3@example.com | 东京 | 日本 |
| 10003 | linus | 彼得松 | 1982-06-03 | example4@example.com | 斯德哥尔摩 | 瑞典 |
| 10004 | aasir | 韦塔卡 | 1976-12-17 | example5@example.com | 内罗毕 | 肯尼亚 |
| 10005 | 费尔南多 | rios | 2002-07-30 | example6@example.com | 圣地亚哥 | 智利 |

可以使用以下预准备语句参数化此SQL查询：

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

现在，可以使用以下调用执行预准备语句：

```sql
EXECUTE getIdRange(10000, 10005);
```

调用此选项时，您会看到与之前完全相同的结果：

| ID | 名字 | 姓氏 | 出生日期 | 电子邮件 | 城市 | 国家/地区 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 亚历山大 | 戴维斯 | 1993-09-15 | example@example.com | 温哥华 | 加拿大 |
| 10001 | 安东尼 | 杜布瓦 | 1967-03-14 | example2@example.com | 巴黎 | 法国 |
| 10002 | 恭子 | 樱花 | 1999-11-26 | example3@example.com | 东京 | 日本 |
| 10003 | linus | 彼得松 | 1982-06-03 | example4@example.com | 斯德哥尔摩 | 瑞典 |
| 10004 | aasir | 韦塔卡 | 1976-12-17 | example5@example.com | 内罗毕 | 肯尼亚 |
| 10005 | 费尔南多 | rios | 2002-07-30 | example6@example.com | 圣地亚哥 | 智利 |

使用完预准备语句后，可以使用以下调用取消分配该语句：

```sql
DEALLOCATE getIdRange;
```
