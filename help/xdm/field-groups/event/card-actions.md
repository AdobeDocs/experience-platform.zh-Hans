---
title: 信息卡操作架构字段组
description: 了解卡片操作架构字段组。
exl-id: 49851544-9118-4b73-b1d1-4cf49b3f1dee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 24%

---

# [!UICONTROL 卡片操作]架构字段组

[!UICONTROL 卡操作]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组。 字段组为架构提供单个`personalFinances.cardActions`字段，用于捕获有关信息卡操作的详细信息，例如信息卡类型、激活状态和锁定状态。

![](../../images/field-groups/card-actions.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `cardActivated` | 整数 | 在成功激活信息卡后进行跟踪。 |
| `cardActivationStart` | 整数 | 在信息卡激活流程启动时进行跟踪。 |
| `cardCancelled` | 整数 | 在取消信息卡后进行跟踪。 |
| `cardControlsLocked` | 整数 | 在锁定信息卡的控制后进行跟踪。 |
| `cardControlsUnlocked` | 整数 | 在解锁信息卡的控制后进行跟踪。 |
| `cardID` | 字符串 | 正在激活的卡的标识符。 此值可能与卡号不同。 |
| `cardLocked` | 整数 | 在锁定信息卡后进行跟踪。 |
| `cardOrderNew` | 整数 | 在请求信息卡后进行跟踪。 |
| `cardOrderType` | 字符串 | 与卡订单事件关联的卡订单类型。 |
| `cardType` | 字符串 | 信息卡的类型。 |
| `cardUnlocked` | 整数 | 在解锁信息卡后进行跟踪。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-card-actions.schema.json)。
