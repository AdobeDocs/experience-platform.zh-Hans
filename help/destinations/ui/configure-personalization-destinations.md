---
keywords: 个性化；目标；目标；个性化目标；配置个性化目标；同一页面；下一页面；
title: 为同一页面和下一页面个性化配置个性化目标
type: Tutorial
description: 了解如何为同一页面和下一页面个性化配置个性化目标。
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 为同一页面和下一页面个性化配置个性化目标

## 概述 {#overview}

>[!NOTE]
>
>时间 [配置Adobe Target连接](../catalog/personalization/adobe-target-connection.md) 如果不使用数据流ID，则不支持本文中描述的用例。

Adobe Experience Platform使用 [边缘分割](../../segmentation/ui/edge-segmentation.md) 使客户能够实时大规模创建和定位受众区段。

此功能可帮助您配置同页和下一页个性化用例。

本文提供了有关如何为这些用例配置Experience Platform和个性化目标的分步说明。

此外，请观看以下视频，了解端到端配置过程的概述。

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>Experience Platform用户界面经常更新，自从录制此视频以来，可能已经更改。 有关最新信息，请参阅以下部分中描述的配置步骤。

## 步骤1：在数据收集UI中配置数据流 {#configure-datastream}

设置个性化目标的第一步是为Experience PlatformWeb SDK配置数据流。 此操作可在数据收集UI中完成。

配置数据流时，位于 **[!UICONTROL Adobe Experience Platform]** 确保两者 **[!UICONTROL 边缘分段]** 和 **[!UICONTROL 个性化目标]** 已选中。

![数据流配置](../assets/ui/configure-personalization-destinations/datastream-config.png)

有关如何设置数据流的更多详细信息，请按照 [Platform Web SDK文档](../../edge/datastreams/overview.md).

## 步骤2：配置个性化目标 {#configure-destination}

配置数据流后，可以开始配置个性化目标。

请遵循 [目标连接创建教程](../ui/connect-destination.md) 以获取有关如何创建新目标连接的详细说明。

根据您配置的目标，请参阅以下文章，了解特定于目标的先决条件和相关信息：

* [Adobe Target连接](../catalog/personalization/adobe-target-connection.md)
* [自定义个性化连接](../catalog/personalization/custom-personalization.md)

## 第3步：创建 [!DNL Active-On-Edge] 合并策略 {#create-merge-policy}

创建目标连接后，必须创建 [!DNL Active-On-Edge] 合并策略。

按照上的说明操作 [创建合并策略](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)，并确保启用 **[!UICONTROL Active-On-Edge合并策略]** 切换。

## 步骤4：在Platform中创建新区段 {#create-segment}

创建之后 [!DNL Active-On-Edge] 合并策略，则必须在Platform中创建新区段。

请遵循 [区段生成器](../../segmentation/ui/segment-builder.md) 指南，以创建新区段，并确保 [分配](../../segmentation/ui/segment-builder.md#merge-policies) 此 [!DNL Active-On-Edge] 您在步骤3中创建的合并策略。

## 步骤5：将区段激活到目标

配置过程的最后一步是将您在步骤4中创建的区段激活到您在步骤2中创建的目标。

为此，请遵循此步骤 [激活教程](../ui/activate-profile-request-destinations.md).

## 验证配置 {#validate-configuration}

成功执行上述步骤后，您应会在个性化目标中看到新区段。
