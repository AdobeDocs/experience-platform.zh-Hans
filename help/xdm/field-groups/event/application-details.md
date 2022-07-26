---
title: 应用程序详细信息架构字段组
description: 本文档概述了“应用程序详细信息”架构字段组。
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 4%

---

# [!UICONTROL 应用程序详细信息] 架构字段组

[!UICONTROL 应用程序详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供了 `application` 对象，该模式可捕获与应用程序相关的详细信息，如崩溃次数、功能使用情况、启动次数和升级次数。

![](../../images/field-groups/application-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `application` | [[!UICONTROL 应用程序]](../../data-types/financial-account.md) | 捕获与事件相关的应用程序信息，包括应用程序名称、应用程序版本、安装、启动、崩溃和关闭。 它可以是事件所定向的应用程序（如发送推送通知的目标），也可以是发起事件的应用程序（如点击或登录）。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
