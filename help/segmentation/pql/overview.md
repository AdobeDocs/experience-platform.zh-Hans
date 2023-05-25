---
keywords: Experience Platform；主页；热门主题；PQL；pql；配置文件查询语言
solution: Experience Platform
title: 配置文件查询语言(PQL)概述
description: 本指南提供了PQL的一般概述，涵盖了格式设置指南并提供了示例PQL表达式。
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---

# [!DNL Profile Query Language] (PQL)概述

[!DNL Profile Query Language] (PQL)是 [!DNL Experience Data Model] (XDM)兼容的查询语言，旨在支持分段查询的定义和执行 [!DNL Real-Time Customer Profile] 数据。

本指南提供了PQL的一般概述，涵盖了格式设置指南并提供了示例PQL表达式。

## PQL查询格式

PQL查询具有以下签名：

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

输入参数可以是简单基元（如布尔值或字符串）或更复杂的类型（如对象、数组或映射）。

有三种不同的方法可引用PQL表达式正文中的输入参数：

### 隐式引用第一个参数

在以下示例中，由于第一个参数始终位于上下文中，因此属性引用(`homeAddress`)可直接生成到其中。

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 对第一个参数的显式引用

在以下示例中， `$1` 指第一个参数。 因此， `$2` 将引用第二个参数等。

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 命名变量的用法，使用lambda表示法

在以下示例中， `Profile` 是一个变量名称，可由查询作者选择。

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL文本

PQL支持以下文本类型：

| 文本 | 定义 | 示例 |
| ------- | ---------- | ------- |
| 字符串 | 由双引号包围的字符组成的数据类型。 | `"pizza"`、`"jobs"`、`"antidisestablishmentarianism"` |
| 布尔值 | true或false的数据类型。 | `true`、`false` |
| 整数 | 表示整数的数据类型。 它可以是正数、负数或零。 | `-201`、`0`、`412` |
| 双精度 | 表示任意实数的数据类型。 它可以是正数、负数或零。 | `-51.24`、`3.14`、`0.6942058` |
| 日期 | 一种数据类型，可用于基于年、月、日创建日期作为整数参数。 格式为 `date(year, month, day)` | `date(2020, 3, 14)` |
| 数组 | 由一组其他文字值组成的数据类型。 它使用方括号对值进行分组，并使用逗号在不同值之间分隔。 <br> **注意：** 您不能直接访问数组中项目的属性。 因此，如果您需要访问数组中的属性，则支持的方法是 `select X from array where X.item = ...`. <br> PQL保留单词 `xEvent` 以引用链接到用户档案的体验事件数组。 | `[1, 4, 7]`、`["US", "CA"]` |
| 相对时间引用 | 可用于形成时间戳和时间间隔引用的保留字。 <ul><li>现在，今天，昨天，明天</li><li>这个，上一个，下一个</li><li>之前、之后、从</li><li>毫秒、秒、分钟、小时、天、周、月、年、十年、世纪/世纪、千年/千年</li></ul> | `X.timestamp occurs before today`、`X.timestamp occurs last month`、`X.timestamp occurs <= 3 days before now` |


## PQL函数

下表概述了支持的不同类型的PQL函数，包括指向更多文档的链接以了解更多信息。

| 类别 | 定义 |
| -------- | ---------- |
| 布尔值 | 用于在PQL中实现布尔代数。 有关这些函数的更多信息，请参阅 [布尔函数文档](./boolean-functions.md). |
| 比较 | 用于比较不同的PQL元素。 有关这些函数的更多信息，请参阅 [比较函数文档](./comparison-functions.md). |
| 数组、列表和设置 | 用于与阵列、列表和集交互。 有关这些函数的更多信息，请参阅 [数组、列表和设置函数文档](./array-functions.md). |
| 地图 | 用于与地图交互。 有关这些函数的更多信息，请参阅 [映射函数文档](./map-functions.md). |
| 字符串 | 用于与字符串交互。 有关这些函数的更多信息，请参阅 [字符串函数文档](./string-functions.md). |
| 对象 | 用于与对象交互。 有关这些函数的更多信息，请参阅 [对象函数文档](./object-functions.md). |
| 算术 | 用于对PQL元素执行基本运算。 有关这些函数的更多信息，请参阅 [算术函数文档](./arithmetic-functions.md) |
| 聚合 | 用于将阵列的结果组合成奇异结果。 有关聚合函数的更多信息，请参阅 [聚合函数文档](./aggregation-functions.md). |
| 日期和时间 | 与date、time和datetime对象一起使用。 有关这些函数的更多信息，请参阅 [日期/时间函数文档](./datetime-functions.md). |
| 过滤器 | 用于筛选阵列中的数据。 有关这些函数的更多信息，请参阅 [筛选函数文档](./filter-functions.md). |
| 逻辑量词 | 用于声明数组中的条件。 欲知更多信息，请参见 [逻辑数量词文档](./logical-quantifiers.md). |
| 其他 | 不符合上述任何类别的函数可在 [杂项函数文档](./misc-functions.md). |

## 后续步骤

现在您已了解如何使用 [!DNL Profile Query Language]中，您可以在创建和修改区段时使用PQL。 有关分段的更多信息，请阅读 [分段概述](../home.md).
