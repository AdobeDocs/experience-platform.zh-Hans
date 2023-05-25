---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；全名；xdm：fullName；人员名称；名称；数据类型；数据类型；
solution: Experience Platform
title: 人员姓名数据类型
description: 本文档提供人员名称XDM数据类型的概述。
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# [!UICONTROL 人员姓名] 数据类型

[!UICONTROL 人员姓名] 是描述人员全名的标准XDM数据类型。 由于不同语言和文化的名称结构约定差异很大，因此应始终使用此数据类型对名称进行建模。

此外，数据类型提供了许多可选属性，在只需要使用全名的片段的情况下（例如创建正式或非正式问候语）可以使用这些属性。

<img src="../images/data-types/person-name.png" width="500" /><br />

| 属性 | 描述 |
| --- | --- |
| `courtesyTitle` | 人员的职务、敬语或称呼的缩写(例如 `Mr.`， `Miss.`，或 `Dr.`)。 |
| `firstName` | 在姓名的语言中最常被接受的书写顺序排列的姓名第一部分。 |
| `fullName` | 人员的全名，按照姓名语言中最常接受的书写顺序。 |
| `lastName` | 在姓名的语言中最常被接受的书写顺序中的姓名的末尾部分。 |
| `middleName` | 在名字和姓氏之间提供的中间名、备用名或附加名。 |
| `suffix` | 在个人姓名之后提供的一组信件，以提供更多信息(例如 `Jr.`， `Sr.`， `M.D.`， `PhD`， `I`， `II`， `III`，等等)。 |

{style="table-layout:auto"}

有关人员姓名数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
