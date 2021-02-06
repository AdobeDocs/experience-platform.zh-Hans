---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；全名；xdm:fullName;person name;name;datatype;datatype；数据类型；
solution: Experience Platform
title: 人员姓名数据类型
topic: overview
description: 此文档概述了人员姓名XDM数据类型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# [!UICONTROL 人员] 姓名数据类型

[!UICONTROL 人] 名是一种标准XDM数据类型，用于描述人的全名。由于名称结构的惯例在不同语言和文化中差异很大，因此名称应始终使用此数据类型建模。

此外，数据类型还提供许多可选属性，这些属性可用于仅使用全名片段（如创建正式问候语或非正式问候语）的情况。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 属性 | 描述 |
| --- | --- |
| `courtesyTitle` | 人物的标题、荣誉或问候语的缩写（如`Mr.`、`Miss.`或`Dr.`）。 |
| `firstName` | 以书写顺序排列的名称的第一段，最常用的名称语言。 |
| `fullName` | 该人的全名，以最常用的姓名语言书写。 |
| `lastName` | 以书写顺序排列的名称的最后一段最常用的名称语言。 |
| `middleName` | 名和姓之间提供的中间名、替代名或其他名。 |
| `suffix` | 在人名后提供的一组字母，用于提供附加信息（如`Jr.`、`Sr.`、`M.D.`、`PhD`、`I`、`II`、`III`等）。 |

有关人员姓名数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)