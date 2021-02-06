---
keywords: Experience Platform；主页；热门主题；PQL;pql;用户档案查询语
solution: Experience Platform
title: 用户档案查询语言(PQL)概述
topic: developer guide
description: 本指南提供PQL的一般概述，其中包括格式准则和PQL表达式示例。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---


# [!DNL Profile Query Language] (PQL)概述

[!DNL Profile Query Language] (PQL)是一种符 [!DNL Experience Data Model] 合(XDM)标准的查询语言，旨在支持数据分段查询的定义和执行 [!DNL Real-time Customer Profile] 工作。

本指南提供PQL的一般概述，其中包括格式准则和PQL表达式示例。

## PQL查询格式

PQL查询具有以下签名：

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

输入参数可以是简单的基元，如布尔值或字符串，也可以是更复杂的类型，如对象、数组或映射。

有三种不同的方法可引用PQL表达式正文中的输入参数：

### 对第一个参数的隐式引用

在以下示例中，由于第一个参数始终处于上下文中，因此可以直接为其创建属性引用(`homeAddress`)。

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 对第一个参数的显式引用

在以下示例中，`$1`引用第一个参数。 因此，`$2`将引用第二个参数，等等。

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 使用命名变量，使用lambda记号

在以下示例中，`Profile`是变量名称，可由查询作者选择。

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL文本

PQL支持以下文字类型：

| 文本 | 定义 | 示例 |
| ------- | ---------- | ------- |
| 字符串 | 一种数据类型，由多次引号环绕的字符组成。 | `"pizza"`、`"jobs"`、`"antidisestablishmentarianism"` |
| 布尔值 | 为true或false的数据类型。 | `true`、`false` |
| 整数 | 表示整数的数据类型。 它可以是正的、负的或零的。 | `-201`、`0`、`412` |
| 双精度 | 表示任意实数的数据类型。 它可以是正的、负的或零的。 | `-51.24`、`3.14`、`0.6942058` |
| 日期 | 一种数据类型，可用于根据年、月和日创建作为整数参数的日期。 其格式为`date(year, month, day)` | `date(2020, 3, 14)` |
| 阵列 | 由一组其他文字值组成的数据类型。 它使用方括号进行分组，使用逗号在不同值之间进行分隔。<br> **注意：** 您不能直接访问数组中项的属性。因此，如果您需要访问数组中的属性，支持的方法为`select X from array where X.item = ...`。 <br> PQL保留该字 `xEvent` 词以引用链接到事件的一组体验用户档案。 | `[1, 4, 7]`、`["US", "CA"]` |
| 相对时间引用 | 可用于形成时间戳和时间间隔引用的保留字。 <ul><li>现在，今天，昨天，明天</li><li>这，最后，下一个</li><li>之前，之后，</li><li>毫秒，秒，分钟，小时，天，周，月，年，十年，世纪／世纪，千年／千年</li></ul> | `X.timestamp occurs before today`、`X.timestamp occurs last month`、`X.timestamp occurs <= 3 days before now` |


## PQL函数

下表概述了支持的PQL功能的不同类别，包括指向更多文档的链接以了解更多信息。

| 类别 | 定义 |
| -------- | ---------- |
| 布尔值 | 用于在PQL中实现布尔代数。 有关这些函数的详细信息，请参阅[布尔函数文档](./boolean-functions.md)。 |
| 比较 | 用于比较不同的PQL元素。 有关这些函数的详细信息，请参阅[比较函数文档](./comparison-functions.md)。 |
| 阵列、列表和设置 | 用于与阵列、列表和集进行交互。 有关这些函数的详细信息，请参阅[数组、列表和设置函数文档](./array-functions.md)。 |
| 地图 | 用于与地图交互。 有关这些函数的详细信息，请参阅[映射函数文档](./map-functions.md)。 |
| 字符串 | 用于与字符串交互。 有关这些函数的详细信息，请参阅[字符串函数文档](./string-functions.md)。 |
| 对象 | 用于与对象交互。 有关这些函数的详细信息，请参阅[对象函数文档](./object-functions.md)。 |
| 算术 | 用于对PQL元素执行基本算术。 有关这些函数的详细信息，请参阅[算术函数文档](./arithmetic-functions.md) |
| 聚合 | 用于将数组结果合并为单个结果。 有关聚合函数的详细信息，请参阅[聚合函数文档](./aggregation-functions.md)。 |
| 日期和时间 | 与date、time和datetime对象结合使用。 有关这些函数的详细信息，请参阅[date/time函数文档](./datetime-functions.md)。 |
| 过滤器 | 用于筛选数组中的数据。 有关这些函数的详细信息，请参阅[过滤器函数文档](./filter-functions.md)。 |
| 逻辑量词 | 用于在数组中声明条件。 有关详细信息，请参阅[逻辑量化符文档](./logical-quantifiers.md)。 |
| 其他 | 在[杂项函数文档](./misc-functions.md)中可以找到不符合以上任何类别的函数。 |

## 后续步骤

您已经学习了如何使用[!DNL Profile Query Language]，现在可以在创建和修改区段时使用PQL。 有关分段的详细信息，请阅读[分段概述](../home.md)。