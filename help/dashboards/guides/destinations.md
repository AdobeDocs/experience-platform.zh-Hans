---
keywords: Experience Platform;用户档案；实时客户用户档案；用户界面；UI；自定义；用户档案仪表板;仪表板
title: 目标仪表板
description: Adobe Experience Platform提供了一个仪表板，您可以通过它视图有关组织活动目标的重要信息。
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 1%

---


# （测试版）[!UICONTROL 目标]仪表板

>[!IMPORTANT]
>
>此文档中概述的仪表板功能当前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platform用户界面(UI)提供了一个仪表板，通过它可以视图有关组织活动目标的重要信息，这些信息是在每日快照中捕获的。 本指南概述了如何在UI中访问和使用目标仪表板，并提供了有关仪表板中显示的量度的更多信息。

有关目标的概述，以及Experience Platform中所有可用目标的目录，请访问[目标概述](../../destinations/home.md)。

## [!UICONTROL 目] 标sdashboard数据  {#destinations-dashboard-data}

[!UICONTROL 目标]仪表板显示您的组织在体验用户档案中启用的目标的快照。 快照中的数据与拍摄快照时在特定时间点显示的数据完全一样。 换句话说，快照不是数据的近似值或样本，目标仪表板不会实时更新。

>[!NOTE]
>
>自拍摄快照以来对数据所做的任何更改或更新将不会反映在仪表板中，直到拍摄下一个快照。

## 浏览目标仪表板

要导航到平台UI中的目标仪表板，请在左边栏中选择&#x200B;**[!UICONTROL 目标]**，然后选择&#x200B;**[!UICONTROL 概述]**&#x200B;选项卡以显示仪表板。

![](../images/destinations/dashboard-overview.png)

## 可用构件

Experience Platform提供了多个构件，您可以使用这些构件来可视化与目标相关的不同量度。 选择下面的Widget名称以了解更多信息：

* [[!UICONTROL 最常用的目标]](#most-used-destinations)
* [[!UICONTROL 最近创建的目标]](#recently-created-destinations)
* [[!UICONTROL 最近激活的区段]](#recently-activated-segments)

### [!UICONTROL 最常用的目标] {#most-used-destinations}

**[!UICONTROL 最常用目标]**&#x200B;构件按映射的区段数显示您组织的最佳目标，截止到上次快照。 此排名提供了有关哪些目标正被利用的分析，同时可能还显示可能未充分利用的目标。

例如，如果您昨天配置了目标，但没有将任何区段映射到目标，您将能够看到目标当前未充分利用。

区段计数列中显示的映射区段数与上次每日快照时一致。 将新区段映射到目标将不会更新计数，直到拍摄下一个快照。

从Widget上显示的列表中选择目标的名称将带您进入&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中链接的目标详细信息。 您还可以选择&#x200B;**[!UICONTROL 视图All]**&#x200B;以导航到&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡，然后选择目标名称以视图其详细信息。

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL 最近创建的目标] {#recently-created-destinations}

**[!UICONTROL 最近创建的目标]**&#x200B;构件允许您查看组织最近配置的目标的列表。

显示的创建日期准确到最后一个每日快照。 换句话说，如果您创建了新目标，则直到拍摄下一个快照后，新目标才会显示在列表中。

从Widget上显示的列表中选择目标的名称将带您进入&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中链接的目标详细信息。 您还可以选择&#x200B;**[!UICONTROL 视图All]**&#x200B;以导航到&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡，然后选择目标名称以视图其详细信息。

要了解有关如何配置特定目标类型的更多信息，请访问[目标文档](../../destinations/home.md)。

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 最近激活的区段] {#recently-activated-segments}

**[!UICONTROL 最近激活的区段]**&#x200B;构件提供最近映射到目标的区段的列表。 此列表提供了系统中正在使用哪些区段和目标的快照，并有助于排除任何错误映射。

显示的更新日期显示区段上次激活到目标的时间，并准确到最后的每日快照。 换言之，如果您将区段激活到目标，则更新的日期直到拍摄下一个快照后才会更改。

从构件上显示的列表中选择区段的名称将带您进入区段详细信息。 您还可以选择&#x200B;**[!UICONTROL 视图全部]**&#x200B;导航到区段浏览选项卡，然后选择区段名称以视图其详细信息。

有关在Experience Platform中使用区段的详细信息，请首先阅读[分段服务概述](../../segmentation/home.md)。

![](../images/destinations/recently-activated-segments.png)

## 后续步骤

通过遵循此文档，您现在应该能够找到目标仪表板并了解可用构件中显示的量度。 要了解有关使用Experience Platform中的目标的更多信息，请参阅[目标文档](../../destinations/home.md)。