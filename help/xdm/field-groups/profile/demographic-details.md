---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；架构设计；字段组；字段组；人员；人员详细信息；个人资料人员详细信息；人员；
solution: Experience Platform
title: 人口统计详细信息架构字段组
description: 了解人口统计详细信息架构字段组。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 26%

---


# [!UICONTROL 人口统计详细信息]架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅有关[字段组名称更新](../name-updates.md)的文档。

[!UICONTROL 人口统计详细信息]是[[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md)的标准架构字段组。 字段组提供了一个根级别的`person`对象，其子字段描述有关个人的信息。

![](../../images/field-groups/demographic-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `person.name` | [人员姓名](../../data-types/person-name.md) | 其子字段描述人员名称的各种元素的对象。 |
| `person.birthDate` | 日期 | 人员的完整出生日期，以ISO 8601时间戳的形式表示。 |
| `person.birthDayAndMonth` | 字符串 | 一个人出生的日期和月份，格式为 MM-DD。当一个人出生的日期和月份是已知的，而不是年份时，应该使用这个字段。 |
| `person.birthYear` | 整数 | 一个人出生的年份，包括世纪（如1989年）。 当只知道个人的年龄而不是完整的出生日期时，应当使用此字段。 |
| `person.gender` | 字符串 | 人员的性别身份。 |
| `person.martialStatus` | 字符串 | 描述一个人与另一个重要的人的关系。 |
| `person.nationality` | 字符串 | 人员与其国家之间的法律关系，使用 ISO 3166-1 Alpha-2 代码表示。 |
| `person.taxId` | 字符串 | 人员的税务/财政ID，例如美国的TIN或西班牙的CIF/NIF。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)