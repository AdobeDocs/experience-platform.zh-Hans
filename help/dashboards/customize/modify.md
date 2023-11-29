---
keywords: Experience Platform；用户界面；UI；功能板；功能板；配置文件；区段；目标；许可证使用情况
title: 在UI中修改Platform功能板
description: 本指南提供了有关自定义组织的Adobe Experience Platform数据在功能板中的显示方式的分步说明。
exl-id: 75e4aea7-b521-434d-9cd5-32a00d00550d
source-git-commit: 32dd90018c990e7013d826b29608a61022ba808b
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# 修改仪表板 {#modify-dashboards}

在Adobe Experience Platform用户界面(UI)中，您可以使用多个功能板查看您的组织数据并与之交互。 这些仪表板中显示的默认小部件和量度可以在单个用户级别调整以显示首选数据，并且可以在同一组织中的用户之间创建和共享小部件。

>[!NOTE]
>
>对功能板所做的任何更新都是按组织和沙盒进行的。

本指南提供了有关自定义仪表板数据在中的显示方式的分步说明。 [!UICONTROL 配置文件]， [!UICONTROL 区段]、和 [!UICONTROL 目标] Platform UI中的功能板。

## 快速入门

从任意仪表板(例如， [!UICONTROL 配置文件] （功能板），您可以选择 **[!UICONTROL 修改仪表板]** 以调整现有小部件的大小并重新排序。

![突出显示“修改”仪表板的“配置文件”仪表板。](../images/customization/modify-dashboard.png)

## 重新排序小组件

选择修改仪表板后，您可以通过选择构件标题并将构件拖放到所需顺序来重新排序构件。 在此示例中， **[!UICONTROL 配置文件计数趋势]** 构件将移至顶行，并且 **[!UICONTROL 配置文件计数]** 构件现在显示在第二行。

![带有两个重新排序小组件的“配置文件”仪表板突出显示。](../images/customization/move-widget.png)

## 调整构件大小

也可以通过选择构件右下角的角度符号来调整构件大小(`⌟`)，并将构件拖动到所需大小。 在此示例中， **[!UICONTROL 按身份列出的配置文件]** 构件将调整大小以填充整个顶行，从而自动将其他构件移动到第二行。 请注意水平轴如何调整以随着小组件变大提供更详细的增量。

>[!NOTE]
>
>在调整构件大小时，会动态地重新放置周围的构件。 这可能会导致某些构件被移动到其他行，从而需要您滚动才能查看所有构件。

![突出显示具有已调整大小小部件的配置文件仪表板。](../images/customization/resize-widget.png)

## 保存仪表板更新

完成移动小部件和调整其大小后，选择 **[!UICONTROL 保存并退出]** 以保存所做更改并返回到主仪表板视图。 如果不希望保留更改，请选择 **[!UICONTROL 取消]** 以重置仪表板并返回到主仪表板视图。

![同时带有“取消”和“保存并退出”的“配置文件”仪表板突出显示。](../images/customization/save-changes.png)

## 构件库

除了调整构件大小并重新排序构件之外，选择 **[!UICONTROL 修改仪表板]** 在 [!UICONTROL 配置文件]， [!UICONTROL 区段]、和 [!UICONTROL 目标] 仪表板允许您访问 **[!UICONTROL 构件库]** 可在其中找到更多要显示的构件或为贵组织创建自定义构件。

有关如何访问和使用 [!UICONTROL 构件库]，请参阅 [构件库指南](widget-library.md).

![突出显示“标准”和“自定义”的小组件库工作区。](../images/customization/widget-library.png)

## 后续步骤

阅读本文档后，您已了解如何使用修改仪表板功能来重新排序小部件并调整其大小以自定义仪表板视图。 要了解如何创建构件并将其添加到功能板，请阅读 [构件库指南](widget-library.md).
