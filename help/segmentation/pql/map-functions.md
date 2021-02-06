---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语；地图函数；地图；
solution: Experience Platform
title: PQL映射函数
topic: developer guide
description: 用户档案查询语言(PQL)优惠函数可简化与地图的交互。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 4%

---


# 地图函数

[!DNL Profile Query Language] (PQL)优惠函数可简化与地图的交互。有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 获取

`get`函数用于检索给定键的映射值。

**Format**

```sql
{MAP}.get({STRING})
```

**示例**

以下PQL查询获取键`example@example.com`的标识映射值。

```sql
identityMap.get("example@example.com")
```

## 按键

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

现在您已经了解了地图功能，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语语言概述](./overview.md)。
