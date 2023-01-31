---
keywords: 激活用户档案请求目标；激活数据；用户档案请求目标
title: 将受众数据激活到用户档案请求目标
type: Tutorial
description: 了解如何通过将区段映射到配置文件请求目标，来激活您在Adobe Experience Platform中拥有的受众数据。
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 9bde403338187409892d76de68805535de03d59f
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# 将受众数据激活到用户档案请求目标

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

## 概述 {#overview}

本文介绍在Adobe Experience Platform用户档案请求目标中激活受众数据所需的工作流。 与一起使用时 [边缘分割](../../segmentation/ui/edge-segmentation.md)，则这些目标可以在您的Web属性上启用同页和下一页个性化用例。 有关更多信息 [启用同页和下一页个性化用例](/help/destinations/ui/configure-personalization-destinations.md).

用户档案请求目标示例包括 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化](../../destinations/catalog/personalization/custom-personalization.md) 连接。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须成功 [连接到目标](./connect-destination.md). 如果您尚未执行此操作，请转到 [目标目录](../catalog/overview.md)，浏览支持的个性化目标，并配置要使用的目标。

### 区段合并策略 {#merge-policy}

目前，配置文件请求目标仅支持激活使用 [边缘活动合并策略](../../segmentation/ui/segment-builder.md#merge-policies) 设置为默认值。

## 选择您的目标 {#select-destination}

1. 转到 **[!UICONTROL 连接>目标]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![“目标目录”选项卡](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 选择 **[!UICONTROL 激活区段]** 在与您要在其中激活区段的个性化目标对应的卡片上，如下图所示。

   ![激活按钮](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 选择要用于激活区段的目标连接，然后选择 **[!UICONTROL 下一个]**.

   ![选择目标](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 移到下一个部分 [选择区段](#select-segments).

## 选择您的区段 {#select-segments}

使用区段名称左侧的复选框选择要激活到目标的区段，然后选择 **[!UICONTROL 下一个]**.

![选择区段](../assets/ui/activate-profile-request-destinations/select-segments.png)

## （测试版）地图属性 {#map-attributes}

>[!IMPORTANT]
>
>映射步骤，该步骤可为 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [通用个性化目标](/help/destinations/catalog/personalization/custom-personalization.md)，当前为测试版，且贵组织可能尚未访问该测试版。 本文档可能会发生更改。

选择要根据为用户启用个性化用例的属性。 这意味着，如果属性的值发生更改或将属性添加到配置文件，则该配置文件将成为区段的成员并将激活到个性化目标。

添加属性是可选的，您仍然可以继续执行下一步，并在不选择属性的情况下启用同页和下一页个性化。 如果此步骤中未添加任何属性，则仍会根据用户档案的区段成员资格和身份映射资格进行个性化。

![显示已选择属性的映射步骤的图像](../assets/ui/activate-profile-request-destinations/mapping-step.png)

### 选择源属性 {#select-source-attributes}

要添加源属性，请选择 **[!UICONTROL 添加新字段]** 控制 **[!UICONTROL 源字段]** 列，并搜索或导航到所需的XDM属性字段，如下所示。

![显示如何在映射步骤中选择目标属性的屏幕记录](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

### 选择目标属性 {#select-target-attributes}

>[!NOTE]
>
>某些目标要求您仅选择源属性，而其他目标则要求同时使用源属性和目标属性。
>
>目前， [Adobe Target V2](../catalog/personalization/adobe-target-connection.md) 目标仅需要源属性，而 [具有属性的自定义个性化](../catalog/personalization/custom-personalization.md) 同时需要源属性和目标属性。

要添加目标属性，请选择 **[!UICONTROL 添加新字段]** 控制 **[!UICONTROL 目标字段]** 列，然后键入要将源属性映射到的自定义属性名称。

![显示如何在映射步骤中选择XDM属性的屏幕记录](../assets/ui/activate-profile-request-destinations/mapping-step-select-target-attribute.gif)

## 计划区段导出 {#scheduling}

默认情况下， [!UICONTROL 区段计划] 页面仅显示您在当前激活流程中选择的新选定区段。

![新区段](../assets/ui/activate-profile-request-destinations/new-segments.png)

要查看激活到您的目标的所有区段，请使用筛选选项并禁用 **[!UICONTROL 仅显示新区段]** 过滤器。

![所有区段](../assets/ui/activate-profile-request-destinations/all-segments.png)

在 **[!UICONTROL 区段计划]** ，选择每个区段，然后使用 **[!UICONTROL 开始日期]** 和 **[!UICONTROL 结束日期]** 选择器来配置向目标发送数据的时间间隔。

![区段计划](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

选择 **[!UICONTROL 下一个]** 转到 [!UICONTROL 审阅] 页面。

## 请查看 {#review}

在 **[!UICONTROL 审阅]** 页面，则可以查看所选内容的摘要。 选择 **[!UICONTROL 取消]** 来分解流量， **[!UICONTROL 返回]** 修改设置，或 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

![审阅步骤中的选择摘要。](../assets/ui/activate-profile-request-destinations/review.png)

### 同意策略评估 {#consent-policy-evaluation}

如果贵组织已购买 **Adobe医疗保健盾** 或 **Adobe隐私和安全防护**，选择 **[!UICONTROL 查看适用的同意策略]** 以了解应用了哪些同意策略以及激活中包含了多少个用户档案。 了解 [同意策略评估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 以了解更多信息。

### 数据使用策略检查 {#data-usage-policy-checks}

在 **[!UICONTROL 审阅]** 步骤中，Experience Platform还会检查是否存在任何数据使用策略违规。 下面显示了违反策略的示例。 在解决违规之前，无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅 [数据使用策略违规](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) 在“数据管理文档”一节中。

![数据策略违规](../assets/common/data-policy-violation.png)

### 过滤区段 {#filter-segments}

此外，在此步骤中，您还可以使用页面上的可用过滤器来仅显示计划或映射已作为此工作流的一部分进行更新的区段。 您还可以切换要查看的表列。

![屏幕记录，其中显示了审阅步骤中可用的区段过滤器。](/help/destinations/assets/ui/activate-profile-request-destinations/filter-segments-review-step.gif)

如果您对您的选择满意，并且未检测到任何策略违规，请选择 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->