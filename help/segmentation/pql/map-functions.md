---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；pql；PQL；配置文件查询语言；映射函数；映射；
solution: Experience Platform
title: PQL映射函数
description: 配置文件查询语言(PQL)提供了一些功能，使与地图的交互更轻松。
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 5%

---

# 映射函数

[!DNL Profile Query Language] (PQL)提供了一些功能，使与映射的交互更轻松。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## Get

此 `get` 函数用于检索给定键的映射值。

**格式**

```sql
{MAP}.get({STRING})
```

**示例**

以下PQL查询获取键的标识映射值 `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## 键

此 `keys` 函数用于检索给定映射的所有键。

**格式**

```sql
{MAP}.keys()
```

**示例**

以下PQL查询获取映射的所有键 `identityMap`.

```sql
identityMap.keys()
```

## 值

此 `values` 函数用于检索给定映射的所有值。

**格式**

```sql
{MAP}.values()
```

**示例**

以下PQL查询获取映射的所有值 `identityMap`.

```sql
identityMap.values()
```

## 后续步骤

现在您已了解映射函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [配置文件查询语言概述](./overview.md).
