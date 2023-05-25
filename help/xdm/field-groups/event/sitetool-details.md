---
title: Sitetool详细信息架构字段组
description: 本文档概述了Sitetool详细信息架构字段组。
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---

# [!UICONTROL Sitetool详细信息] 架构字段组

[!UICONTROL Sitetool详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供一个 `sitetool` 架构的对象，用于捕获sitetool收集的信息。

![字段组结构](../../images/field-groups/sitetool-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `dataGatheringEvent` | 对象 | 指示此事件是否是数据收集事件，以及其他相关详细信息。 包含以下属性：<ul><li>`data`：（映射）包含作为测验、调查或轮询提交事件的一部分收集和提交的JSON数据。</li><li>`isTrue`：（布尔值）指示此事件是测验、调查还是投票等数据收集事件。</li><li>`score`：（整数）操作者根据事件响应所保护的分数。</li></ul> |
| `actor` | 字符串 | 执行操作的人员/成员。 |
| `actorID` | 字符串 | 执行操作的人员/成员的唯一标识符。 |
| `isKeyEvent` | 布尔值 | 指示此事件是否为关键事件。 |
| `name` | 字符串 | Sitetool的名称，例如聊天机器人、调查等。 |
| `section` | 字符串 | Sitetool的相关部分，如main或sub。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
