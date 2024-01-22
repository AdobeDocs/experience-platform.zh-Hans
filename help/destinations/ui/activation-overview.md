---
keywords: 激活目标；激活数据
title: 激活概述
type: Tutorial
description: 了解如何将Adobe Experience Platform中的受众激活到各种类型的目标。
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# 激活概述

>[!IMPORTANT]
> 
>* 要激活数据，您需要 **[!UICONTROL 查看目标]**， **[!UICONTROL 激活目标]**， **[!UICONTROL 查看配置文件]**、和 **[!UICONTROL 查看区段]** [访问控制权限](/help/access-control/home.md#permissions). 阅读 [访问控制概述](/help/access-control/ui/overview.md) 或与产品管理员联系以获取所需的权限。
>* 要导出 *身份*，您需要 **[!UICONTROL 查看身份图]** [访问控制权限](/help/access-control/home.md#permissions). <br> ![选择工作流中突出显示的身份命名空间以将受众激活到目标。](/help/destinations/assets/overview/export-identities-to-destination.png "选择工作流中突出显示的身份命名空间以将受众激活到目标。"){width="100" zoomable="yes"}

Adobe Experience Platform支持各种目标。 受众激活工作流程因目标支持的受众数据类型以及数据导出频率而异。

## 激活方法 {#activation-methods}

在您之后 [配置目标](connect-destination.md)，您可以通过多种方式激活受众：

### 从目标目录激活受众

有关从目标目录将受众激活到目标的详细信息，请参阅以下指南：

* [将受众数据激活到流式受众导出目标](activate-segment-streaming-destinations.md)
* [将受众数据激活到流式配置文件导出目标](activate-streaming-profile-destinations.md)
* [将受众数据激活到批量配置文件导出目标](activate-batch-profile-destinations.md)

### 从激活受众 [!UICONTROL 浏览] 页面

请按照以下步骤将数据激活到 **[!UICONTROL 浏览]** 页面。

1. 转到 **[!UICONTROL “连接”>“目标”]**，然后选择 **[!UICONTROL 浏览]** 选项卡。

   ![“浏览”选项卡](../assets/ui/activation-overview/browse-tab.png)

1. 查找要用于激活区段的目标连接，选择 [!UICONTROL 名称] 列，然后选择 **[!UICONTROL 激活受众]**.

   ![“激活受众”按钮](../assets/ui/activation-overview/activate-segments.png)

1. 根据所选目标，请按照以下文章中所述的步骤操作，从 **[!UICONTROL 选择区段]** 步骤，要完成激活工作流：

   * [将受众数据激活到流式受众导出目标](activate-segment-streaming-destinations.md)
   * [将受众数据激活到流式配置文件导出目标](activate-streaming-profile-destinations.md)
   * [将受众数据激活到批量配置文件导出目标](activate-batch-profile-destinations.md)

### 从受众详细信息页面激活受众 {#activate-audience-details}

您可以从受众详细信息页面将受众激活到目标。 请参阅 [受众详细信息](../../segmentation/ui/overview.md#audience-details) 以了解更多信息。

根据所选目标，请按照以下文章中所述的步骤完成激活工作流：

* [将受众数据激活到流式受众导出目标](activate-segment-streaming-destinations.md)
* [将受众数据激活到流式配置文件导出目标](activate-streaming-profile-destinations.md)
* [将受众数据激活到批量配置文件导出目标](activate-batch-profile-destinations.md)
