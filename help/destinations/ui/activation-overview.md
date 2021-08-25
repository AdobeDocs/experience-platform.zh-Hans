---
keywords: 激活目标；激活数据
title: 激活概述
type: Tutorial
seo-title: Activation overview
description: 了解如何将您在Adobe Experience Platform中拥有的受众数据激活到各种类型的目标。
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform to various types of destinations.
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---


# 激活概述

Adobe Experience Platform支持多种目标。 受众激活工作流因目标所支持的受众数据类型和数据导出频率而异。

## 激活方法 {#activation-methods}

在[配置目标](connect-destination.md)后，可以通过多种方式激活受众区段：

### 从目标目录激活受众

有关从目标目录将受众激活到您的目标的详细信息，请参阅以下指南：

* [将受众数据激活到流区段导出目标](activate-segment-streaming-destinations.md)
* [将受众数据激活到流配置文件导出目标](activate-streaming-profile-destinations.md)
* [激活受众数据以批量配置文件导出目标](activate-batch-profile-destinations.md)

### 从[!UICONTROL Browse]页面中激活受众

请按照以下步骤从&#x200B;**[!UICONTROL Browse]**&#x200B;页面将数据激活到您的目标。

1. 转到&#x200B;**[!UICONTROL 连接>目标]**，然后选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡。

   ![“浏览”选项卡](../assets/ui/activation-overview/browse-tab.png)

1. 找到要用于激活区段的目标连接，选择[!UICONTROL 名称]列中的三个圆点，然后选择&#x200B;**[!UICONTROL 激活区段]**。

   ![“激活区段”按钮](../assets/ui/activation-overview/activate-segments.png)

1. 根据所选目标，按照以下文章中描述的步骤（从&#x200B;**[!UICONTROL 选择区段]**&#x200B;步骤开始）完成激活工作流：

   * [将受众数据激活到流区段导出目标](activate-segment-streaming-destinations.md)
   * [将受众数据激活到流配置文件导出目标](activate-streaming-profile-destinations.md)
   * [激活受众数据以批量配置文件导出目标](activate-batch-profile-destinations.md)

### 从区段详细信息页面激活受众 {#activate-segment-details}

您可以从区段详细信息页面将区段激活到目标。 有关详细信息，请参阅[区段详细信息](../../segmentation/ui/overview.md#segment-details)。

根据所选目标，按照以下文章中描述的步骤完成激活工作流：

* [将受众数据激活到流区段导出目标](activate-segment-streaming-destinations.md)
* [将受众数据激活到流配置文件导出目标](activate-streaming-profile-destinations.md)
* [激活受众数据以批量配置文件导出目标](activate-batch-profile-destinations.md)