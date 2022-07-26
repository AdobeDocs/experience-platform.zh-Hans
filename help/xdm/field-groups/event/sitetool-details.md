---
title: 站点工具详细信息架构字段组
description: 本文档概述了“站点工具详细信息”架构字段组。
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 5%

---

# [!UICONTROL 站点工具详细信息] 架构字段组

[!UICONTROL 站点工具详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供了 `sitetool` 对象，该模式可捕获由站点工具收集的信息。

![字段组结构](../../images/field-groups/sitetool-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `dataGatheringEvent` | 对象 | 指示此事件是否是数据收集事件以及其他相关详细信息。 包含以下属性：<ul><li>`data`:（映射）包含作为测验、调查或投票提交事件的一部分收集和提交的JSON数据。</li><li>`isTrue`:（布尔值）指示此事件是否是数据收集事件，如测验、调查或投票。</li><li>`score`:（整数）由演员根据事件响应获得的分数。</li></ul> |
| `actor` | 字符串 | 执行操作的人员/成员。 |
| `actorID` | 字符串 | 执行操作的人员/成员的唯一标识符。 |
| `isKeyEvent` | 布尔型 | 指示此事件是否为关键事件。 |
| `name` | 字符串 | 站点工具的名称，如聊天、调查等。 |
| `section` | 字符串 | 站点工具的相关部分，如主工具或子工具。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
