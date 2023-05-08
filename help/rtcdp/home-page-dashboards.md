---
keywords: 量度概述；rtcdp量度概述
title: Real-time Customer Data Platform主页和功能板
description: Adobe Experience Platform 的仪表板、主页和首次用户体验
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 8ea657e379248616d3140bc0a7b0c25a918bc857
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] 主页

Adobe Real-time Customer Data Platform(Real-Time CDP)主页是登录到Real-Time CDP后显示的首页。

Real-Time CDP主页包含一个快速入门小组件，通过该小组件，您可以快速访问多个不同的功能，还包含一个量度部分，该部分显示有关您组织内数据的最新信息。

本文档概述了Real-Time CDP主页和量度功能板。

![平台UI主页。](assets/platform-home/home.png)

## 入门小组件

的 [!UICONTROL 实时客户资料快速入门] 小组件分为四个部分：

* **将数据摄取到平台**:此小组件将引导您访问源目录。 使用源目录选择源并摄取数据以Experience Platform。 有关更多信息，请阅读 [源概述](../sources/home.md)
* **模型数据结构**:此小组件将引导您查看架构概述。 使用架构概述可浏览现有架构或创建描述数据结构的构建块。 有关更多信息，请阅读 [架构概述](../xdm/home.md).
* **区段受众**:此小组件将引导您访问 [!DNL Segment Builder] 中。 使用 [!DNL Segment Builder] 与用户档案数据元素交互并定义区段规则。 有关更多信息，请阅读 [Segmentation Service概述](../segmentation/home.md).
* **将数据发送到目标**:此小组件将引导您访问目标目录。 使用目标目录选择一个目标，然后您可以将其连接到并将区段发送到该目标。 有关更多信息，请阅读 [目标概述](../destinations/home.md)

![Platform UI主页，显示入门小组件](assets/platform-home/getting-started-widget.png)

## 量度功能板

量度功能板显示有关您的Experience Platform数据的最新信息。 功能板分为两个部分：

### 排行榜

排行榜显示了您组织中当前的架构、数据集、用户档案和区段总数，以及其最新更新日期。

![平台UI主页中的列表板部分。](assets/platform-home/leaderboard.png)

* **总架构**:的 **总架构** 计数器显示系统中的架构数。 创建架构时，此计数器会更新。 有关更多信息，请阅读 [架构概述](../xdm/home.md).
* **数据集总数**:的 **数据集总数** 计数器显示系统中数据集的数量和 [!DNL Platform]. 创建数据集时，此计数器会更新。 有关数据集的更多信息，请阅读 [数据集概述](../catalog/datasets/overview.md).
* **用户档案总数**:的 **用户档案** count显示 [!DNL Real-Time Customer Profile]. 它不包括配置文件片段。 这是您的可寻址受众总数。 此计数使用默认 [合并策略](profile/merge-policies.md) 在统一配置文件的合并策略配置中设置。 每24小时更新一次用户档案数。 有关用户档案的更多信息，请阅读 [实时客户资料概述](../profile/home.md).
* **总区段**: **区段** 显示为组织创建的区段总数。 此数字会在创建新区段时更新。 有关区段的更多信息，请阅读 [Segmentation Service概述](../segmentation/home.md).

### 近期项目

最近的项目列出了您组织中最近的更改。 在以下示例中，最近的更改与数据集、源、区段和目标有关。

![Platform UI主页中的“最近的项目”部分。](assets/platform-home/recent-items.png)

* **最近的数据集**:的 **[!UICONTROL 最近的数据集]** 卡片会显示组织内创建的五个最新数据集。 此列表会在创建新数据集时更新。 选择一个数据集以查看该项目的详细信息，或选择 **[!UICONTROL 查看全部]** 数据集列表。 从此处，您可以选择特定的来源以了解详细信息。 有关数据集的更多信息，请参阅 [数据集概述](../catalog/datasets/overview.md).
* **最近来源**:的 **[!UICONTROL 最近来源]** 量度卡片会显示组织内创建的五个最近的源。 此列表将在创建新源时更新。 选择源以查看该项的详细信息，或选择 **[!UICONTROL 查看全部]** 来源列表。 从此处，您可以选择特定的来源以了解详细信息。 有关源的详细信息，请参阅 [源概述](../sources/home.md).
* **近期区段**:的 **[!UICONTROL 近期区段]** 量度卡片会显示组织内创建的五个最近的区段。 此列表会在创建新区段时更新。 选择一个区段以查看该项目的详细信息，或选择 **[!UICONTROL 查看全部]** ，以查看区段列表。 有关区段的更多信息，请参阅 [Segmentation Service概述](../segmentation/home.md).
* **近期目标**:的 **[!UICONTROL 近期目标]** 量度卡片会显示组织中创建的五个最近的目标。 创建新目标时，此列表会更新。 选择要查看该项目详细信息的目标，或选择 **[!UICONTROL 查看全部]** 以查看目标列表。 有关更多信息，请阅读 [目标概述](../destinations/home.md).

## 资源

最后，资源小组件会为您提供可参考的其他文档资源。 其中包括：

![平台UI主页中的“资源”部分。](assets/platform-home/resources.png)

* [了解模式](../xdm/schema/composition.md)
* [连接源](../sources/home.md)
* [如何填充实时客户用户档案](../profile/home.md)
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
