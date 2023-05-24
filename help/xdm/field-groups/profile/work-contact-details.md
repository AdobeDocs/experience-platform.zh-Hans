---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；個人設定檔；欄位；結構描述；結構描述設計；mixin；mixin；工作詳細資訊；設定檔工作；
solution: Experience Platform
title: 工作連絡人詳細資料結構描述欄位群組
description: 本檔案提供「工作連絡人詳細資訊」結構描述欄位群組的概觀。
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---


# [!UICONTROL 工作聯絡詳細資訊] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 工作聯絡詳細資訊] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md). 欄位群組提供數個欄位，可擷取有關個人的職業資訊，例如工作地址、工作電子郵件、工作電話號碼和個人所屬的組織。

![](../../images/field-groups/work-contact-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `workAddress` | [郵寄地址](../../data-types/postal-address.md) | 說明人員的工作地址。 |
| `workEmail` | [电子邮件地址](../../data-types/email-address.md) | 說明個人的工作電子郵件地址。 |
| `workPhone` | [电话号码](../../data-types/phone-number.md) | 說明個人的工作電話號碼。 |
| `organizations` | 字串（陣列） | 自由格式字串陣列，代表該人員所屬的組織。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
