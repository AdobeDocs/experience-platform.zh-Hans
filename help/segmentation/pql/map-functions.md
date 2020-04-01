---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 地图函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 地图函数

用户档案查询语(PQL)优惠函数，可简化与地图的交互。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语言概述](./overview.md)。

## 获取

该函 `get` 数用于检索给定键的映射值。

**格式**

```sql
{MAP}.get({STRING})
```

**示例**

以下PQL查询获取密钥的标识映射的值 `example@example.com`。

```sql
identityMap.get("example@example.com")
```

## 按键

该函 `keys` 数用于检索给定映射的所有键。

**格式**

```sql
{MAP}.keys()
```

**示例**

以下PQL查询获取映射的所有键 `identityMap`。

```sql
identityMap.keys()
```

## 值

该函 `values` 数用于检索给定映射的所有值。

**格式**

```sql
{MAP}.values()
```

**示例**

以下PQL查询获取映射的所有值 `identityMap`。

```sql
identityMap.values()
```

## 后续步骤

现在您已经了解了地图功能，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语概述](./overview.md)。
