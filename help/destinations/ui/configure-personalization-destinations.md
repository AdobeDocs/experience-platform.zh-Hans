---
keywords: 个性化；目标；目的地；个性化目标；配置个性化目标；同一页面；下一页；
title: 为同一页面和下一页面个性化配置个性化目标
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: 了解如何为同一页面和下一页面个性化配置个性化目标。
seo-description: Configure personalization destinations for same-page and next-page personalization.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: dd9493077706b102467493e90b363ac202550eee
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---

# 为同一页面和下一页面个性化配置个性化目标

## 概述 {#overview}

Adobe Experience Platform使用 [边缘分割](../../segmentation/ui/edge-segmentation.md) 使客户能够实时、高规模地创建和定位受众区段。

此功能可帮助您配置同页和下一页个性化用例。

本文提供了有关如何为这些用例配置Experience Platform和个性化目标的分步说明。

## 步骤1:配置Experience PlatformWeb SDK数据流 {#configure-datastream}

配置个性化用例的第一步是配置 [!DNL Web SDK datastream].

按照 [数据流配置](../../edge/fundamentals/datastreams.md) 文档。

## 步骤2:配置个性化目标 {#configure-destination}

配置数据流后，您可以开始配置个性化目标。

关注 [目标连接创建教程](../ui/connect-destination.md) 有关如何创建新目标连接的详细说明。

根据您配置的目标，请参阅以下文章以了解特定于目标的先决条件和相关信息：

* [Adobe Target连接](../catalog/personalization/adobe-target-connection.md)
* [自定义个性化连接](../catalog/personalization/custom-personalization.md)

## 步骤3:创建 [!DNL Active-On-Edge] 合并策略 {#create-merge-policy}

创建目标连接后，必须创建 [!DNL Active-On-Edge] 合并策略。

按照 [创建合并策略](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)，并确保启用 **[!UICONTROL 边缘活动合并策略]** 切换。

## 步骤4:在平台中创建新区段 {#create-segment}

创建 [!DNL Active-On-Edge] 合并策略，则必须在平台中创建新区段。

关注 [区段生成器](../../segmentation/ui/segment-builder.md) 创建新区段的指南，并确保 [分配](../../segmentation/ui/segment-builder.md#merge-policies) the [!DNL Active-On-Edge] 合并在步骤3中创建的策略。

## 步骤5:将区段激活到您的目标

配置过程的最后一步是将您在步骤4中创建的区段激活到您在步骤2中创建的目标。

要执行此操作，请遵循以下步骤 [激活教程](../ui/activate-profile-request-destinations.md).

## 验证配置 {#validate-configuration}

成功执行上述步骤后，您应会在个性化目标中看到新区段。
