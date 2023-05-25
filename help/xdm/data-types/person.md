---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；人员；数据类型；数据类型；
solution: Experience Platform
title: 人员数据类型
description: 本文档概述了Person Experience Data Model (XDM)数据类型。
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---

# [!UICONTROL 人员] 数据类型

[!UICONTROL 人员] 是描述个人的标准体验数据模型(XDM)数据类型。 此数据类型可以表示担任各种角色的人员，例如客户、联系人或所有者。

<img src="../images/data-types/person.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `name` | [[!UICONTROL 人员姓名]](./person-name.md) | 描述有关人员全名的详细信息。 |
| `birthDate` | 日期 | 人员的完整出生日期。 日期格式（不带时间）应遵循 [RFC 3339,5.6节](https://tools.ietf.org/html/rfc3339#section-5.6) 标准。 |
| `birthDayAndMonth` | 字符串 | 一个人出生的日期和月份，格式为MM-DD。 当已知人员出生的日期和月份但不知道年份时，应使用此字段。 此属性的格式必须符合此正则表达式 `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | 整数 | 一个人出生的年份，包括世纪(例如， `1983`)。 当只知道个人的年龄而不是完整的出生日期时，应使用此字段。 此值必须介于1和32767之间。 |
| `gender` | 字符串 | 人员的性别标识。 此属性的值必须等于以下已知枚举值之一。 <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 此值的默认值为 `not_specified`. |
| `maritalStatus` | 字符串 | 描述一个人与另一个重要的人的关系。 此属性的值必须等于以下枚举值之一。 <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 此值的默认值为 `not_specified`. |
| `nationality` | 字符串 | 一个人与其国家之间的法律关系，使用ISO 3166-1 Alpha-2代码表示。 此属性的格式必须符合此正则表达式 `^[A-Z]{2}$`. |
| `taxId` | 字符串 | 个人的税务或财政ID，例如美国的纳税人识别号(TIN)或西班牙的Certificado de Identification Fiscal (CIF/NIF)。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
