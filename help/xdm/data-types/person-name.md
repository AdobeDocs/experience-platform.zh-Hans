---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；全名；xdm:fullName;person name;name;datatype;datatype；数据类型；
solution: Experience Platform
title: 人员姓名数据类型
topic-legacy: overview
description: 此文档概述了人员姓名XDM数据类型。
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# [!UICONTROL Person name] 数据类型

[!UICONTROL Person name] 是描述人员全名的标准XDM数据类型。由于不同语言和文化中名称结构的惯例差异很大，因此名称应始终使用此数据类型建模。

此外，数据类型提供了许多可选属性，这些属性可用于仅使用全名片段（如创建正式问候语或非正式问候语）的情况。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 属性 | 描述 |
| --- | --- |
| `courtesyTitle` | 人物的标题、荣誉或问候语的缩写（如`Mr.`、`Miss.`或`Dr.`）。 |
| `firstName` | 以书写顺序排列的名称的第一段，最常用的名称语言。 |
| `fullName` | 人的全名，以最常用的文字形式写成。 |
| `lastName` | 以书写顺序排列的名称的最后一段，最常用的名称语言。 |
| `middleName` | 名和姓之间提供的中间名、替代名或其他名。 |
| `suffix` | 在人名之后提供的一组字母，用于提供附加信息（如`Jr.`、`Sr.`、`M.D.`、`PhD`、`I`、`II`、`III`等）。 |

有关人员姓名数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)
