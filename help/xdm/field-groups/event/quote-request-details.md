---
title: 報價請求詳細資料結構描述欄位群組
description: 本檔案提供「報價請求詳細資訊」結構描述欄位群組的概觀。
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# [!UICONTROL 報價請求細節] 結構描述欄位群組

[!UICONTROL 報價請求細節] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 欄位群組提供單一 `quotes` object to a schema會擷取各種型別報價的請求流程詳細資料，包括保單、醫療保健、製造訂單和高科技訂單。

![](../../images/field-groups/quote-request-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `discount` | [[!UICONTROL 货币]](../../data-types/currency.md) | 向訪客顯示的報價的折扣金額。 |
| `premium` | [[!UICONTROL 货币]](../../data-types/currency.md) | 向訪客顯示的報價優惠金額。 |
| `location` | [!UICONTROL 字符串] | 用於尋找接近訪客地點的零售商的郵遞區號。 |
| `requestID` | [!UICONTROL 字符串] | 報價請求的唯一識別碼。 |
| `selectedRetailer` | [!UICONTROL 字符串] | 報價請求的所選零售商（如果適用）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
