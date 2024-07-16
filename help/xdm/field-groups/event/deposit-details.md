---
title: 存款详细信息架构字段组
description: 了解“存款详细信息”架构字段组。
exl-id: a40d17b3-cb76-4b63-9328-735fc7c55672
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 4%

---

# [!UICONTROL 存款详细信息]架构字段组

[!UICONTROL 存款详细信息]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组。 字段组为架构提供单个`personalFinances.deposits`字段，用于捕获有关银行存款的详细信息。

![](../../images/field-groups/deposit-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `account` | [[!UICONTROL 财务帐户]](../../data-types/financial-account.md) | 描述与存款关联的财务帐户。 |
| `transaction` | [[!UICONTROL 事务]](../../data-types/transaction.md) | 描述与存款关联的财务交易记录。 |
| `mobileDeposit` | [!UICONTROL 布尔值] | 指示存款是否通过移动平台进行。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json)。
