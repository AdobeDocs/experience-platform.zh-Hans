---
title: 实时客户数据平台主页和仪表板
seo-title: 实时客户数据平台主页和仪表板
description: Adobe Experience Platform的仪表板、主页和首次用户体验
seo-description: Adobe Experience Platform的仪表板、主页和首次用户体验
translation-type: tm+mt
source-git-commit: 6c8d0757d7e7568b1976823d9c52221374e67cbb

---


# 实时客户数据平台指标概述

Adobe实时客户数据平台（实时CDP）主页在您登录实时CDP时显示，该主页包含一个指标仪表板。

主页仅是显示度量卡的位置之一。 实时CDP在整个体验中提供度量卡。 这些指标会通知您系统中的数据、档案和细分受众。

![image](assets/home2.jpg)

如果登录到实时CDP时系统中没有数据，则主页上的仪表板不显示。 在这种情况下，主页会为首次用户体验提供学习材料。 在收集数据时（即，创建数据集、配置文件、区段和目标并将数据流入系统时），仪表板会自动更新以显示有关该数据的信息 <!--sources--><!-- in metric cards-->。

## 主页功能板视图

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

功能板分为<!-- two areas.-->:

* **排行榜** ，位于仪表板的顶部。 排行榜显示系统中的数据集、配置文件、区段和目标数量。

   ![image](assets/home-leaderboard2.jpg)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **最近的项目** ，列出了添加到系统的五个最新数据集、源、区段和目标。

   ![image](assets/home-recent.jpg)

实时客户数据平台的其他部分提供了其他指标，例如档案和细分。

### 数据集

计数 **[!UICONTROL Datasets]** 器显示系统中数据集的数量和平台中的数据量。 此计数器在创建数据集时更新。

有关数据集的更多信息，请参 [阅将数据引入Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md)。

### 配置文件

该 **[!UICONTROL Profiles]** 计数显示实时客户档案中具有档案的总人数。 它不包括配置文件片段。 这是您可接触的总受众。

此计数使用在统一配 [置文件中](profile/merge-policies.md) ，合并策略配置中设置的默认合并策略。

每24小时更新一次配置文件数。

有关客户档案的更多信息， [请参阅实时CDP中统一的客户视图](profile/profile-overview.md)。

### 区段

**[!UICONTROL Segments]** 显示为组织创建的区段总数。 此编号在创建新区段时更新。

有关区段的详细信息，请参阅 [分段服务概述](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)。

### 目标

**[!UICONTROL Destinations]** 显示为组织创建的目标总数。 此编号在创建新目标时更新。

有关目标的详细信息，请参阅目 [标概述](destinations/destinations-overview.md)。

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Click **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Click **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Click **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### 最近的数据集

卡片 **[!UICONTROL Recent datasets]** 中显示了组织内创建的五个最近的数据集。 此列表在创建新数据集时更新。

单击数据集可查看该项目的详细信息，或 **[!UICONTROL View all]** 查看数据集列表。 在此处，您可以单击特定源以获取详细信息。

有关数据集的更多信息，请参 [阅将数据引入Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md)。

### 近期来源

度 **[!UICONTROL Recent sources]** 量卡显示在组织内创建的五个最近的源。 此列表在创建新源时更新。

单击源可查看该项目的详细信息，或 **[!UICONTROL View all]** 查看源列表。 在此处，您可以单击特定源以获取详细信息。

有关源的详细信息，请参阅 [源概述](sources/sources-overview.md)。

### 近期细分

度 **[!UICONTROL Recent segments]** 量卡显示组织内创建的五个最近的区段。 此列表在创建新区段时更新。

单击区段可查看该项目的详细信息，或查 **[!UICONTROL View all]** 看有关更多区段的信息。

有关区段的详细信息，请参阅 [分段服务概述](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)。

### 近期目标

度 **[!UICONTROL Recent destinations]** 量卡显示组织内创建的五个最近的目标。 此列表在创建新目标时更新。

单击目标可查看该项目的详细信息，或查 **[!UICONTROL View all]** 看有关更多目标的信息。

有关目标的详细信息，请参阅目 [标概述](destinations/destinations-overview.md)。
