---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语言；地图功能；
solution: Experience Platform
title: PQL映射函数
topic-legacy: developer guide
description: 用户档案查询语言(PQL)优惠函数可简化与映射的交互。
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 4%

---

# 地图函数

[!DNL Profile Query Language] (PQL)优惠函数，使与地图的交互更简单。有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] overview](./overview.md)。

## 获取

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

## 按键

`keys`函数用于检索给定映射的所有键。

**格式**

```sql
{MAP}.keys()
```

**示例**

以下PQL查询将获取映射`identityMap`的所有键。

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

以下PQL查询将获取映射`identityMap`的所有值。

```sql
identityMap.values()
```

## 后续步骤

现在，您已经了解了地图功能，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语言概述](./overview.md)。
