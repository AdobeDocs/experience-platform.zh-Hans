---
keywords: 量度概述；rtcdp量度概述
title: Real-time Customer Data Platform主页和功能板
description: 仪表板、主页和 Adobe Experience Platform 的首次用户体验
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---

# [!DNL Real-Time Customer Data Platform] 主页和功能板

登录Adobe Real-time Customer Data Platform(Real-Time CDP)时，会显示该主页（其中包含量度功能板）。

主页只是显示量度卡的位置之一。 Real-Time CDP会在您的整个体验中提供量度卡。 这些量度可告知您系统中的数据、用户档案和区段受众。

![image](assets/home.png)

如果您登录Real-Time CDP时系统中没有数据，则主页上的功能板不会显示。 在这种情况下，主页会首次提供用户体验的学习材料。 在收集数据时 — 换言之， <!--sources-->数据集、用户档案、区段和目标被创建并流入系统 — 功能板会自动更新以显示有关该数据的信息<!-- in metric cards-->.

## 主页功能板视图

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

功能板分为<!-- two areas.-->:

* **排行榜** 位于功能板顶部。 排行榜显示系统中的数据集、用户档案、区段和目标的数量。

   ![image](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **近期项目** 列出添加到系统中的五个最新数据集、源、区段和目标。

   ![image](assets/recent.png)

其他量度（例如，用户档案和区段）在Real-time Customer Data Platform的其他部分中可用。

### 数据集

的 **[!UICONTROL 数据集]** 计数器显示系统中数据集的数量和 [!DNL Platform]. 创建数据集时，此计数器会更新。

有关数据集的更多信息，请参阅 [数据集概述](../catalog/datasets/overview.md).

### 用户档案

的 **[!UICONTROL 用户档案]** count显示 [!DNL Real-Time Customer Profile]. 它不包括配置文件片段。 这是您的可寻址受众总数。

此计数使用默认 [合并策略](profile/merge-policies.md) 在统一配置文件的合并策略配置中设置。

每24小时更新一次用户档案数。

有关用户档案的更多信息，请参阅 [在Real-Time CDP中统一了解客户](profile/profile-overview.md).

### 区段

**[!UICONTROL 区段]** 显示为组织创建的区段总数。 此数字会在创建新区段时更新。

有关区段的更多信息，请参阅 [Segmentation Service概述](segmentation/segmentation-overview.md).

### 目标

**[!UICONTROL 目标]** 显示为组织创建的目标总数。 当创建新目标时，此数字会更新。

有关目标的更多信息，请参阅 [目标概述](destinations/overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### 最近的数据集

的 **[!UICONTROL 最近的数据集]** 卡片会显示组织内创建的五个最新数据集。 此列表会在创建新数据集时更新。

选择一个数据集以查看该项目的详细信息，或 **[!UICONTROL 查看全部]** 以查看数据集列表。 从此处，您可以选择特定的来源以了解详细信息。

有关数据集的更多信息，请参阅 [数据集概述](../catalog/datasets/overview.md).

### 最近来源

的 **[!UICONTROL 最近来源]** 量度卡片会显示组织内创建的五个最近的源。 此列表将在创建新源时更新。

选择源以查看该项的详细信息，或 **[!UICONTROL 查看全部]** 查看源列表。 从此处，您可以选择特定的来源以了解详细信息。

有关源的详细信息，请参阅 [源概述](sources/sources-overview.md).

### 近期区段

的 **[!UICONTROL 近期区段]** 量度卡片会显示组织内创建的五个最近的区段。 此列表会在创建新区段时更新。

选择一个区段以查看该项目的详细信息，或 **[!UICONTROL 查看全部]** 以查看有关更多区段的信息。

有关区段的更多信息，请参阅 [Segmentation Service概述](segmentation/segmentation-overview.md).

### 近期目标

的 **[!UICONTROL 近期目标]** 量度卡片会显示组织中创建的五个最近的目标。 创建新目标时，此列表会更新。

选择要查看该项目详细信息的目标，或 **[!UICONTROL 查看全部]** 以查看有关更多目标的信息。

有关目标的更多信息，请参阅 [目标概述](destinations/overview.md).
