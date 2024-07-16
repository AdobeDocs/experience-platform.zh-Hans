---
solution: Experience Platform
title: Profile Query Language (PQL)概述
description: 本指南提供了PQL的一般概述，涵盖了格式设置指南并提供了示例PQL表达式。
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 3%

---

# [!DNL Profile Query Language] (PQL)概述

[!DNL Profile Query Language] (PQL)是符合[!DNL Experience Data Model] (XDM)的查询语言，它支持对[!DNL Real-Time Customer Profile]数据进行分段查询的定义和执行。

本指南提供了PQL的一般概述，涵盖了格式设置指南并提供了示例PQL表达式。

## PQL查询格式

PQL查询具有以下签名：

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

输入参数可以是简单基元（如布尔值或字符串）或更复杂的类型（如对象、数组或映射）。

在PQL表达式的正文中可通过三种不同的方式来引用输入参数：

### 隐式引用第一个参数

在下面的示例中，由于第一个参数始终位于上下文中，因此可以直接对其生成属性引用(`homeAddress`)。

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 对第一个参数的显式引用

在下面的示例中，`$1`引用第一个参数。 因此，`$2`将引用第二个参数等。

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 命名变量的用法，使用lambda表示法

在下面的示例中，`Profile`是一个变量名称，查询作者可以选择该名称。

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL文本

PQL支持以下文本类型：

| 文本 | 定义 | 示例 |
| ------- | ---------- | ------- |
| 字符串 | 由双引号括起来的字符组成的数据类型。 | `"pizza"`、`"jobs"`、`"antidisestablishmentarianism"` |
| 布尔值 | true或false的数据类型。 | `true`、`false` |
| 整数 | 表示整数的数据类型。 它可以是正数、负数或零。 | `-201`、`0`、`412` |
| 两次 | 表示任意实数的数据类型。 它可以是正数、负数或零。 | `-51.24`、`3.14`、`0.6942058` |
| 日期 | 一种数据类型，可用于基于年、月和日创建日期作为整数参数。 格式为`date(year, month, day)` | `date(2020, 3, 14)` |
| 数组 | 由一组其他文字值组成的数据类型。 它使用方括号将不同的值分组，并使用逗号分隔不同的值。<br> **注意：**&#x200B;您不能直接访问数组中项的属性。 因此，如果您需要访问数组中的属性，支持的方法是`select X from array where X.item = ...`。 <br> PQL保留`xEvent`一词以引用链接到用户档案的体验事件数组。 | `[1, 4, 7]`、`["US", "CA"]` |
| 相对时间引用 | 可用于形成时间戳和时间间隔引用的保留字。 <ul><li>现在，今天，昨天，明天</li><li>这个，上一个，下一个</li><li>之前、之后、从</li><li>毫秒、秒、分钟、小时、天、周、月、年、十年、世纪/世纪、千年/千年</li></ul> | `X.timestamp occurs before today`、`X.timestamp occurs last month`、`X.timestamp occurs <= 3 days before now` |

## PQL函数

下表概述了各种支持的PQL函数，包括指向更多文档的链接，以便获取更多信息。

| 类别 | 定义 |
| -------- | ---------- |
| 布尔值 | 用于在PQL中实现布尔代数。 有关这些函数的更多信息，请参阅[布尔函数文档](./boolean-functions.md)。 |
| 比较 | 用于比较不同的PQL元素。 有关这些函数的更多信息，请参阅[比较函数文档](./comparison-functions.md)。 |
| 数组、列表和设置 | 用于与数组、列表和集交互。 有关这些函数的详细信息可在[数组、列表和集函数文档](./array-functions.md)中找到。 |
| 地图 | 用于与地图交互。 有关这些函数的更多信息，请参阅[映射函数文档](./map-functions.md)。 |
| 字符串 | 用于与字符串交互。 有关这些函数的更多信息，请参阅[字符串函数文档](./string-functions.md)。 |
| 对象 | 用于与对象交互。 有关这些函数的更多信息，请参阅[对象函数文档](./object-functions.md)。 |
| 算术 | 用于对PQL元素执行基本运算。 有关这些函数的更多信息，请参阅[算术函数文档](./arithmetic-functions.md) |
| 聚合 | 用于将阵列的结果组合成单个结果。 在[聚合函数文档](./aggregation-functions.md)中可以找到有关聚合函数的更多信息。 |
| 日期和时间 | 与date、time和datetime对象一起使用。 有关这些函数的更多信息，请参阅[日期/时间函数文档](./datetime-functions.md)。 |
| 筛选条件 | 用于筛选数组中的数据。 有关这些函数的更多信息，请参阅[筛选函数文档](./filter-functions.md)。 |
| 逻辑量化符 | 用于声明数组中的条件。 有关详细信息，请参阅[逻辑量化符文档](./logical-quantifiers.md)。 |
| 其他 | 在[杂项函数文档](./misc-functions.md)中找到不适合上述任何类别的函数。 |

## 后续步骤

现在您已了解如何使用[!DNL Profile Query Language]，您可以在创建和修改区段定义时使用PQL。 有关分段的详细信息，请阅读[分段概述](../home.md)。
