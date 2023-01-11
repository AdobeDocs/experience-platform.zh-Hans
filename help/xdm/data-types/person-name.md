---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；fullName;xdm:fullName；人员名称；名称；数据类型；数据类型；
solution: Experience Platform
title: 人员姓名数据类型
description: 本文档概述了人员名称XDM数据类型。
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# [!UICONTROL 人员姓名] 数据类型

[!UICONTROL 人员姓名] 是描述人员全名的标准XDM数据类型。 由于名称结构的惯例在不同语言和文化中存在很大差异，因此名称应始终使用此数据类型进行建模。

此外，数据类型还提供了许多可选属性，这些属性可用于仅使用全名片段的情况，例如创建正式或非正式问候语。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 属性 | 描述 |
| --- | --- |
| `courtesyTitle` | 人员标题、称号或称呼(例如 `Mr.`, `Miss.`或 `Dr.`)。 |
| `firstName` | 按书写顺序排列的名称的第一个片段，最常用的名称语言。 |
| `fullName` | 人员的全名，按最常用的语言书写顺序。 |
| `lastName` | 按书写顺序排列的名称的最后一段，最常用的名称语言。 |
| `middleName` | 名字和姓氏之间提供的中间名、替代名或其他名称。 |
| `suffix` | 在人员姓名之后提供的一组信件，用于提供其他信息(例如 `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`，等等)。 |

{style=&quot;table-layout:auto&quot;}

有关人员姓名数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
