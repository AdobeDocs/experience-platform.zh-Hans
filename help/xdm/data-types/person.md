---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；人员；数据类型；数据类型；
solution: Experience Platform
title: 人员数据类型
description: 本文档概述了人员体验数据模型(XDM)数据类型。
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 4%

---

# [!UICONTROL 人员] 数据类型

[!UICONTROL 人员] 是一种用于描述个人的标准体验数据模型(XDM)数据类型。 此数据类型可以表示具有各种角色的人员，如客户、联系人或所有者。

<img src="../images/data-types/person.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `name` | [[!UICONTROL 人员姓名]](./person-name.md) | 描述有关人员全名的详细信息。 |
| `birthDate` | 日期 | 一个人出生的完整日期。 日期格式（无时间）应遵循 [RFC 3339，第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6) 标准。 |
| `birthDayAndMonth` | 字符串 | 人出生的日期和时间，格式为MM-DD。 当某人出生的日期和月份已知，但不是年份时，应使用此字段。 此属性的格式必须符合此正则表达式 `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | 整数 | 人出生的年份，包括世纪(例如， `1983`)。 当仅知道人员的年龄，而不是完整的出生日期时，应使用此字段。 此值必须介于1到32767之间。 |
| `gender` | 字符串 | 人员的性别身份。 此属性的值必须等于以下已知枚举值之一。 <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 此值的默认值为 `not_specified`. |
| `maritalStatus` | 字符串 | 描述一个人与另一个重要人的关系。 此属性的值必须等于以下枚举值之一。 <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 此值的默认值为 `not_specified`. |
| `nationality` | 字符串 | 使用ISO 3166-1 Alpha-2代码表示的个人与其国家之间的法律关系。 此属性的格式必须符合此正则表达式 `^[A-Z]{2}$`. |
| `taxId` | 字符串 | 人员的税或会计ID，如美国的纳税人标识号(TIN)或西班牙的财政标识证书(CIF/NIF)。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
