---
title: 机器人检测字段组
description: 了解机器人检测字段组(XDM)架构字段组。
exl-id: 8ade14a8-9a34-4060-95b2-812d1a21deeb
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 7%

---

# [!UICONTROL 机器人检测]字段组

[!UICONTROL 机器人检测]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组。 字段组提供有关机器人生成的流量的信息。

![&#x200B; [!UICONTROL 机器人检测]字段组的图表。](../../images/field-groups/bot-detection-information.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL 机器人检测] | `botDetection` | 对象 | 提供有关机器人生成的流量的信息。 |
| [!UICONTROL 得分] | `score` | 数字 | 机器人概率分数从0到1。 如果得分为零，则表示流量不是机器人。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)
