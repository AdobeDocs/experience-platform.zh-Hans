---
keywords: 激活配置文件请求目标；激活数据；配置文件请求目标
title: 将受众数据激活到配置文件请求目标
type: Tutorial
description: 了解如何通过将区段映射到配置文件请求目标来激活您在Adobe Experience Platform中的受众数据。
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: f771cf0c9ea692ad02cf987608b3710772712d54
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 4%

---

# 将受众数据激活到配置文件请求目标

>[!IMPORTANT]
> 
> * 要激活数据并启用 [映射步骤](#mapping) 的工作流，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
> * 要激活数据，而不通过 [映射步骤](#mapping) 的工作流，您需要 **[!UICONTROL 管理目标]**， **[!UICONTROL 激活没有映射的区段]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions).
> 
> 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。

## 概述 {#overview}

本文介绍了在Adobe Experience Platform配置文件请求目标中激活受众数据所需的工作流。 当与一起使用时 [边缘分割](../../segmentation/ui/edge-segmentation.md)，这些目标在您的Web和移动资产上启用同页和下一页个性化用例。 详细了解 [启用同页和下一页个性化用例](/help/destinations/ui/configure-personalization-destinations.md).

配置文件请求目标示例包括 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化](../../destinations/catalog/personalization/custom-personalization.md) 连接。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成功 [已连接到目标](./connect-destination.md). 如果您尚未这样做，请转到 [目标目录](../catalog/overview.md)，浏览支持的个性化目标，并配置要使用的目标。

### 区段合并策略 {#merge-policy}

目前，配置文件请求目标仅支持激活使用 [Active-on-Edge合并策略](../../segmentation/ui/segment-builder.md#merge-policies) 设置为默认值。

## 选择您的目标 {#select-destination}

1. 转到 **[!UICONTROL 连接>目标]**，并选择 **[!UICONTROL 目录]** 选项卡。

   ![“目标目录”选项卡](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 选择 **[!UICONTROL 激活区段]** ，位于要激活区段的个性化目标对应的卡片上，如下图所示。

   ![激活按钮](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 选择要用于激活区段的目标连接，然后选择 **[!UICONTROL 下一个]**.

   ![选择目标](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 移到下一部分以 [选择您的区段](#select-segments).

## 选择您的区段 {#select-segments}

使用区段名称左侧的复选框可选择要激活到目标的区段，然后选择 **[!UICONTROL 下一个]**.

![选择区段](../assets/ui/activate-profile-request-destinations/select-segments.png)

## （测试版）映射属性 {#map-attributes}

>[!IMPORTANT]
>
>映射步骤，用于启用基于属性的个性化 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [通用个性化目标](/help/destinations/catalog/personalization/custom-personalization.md)，目前为测试版，您的组织可能还无法访问。 此文档可能会发生更改。

选择要为用户启用个性化用例的属性。 这意味着，如果属性的值发生更改或将属性添加到用户档案，则该用户档案将成为区段的成员，并将激活到个性化目标。

添加属性是可选的，您仍然可以继续下一步并在不选择属性的情况下启用同页和下一页个性化。 如果您未在此步骤中添加任何属性，则仍会根据用户档案的区段成员资格和身份映射资格进行个性化。

![显示选择了属性的映射步骤的图像](../assets/ui/activate-profile-request-destinations/mapping-step.png)

### 选择源属性 {#select-source-attributes}

要添加源属性，请选择 **[!UICONTROL 添加新字段]** 控制 **[!UICONTROL 源字段]** 列并搜索或导航到所需的XDM属性字段，如下所示。

![显示如何在映射步骤中选择目标属性的屏幕录制](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

### 选择目标属性 {#select-target-attributes}

>[!NOTE]
>
>某些目标要求您仅选择源属性，而其他目标同时要求源属性和目标属性。
>
>目前， [Adobe Target V2](../catalog/personalization/adobe-target-connection.md) 目标仅需要源属性，而 [使用属性进行自定义个性化](../catalog/personalization/custom-personalization.md) 需要源属性和目标属性。

要添加目标属性，请选择 **[!UICONTROL 添加新字段]** 控制 **[!UICONTROL 目标字段]** 列并键入要映射源属性的自定义属性名称。

![显示如何在映射步骤中选择XDM属性的屏幕录制](../assets/ui/activate-profile-request-destinations/mapping-step-select-target-attribute.gif)

## 计划区段导出 {#scheduling}

默认情况下， [!UICONTROL 区段计划] 页面仅显示您在当前激活流程中选择的新选择区段。

![新区段](../assets/ui/activate-profile-request-destinations/new-segments.png)

要查看激活到目标的所有区段，请使用筛选选项并禁用 **[!UICONTROL 仅显示新区段]** 筛选条件。

![所有区段](../assets/ui/activate-profile-request-destinations/all-segments.png)

在 **[!UICONTROL 区段计划]** 页面中，选择每个区段，然后使用 **[!UICONTROL 开始日期]** 和 **[!UICONTROL 结束日期]** 选择器，用于配置将数据发送到目标的时间间隔。

![区段计划](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

选择 **[!UICONTROL 下一个]** 以转到 [!UICONTROL 审核] 页面。

## 请查看 {#review}

在 **[!UICONTROL 审核]** 页面时，您可以看到所选内容的摘要。 选择 **[!UICONTROL 取消]** 来打破气流， **[!UICONTROL 返回]** 修改设置，或者 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

![审核步骤中的选择摘要。](../assets/ui/activate-profile-request-destinations/review.png)

### 同意政策评估 {#consent-policy-evaluation}

如果您的组织购买了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，请选择&#x200B;**[!UICONTROL 查看适用的同意策略]**&#x200B;以查看应用了哪些同意策略以及作为其结果包含在激活中的配置文件数量。阅读关于 [同意政策评估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 了解更多信息。

### 数据使用策略检查 {#data-usage-policy-checks}

在 **[!UICONTROL 审核]** 步骤，Experience Platform还会检查是否存在任何数据使用策略违规。 下面显示了一个违反策略的示例。 在解决违规之前，无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅 [数据使用策略违规](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) 在数据治理文档部分中。

![数据策略违规](../assets/common/data-policy-violation.png)

### 过滤区段 {#filter-segments}

此外，在此步骤中，您可以使用页面上的可用过滤器仅显示其计划或映射已作为此工作流的一部分更新的区段。 您还可以切换要查看的表列。

![屏幕录制，其中显示审核步骤中的可用区段过滤器。](/help/destinations/assets/ui/activate-profile-request-destinations/filter-segments-review-step.gif)

如果您对您的选择感到满意，并且未检测到违反策略的情况，请选择 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->