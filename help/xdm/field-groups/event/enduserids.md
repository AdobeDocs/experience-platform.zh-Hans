---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；ExperienceEvent；欄位；結構描述；結構描述設計；欄位群組；欄位群組；enduserids；一般使用者；id；
solution: Experience Platform
title: 一般使用者ID詳細資料結構描述欄位群組
description: 本檔案提供「一般使用者ID詳細資訊」結構描述欄位群組的概觀。
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 4%

---


# [!UICONTROL 一般使用者ID詳細資訊] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 一般使用者ID詳細資訊] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)，用於說明個人在多個Adobe應用程式中的身分資訊。 欄位群組提供根層級 `endUserIDs` 物件，其本身包含唯讀 `_experience` 其值會在擷取資料時自動更新的欄位。

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `aacustomid` | [标识](../../data-types/identity.md) | Adobe Analytics Cloud的自訂一般使用者ID。 |
| `aaid` | [标识](../../data-types/identity.md) | Adobe Analytics Cloud的一般使用者ID。 |
| `acid` | [标识](../../data-types/identity.md) | Adobe Campaign的一般使用者ID。 |
| `adcloud` | [标识](../../data-types/identity.md) | Adobe Advertising Cloud的一般使用者ID。 |
| `emailid` | [标识](../../data-types/identity.md) | 電子郵件地址ID。 |
| `mcid` | [标识](../../data-types/identity.md) | Adobe Marketing Cloud ID (MCID)。 MCID現在稱為Experience CloudID (ECID)。 |
| `phonenumberid` | [标识](../../data-types/identity.md) | 電話號碼識別碼。 |
| `tntid` | [标识](../../data-types/identity.md) | Adobe Target的一般使用者ID。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
