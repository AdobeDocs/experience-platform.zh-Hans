---
title: 卡片動作結構描述欄位群組
description: 本檔案提供「卡片動作」結構描述欄位群組的概觀。
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 6%

---

# [!UICONTROL 卡片動作] 結構描述欄位群組

[!UICONTROL 卡片動作] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 欄位群組提供單一 `personalFinances.cardActions` 結構描述的欄位，可擷取有關卡片動作的詳細資訊，例如卡片型別、啟用狀態和鎖定狀態。

![](../../images/field-groups/card-actions.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `cardActivated` | 整数 | 追蹤卡片何時已成功啟動。 |
| `cardActivationStart` | 整数 | 追蹤卡片啟用程式何時開始。 |
| `cardCancelled` | 整数 | 追蹤卡片何時已取消。 |
| `cardControlsLocked` | 整数 | 追蹤卡片的控制何時已鎖定。 |
| `cardControlsUnlocked` | 整数 | 追蹤卡片的控制何時已解鎖。 |
| `cardID` | 字符串 | 正在啟用的卡片識別碼。 此值可能與卡片編號不同。 |
| `cardLocked` | 整数 | 追蹤卡片何時已鎖定。 |
| `cardOrderNew` | 整数 | 追蹤何時已要求卡片。 |
| `cardOrderType` | 字符串 | 與卡片訂購事件相關聯的卡片訂購型別。 |
| `cardType` | 字符串 | 卡片型別。 |
| `cardUnlocked` | 整数 | 追蹤卡片何時已解鎖。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
