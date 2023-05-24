---
title: 醫療保健提供者結構描述欄位群組
description: 本檔案提供醫療保健提供者結構描述欄位群組的概觀。
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 4%

---

# [!UICONTROL 醫療保健提供者] 結構描述欄位群組

[!UICONTROL 醫療保健提供者] 是的標準結構描述欄位群組 [[!UICONTROL 提供者] 類別](../../classes/provider.md). 它提供單一物件型別欄位 `healthcareProvider` 擷取與獲授權提供醫療保健診斷和治療服務的個人健康專業人士或健康設施組織相關的屬性。

![](../../images/field-groups/healthcare-provider.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `addressDetails` | 物件陣列 | 列出提供者的地址詳細資料。 每個物件包含下列屬性： <ul><li>`address`： ([[!UICONTROL 郵寄地址]](../../data-types/postal-address.md))：提供者的郵寄地址。</li><li>`addressType`：（字串）位址型別，指出提供者提供服務的位置。</li></ul> |
| `emailAddress` | [[!UICONTROL 电子邮件地址]](../../data-types/email-address.md) | 提供者的電子郵件地址。 |
| `fax` | [[!UICONTROL 电话号码]](../../data-types/phone-number.md) | 提供者的傳真號碼。 |
| `phoneNumber` | [[!UICONTROL 电话号码]](../../data-types/phone-number.md) | 提供者的電話號碼。 |
| `qualifications` | 物件陣列 | 列出與提供照護相關的認證、授權或培訓。 每個物件包含下列屬性： <ul><li>`issuer`： ([[!UICONTROL 帳戶詳細資料]](../../data-types/account-details.md))：監管和發佈資格的組織。</li><li>`activePeriod`：（整數）資格生效之前的年份。</li><li>`code`：（字串）資格的編碼表示法。</li></ul> |
| `classification` | 字符串 | 根據類別或類別（例如病人護理、非病人護理等）的服務提供者分類。 |
| `isActive` | 布尔值 | 指出提供者是否使用中。 |
| `languages` | 字串陣列 | 提供者在其下執行作業的語言清單。 |
| `practiceGroupName` | 字符串 | 服務提供者的實務群組名稱。 |
| `practiceGroupType` | 字符串 | 服務提供者的實務群組型別。 |
| `practiceType` | 字符串 | 服務提供者的實務型別。 |
| `specialties` | 字串陣列 | 此提供者提供的專業清單。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
