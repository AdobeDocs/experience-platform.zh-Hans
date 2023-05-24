---
title: XDM商業機會個人關係類別
description: 本檔案提供Experience Data Model (XDM)中XDM商業機會個人關係類別的概觀。
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# [!UICONTROL XDM商業機會個人關係] 類別

>[!IMPORTANT]
>
>此類別旨在供擁有下列許可權的組織使用： [Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B Edition的存取權，此類別才能參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業機會個人關係] 是一個標準Experience Data Model (XDM)類別，可擷取與商業機會相關聯之個人的最低要求屬性。

![XDM商業機會人員類別在UI中的結構](../../images/classes/b2b/business-opportunity-person-relation.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL 外部來源系統稽核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果業務人員關係來自外部來源系統，則此物件會擷取該系統的稽核屬性。 |
| `opportunityKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 機會 — 個人關係中機會的複合識別碼。 |
| `opportunityPersonKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 機會 — 個人關係實體的複合識別碼。 |
| `personKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 機會 — 個人關係中個人的複合識別碼。 |
| `_id` | 字符串 | 記錄的唯一識別碼。 這是系統產生的值，與類別擷取的其他ID欄位不同。 |
| `isDeleted` | 布尔值 | 指出此行銷清單實體是否已在Marketo Engage中刪除。<br><br>使用時 [Marketo來源聯結器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，任何在Marketo中刪除的記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄可能仍會保留在資料湖中。 透過設定 `isDeleted` 至 `true`，您可使用欄位來篩選在查詢資料湖時已從來源中刪除哪些記錄。 |
| `isPrimary` | 布尔值 | 指出此人是否為此機會的主要聯絡人。 |
| `opportunityID` | 字符串 | 機會 — 個人關係中機會的唯一識別碼。 |
| `opportunityPersonID` | 字符串 | 機會 — 個人關係實體的唯一識別碼 |
| `personID` | 字符串 | 機會 — 個人關係中個人的唯一識別碼。 |
| `personRole` | 字符串 | 個人在機會 — 個人關係中的角色。 |

{style="table-layout:auto"}

請參閱指南： [Real-Time CDP B2B Edition中的結構描述關係](../../tutorials/relationship-b2b.md) 瞭解此類別與其他B2B類別在概念上的關聯性，以及如何在Adobe Experience Platform UI中建立這些關聯性。
