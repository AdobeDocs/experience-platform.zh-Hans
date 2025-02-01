---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；全名；xdm：全名；人员名称；名称；数据类型；数据类型；
solution: Experience Platform
title: 人员姓名数据类型
description: 了解人员名称XDM数据类型。
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 6%

---

# [!UICONTROL 人员姓名]数据类型

[!UICONTROL 人员姓名]是描述人员全名的标准XDM数据类型。 由于不同语言和文化的名称结构约定差异很大，因此应始终使用此数据类型对名称进行建模。

此外，数据类型提供了许多可选属性，可在只需要使用全名片段的情况（如创建正式或非正式问候语）中使用。

![](../images/data-types/person-name.png){width=500}

| 属性 | 描述 |
| --- | --- |
| `courtesyTitle` | 人员的职务、敬语或称呼的缩写（如`Mr.`、`Miss.`或`Dr.`）。 |
| `firstName` | 在姓名的语言中最常被接受的书写顺序排列的姓名第一部分。 |
| `fullName` | 人员的全名，采用姓名语言中最常接受的书写顺序。 |
| `lastName` | 在姓名的语言中最常被接受的书写顺序中的姓名的末尾部分。 |
| `middleName` | 在名字和姓氏之间提供的中间名、备用名或附加名。 |
| `suffix` | 在人员姓名后提供的一组字母，用于提供附加信息（如`Jr.`、`Sr.`、`M.D.`、`PhD`、`I`、`II`、`III`等）。 |

{style="table-layout:auto"}

有关人员名称数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
