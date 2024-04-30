---
title: 通过扩展的激活来激活Audience Manager受众
description: 了解如何通过Audience Manager扩展的激活，将Audience Manager受众激活到社交和广告目标。
source-git-commit: 19fb369a7faa0c5ac27a34db7b848b0332cb8695
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# 通过Audience Manager扩展激活来激活受众

本页介绍了要将受众从Audience Manager激活到扩展激活支持的目标平台，必须遵循的端到端工作流程。

## 开始之前 {#before-you-begin}

本指南中描述的步骤假定您已阅读 [扩展的激活概述页面](overview.md) 并且您已确认符合audience activation的先决条件。

>[!IMPORTANT]
>
>要通过激活受众，请执行以下操作 [!DNL Expanded Activation]，确保您的Audience Manager受众基于 **经过哈希处理的电子邮件地址**. 请参阅 [先决条件](overview.md#prerequisites) 以了解更多详细信息。

## 步骤1：配置Audience Manager源连接 {#configure-source}

此 [Audience Manager源连接器](../sources/connectors/adobe-applications/audience-manager.md) 发送在Adobe Audience Manager中收集以供激活的受众数据，以将其发送到扩展激活支持的目标平台。

遵循指南以了解如何 [创建Audience Manager源连接](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 以配置源连接器。

![显示具有Audience Manager源连接的“源”选项卡的Platform UI图像。](assets/sources-tab.png)

>[!TIP]
>
>Adobe Audience Manager源连接器是“扩展激活”中唯一可用的源连接器。
>
>如果要基于其他标识符摄取受众，则必须购买的 [Real-Time CDP](../rtcdp/overview.md). 有关更多详细信息，请联系您的Adobe代表。

### 查看和监视摄取的受众 {#view-audiences}

您可以从Audience Manager中查看带入扩展激活的受众，也可以在 **[!UICONTROL 受众]** 仪表板。

要查看您的受众，请转到 **[!UICONTROL 客户]** -> **[!UICONTROL 受众]** -> **[!UICONTROL 浏览]**.

![显示受众页面的Platform UI图像。](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* 在“扩展激活”中完全填充受众最多可能需要48小时。 这也适用于对现有Audience Manager受众的更新。
>* 新创建的Audience Manager受众不会自动显示在扩展激活中。 要在扩展激活中摄取新区段，必须通过Audience Manager源连接器添加它们。

配置Audience Manager源连接器后，移至 [步骤2](#create-destination-connection).

## 步骤2：创建新的目标连接 {#create-destination-connection}

在您可以将Audience Manager受众发送到所选的目标平台之前，必须首先创建与目标平台的连接。

在左侧边栏中，转到 **[!UICONTROL 连接]** -> **[!UICONTROL 目标]** -> **[!UICONTROL 目录]**.

可用的目标类别 [!DNL Expanded Activation] 是 [广告](../destinations/catalog/advertising/overview.md) 和 [社交](../destinations/catalog/social/overview.md).

![显示扩展激活目标目录的Platform UI图像。](assets/destination-catalog.png)

要创建与目标平台的新连接，请遵循上的指南 [如何创建新的目标连接](../destinations/ui/connect-destination.md). 然后，移至 [步骤3](#activate-audiences).

## 步骤3：将受众激活到您的目标 {#activate-audiences}

成功完成之后 [引入的Audience Manager受众](#configure-source) 和 [已创建新的目标连接](#create-destination-connection)，您现在可以将受众激活到所选的目标平台。

![显示扩展激活目标目录的Platform UI图像。](assets/activate-audiences.png)

要将受众激活到您的目标，请按照以下指南操作： [如何将受众激活到流目标](../destinations/ui/activate-segment-streaming-destinations.md).

## 验证受众激活 {#verify}

查看 [目标监视文档](../dataflows/ui/monitor-destinations.md) ，了解有关如何监控流向您目标的数据流的详细信息。