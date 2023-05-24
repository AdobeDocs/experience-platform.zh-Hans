---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；個人設定檔；欄位；結構描述；結構描述設計；欄位群組；欄位群組；人員；個人詳細資訊；個人資料個人詳細資訊；人員；
solution: Experience Platform
title: 人口統計詳細資料結構欄位群組
description: 本檔案提供「人口統計詳細資訊」結構描述欄位群組的概觀。
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 3%

---


# [!UICONTROL 人口統計細節] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 人口統計細節] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md). 欄位群組提供根層級 `person` 物件，其子欄位描述有關個人的資訊。

![](../../images/field-groups/demographic-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `person.name` | [個人名稱](../../data-types/person-name.md) | 此物件的子欄位可描述個人名稱的各種元素。 |
| `person.birthDate` | 日期 | 個人出生的完整日期，採用ISO 8601時間戳記的形式。 |
| `person.birthDayAndMonth` | 字符串 | 個人出生的日期和月份（MM-DD格式）。 若只知道個人出生的日期和月份，但不知道出生年份，應使用此欄位。 |
| `person.birthYear` | 整数 | 個人出生的年份，包括世紀（例如1989）。 只知道個人的年齡而不知道完整的出生日期時，應使用此欄位。 |
| `person.gender` | 字符串 | 個人的性別識別。 |
| `person.martialStatus` | 字符串 | 說明個人與另一個重要的人的關係。 |
| `person.nationality` | 字符串 | 個人與其使用ISO 3166-1 Alpha-2代碼表示的狀態之間的法律關係。 |
| `person.taxId` | 字符串 | 個人的稅務/財政ID，例如美國的TIN或西班牙的CIF/NIF。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)