---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语；对象函数；对象；
solution: Experience Platform
title: PQL对象函数
topic: developer guide
description: 用户档案查询语言(PQL)优惠函数可简化与对象的交互。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---


# 对象函数

[!DNL Profile Query Language] (PQL)优惠函数可简化与对象的交互。有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 为空

`isNull`函数确定对象引用是否不存在。

**Format**

```sql
{OBJECT}.isNull()
```

**示例**

以下PQL查询检查人员的家庭地址是否不存在。

```sql
person.homeAddress.isNull()
```

## 不为空

`isNotNull`函数确定是否存在对象引用。

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

现在您已经了解了对象函数，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语语言概述](./overview.md)。