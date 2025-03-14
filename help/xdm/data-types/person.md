---
keywords: Experience Platform；主页；热门主题；架构；XDM；字段；架构；架构；人员；数据类型；数据类型；
solution: Experience Platform
title: 人员数据类型
description: 了解人员体验数据模型(XDM)数据类型。
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---

# [!UICONTROL 人员]数据类型

[!UICONTROL 人员]是描述个人信息的标准体验数据模型(XDM)数据类型。 此数据类型可以表示担任各种角色的人员，例如客户、联系人或所有者。

![人员图像](../images/data-types/person.PNG){width=500}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `name` | [[!UICONTROL 人员姓名]](./person-name.md) | 描述有关人员全名的详细信息。 |
| `birthDate` | 日期 | 人员的完整出生日期。 日期格式（不带时间）应遵循[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节标准。 |
| `birthDayAndMonth` | 字符串 | 人员出生的日期和月份，格式为MM-DD。 当已知人员出生的日期和月份但不知道出生年份时，应使用此字段。 此属性的格式必须符合此正则表达式`[0-1][0-9]-[0-9][0-9]`。 |
| `birthYear` | 整数 | 包括世纪的个人出生年（例如，`1983`）。 当只知道个人的年龄而不是完整的出生日期时，应当使用此字段。 此值必须介于1和32767之间。 |
| `gender` | 字符串 | 人员的性别身份。 此属性的值必须等于以下已知枚举值之一。 <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 此值的默认值为`not_specified`。 |
| `maritalStatus` | 字符串 | 描述一个人与另一个重要的人的关系。 此属性的值必须等于以下枚举值之一。 <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 此值的默认值为`not_specified`。 |
| `nationality` | 字符串 | 一个人与其国家之间的法律关系，使用ISO 3166-1Alpha2代码表示。 此属性的格式必须符合此正则表达式`^[A-Z]{2}$`。 |
| `taxId` | 字符串 | 人员的税务或财政ID，例如美国的纳税人识别号(TIN)或西班牙的Certificado de Identification Fiscal (CIF/NIF)。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
