---
title: 卡片操作架构字段组
description: 本文档概述了卡片操作架构字段组。
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 8%

---

# [!UICONTROL 卡片操作] 架构字段组

[!UICONTROL 卡片操作] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供了 `personalFinances.cardActions` 字段，用于捕获有关卡操作的详细信息（如卡类型、激活状态和锁定状态）。

![](../../images/field-groups/card-actions.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `cardActivated` | 整数 | 跟踪卡成功激活的时间。 |
| `cardActivationStart` | 整数 | 跟踪卡激活过程的启动时间。 |
| `cardCancelled` | 整数 | 跟踪信息卡被取消的时间。 |
| `cardControlsLocked` | 整数 | 跟踪卡控件被锁定的时间。 |
| `cardControlsUnlocked` | 整数 | 跟踪卡控件解锁的时间。 |
| `cardID` | 字符串 | 要激活的卡的标识符。 此值可能与卡号不同。 |
| `cardLocked` | 整数 | 跟踪卡被锁定的时间。 |
| `cardOrderNew` | 整数 | 跟踪请求信息卡的时间。 |
| `cardOrderType` | 字符串 | 与卡订单事件关联的卡订单类型。 |
| `cardType` | 字符串 | 卡的类型。 |
| `cardUnlocked` | 整数 | 跟踪卡解锁的时间。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json).
