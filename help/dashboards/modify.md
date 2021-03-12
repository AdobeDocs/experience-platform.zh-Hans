---
keywords: Experience Platform；用户界面；UI;仪表板;仪表板;用户档案；区段；目标；许可证使用
title: 在UI中修改平台仪表板
description: '本指南提供有关自定义组织的Adobe Experience Platform数据在仪表板中的显示方式的分步说明。 '
topic: 指南
translation-type: tm+mt
source-git-commit: 5cc973a5db88eb23c6e1aeee3695820a0555e4cf
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 2%

---


# （测试版）修改仪表板{#modify-dashboards}

>[!IMPORTANT]
>
>仪表板功能当前处于测试阶段，并非所有用户都可用。 文档和功能可能会发生变化。

在Adobe Experience Platform用户界面(UI)中，您可以使用多个仪表板来视图组织的数据并与其交互。 仪表板中显示的默认构件和量度可在单个用户级别进行调整，以显示首选数据，并可创建并在同一组织中的用户之间共享构件。

本指南提供了分步说明，用于自定义在平台UI中[!UICONTROL 仪表板]、[!UICONTROL 用户档案]和[!UICONTROL 目标]仪表板中显示数据的方式。

>[!NOTE]
>
>无法自定义许可证使用仪表板中显示的构件。 请参阅[许可证使用仪表板文档](guides/license-usage.md)，进一步了解此独特仪表板。

## 入门指南

从任何仪表板(例如，[!UICONTROL 用户档案]仪表板)中，您可以选择&#x200B;**[!UICONTROL 修改仪表板]**&#x200B;以调整现有构件的大小和对其重新排序。

![](images/customization/modify-dashboard.png)

## 重新排序构件

选择修改仪表板后，您可以通过选择构件标题并将构件拖放到所需顺序来重新排序构件。 在此示例中，按标识命名空间&#x200B;]**构件的**[!UICONTROL &#x200B;用户档案将移到顶行，而[!UICONTROL 用户档案计数]构件现在显示在第二行中。

![](images/customization/move-widget.png)

## 调整构件大小

您还可以通过选择构件右下角的角度符号(`⌟`)并将构件拖动到所需大小来调整构件大小。 在此示例中，按标识命名空间&#x200B;]**构件调整**[!UICONTROL &#x200B;用户档案的大小以填充整个顶行，并自动将其他构件移动到第二行。 请注意水平轴如何调整，以在构件变大时提供更详细的增量。

>[!NOTE]
>
>在调整构件大小时，周围的构件会动态重新定位。 这可能导致某些构件被移动到其他行，这要求您滚动以查看所有构件。

![](images/customization/resize-widget.png)

## 保存仪表板更新

移动完构件并调整其大小后，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改并返回主仪表板视图。 如果您不希望保留更改，请选择&#x200B;**[!UICONTROL 取消]**&#x200B;以重置仪表板并返回到主仪表板视图。

![](images/customization/save-changes.png)

## 构件库

除了调整小部件的大小和重新排序外，在[!UICONTROL 用户档案]和[!UICONTROL 区段]仪表板中，您还可以使用&#x200B;**[!UICONTROL 小部件库]**&#x200B;选择要显示或创建小部件的更多小部件。

有关如何访问和使用[!UICONTROL Widget库]的分步说明，请参阅[Widget库指南](widget-library.md)。

## 后续步骤

阅读此文档后，您学会了如何使用修改仪表板功能对构件重新排序和调整大小以自定义仪表板视图。 要了解如何创建构件并将其添加到仪表板，请阅读[构件库指南](widget-library.md)。