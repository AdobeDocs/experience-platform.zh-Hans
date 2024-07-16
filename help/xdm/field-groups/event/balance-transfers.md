---
title: 余额转移架构字段组
description: 了解余额转移架构字段组。
exl-id: be0d2ed6-6547-432a-af2f-409c33e268d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 3%

---

# [!UICONTROL 余额转帐]架构字段组

[!UICONTROL 余额转帐]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组。 字段组为架构提供单个`personalFinances.balanceTransfers`对象，该架构捕获有关帐户之间财务余额转移的详细信息。

![](../../images/field-groups/balance-transfers.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `accountFrom` | [[!UICONTROL 财务帐户]](../../data-types/financial-account.md) | 描述从中转移余额的财务帐户。 |
| `accountTo` | [[!UICONTROL 财务帐户]](../../data-types/financial-account.md) | 描述余额将转移到的财务帐户。 |
| `transaction` | [[!UICONTROL 事务]](../../data-types/transaction.md) | 描述与余额转移关联的财务交易记录。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-balance-transfers.schema.json)。
