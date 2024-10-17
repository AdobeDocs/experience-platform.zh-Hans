---
solution: Experience Platform
title: PQL对象函数
description: Profile Query Language (PQL)提供了一些函数，可简化与对象的交互。
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 8%

---

# 目标函数

[!DNL Profile Query Language] (PQL)提供了一些功能，可简化与对象的交互。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 为空

`isNull`函数确定是否不存在作为布尔值的对象引用。

**格式**

```sql
{OBJECT}.isNull()
```

**示例**

以下PQL查询检查人员的家庭地址是否不存在。

```sql
person.homeAddress.isNull()
```

## 不为空

`isNotNull`函数确定对象引用是否作为布尔值存在。

**格式**

```sql
{OBJECT}.isNotNull()
```

**示例**

以下PQL查询检查人员的家庭地址是否存在。

```sql
person.homeAddress.isNotNull()
```

## 后续步骤

现在您已了解对象函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。
