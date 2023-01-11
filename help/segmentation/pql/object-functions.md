---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；对象函数；对象；
solution: Experience Platform
title: PQL对象函数
description: 配置文件查询语言(PQL)提供了一些函数，可简化与对象的交互。
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 5%

---

# 目标函数

[!DNL Profile Query Language] (PQL)提供了一些函数，可简化与对象的交互。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 为null

的 `isNull` 函数确定对象引用是否不存在。

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

的 `isNotNull` 函数确定对象引用是否存在。

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

现在，您已经了解了对象函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).
