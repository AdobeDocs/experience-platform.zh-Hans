---
title: 机器人检测字段组
description: 了解机器人检测字段组(XDM)架构字段组。
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 4%

---

# [!UICONTROL 机器人检测] 字段组

[!UICONTROL 机器人检测] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供有关机器人生成的流量的信息。

![的图表 [!UICONTROL 机器人检测] 字段组。](../../images/field-groups/bot-detection-information.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------------|-----------------|-----------|---------------------------------------------------------|
| [!UICONTROL 机器人检测] | `botDetection` | 对象 | 提供有关机器人生成的流量的信息。 |
| [!UICONTROL 分数] | `score` | 数字 | 机器人概率分数从0到1。 如果得分为零，则表示流量不是机器人。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-bot-detection.schema.json)

