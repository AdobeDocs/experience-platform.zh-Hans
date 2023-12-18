---
title: 应用程序详细信息架构字段组
description: 了解应用程序详细信息架构字段组。
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 4%

---

# [!UICONTROL 应用程序详细信息] 架构字段组

[!UICONTROL 应用程序详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 字段组提供单个 `application` 架构的对象，用于捕获与应用程序相关的详细信息，例如崩溃、功能使用、启动和升级。

![](../../images/field-groups/application-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `application` | [[!UICONTROL 应用程序]](../../data-types/financial-account.md) | 捕获与事件相关的应用程序信息，包括应用程序名称、应用程序版本、安装、启动、崩溃和关闭。 它可以是事件所针对的应用程序（例如发送推送通知的目标）或发起事件的应用程序（例如单击或登录）。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
