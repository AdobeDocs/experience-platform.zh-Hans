---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;map functions;map;
solution: Experience Platform
title: 地图函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 5%

---


# 地图函数

[!DNL Profile Query Language] (PQL)优惠函数可简化与地图的交互。 有关其他PQL功能的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md)。

## 获取

函 `get` 数用于检索给定键的映射值。

**Format**

```sql
{MAP}.get({STRING})
```

**示例**

以下PQL查询获取密钥的标识映射值 `example@example.com`。

```sql
identityMap.get("example@example.com")
```

## 按键

函数 `keys` 用于检索给定映射的所有键。

**Format**

```sql
{MAP}.keys()
```

**示例**

以下PQL查询获取映射的所有键 `identityMap`。

```sql
identityMap.keys()
```

## 值

函 `values` 数用于检索给定映射的所有值。

**Format**

```sql
{MAP}.values()
```

**示例**

以下PQL查询获取映射的所有值 `identityMap`。

```sql
identityMap.values()
```

## 后续步骤

现在您已经了解了地图功能，可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。
