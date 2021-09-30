---
keywords: 激活用户档案请求目标；激活数据；用户档案请求目标
title: 将受众数据激活到用户档案请求目标
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: 了解如何通过将区段映射到配置文件请求目标，来激活您在Adobe Experience Platform中拥有的受众数据。
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: caccd096c9165139d9b966bbfcb311456276192a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# 将受众数据激活到用户档案请求目标（测试版）

## 概述 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform中的用户档案请求目标当前处于测试阶段。 文档和功能可能会发生更改。

本文介绍在Adobe Experience Platform用户档案请求目标中激活受众数据所需的工作流。 配置文件请求目标的示例包括[Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)和[Custom personalization](../../destinations/catalog/personalization/custom-personalization.md)连接。

## 先决条件 {#prerequisites}

要将数据激活到目标，您必须已成功地[连接到目标](./connect-destination.md)。 如果您尚未执行此操作，请转到[目标目录](../catalog/overview.md)，浏览支持的目标，并配置要使用的目标。

### 区段合并策略 {#merge-policy}

配置文件请求目标当前仅支持激活使用默认合并策略的区段。 尝试激活具有不同合并策略的区段时，会在[[!UICONTROL Review]](#review)页面中导致错误。

## 选择您的目标 {#select-destination}

1. 转到&#x200B;**[!UICONTROL 连接>目标]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。

   ![“目标目录”选项卡](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 在与要激活区段的目标对应的卡上选择&#x200B;**[!UICONTROL 激活区段]**，如下图所示。

   ![激活按钮](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 选择要用于激活区段的目标连接，然后选择&#x200B;**[!UICONTROL Next]**。

   ![选择目标](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 移到下一部分，选择[区段](#select-segments)。

## 选择您的区段 {#select-segments}

使用区段名称左侧的复选框选择要激活到目标的区段，然后选择&#x200B;**[!UICONTROL Next]**。

![选择区段](../assets/ui/activate-profile-request-destinations/select-segments.png)

## 计划区段导出 {#scheduling}

默认情况下，[!UICONTROL 区段计划]页面仅显示您在当前激活流程中选择的新选定区段。

![新区段](../assets/ui/activate-profile-request-destinations/new-segments.png)

要查看已激活到您目标的所有区段，请使用筛选选项并禁用&#x200B;**[!UICONTROL 仅显示新区段]**&#x200B;筛选器。

![所有区段](../assets/ui/activate-profile-request-destinations/all-segments.png)

在&#x200B;**[!UICONTROL 区段计划]**&#x200B;页面上，选择每个区段，然后使用&#x200B;**[!UICONTROL 开始日期]**&#x200B;和&#x200B;**[!UICONTROL 结束日期]**&#x200B;选择器来配置向目标发送数据的时间间隔。

![区段计划](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

选择&#x200B;**[!UICONTROL Next]**&#x200B;以转到[!UICONTROL Review]页面。

## 审阅 {#review}

在&#x200B;**[!UICONTROL Review]**&#x200B;页面上，您可以看到您选择的摘要。 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以划分流程，选择&#x200B;**[!UICONTROL 返回]**&#x200B;以修改设置，或选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择并开始向目标发送数据。

>[!IMPORTANT]
>
>在此步骤中，Adobe Experience Platform会检查是否存在数据使用策略违规。 下面显示了违反策略的示例。 在解决违规之前，无法完成区段激活工作流。 有关如何解决策略违规的信息，请参阅数据管理文档一节中的[策略执行](../../rtcdp/privacy/data-governance-overview.md#enforcement)。

![数据策略违规](../assets/common/data-policy-violation.png)

如果未检测到任何违反策略的情况，请选择&#x200B;**[!UICONTROL 完成]**&#x200B;以确认您的选择并开始向目标发送数据。

![审阅](../assets/ui/activate-profile-request-destinations/review.png)

## 验证区段激活 {#verify}

请查看[目标监控文档](../../dataflows/ui/monitor-destinations.md) ，以了解有关如何监控目标数据流的详细信息。