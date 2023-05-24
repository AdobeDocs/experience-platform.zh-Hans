---
title: 醫療保健計畫詳細資料結構欄位群組
description: 本檔案提供「醫療保健計畫詳細資訊」結構描述欄位群組的概觀。
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 3%

---

# [!UICONTROL 醫療保健計畫詳細資料] 結構描述欄位群組

[!UICONTROL 醫療保健計畫詳細資料] 是的標準結構描述欄位群組 [[!UICONTROL 計畫] 類別](../../classes/plan.md). 它提供單一物件型別欄位 `healthcarePlanDetails` 擷取和醫療計畫相關的屬性。

![](../../images/field-groups/plan/healthcare-plan-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `networkDetails` | 物件陣列 | 列出由保險公司定義且受益人可能尋求治療的提供者網路的詳細資訊，並將以「網路內」費率承保。 每個物件包含下列屬性： <ul><li>`networkID`：（字串）網路的保險公司專用ID。</li><li>`networkName`：（字串）網路的保險公司特定名稱。</li></ul> |
| `affiliations` | 字串陣列 | 與計畫相關聯的商業實體清單。 |
| `coverageType` | 字符串 | 計畫涵蓋範圍型別。 接受的值包括：<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | 布尔值 | 指出計畫是否有效。 |
| `lastVerificationDate` | 日期時間 | 上次驗證計畫的日期。 |
| `payerID` | 字符串 | 付款人的唯一識別碼（換言之，計畫的保險提供者）。 |
| `planLevel` | 字符串 | 表示計畫層次。 接受的值包括：<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | 字符串 | 指示計畫型別。 接受的值包括：<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | 字符串 | 計畫適用的擁有者型別。 範例包括個人、群組、組織等。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
