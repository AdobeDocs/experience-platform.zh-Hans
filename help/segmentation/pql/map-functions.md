---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；映射函数；映射；
solution: Experience Platform
title: PQL映射函数
description: 配置文件查询语言(PQL)提供了一些函数，可简化与映射的交互。
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 5%

---

# 映射函数

[!DNL Profile Query Language] (PQL)提供了一些函数，可简化与映射的交互。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 获取

的 `get` 函数用于检索给定键值的映射值。

**格式**

```sql
{MAP}.get({STRING})
```

**示例**

以下PQL查询获取键的身份映射值 `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## 键

的 `keys` 函数用于检索给定映射的所有键。

**格式**

```sql
{MAP}.keys()
```

**示例**

以下PQL查询将获取映射的所有键 `identityMap`.

```sql
identityMap.keys()
```

## 值

的 `values` 函数检索给定映射的所有值。

**格式**

```sql
{MAP}.values()
```

**示例**

以下PQL查询将获取映射的所有值 `identityMap`.

```sql
identityMap.values()
```

## 后续步骤

现在，您已经了解了映射函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).
