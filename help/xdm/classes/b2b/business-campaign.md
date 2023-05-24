---
title: XDM商業活動類別
description: 本檔案提供Experience Data Model (XDM)中XDM商業活動類別的概觀。
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# [!UICONTROL XDM商業活動] 類別

>[!IMPORTANT]
>
>此類別旨在供擁有下列許可權的組織使用： [Adobe Real-time Customer Data Platform B2B版本](../../../rtcdp/b2b-overview.md). 您必須擁有Real-Time CDP B2B Edition的存取權，此類別才能參與 [即時客戶個人檔案](../../../profile/home.md).

[!UICONTROL XDM商業活動] 是一個標準Experience Data Model (XDM)類別，可擷取商業促銷活動的最低要求屬性。

![XDM商業活動類別在UI中的結構](../../images/classes/b2b/business-campaign.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 行銷活動實體的複合識別碼。 |
| `extSourceSystemAudit` | [[!UICONTROL 外部來源系統稽核屬性]](../../data-types/external-source-system-audit-attributes.md) | 如果行銷活動來自外部來源系統，此物件會擷取該系統的稽核屬性。 |
| `_id` | 字符串 | 記錄的唯一識別碼。 這是系統產生的值，與 `campaignID`. |
| `campaignDescription` | 字符串 | 行銷活動的說明。 |
| `campaignID` | 字符串 | 行銷活動實體的唯一識別碼。 |
| `campaignName` | 字符串 | 行銷活動的名稱。 |
| `campaignType` | 字符串 | 行銷活動型別或目標對象。 |

{style="table-layout:auto"}

若要瞭解此類別與其他B2B類別在概念上的關聯性，以及如何在Adobe Experience Platform UI中建立這些關聯性，請參閱以下指南： [Real-Time CDP B2B Edition中的結構描述關係](../../tutorials/relationship-b2b.md)

如需與此類別相容的其他欄位，請參閱欄位群組參考資料， [[!UICONTROL XDM商業活動細節]](../../field-groups/b2b-campaign/details.md).
