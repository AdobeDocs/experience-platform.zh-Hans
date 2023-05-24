---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql；PQL；設定檔查詢語言；物件函式；物件；
solution: Experience Platform
title: PQL物件函式
description: 設定檔查詢語言(PQL)提供可讓您更輕鬆與物件互動的函式。
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 5%

---

# 目标函数

[!DNL Profile Query Language] (PQL)提供的函式可簡化與物件的互動。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概觀](./overview.md).

## 為null

此 `isNull` 函式決定物件參考是否不存在。

**格式**

```sql
{OBJECT}.isNull()
```

**示例**

以下PQL查詢會檢查個人的住家地址是否不存在。

```sql
person.homeAddress.isNull()
```

## 不是Null

此 `isNotNull` 函式決定物件參考是否存在。

**格式**

```sql
{OBJECT}.isNotNull()
```

**示例**

以下PQL查詢會檢查個人的住家地址是否存在。

```sql
person.homeAddress.isNotNull()
```

## 后续步骤

現在您已瞭解物件函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).
