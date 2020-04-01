---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 用户档案查询语(PQL)概述
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 用户档案查询语(PQL)概述

用户档案查询语言(PQL)是一种符合Experience Data Model(XDM)规范的查询语言，旨在支持实时客户用户档案数据的细分查询的定义和执行。

本指南提供PQL的一般概述，其中包括格式准则和PQL表达式示例。

## PQL查询格式

PQL查询具有以下签名：

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

输入参数可以是简单的基元，如布尔值或字符串，也可以是更复杂的类型，如对象、数组或映射。

有三种 **不同的方式** ，可以引用PQL表达式正文中的输入参数：

### 对第一个参数的隐式引用

在以下示例中，由于第一个参数始终位于上下文中，因此可以直接为其创建属性引用(`homeAddress`)。

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 对第一个参数的显式引用

在以下示例中， `$1` 引用第一个参数。 因此，将引 `$2` 用第二个参数等。

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 使用命名变量，使用λ表示法

在以下示例中， `Profile` 是变量名称，查询作者可以选择该名称。

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL文本

PQL支持以下文本类型：

| 文本 | 定义 | 示例 |
| ------- | ---------- | ------- |
| 字符串 | 一种数据类型，由用多次引号包围的字符组成。 | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Boolean | 数据类型为true或false。 | `true`, `false` |
| 整数 | 表示整数的数据类型。 它可以是正、负或零。 | `-201`, `0`, `412` |
| 双精度 | 表示任意实数的数据类型。 它可以是正、负或零。 | `-51.24`, `3.14`, `0.6942058` |
| 日期 | 一种数据类型，可用于根据年、月和日创建作为整数参数的日期。 格式设置为 `date(year, month, day)` | `date(2020, 3, 14)` |
| 阵列 | 作为一组其他文字值组成的数据类型。 它使用方括号进行分组，使用逗号在不同值之间进行分隔。 <br> **注意：** 不能直接访问数组中项的属性。 因此，如果您需要访问数组中的属性，则支持的方法是 `select X from array where X.item = ...`。 <br> PQL保留该词 `xEvent` 以引用链接到用户档案的一组体验事件。 | `[1, 4, 7]`, `["US", "CA"]` |
| 相对时间引用 | 可用于形成时间戳和时间间隔引用的保留字。 <ul><li>现在，今天，昨天，明天</li><li>这，最后，下一个</li><li>之前，之后，从</li><li>毫秒，秒，分钟，小时，天，周，月，年，十年，世纪／世纪，千年／千年</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## PQL函数

下表概述了支持的PQL功能的不同类别，包括指向进一步文档的链接以获取更多信息。

| 类别 | 定义 |
| -------- | ---------- |
| Boolean | 用于在PQL中实现布尔代数。 有关这些函数的更多信息，请参阅布尔函 [数文档](./boolean-functions.md)。 |
| 比较 | 用于比较不同的PQL元素。 有关这些函数的更多信息，请参阅比 [较函数文档](./comparison-functions.md)。 |
| 阵列、列表和设置 | 用于与阵列、列表和集交互。 有关这些函数的更多信息，请参 [阅数组、列表和设置函数文档](./array-functions.md)。 |
| 地图 | 用于与地图交互。 有关这些函数的更多信息，请参 [阅地图函数文档](./map-functions.md)。 |
| 字符串 | 用于与字符串交互。 有关这些函数的更多信息，请参阅 [字符串函数文档](./string-functions.md)。 |
| 算术 | 用于对PQL元素执行基本算术。 有关这些函数的更多信息可在算术函数 [文档中找到](./arithmetic-functions.md) |
| 聚合 | 用于将数组的结果合并为单个结果。 有关聚合函数的更多信息可在聚合函 [数文档中找到](./aggregation-functions.md)。 |
| 日期和时间 | 与date、time和datetime对象一起使用。 有关这些函数的更多信息，请参 [阅日期／时间函数文档](./datetime-functions.md)。 |
| 过滤器 | 用于筛选数组内的数据。 有关这些函数的更多信息，请参阅过滤 [器函数文档](./filter-functions.md)。 |
| 逻辑量词 | 用于声明数组中的条件。 更多信息可在逻辑量化符 [文档中找到](./logical-quantifiers.md)。 |
| 其他 | 在杂项函数类别中可以找到不符合上述任何文档的 [函数](./misc-functions.md)。 |

## 后续步骤

您已经学习了如何使用用户档案查询语言，现在可以在创建和修改区段时使用PQL。 有关分段的详细信息，请阅读分段 [概述](../home.md)。