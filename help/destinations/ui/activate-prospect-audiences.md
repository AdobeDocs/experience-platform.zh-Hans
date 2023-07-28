---
title: 将目标受众激活到目标
type: Tutorial
hide: true
hidefromtoc: true
description: 了解如何将潜在客户受众激活到目标
source-git-commit: e04d7a3cd75f4e61329a2de8ca5ddcc4d9518a57
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# 激活目标客户受众

>[!AVAILABILITY]
>
>已购买Real-Time CDP Prime和Ultimate包的客户可以使用此功能。 有关更多信息，请与您的Adobe代表联系。

本文介绍了导出所需的工作流 [潜在客户受众](/help/segmentation/ui/prospect-audience.md) 从Adobe Experience Platform到您的首选目标。

## 支持的目标 {#supported-destinations}

转到 **[!UICONTROL 连接]** > **[!UICONTROL 目标]**，然后选择 **[!UICONTROL 目录]** 选项卡。 使用 **[!UICONTROL 数据类型]** 筛选并选择 **[!UICONTROL 潜在客户]** 查看支持激活潜在客户受众的目标。 目前，导出潜在客户受众仅适用于 [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) 目标。

![支持数据集导出的目标](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

## 先决条件 {#prerequisites}

* 您必须先摄取 [目标客户配置文件](/help/profile/ui/prospect-profile.md) 和创建 [潜在客户受众](/help/segmentation/ui/prospect-audience.md) 才能将其激活到下游目标。
* 要将潜在客户受众激活到目标，您必须已成功连接到目标。 如果您尚未这样做，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。 阅读有关的UI教程 [连接到目标](./connect-destination.md) 以了解更多信息。

### 所需权限 {#permissions}

要激活潜在客户受众，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

要确保您具有激活潜在客户受众的必要权限，请浏览目标目录。 如果目标具有 **[!UICONTROL 激活]** 则您具有相应的权限。

## 选择您的目标 {#select-destination}

按照相关说明选择一个可导出数据集的目标：

1. 转到 **[!UICONTROL “连接”>“目标”]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![突出显示目录控件的目标目录选项卡。](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

2. 选择 **[!UICONTROL 激活]** 在与要将数据集导出到的目标对应的卡上。

>[!TIP]
>
>可导出配置文件受众的目标在卡片的右上角有一个图标，类似于下面高亮显示的目标，或者，您可以使用数据类型过滤器仅显示可导出目标受众的目标，如 [显示在页面上的较高位置](#supported-destinations).

![可导出突出显示的配置文件受众的Amazon S3目标页面。](/help/destinations/assets/ui/activate-prospect-audiences/amazon-s3-icon-activate-prospect-audiences.png)

1. 选择 **[!UICONTROL 数据类型潜在客户]**，然后选择要将数据集导出到的目标连接，然后选择 **[!UICONTROL 下一个]**.

>[!TIP]
> 
>如果要设置新目标以激活目标客户受众，请选择 **[!UICONTROL 配置新目标]** 以触发 [连接到目标](/help/destinations/ui/connect-destination.md) 工作流。

![突出显示具有潜在客户控件的目标激活工作流。](/help/destinations/assets/ui/activate-prospect-audiences/activate-prospects-highlighted.png)

1. 继续下一节以 [选择您的配置文件受众](#select-profile-audiences) 以导出。

## 选择您的目标客户受众 {#select-prospect-audiences}

使用潜在客户受众名称左侧的复选框选择要导出到目标的受众，然后选择 **[!UICONTROL 下一个]**. 请注意，此视图中只显示目标客户受众，不显示其他受众。

![数据集导出工作流显示了“选择受众”步骤，您可以在该步骤中选择要导出的目标客户受众。](/help/destinations/assets/ui/activate-prospect-audiences/select-prospect-audiences.png)

## 计划和后续步骤

在激活工作流的其余部分以导出潜在客户受众时，请阅读有关将数据激活到基于文件的目标的教程。 继续从 [计划受众导出步骤](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).

>[!NOTE]
>
>请注意，在计划步骤中，激活目标客户受众的工作流仅允许您 [导出完整文件](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). 不支持增量文件导出。

<!--

Note that we will need to add links to other destination types here as more destinations become supported 

-->