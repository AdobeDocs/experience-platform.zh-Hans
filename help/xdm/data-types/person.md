---
keywords: Experience Platform；主题；热门主题；模式;模式;XDM；字段；模式;模式；人员；数据类型；数据类型；
solution: Experience Platform
title: 人员数据类型
topic: overview
description: 此文档概述了个人体验数据模型(XDM)数据类型。
translation-type: tm+mt
source-git-commit: 194b604d4b23f2acfaa4243155b04a6793fb0727
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---


# [!UICONTROL 个] 人数据类型

[!UICONTROL 个] 人是一种标准的体验数据模型(XDM)数据类型，用于描述个人。此数据类型可以表示担任各种角色的人员，如客户、联系人或所有者。

<img src="../images/data-types/person.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `name` | [[!UICONTROL 人员姓名]](./person-name.md) | 描述有关人员全名的详细信息。 |
| `birthDate` | 日期 | 一个人出生的完整日期。 日期格式（无时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)条标准。 |
| `birthDayAndMonth` | 字符串 | 一个人出生的日月，格式为MM-DD。 此字段应当在已知某人出生的日期和月份时使用，但不应在年份使用。 此属性的格式必须符合此常规表达式`[0-1][0-9]-[0-9][0-9]`。 |
| `birthYear` | 整数 | 出生的年份，包括世纪（例如`1983`）。 当仅知道人的年龄而不知道完整出生日期时，应使用此字段。 此值必须介于1和32767之间。 |
| `gender` | 字符串 | 人的性别身份。 此属性的值必须等于以下已知枚举值之一。 <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 此值的默认值为`not_specified`。 |
| `maritalStatus` | 字符串 | 描述一个人与重要人的关系。 此属性的值必须等于以下枚举值之一。 <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 此值的默认值为`not_specified`。 |
| `nationality` | 字符串 | 使用ISO 3166-1 Alpha-2代码表示的个人与其国家之间的法律关系。 此属性的格式必须符合此常规表达式`^[A-Z]{2}$`。 |
| `taxId` | 字符串 | 个人的税或会计ID，如美国的纳税人身份识别号(TIN)或西班牙的“财务识别证书”(CIF/NIF)。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)