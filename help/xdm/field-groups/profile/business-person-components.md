---
title: XDM商業人士元件結構描述欄位群組
description: 本檔案提供XDM業務人員元件結構描述欄位群組的概觀。
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# [!UICONTROL XDM商業人士要素] 結構描述欄位群組

[!UICONTROL XDM商業人士要素] 是的標準結構描述欄位群組 [[!DNL XDM Individual Profile] 類別](../../classes/individual-profile.md) 擷取個人的多個來源記錄，以及個人細分所需的其他屬性。

為人員建立設定檔時，透過 [即時客戶個人檔案](../../../profile/home.md) 在Real-Time CDP的B2B版本中，用來建立該設定檔的資訊可能來自許多來源記錄。 例如，如果某人供職於兩家不同的公司，則許多CRM系統都會刻意複製該人的副本，使一份連結至公司A，另一份連結至公司B。將該資料引進Adobe Experience Platform時，此欄位群組用於將這些不同的來源記錄合併為單一表示法。

欄位群組提供根層級 `personComponents` 欄位，物件陣列。 陣列中的每個物件代表不同的來源記錄。

>[!IMPORTANT]
>
>您必須依照以下說明中的擷取模式操作 [來原始檔](../../../rtcdp/sources/b2b.md). 無法保證其他欄位對應方法有效。
>
>例如，每個物件 `personComponents` 陣列會在標準擷取模式期間個別提交，然後由Platform新增至陣列。 手動將物件陣列新增至業務人員元件將傳回錯誤。
>建立B2B資料的結構描述時，應使用自動產生公用程式。 請參閱檔案以瞭解如何使用 [B2B名稱空間和結構描述自動產生公用程式](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). 如果您未使用自動產生公用程式，且打算手動對應資料模型，請務必參閱 [Adobe Real-time Customer Data Platform B2B Edition XDM類別](../../../rtcdp/schemas/b2b.md) 對映資料之前。
>
>請參閱 [端到端教學課程](../../../rtcdp/b2b-tutorial.md) 以取得有關B2B資料的建議工作流程資訊。

![](../../images/field-groups/business-person-components.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 與個人相關聯之帳戶的複合識別碼。 |
| `sourceConvertedContactKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 如果此潛在客戶已轉換，則為相關連絡人的複合識別碼。 |
| `sourceExternalKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 此人的資料源自的來源系統的複合識別碼。 |
| `sourcePersonKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 個人的複合識別碼。 |
| `workEmail` | [[!UICONTROL 电子邮件地址]](../../data-types/b2b-source.md) | 個人的工作電子郵件ID。 |
| `personGroupID` | 字符串 | 適用於個人的群組識別碼。 |
| `personScore` | 字符串 | CRM系統產生的個人分數。 |
| `personSource` | 字符串 | 此人的資料源自的來源系統的唯一字串型識別碼。 |
| `personStatus` | 字符串 | 個人目前的行銷或銷售狀態。 |
| `personType` | 字符串 | B2B內容中的人員型別。 |
| `sourceAccountID` | 字符串 | 來源系統中與個人相關聯之帳戶的唯一字串型識別碼。 此欄位被系統當作外部索引鍵使用，以查詢此人供職的不同公司。 |
| `sourceConvertedContactID` | 字符串 | 如果此潛在客戶已轉換，則為相關聯絡人的唯一字串型識別碼。 |
| `sourceExternalID` | 字符串 | 此人的資料源自的來源系統的唯一字串型識別碼。 |
| `sourcePersonID` | 字符串 | 適用於個人的唯一字串型識別碼。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
