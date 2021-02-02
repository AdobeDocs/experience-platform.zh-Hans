---
keywords: 指标概述；rtcdp度量概述
title: 实时客户数据平台主页和仪表板
seo-title: 实时客户数据平台主页和仪表板
description: 仪表板、主页和 Adobe Experience Platform 的首次用户体验
seo-description: 仪表板、主页和 Adobe Experience Platform 的首次用户体验
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 4%

---


# [!DNL Real-time Customer Data Platform] 度量概述

实时客户数据平台(Real-time CDP)主页，在您登录到实时CDP时，会显示该仪表板，其中包括一个指标。

主页只是显示度量卡的位置之一。 实时CDP在您的整个体验中提供度量卡。 这些指标会通知您系统中的数据、用户档案和细分受众。

![image](assets/home.png)

如果登录到实时CDP时系统中没有仪表板，则不会显示主页上的数据。 在这种情况下，主页首次为用户提供学习材料。 在收集数据时——换言之，作为<!--sources-->数据集、用户档案、段和目标被创建并且数据流入系统时—仪表板会自动更新以显示有关该数据的信息。<!-- in metric cards-->

## 主页仪表板视图

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

仪表板分为<!-- two areas.-->:

* **领** 导人在仪表板的顶端。排行榜显示系统中的数据集、用户档案、细分和目标数。

   ![图像](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **最近** 的项目列出了添加到系统的5个最新数据集、源、细分和目标。

   ![图像](assets/recent.png)

其他指标(例如用户档案和细分)在实时客户数据平台的其他部分提供。

### 数据集

**[!UICONTROL 数据集]**&#x200B;计数器显示系统中的数据集数和[!DNL Platform]中的数据量。 创建数据集时更新此计数器。

有关数据集的详细信息，请参阅[数据集概述](../catalog/datasets/overview.md)。

### 配置文件

**[!UICONTROL 用户档案数]**&#x200B;显示具有[!DNL Real-time Customer Profile]中用户档案的总人数。 它不包含用户档案片段。 这是您的可寻址受众。

此计数使用在“统一”用户档案的合并策略配置中设置的默认[合并策略](profile/merge-policies.md)。

每24小时更新一次用户档案数。

有关用户档案的详细信息，请参见[实时CDP中客户的统一视图](profile/profile-overview.md)。

### 区段

**[!UICONTROL 段]** 显示为组织创建的段总数。此编号在创建新区段时更新。

有关区段的详细信息，请参阅[分段服务概述](segmentation/segmentation-overview.md)。

### 目标

**[!UICONTROL 目]** 标显示为组织创建的目标总数。此编号在创建新目标时更新。

有关目标的详细信息，请参阅[目标概述](destinations/overview.md)。

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### 最近的数据集

**[!UICONTROL 最近的数据集]**&#x200B;卡显示组织内创建的五个最近的数据集。 此列表在创建新数据集时更新。

选择一个视图集以视图该项的详细信息，或选择&#x200B;**[!UICONTROL all]**&#x200B;以查看数据集的列表。 从此处，您可以选择特定的源来获取详细信息。

有关数据集的详细信息，请参阅[数据集概述](../catalog/datasets/overview.md)。

### 近期来源

**[!UICONTROL 最近源]**&#x200B;度量卡显示组织内创建的五个最近源。 此列表在创建新源时更新。

选择源以视图该项的详细信息，或&#x200B;**[!UICONTROL 视图all]**&#x200B;以查看源的列表。 从此处，您可以选择特定的源来获取详细信息。

有关源的详细信息，请参阅[源概述](sources/sources-overview.md)。

### 近期细分

**[!UICONTROL 最近区段]**&#x200B;度量卡显示组织内创建的五个最近区段。 此列表会在创建新区段时更新。

选择一个区段以视图该项的详细信息，或&#x200B;**[!UICONTROL 视图all]**&#x200B;以查看有关更多区段的信息。

有关区段的详细信息，请参阅[分段服务概述](segmentation/segmentation-overview.md)。

### 近期目标

**[!UICONTROL 最近目标]**&#x200B;度量卡显示组织内创建的五个最近目标。 此列表在创建新目标时更新。

选择一个目标以视图该项目的详细信息，或选择&#x200B;**[!UICONTROL 视图all]**&#x200B;以查看有关更多目标的信息。

有关目标的详细信息，请参阅[目标概述](destinations/overview.md)。
