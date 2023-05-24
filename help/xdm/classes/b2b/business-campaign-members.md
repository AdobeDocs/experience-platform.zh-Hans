---
title: XDM商業活動會員類別
description: 本檔案提供Experience Data Model (XDM)中XDM商業活動會員類別的概觀。
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 1%

---

# [!UICONTROL XDM商業活動會員] 類別

>[!IMPORTANT]
>
>此類別旨在供擁有下列許可權的組織使用： [Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B Edition的存取權，此類別才能參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業活動會員] 是一個標準的體驗資料模型(XDM)類別，可描述與商業促銷活動相關聯的聯絡人或銷售機會。

![XDM商業活動成員類別在UI中的結構](../../images/classes/b2b/business-campaign-members.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 相關行銷活動的複合識別碼。 |
| `campaignMemberKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 行銷活動會籍實體的複合識別碼。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部來源系統稽核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果促銷活動會籍來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `personKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 關聯行銷活動會員個人的複合識別碼。 |
| `_id` | 字符串 | 記錄的唯一識別碼。 這是系統產生的值，與 `campaignMemberID`. |

{style="table-layout:auto"}

若要瞭解此類別與其他B2B類別在概念上的關聯性，以及如何在Adobe Experience Platform UI中建立這些關聯性，請參閱以下指南： [Real-Time CDP B2B Edition中的結構描述關係](../../tutorials/relationship-b2b.md)

如需與此類別相容的其他欄位，請參閱欄位群組參考資料， [[!UICONTROL XDM商業活動會員詳細資料]](../../field-groups/b2b-campaign-members/details.md).
