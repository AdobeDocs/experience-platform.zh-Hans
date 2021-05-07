---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；个人用户档案；字段；模式;模式;模式设计；字段组；字段组；人物；人物详细信息；用户档案人详细信息；人物；
solution: Experience Platform
title: 人口统计详细信息模式字段组
topic-legacy: overview
description: 此文档概述了“人口统计详细信息”模式字段组。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
translation-type: tm+mt
source-git-commit: f5beb57acf4cc1827bf08b549cd2b3a02fd82b18
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 3%

---


# [!UICONTROL Demographic Details] 模式字段组

>[!NOTE]
>
>多个模式字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL Demographic Details] 是类的标准模式字 [[!DNL XDM Individual Profile] 段组](../../classes/individual-profile.md)。字段组提供一个根级别`person`对象，其子字段描述有关个人的信息。

![](../../images/field-groups/demographic-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `person.name` | [人员姓名](../../data-types/person-name.md) | 其子字段描述人员姓名的各种元素的对象。 |
| `person.birthDate` | 日期 | 以ISO 8601时间戳形式出生的完整日期。 |
| `person.birthDayAndMonth` | 字符串 | 一个人出生的日月，格式为MM-DD。 在知道某人出生的日期和月份时，应使用此字段，但不是在年份。 |
| `person.birthYear` | 整数 | 一个人出生的年份，包括世纪（如1989年）。 只知道人的年龄，而不是完整的出生日期时，应使用此字段。 |
| `person.gender` | 字符串 | 人的性别认同。 |
| `person.martialStatus` | 字符串 | 描述某人与另一重要人的关系。 |
| `person.nationality` | 字符串 | 使用ISO 3166-1 Alpha-2代码表示的个人与其国家之间的法律关系。 |
| `person.taxId` | 字符串 | 人员的税务/财务标识，例如美国的TIN或西班牙的CIF/NIF。 |

有关字段组的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)