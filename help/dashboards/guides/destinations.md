---
keywords: Experience Platform；配置文件；实时客户配置文件；用户界面；UI；自定义；配置文件功能板；功能板
title: 目标功能板
description: Adobe Experience Platform提供了一个功能板，您可以通过该功能板查看有关贵组织活动目标的重要信息。
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 8571d86e1ce9dc894e54fe72dea75b9f8fe84f0b
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# [!UICONTROL 目标] 仪表板

Adobe Experience Platform用户界面(UI)提供了一个功能板，您可以通过该功能板查看有关贵组织活动目标的重要信息，这些信息是在每日快照期间捕获的。 本指南概述了如何在UI中访问和使用目标功能板，并提供了有关功能板中显示的量度的更多信息。

有关目标的概述以及Experience Platform中所有可用目标的目录，请访问 [目标文档](../../destinations/home.md).

## [!UICONTROL 目标] 仪表板数据 {#destinations-dashboard-data}

的 [!UICONTROL 目标] 功能板显示贵组织在Experience Platform中启用的目标快照。 快照中的数据与拍摄快照时在特定时间点显示的数据完全一样。 换句话说，快照不是数据的近似值或样本，目标功能板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新，在拍摄下一个快照之前不会反映在功能板中。

## 浏览目标仪表板

要导航到Platform UI中的目标功能板，请选择 **[!UICONTROL 目标]** 在左边栏中，选择 **[!UICONTROL 概述]** 选项卡来显示功能板。

>[!NOTE]
>
>如果贵组织是新Experience Platform，并且还没有活动目标，则 [!UICONTROL 目标] 功能板和 [!UICONTROL 概述] 选项卡。 而是选择 [!UICONTROL 目标] 在左侧导航中， [!UICONTROL 目录] 选项卡。 要进一步了解 [!UICONTROL 目录] 选项卡，请参阅 [[!UICONTROL 目标] 工作区指南](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### 修改目标功能板

您可以通过选择 **[!UICONTROL 修改功能板]**. 这样，您就可以在功能板中移动、添加和删除小组件，以及访问 **[!UICONTROL 构件库]** 以浏览可用小组件并为贵组织创建自定义小组件。

请参阅 [修改功能板](../customize/modify.md) 和 [构件库概述](../customize/widget-library.md) 文档以了解更多信息。

## 标准小组件

Adobe提供了多个标准小组件，您可以使用这些小组件来可视化与目标相关的不同量度。 您还可以使用 [!UICONTROL 构件库]. 要了解有关创建自定义小组件的更多信息，请首先阅读 [构件库概述](../customize/widget-library.md).

要进一步了解每个可用的标准小组件，请从以下列表中选择小组件的名称：

* [[!UICONTROL 最常用的目标]](#most-used-destinations)
* [[!UICONTROL 最近创建的目标]](#recently-created-destinations)
* [[!UICONTROL 最近激活的区段]](#recently-activated-segments)

### [!UICONTROL 最常用的目标] {#most-used-destinations}

的 **[!UICONTROL 最常用的目标]** 小组件按映射的区段数显示自上次快照起，您组织的热门目标。 此排名提供了有关哪些目标正在被利用的洞察信息，同时还可能显示那些可能未充分利用的目标。

例如，如果您昨天配置了一个目标，但尚未将任何区段映射到该目标，则您将能够看到该目标当前未充分利用。

截至上次每日快照时，区段计数列中显示的已映射区段数是准确的。 将新区段映射到目标将不会更新计数，直到拍摄下一个快照。

从小组件上显示的列表中选择目标名称后，您将转到 **[!UICONTROL 浏览]** 选项卡。 您还可以选择 **[!UICONTROL 查看全部]** 导航到 **[!UICONTROL 浏览]** 选项卡，然后选择目标的名称以查看其详细信息。

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL 最近创建的目标] {#recently-created-destinations}

的 **[!UICONTROL 最近创建的目标]** 小组件允许您查看组织最近配置的目标列表。

显示的创建日期精确到最后的每日快照。 换言之，如果您创建了新目标，则在拍摄下一个快照之后，该目标才会显示在列表中。

从小组件上显示的列表中选择目标名称后，您将转到 **[!UICONTROL 浏览]** 选项卡。 您还可以选择 **[!UICONTROL 查看全部]** 导航到 **[!UICONTROL 浏览]** 选项卡，然后选择目标的名称以查看其详细信息。

要进一步了解如何配置特定类型的目标，请访问 [目标文档](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 最近激活的区段] {#recently-activated-segments}

的 **[!UICONTROL 最近激活的区段]** 小组件提供了最近映射到目标的区段列表。 此列表提供了系统中正在使用哪些区段和目标的快照，并有助于对任何错误映射进行故障诊断。

显示的更新日期显示区段上次激活到目标的时间，并准确到最后的每日快照。 换句话说，如果您将区段激活到目标，则更新日期在拍摄下一个快照之后才会更改。

从小组件上显示的列表中选择区段名称后，您将转到区段详细信息。 您还可以选择 **[!UICONTROL 查看全部]** 导航到区段浏览选项卡，然后选择区段名称以查看其详细信息。

有关在Experience Platform中使用区段的更多信息，请首先阅读 [Segmentation Service概述](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## 后续步骤

通过阅读本文档，您现在应该能够找到目标功能板并了解可用小组件中显示的量度。 要了解有关在Experience Platform中使用目标的更多信息，请参阅 [目标文档](../../destinations/home.md).
