---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;fullName;xdm:fullName;person name;name;datatype;data-type;data type;
solution: Experience Platform
title: 人员姓名数据类型
topic: overview
description: 此文档概述了人员姓名XDM数据类型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# [!UICONTROL 人员姓名] 数据类型

[!UICONTROL 人员姓名] 是一种标准XDM数据类型，用于描述人员的全名。 由于名称结构的惯例在不同语言和文化中差异很大，因此名称应始终使用此数据类型建模。

此外，数据类型还提供许多可选属性，这些属性可用于仅使用全名片段（如创建正式问候语或非正式问候语）的情况。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 属性 | 描述 |
| --- | --- |
| `courtesyTitle` | 人物标题、荣誉或问候语(如、 `Mr.`或 `Miss.`等 `Dr.`)的缩写。 |
| `firstName` | 以书写顺序排列的名称的第一段，最常用的名称语言。 |
| `fullName` | 该人的全名，以最常用的姓名语言书写。 |
| `lastName` | 以书写顺序排列的名称的最后一段最常用的名称语言。 |
| `middleName` | 名和姓之间提供的中间名、替代名或其他名。 |
| `suffix` | 在人名后提供的一组信件，用于提供其他信 `Jr.`息 `Sr.`(如 `M.D.`、、 `PhD``I`、 `II``III`、等等)。 |

有关人员姓名数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)