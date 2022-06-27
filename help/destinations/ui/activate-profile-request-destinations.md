---
keywords: 激活用户档案请求目标；激活数据；用户档案请求目标
title: 将受众数据激活到用户档案请求目标
type: Tutorial
description: 了解如何通过将区段映射到配置文件请求目标，来激活您在Adobe Experience Platform中拥有的受众数据。
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 将受众数据激活到用户档案请求目标

>[!IMPORTANT]
> 
>要激活数据，您需要 **[!UICONTROL 管理目标]**, **[!UICONTROL 激活目标]**, **[!UICONTROL 查看配置文件]**&#x200B;和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或联系您的产品管理员以获取所需的权限。

## 概述 {#overview}

本文介绍在Adobe Experience Platform用户档案请求目标中激活受众数据所需的工作流。 用户档案请求目标示例包括 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化](../../destinations/catalog/personalization/custom-personalization.md) 连接。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须成功 [连接到目标](./connect-destination.md). 如果您尚未执行此操作，请转到 [目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

### 区段合并策略 {#merge-policy}

目前，配置文件请求目标仅支持激活使用 [边缘活动合并策略](../../segmentation/ui/segment-builder.md#merge-policies) 设置为默认值。

## 选择您的目标 {#select-destination}

1. 转到 **[!UICONTROL 连接>目标]**，然后选择 **[!UICONTROL 目录]** 选项卡。

   ![“目标目录”选项卡](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 选择 **[!UICONTROL 激活区段]** 在与要激活区段的目标对应的卡上，如下图所示。

   ![激活按钮](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 选择要用于激活区段的目标连接，然后选择 **[!UICONTROL 下一个]**.

   ![选择目标](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 移到下一个部分 [选择区段](#select-segments).

## 选择您的区段 {#select-segments}

使用区段名称左侧的复选框选择要激活到目标的区段，然后选择 **[!UICONTROL 下一个]**.

![选择区段](../assets/ui/activate-profile-request-destinations/select-segments.png)

## 计划区段导出 {#scheduling}

默认情况下， [!UICONTROL 区段计划] 页面仅显示您在当前激活流程中选择的新选定区段。

![新区段](../assets/ui/activate-profile-request-destinations/new-segments.png)

要查看激活到您的目标的所有区段，请使用筛选选项并禁用 **[!UICONTROL 仅显示新区段]** 过滤器。

![所有区段](../assets/ui/activate-profile-request-destinations/all-segments.png)

在 **[!UICONTROL 区段计划]** ，选择每个区段，然后使用 **[!UICONTROL 开始日期]** 和 **[!UICONTROL 结束日期]** 选择器来配置向目标发送数据的时间间隔。

![区段计划](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

选择 **[!UICONTROL 下一个]** 转到 [!UICONTROL 审阅] 页面。

## 审阅 {#review}

在 **[!UICONTROL 审阅]** 页面，则可以查看所选内容的摘要。 选择 **[!UICONTROL 取消]** 来分解流量， **[!UICONTROL 返回]** 修改设置，或 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform会检查是否存在数据使用策略违规。 下面显示了违反策略的示例。 在解决违规之前，无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅 [策略执行](../../rtcdp/privacy/data-governance-overview.md#enforcement) 在“数据管理文档”一节中。

![数据策略违规](../assets/common/data-policy-violation.png)

如果未检测到任何策略违规，请选择 **[!UICONTROL 完成]** 以确认您的选择并开始向目标发送数据。

![审阅](../assets/ui/activate-profile-request-destinations/review.png)

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->