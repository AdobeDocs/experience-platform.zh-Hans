---
solution: Experience Platform
title: PQL Map函数
description: Profile Query Language (PQL)提供了一些功能，可简化与地图的交互。
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 6%

---

# 映射函数

[!DNL Profile Query Language] (PQL)提供了一些功能，可简化与地图的交互。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## Get

`get`函数用于检索给定键的映射值。

**格式**

```sql
{MAP}.get({STRING})
```

**示例**

以下PQL查询获取键`example@example.com`的标识映射值。

```sql
identityMap.get("example@example.com")
```

## 键

`keys`函数用于检索给定映射的所有键。

**格式**

```sql
{MAP}.keys()
```

**示例**

以下PQL查询获取映射`identityMap`的所有键。

```sql
identityMap.keys()
```

## 值

`values`函数用于检索给定映射的所有值。

**格式**

```sql
{MAP}.values()
```

**示例**

以下PQL查询获取映射`identityMap`的所有值。

```sql
identityMap.values()
```

## 后续步骤

现在您已了解映射函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。
