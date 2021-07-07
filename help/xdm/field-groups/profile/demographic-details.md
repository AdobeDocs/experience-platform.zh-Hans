---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;field group;field group;person;person details;profile person details;person;
solution: Experience Platform
title: 人口统计详细信息架构字段组
topic-legacy: overview
description: 本文档概述了“人口统计详细信息”架构字段组。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 4%

---


# [!UICONTROL 人口统] 计详细信息架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL Demographic Details] is a standard schema field group for the [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). 字段组提供一个根级别`person`对象，其子字段描述有关个人的信息。

![](../../images/field-groups/demographic-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `person.name` | [人员姓名](../../data-types/person-name.md) | 子字段描述人员姓名的各种元素的对象。 |
| `person.birthDate` | 日期 | 以ISO 8601时间戳形式出生的完整日期。 |
| `person.birthDayAndMonth` | 字符串 | The day and month a person was born, in the format MM-DD. 当某人出生的日期和月份已知，但不是年份时，应使用此字段。 |
| `person.birthYear` | 整数 | 一个人出生的年份，包括世纪（如1989年）。 This field should be used when only the person&#39;s age is known, not the full birth date. |
| `person.gender` | 字符串 | 人员的性别身份。 |
| `person.martialStatus` | 字符串 | Describes a person&#39;s relationship with a significant other. |
| `person.nationality` | 字符串 | 使用ISO 3166-1 Alpha-2代码表示的个人与其国家之间的法律关系。 |
| `person.taxId` | 字符串 | The tax/fiscal ID of the person, such the TIN in the US or the CIF/NIF in Spain. |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)