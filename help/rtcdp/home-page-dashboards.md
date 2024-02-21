---
keywords: 指标概述； rtcdp指标概述
title: Real-time Customer Data Platform主页和功能板
description: Adobe Experience Platform 的仪表板、主页和首次用户体验
feature: Dashboards, Get Started
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: d052f307d91890f89d6cb3f18525fe395c116f95
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 6%

---

# [!DNL Real-Time Customer Data Platform] 主页

Adobe Real-time Customer Data Platform (Real-Time CDP)主页是登录Real-Time CDP后显示的第一个页面。

Real-Time CDP主页包括一个快速入门小组件，允许您快速访问多项不同功能，以及一个量度部分，其中显示与组织中数据相关的最新信息。

本文档概述了Real-Time CDP主页和量度功能板。

![Platform UI主页。](assets/platform-home/home.png)

## 快速入门小组件

此 [!UICONTROL Real-Time Customer Profile快速入门] 构件分为四个部分：

* **将数据摄取到Platform**：此构件会将您定向到源目录。 使用源目录选择源并摄取数据以Experience Platform。 选择 **[配置源]** 导航到源目录。 欲知更多信息，请参阅 [源概述](../sources/home.md).
* **模型数据结构**：此构件将引导您查看架构概述。 使用架构概述浏览现有架构或创建描述数据结构的Blueprint。 选择 **[!UICONTROL 创建架构]** 导航到架构创建界面。 欲知更多信息，请参阅 [架构概述](../xdm/home.md).
* **构建受众**：此构件会将您定向到UI中的区段生成器。 使用区段生成器可与配置文件数据元素交互并定义区段定义的标准。 选择 **[!UICONTROL 创建受众]** 导航到区段生成器。 欲知更多信息，请参阅 [分段服务概述](../segmentation/home.md).
* **将数据发送到目标**：此构件会将您定向到目标目录。 使用目标目录选择一个目标，然后您可以连接到该目标并将区段发送到该目标。 选择 **[!UICONTROL 设置目标]** 导航到目标目录。 欲知更多信息，请参阅 [目标概述](../destinations/home.md).

![显示入门小组件的Platform UI主页](assets/platform-home/getting-started-widget.png)

## 量度仪表板 {#metrics-dashboard}

>[!CONTEXTUALHELP]
>id="platform_home_metrics_totalProfiles"
>title="配置文件总数"
>abstract="您的组织在 Experience Platform 中拥有的配置文件的总数。此计数基于您组织的合并策略，并且不包括配置文件片段。每 24 小时更新一次配置文件数。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=zh-Hans#profile-count" text="请在文档中了解详情"

量度仪表板可显示有关Experience Platform数据的最新信息。 仪表板分为两个部分：

### 排行榜

排行榜显示贵组织中当前的架构、数据集、用户档案和区段总数及其最近更新日期。

![Platform UI主页中的“排行榜”部分。](assets/platform-home/leaderboard.png)

* **架构总数**：和 **架构总数** 计数器显示系统中的架构数。 此计数器会在创建架构时更新。 欲知更多信息，请参阅 [架构概述](../xdm/home.md).
* **数据集总数**：和 **数据集总数** 计数器显示系统中的数据集数以及Experience Platform中的数据量。 此计数器会在创建数据集时更新。 有关数据集的更多信息，请参阅 [数据集概述](../catalog/datasets/overview.md).
* **配置文件总数**：和 **配置文件** count显示贵组织在Experience Platform内拥有的配置文件总数。 它不包括配置文件片段。 这是您的总可寻址受众。 此计数使用默认值 [合并策略](profile/merge-policies.md) 在实时客户档案的合并策略配置中设置。 每24小时更新一次配置文件数。 选择 **[!UICONTROL 配置文件]** 导航到配置文件概述页面，并查看所有配置文件量度。 有关用户档案的详细信息，请阅读 [Real-time Customer Profile概述](../profile/home.md).
* **受众总数**：和 **受众总数** 计数器显示为您的组织创建的受众总数。 此数字将在创建新受众时更新。 有关受众的详细信息，请参阅 [分段服务概述](../segmentation/home.md).

### 最近项目

“最近项目”列出组织中最近的更改。 在以下示例中，最近的更改与数据集、源、区段和目标有关。

![Platform UI主页中的“最近项目”部分。](assets/platform-home/recent-items.png)

* **最近数据集**：和 **[!UICONTROL 最近数据集]** 信息卡显示了在组织内创建的五个最新数据集。 此列表会在创建新数据集时更新。 选择一个数据集以查看该项目的详细信息，或选择 **[!UICONTROL 查看全部]** 以获取数据集列表。 从该位置，您可以选择特定源以了解详细信息。 有关数据集的更多信息，请参见 [数据集概述](../catalog/datasets/overview.md).
* **最近的源**：和 **[!UICONTROL 最近的源]** 量度卡显示组织中最近创建的五个源。 此列表会在创建新源时更新。 选择源以查看该项目的详细信息，或选择 **[!UICONTROL 查看全部]** 获取源列表。 从该位置，您可以选择特定源以了解详细信息。 有关源的详细信息，请参阅 [源概述](../sources/home.md).
* **最近的区段**：和 **[!UICONTROL 最近的区段]** 量度卡显示组织中最近创建的五个区段。 此列表会在创建新区段时更新。 选择区段以查看该项目的详细信息，或选择 **[!UICONTROL 查看全部]** 以获取区段的列表。 有关区段的更多信息，请参阅 [分段服务概述](../segmentation/home.md).
* **最近的目标**：和 **[!UICONTROL 最近的目标]** 量度卡显示组织内创建的五个最新目标。 此列表会在创建新目标时更新。 选择一个目标以查看该项目的详细信息，或选择 **[!UICONTROL 查看全部]** 以获取目标列表。 欲知更多信息，请参阅 [目标概述](../destinations/home.md).

## 资源

最后，资源小组件提供了您可以参考的其他文档资源。 其中包括：

![Platform UI主页中的“资源”部分。](assets/platform-home/resources.png)

* [了解架构](../xdm/schema/composition.md)
* [连接源](../sources/home.md)
* [如何填充Real-Time Customer Profile](../profile/home.md)
* [连接目标](../destinations/home.md)
* [管理访问权限](../access-control/abac/overview.md)

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
