---
title: 存款详细信息架构字段组
description: 本文档概述了存款详细信息架构字段组。
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 5%

---

# [!UICONTROL 存款详细信息] 架构字段组

[!UICONTROL 存款详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供了 `personalFinances.deposits` 字段，用于捕获有关金融存款的详细信息。

![](../../images/field-groups/deposit-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `account` | [[!UICONTROL 财务帐户]](../../data-types/financial-account.md) | 描述与存款关联的财务帐户。 |
| `transaction` | [[!UICONTROL 交易]](../../data-types/transaction.md) | 描述与存款关联的财务交易记录。 |
| `mobileDeposit` | [!UICONTROL 布尔型] | 指示存款是否通过移动平台完成。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/industry-verticals/experienceevent-deposit-details.schema.json).
