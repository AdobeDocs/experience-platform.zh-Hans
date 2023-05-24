---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；人員；資料型別；資料型別；
solution: Experience Platform
title: 個人資料型別
description: 本檔案提供個人體驗資料模型(XDM)資料型別的概觀。
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 4%

---

# [!UICONTROL 個人] 資料型別

[!UICONTROL 個人] 是描述個人身分的標準Experience Data Model (XDM)資料型別。 此資料型別可代表擔任各種角色的人員，例如客戶、聯絡人或擁有者。

<img src="../images/data-types/person.PNG" width="500" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `name` | [[!UICONTROL 個人名稱]](./person-name.md) | 說明個人全名的詳細資訊。 |
| `birthDate` | 日期 | 個人出生的完整日期。 日期格式（沒有時間）應遵循 [RFC 3339,5.6節](https://tools.ietf.org/html/rfc3339#section-5.6) 標準。 |
| `birthDayAndMonth` | 字符串 | 個人出生的日期和月份（MM-DD格式）。 若只知道個人出生的日期和月份，但不知道出生年份，應使用此欄位。 此屬性的格式必須符合此規則運算式 `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | 整数 | 個人出生的年份，包括世紀(例如， `1983`)。 只知道個人的年齡而不知道完整的出生日期時，應使用此欄位。 此值必須介於1到32767之間。 |
| `gender` | 字符串 | 個人的性別識別。 此屬性的值必須等於下列已知列舉值之一。 <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> 此值的預設值為 `not_specified`. |
| `maritalStatus` | 字符串 | 說明個人與另一個重要的人的關係。 此屬性的值必須等於下列其中一個列舉值。 <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> 此值的預設值為 `not_specified`. |
| `nationality` | 字符串 | 個人與其使用ISO 3166-1 Alpha-2代碼表示的狀態之間的法律關係。 此屬性的格式必須符合此規則運算式 `^[A-Z]{2}$`. |
| `taxId` | 字符串 | 個人的稅務或稅務ID，例如美國的納稅人識別碼(TIN)或西班牙的Certificado de Identification Fiscal (CIF/NIF)。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
