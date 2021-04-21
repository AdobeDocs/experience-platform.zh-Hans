---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；人；数据类型；数据类型；
solution: Experience Platform
title: 人员数据类型
topic-legacy: overview
description: 本文档概述了“个人体验数据模型”(XDM)数据类型。
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 4%

---

# [!UICONTROL Person] 数据类型

[!UICONTROL Person] 是一种标准的体验数据模型(XDM)数据类型，用于描述个人。此数据类型可以表示以各种角色（如客户、联系人或所有者）行事的人。

<img src="../images/data-types/person.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `name` | [[!UICONTROL Person name]](./person-name.md) | 描述有关人员全名的详细信息。 |
| `birthDate` | Date | 一个人出生的完整日期。 日期格式（无时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `birthDayAndMonth` | 字符串 | 一个人出生的日月，格式为MM-DD。 在知道某人出生的日期和月份时，应使用此字段，但不是在年份。 此属性的格式必须符合此常规表达式`[0-1][0-9]-[0-9][0-9]`。 |
| `birthYear` | 整数 | 出生年份，包括世纪（例如`1983`）。 只知道人的年龄，而不知道完整的出生日期时，应使用此字段。 此值必须介于1和32767之间。 |
| `gender` | 字符串 | 人的性别认同。 此属性的值必须等于以下已知枚举值之一。 <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 此值的默认值为`not_specified`。 |
| `maritalStatus` | 字符串 | 描述某人与另一重要人的关系。 此属性的值必须等于以下枚举值之一。 <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 此值的默认值为`not_specified`。 |
| `nationality` | 字符串 | 使用ISO 3166-1 Alpha-2代码表示的个人与其国家之间的法律关系。 此属性的格式必须符合此常规表达式`^[A-Z]{2}$`。 |
| `taxId` | 字符串 | 人员的税或财务标识，如美国的纳税人标识号(TIN)或西班牙的CIF/NIF证书。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
