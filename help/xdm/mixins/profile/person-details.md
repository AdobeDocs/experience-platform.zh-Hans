---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixin;person;person details;profile person details;person;
solution: Experience Platform
title: 人口统计详细信息混合
topic: overview
description: 此文档提供“人口统计详细信息”混合的概述。
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 3%

---


# [!UICONTROL 混合人口统计详细信息] （英文）

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请 [参阅混合名称](../name-updates.md) 更新文档。

[!UICONTROL “人口统计] 详细信息”是课程的标准 [[!DNL XDM Individual Profile] 混音](../../classes/individual-profile.md)。 混音提供根级对 `person` 象，其子字段描述有关个人的信息。

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `person.name` | [人员姓名](../../data-types/person-name.md) | 子字段描述人员姓名的各种元素的对象。 |
| `person.birthDate` | 日期 | 以ISO 8601时间戳形式出生的完整日期。 |
| `person.birthDayAndMonth` | 字符串 | 一个人出生的日月，格式为MM-DD。 此字段应当在已知某人出生的日期和月份时使用，但不应在年份使用。 |
| `person.birthYear` | 整数 | 一个人出生的年份，包括世纪（如1989年）。 当仅知道人的年龄，而不知道完整出生日期时，应使用此字段。 |
| `person.gender` | 字符串 | 人的性别身份。 |
| `person.martialStatus` | 字符串 | 描述一个人与重要人的关系。 |
| `person.nationality` | 字符串 | 使用ISO 3166-1 Alpha-2代码表示的个人与其国家之间的法律关系。 |
| `person.taxId` | 字符串 | 人员的税务／会计标识，如美国的TIN或西班牙的CIF/NIF。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [全模式](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)å