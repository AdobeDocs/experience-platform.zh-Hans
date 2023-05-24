---
title: 存款詳細資料結構描述欄位群組
description: 本檔案提供「存款詳細資訊」結構描述欄位群組的概觀。
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 2%

---

# [!UICONTROL 存款細節] 結構描述欄位群組

[!UICONTROL 存款細節] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 欄位群組提供單一 `personalFinances.deposits` 結構描述的欄位，可擷取關於財務存款的詳細資訊。

![](../../images/field-groups/deposit-details.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `account` | [[!UICONTROL 財務帳戶]](../../data-types/financial-account.md) | 說明與存款相關聯的財務帳戶。 |
| `transaction` | [[!UICONTROL 交易]](../../data-types/transaction.md) | 說明與存款相關的財務交易。 |
| `mobileDeposit` | [!UICONTROL 布尔型] | 指出是否透過行動平台完成存款。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
