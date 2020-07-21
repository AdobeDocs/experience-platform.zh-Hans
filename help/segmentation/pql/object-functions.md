---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 对象函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---


# 对象函数

[!DNL Profile Query Language] (PQL)优惠函数可简化与对象的交互。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语概述](./overview.md)。

## 为空

函数 `isNull` 确定对象引用是否不存在。

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

该函 `isNotNull` 数确定对象引用是否存在。

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

现在您已经了解了对象函数，可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。