---
solution: Experience Platform
title: PQL Map函数
description: Profile Query Language (PQL)提供了一些功能，可简化与地图的交互。
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%

---

# 映射函数

[!DNL Profile Query Language] (PQL)提供了一些功能，可简化与地图的交互。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## Get

`get`函数用于将给定键的映射值作为对象进行检索。

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

`keys`函数用于将给定映射的所有键检索为数组或列表。

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

`values`函数用于将给定映射的所有值检索为数组或列表。

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
