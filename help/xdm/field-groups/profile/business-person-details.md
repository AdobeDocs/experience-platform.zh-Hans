---
title: XDM商業人士詳細資料結構描述欄位群組
description: 本檔案提供XDM業務人員詳細資料結構描述欄位群組的概觀。
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 6%

---

# [!UICONTROL XDM商業人士詳細資料] 結構描述欄位群組

[!UICONTROL XDM商業人士詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md) 擷取企業對企業(B2B)背景下個別人員的相關資訊。

![](../../images/field-groups/business-person-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `b2b` | 对象 | 擷取有關個人的B2B特定詳細資料的物件。 |
| `b2b.accountKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 與個人相關的商業帳戶的複合識別碼。 |
| `b2b.convertedContactKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 如果潛在客戶已轉換，則為關聯聯絡人的複合識別碼。 |
| `b2b.personKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 人員或個人資料片段的複合識別碼。 |
| `b2b.accountID` | 字符串 | 此人員相關聯之商業帳戶的唯一ID。 |
| `b2b.blockedCause` | 字符串 | 如果人員遭到封鎖，此屬性會提供原因。 |
| `b2b.convertedContactID` | 字符串 | 聯絡人ID （若已成功轉換潛在客戶）。 |
| `b2b.convertedDate` | 日期時間 | 成功轉換潛在客戶時的轉換日期。 |
| `b2b.isBlocked` | 布尔值 | 指出此人是否遭到封鎖。 |
| `b2b.isConverted` | 布尔值 | 指出是否轉換潛在客戶。 |
| `b2b.isMarketingSuspended` | 布尔值 | 指出該人員的行銷是否暫停。 |
| `b2b.marketingSuspendedCause` | 字符串 | 如果個人的行銷活動暫停，此屬性會提供原因。 |
| `b2b.personGroupID` | 字符串 | 適用於個人的群組識別碼。 |
| `b2b.personScore` | 双精度 | CRM系統產生的個人分數。 |
| `b2b.personSource` | 字符串 | 接收個人資訊的來源。 |
| `b2b.personStatus` | 字符串 | 個人目前的行銷或銷售狀態。 |
| `b2b.personType` | 字符串 | B2B個人的型別。 |
| `extSourceSystemAudit` | [外部來源系統稽核屬性](../../data-types/external-source-system-audit-attributes.md) | 如果業務人員關係來自外部來源系統，則此物件會擷取該系統的稽核屬性。 |
| `extendedWorkDetails` | 对象 | 擷取有關個人的其他工作相關細節。 |
| `extendedWorkDetails.assistantDetails` | 对象 | 擷取與個人助理相關的下列屬性： <ul><li>`name`： ([個人名稱](../../data-types/person-name.md))助理的全名。</li><li>`phone`： ([電話號碼](../../data-types/phone-number.md))助理的電話號碼。</li></ul> |
| `extendedWorkDetails.departments` | 字串陣列 | 個人工作的部門名稱清單。 |
| `extendedWorkDetails.jobTitle` | 字符串 | 個人的職稱。 |
| `extendedWorkDetails.photoUrl` | 字符串 | 個人像片的URL。 |
| `extendedWorkDetails.reportsToID` | 字符串 | 個人報表管理員的識別碼。 |
| `faxPhone` | [电话号码](../../data-types/phone-number.md) | 個人的傳真電話號碼。 |
| `homeAddress` | [郵寄地址](../../data-types/postal-address.md) | 個人的住家地址。 |
| `homePhone` | [电话号码](../../data-types/phone-number.md) | 個人的住家電話號碼。 |
| `mobilePhone` | [电话号码](../../data-types/phone-number.md) | 個人的行動電話號碼。 |
| `otherAddress` | [郵寄地址](../../data-types/postal-address.md) | 人員的替代地址。 |
| `otherPhone` | [电话号码](../../data-types/phone-number.md) | 個人的替代電話號碼。 |
| `person` | [人员](../../data-types/person.md) | 個別執行者、連絡人或擁有者。 |
| `personalEmail` | [电子邮件地址](../../data-types/email-address.md) | 個人的個人電子郵件地址。 |
| `workAddress` | [郵寄地址](../../data-types/postal-address.md) | 個人的工作地址。 |
| `workEmail` | [电子邮件地址](../../data-types/email-address.md) | 個人的工作電子郵件地址。 |
| `workPhone` | [电话号码](../../data-types/phone-number.md) | 個人的工作電話號碼。 |
| `identityMap` | 地图 | 包含人員的一組名稱空間身分的對映欄位。 系統會在擷取身分資料時自動更新此欄位。 為了正確使用此欄位 [即時客戶個人檔案](../../../profile/home.md)，請勿嘗試手動更新資料作業中的欄位內容。<br /><br />請參閱「 」中有關身分對應的章節 [結構描述組合基本概念](../../schema/composition.md#identityMap) 以取得其使用案例的詳細資訊。 |
| `isDeleted` | 布尔值 | 指出此人是否已在Marketo Engage中刪除。<br><br>使用時 [Marketo來源聯結器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，任何在Marketo中刪除的記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄可能仍會保留在資料湖中。 透過設定 `isDeleted` 至 `true`，您可使用欄位來篩選在查詢資料湖時已從來源中刪除哪些記錄。 |
| `organizations` | 字串陣列 | 個人工作的組織名稱清單。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
