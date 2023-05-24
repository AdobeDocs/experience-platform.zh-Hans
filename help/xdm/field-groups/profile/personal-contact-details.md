---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個人設定檔；欄位；結構；結構；個人詳細資訊；結構描述設計；欄位群組；欄位群組；
solution: Experience Platform
title: 個人聯絡詳細資料結構描述欄位群組
description: 本檔案提供「個人連絡人詳細資訊」結構描述欄位群組的概觀。
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---


# [!UICONTROL 個人聯絡詳細資訊] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 個人聯絡詳細資訊] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md) 說明個人的聯絡資訊。

![](../../images/field-groups/personal-contact-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `faxPhone` | [电话号码](../../data-types/phone-number.md) | 說明人員的傳真號碼。 |
| `homeAddress` | [郵寄地址](../../data-types/postal-address.md) | 說明個人的住址。 |
| `homePhone` | [电话号码](../../data-types/phone-number.md) | 說明個人的住家電話號碼。 |
| `mobilePhone` | [电话号码](../../data-types/phone-number.md) | 說明個人的行動電話號碼。 |
| `personalEmail` | [电子邮件地址](../../data-types/email-address.md) | 說明個人的電子郵件地址。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
