---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；架构设计；字段组；人员；人员详细信息；人员详细信息；个人资料；
solution: Experience Platform
title: 人口统计详细信息架构字段组
description: 本文档概述了“人口统计详细信息”架构字段组。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 4%

---


# [!UICONTROL 人口统计详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 请参阅 [字段组名称更新](../name-updates.md) 以了解更多信息。

[!UICONTROL 人口统计详细信息] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md). 字段组提供根级别 `person` 对象，其子字段描述有关个人的信息。

![](../../images/field-groups/demographic-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `person.name` | [人员姓名](../../data-types/person-name.md) | 子字段描述人员姓名的各种元素的对象。 |
| `person.birthDate` | 日期 | 以ISO 8601时间戳形式出生的完整日期。 |
| `person.birthDayAndMonth` | 字符串 | 人出生的日期和时间，格式为MM-DD。 当某人出生的日期和月份已知，但不是年份时，应使用此字段。 |
| `person.birthYear` | 整数 | 一个人出生的年份，包括世纪（如1989年）。 当只知道人员的年龄，而不是完整的出生日期时，应使用此字段。 |
| `person.gender` | 字符串 | 人员的性别身份。 |
| `person.martialStatus` | 字符串 | 描述一个人与另一个重要人的关系。 |
| `person.nationality` | 字符串 | 使用ISO 3166-1 Alpha-2代码表示的个人与其国家之间的法律关系。 |
| `person.taxId` | 字符串 | 人员的税/会计ID，例如美国的TIN或西班牙的CIF/NIF。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)