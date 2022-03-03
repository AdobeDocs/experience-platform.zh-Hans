---
title: 余额转移方案字段组
description: 本文档提供了“转帐余额”架构字段组的概览。
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 4%

---

# [!UICONTROL 余额转移] 架构字段组

[!UICONTROL 余额转移] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供了 `personalFinances.balanceTransfers` 对象为架构，该架构捕获有关帐户之间财务余额转移的详细信息。

![](../../images/field-groups/balance-transfers.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL 财务帐户]](../../data-types/financial-account.md) | 描述从中转移余额的财务帐户。 |
| `accountTo` | [[!UICONTROL 财务帐户]](../../data-types/financial-account.md) | 描述要转入余额的财务帐户。 |
| `transaction` | [[!UICONTROL 交易]](../../data-types/transaction.md) | 描述与余额转移关联的财务交易记录。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json).
