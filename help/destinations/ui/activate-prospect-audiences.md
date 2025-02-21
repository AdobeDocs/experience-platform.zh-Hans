---
title: 将目标受众激活到目标
type: Tutorial
description: 了解如何将潜在客户受众激活到目标
exl-id: 3e034a14-09d0-4b08-b171-5afb62ae4b62
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 16%

---

# 激活潜在客户受众

>[!AVAILABILITY]
>
>已购买Real-Time CDP Prime和Ultimate包的客户可以使用此功能。 有关更多信息，请与Adobe代表联系。

本文介绍了将[潜在受众](/help/segmentation/types/prospect-audiences.md)从Adobe Experience Platform导出到您的首选目标所需的工作流。

## 支持的目标 {#supported-destinations}

转到&#x200B;**[!UICONTROL 连接]** > **[!UICONTROL 目标]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。 使用&#x200B;**[!UICONTROL 数据类型]**&#x200B;筛选器并选择&#x200B;**[!UICONTROL 潜在客户]**&#x200B;查看支持激活潜在客户受众的目标。 目前，导出潜在客户受众仅适用于云存储目标。

![支持潜在客户受众的目标。](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## 先决条件 {#prerequisites}

* 必须先摄取[潜在客户配置文件](/help/profile/ui/prospect-profile.md)并创建[潜在客户受众](/help/segmentation/types/prospect-audiences.md)，然后才能将其激活到下游目标。
* 要将潜在客户受众激活到目标，您必须已成功连接到目标。 如果您尚未这样做，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，然后配置要使用的目标。 有关详细信息，请阅读有关[连接到目标](./connect-destination.md)的用户界面教程。

### 所需的权限 {#permissions}

若要激活潜在客户受众，您需要&#x200B;**[!UICONTROL 查看目标]**&#x200B;和&#x200B;**[!UICONTROL 激活目标]** [访问控制权限](/help/access-control/home.md#permissions)。 阅读[访问控制概述](/help/access-control/ui/overview.md)或联系您的产品管理员以获取所需的权限。

要确保您具有激活潜在客户受众的必要权限，请浏览目标目录。 如果目标具有&#x200B;**[!UICONTROL 激活]**&#x200B;控件，则您具有相应的权限。

## 选择您的目标 {#select-destination}

按照相关说明选择一个可导出数据集的目标：

1. 转到&#x200B;**[!UICONTROL 连接>目标]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。

   ![目录控件突出显示的目标目录选项卡。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. 在与要将数据集导出到的目标对应的卡片上，选择&#x200B;**[!UICONTROL 激活]**。

>[!TIP]
>
>可导出配置文件受众的目标在卡片的右上角以图标指示，类似于下面高亮显示的目标，或者，您可以使用数据类型筛选器仅显示可导出目标受众的目标，如页面上较高位置显示的[](#supported-destinations)。

![可导出突出显示的配置文件受众的Amazon S3目标页面。](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. 选择&#x200B;**[!UICONTROL 数据类型Prospects]**，然后选择要将数据集导出到的目标连接，然后选择&#x200B;**[!UICONTROL 下一步]**。

>[!TIP]
> 
>如果要设置新目标以激活目标受众，请选择&#x200B;**[!UICONTROL 配置新目标]**&#x200B;以触发[连接到目标](/help/destinations/ui/connect-destination.md)工作流。

![目标激活工作流中突出显示了潜在客户控件。](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. 继续到[选择要导出的配置文件受众](#select-profile-audiences)的下一部分。

## 选择您的目标客户受众 {#select-prospect-audiences}

使用潜在客户受众名称左侧的复选框选择要导出到目标的受众，然后选择&#x200B;**[!UICONTROL 下一步]**。 请注意，此视图中只显示目标客户受众，不显示其他受众。

![数据集导出工作流显示“选择受众”步骤，您可以在该步骤中选择要导出的潜在客户受众。](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## 计划和后续步骤

在激活工作流的其余部分以导出潜在客户受众时，请阅读有关将数据激活到基于文件的目标的教程。 从[计划受众导出步骤](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)继续。

>[!NOTE]
>
>请注意，在计划步骤中，激活目标客户受众的工作流仅允许您[导出完整文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)。 不支持增量文件导出。

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->

## 由合作伙伴数据支持实现的其他用例 {#other-use-cases}

探索通过 Real-Time CDP 中的合作伙伴数据支持实现的更多用例：

* [用受信任的数据合作伙伴提供的属性补充第一方轮廓](/help/rtcdp/partner-data/supplement-first-party-profiles.md)，以改善您的数据基础、了解客户群的新情况并获得更好的受众优化。
* 使用 Real-Time CDP 中的第三方数据支持，[通过数据合作伙伴提供的潜在客户轮廓扩充您的轮廓基础并与其交流以获取或接触新客户](/help/rtcdp/partner-data/prospecting.md)。
* [](/help/rtcdp/partner-data/onsite-personalization.md)利用合作伙伴辅助的认可在访问期间提供个性化现场体验，而无需用户进行身份验证或之前使用过您的品牌。
