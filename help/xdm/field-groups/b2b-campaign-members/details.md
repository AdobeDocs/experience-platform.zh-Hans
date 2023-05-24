---
title: XDM商業活動會員詳細資料結構描述欄位群組
description: 本檔案提供XDM商業活動會員詳細資料結構描述欄位群組的概觀。
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# [!UICONTROL XDM商業活動會員詳細資料] 結構描述欄位群組

[!UICONTROL XDM商業活動會員詳細資料] 是的標準結構描述欄位群組 [[!UICONTROL XDM商業活動會員] 類別](../../classes/b2b/business-campaign-members.md)，可擷取商業促銷活動的詳細資訊。

![XDM商業活動會員詳細資訊欄位群組的結構，如其顯示在UI中](../../images/field-groups/b2b/business-campaign-member-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `acquiredByCampaignKey` | [[!UICONTROL B2B來源]](../../data-types/b2b-source.md) | 取得此行銷活動會員之行銷活動的複合ID。 |
| `acquiredByCampaignID` | [!UICONTROL 字符串] | 取得此行銷活動會員之行銷活動的字串識別碼。 |
| `firstRespondedDate` | [!UICONTROL 日期時間] | 個人首次回應行銷活動時的ISO 8601時間戳記。 |
| `hasReachedSuccess` | [!UICONTROL 布尔型] | 指出此行銷活動會員是否帶來成功的轉換。 |
| `hasResponded` | [!UICONTROL 布尔型] | 指出此行銷活動會員是否已回應行銷活動。 |
| `isDeleted` | [!UICONTROL 布尔型] | 指出是否已在Marketo Engage中刪除此行銷活動成員。<br><br>使用時 [Marketo來源聯結器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，任何在Marketo中刪除的記錄都會自動反映在即時客戶個人檔案中。 不過，與這些設定檔相關的記錄可能仍會保留在資料湖中。 透過設定 `isDeleted` 至 `true`，您可使用欄位來篩選在查詢資料湖時已從來源中刪除哪些記錄。 |
| `isExhausted` | [!UICONTROL 布尔型] | 指出此行銷活動會員是否已用盡所有行銷活動互動。 |
| `lastStatus` | [!UICONTROL 字符串] | 行銷活動成員的最後一個狀態。 |
| `memberStatus` | [!UICONTROL 字符串] | 行銷活動成員的目前狀態。 |
| `memberStatusReason` | [!UICONTROL 字符串] | 行銷活動成員目前狀態背後的原因。 |
| `membershipDate` | [!UICONTROL 日期時間] | 行銷活動成員目前狀態背後的原因。 |
| `nurtureCadence` | [!UICONTROL 字符串] | 要向行銷活動會員顯示行銷活動相關資訊的時間步調。 |
| `nurtureTrackName` | [!UICONTROL 字符串] | 此行銷活動成員須遵守的Nurture方案名稱。 |
| `reachedSuccessDate` | [!UICONTROL 日期時間] | 促銷活動會員成功轉換時間的ISO 8601時間戳記。 |
| `webinarConfirmationUrl` | [!UICONTROL 字符串] | 行銷活動成員的網路研討會確認URL。 |
| `webinarRegistrationID` | [!UICONTROL 字符串] | 行銷活動成員的網路研討會註冊ID。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
