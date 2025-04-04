---
title: 通过扩展的激活来激活Audience Manager受众
description: 了解如何通过Audience Manager扩展的激活，将Audience Manager受众激活到社交和广告目标。
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 通过Audience Manager扩展激活来激活受众

本页介绍了要将受众从Audience Manager激活到扩展激活支持的目标平台，必须遵循的端到端工作流程。

## 开始之前 {#before-you-begin}

本指南中描述的步骤假定您已阅读[扩展激活概述页面](overview.md)，并且已确认您满足受众激活的先决条件。

>[!IMPORTANT]
>
>要通过[!DNL Expanded Activation]激活受众，请确保您的Audience Manager受众基于&#x200B;**哈希电子邮件地址**。 有关详细信息，请参阅[先决条件](overview.md#prerequisites)。

## 步骤1：配置Audience Manager源连接 {#configure-source}

[Audience Manager源连接器](../sources/connectors/adobe-applications/audience-manager.md)发送在Adobe Audience Manager中收集的受众数据，以便在扩展激活支持的目标平台中进行激活。

按照如何[创建Audience Manager源连接](../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的指南配置源连接器。

![Experience Platform UI图像显示“源”选项卡与Audience Manager源连接。](assets/sources-tab.png)

>[!TIP]
>
>Adobe Audience Manager源连接器是“扩展激活”中唯一可用的源连接器。
>
>如果要基于其他标识符摄取受众，则必须购买[Real-Time CDP](../rtcdp/overview.md)的版本。 有关更多详细信息，请与Adobe代表联系。

### 查看和监视摄取的受众 {#view-audiences}

您从Audience Manager引入扩展激活的受众可以在&#x200B;**[!UICONTROL 受众]**&#x200B;功能板中查看。

要查看您的受众，请转到&#x200B;**[!UICONTROL 客户]** -> **[!UICONTROL 受众]** -> **[!UICONTROL 浏览]**。

![Experience Platform UI图像显示“受众”页面。](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* 在“扩展激活”中完全填充受众最多可能需要48小时。 这也适用于对现有Audience Manager受众的更新。
>* 新创建的Audience Manager受众不会自动显示在扩展的激活中。 要在扩展激活中摄取新区段，必须通过Audience Manager源连接器添加它们。

配置Audience Manager源连接器后，请移至[步骤2](#create-destination-connection)。

## 步骤2：创建新的目标连接 {#create-destination-connection}

在您可以将Audience Manager受众发送到所选的目标平台之前，必须首先创建与目标平台的连接。

在左侧边栏中，转到&#x200B;**[!UICONTROL 连接]** -> **[!UICONTROL 目标]** -> **[!UICONTROL 目录]**。

[!DNL Expanded Activation]的可用目标类别为[广告](../destinations/catalog/advertising/overview.md)和[社交](../destinations/catalog/social/overview.md)。

![Experience Platform UI图像显示扩展激活的目标目录。](assets/destination-catalog.png)

若要创建到目标平台的新连接，请按照[上的指南进行操作，以创建新的目标连接](../destinations/ui/connect-destination.md)。 然后，移至[步骤3](#activate-audiences)。

## 步骤3：将受众激活到您的目标 {#activate-audiences}

在成功[引入Audience Manager受众](#configure-source)和[创建新的目标连接](#create-destination-connection)后，您现在可以将受众激活到您选择的目标平台。

![Experience Platform UI图像显示扩展激活的目标目录。](assets/activate-audiences.png)

若要将受众激活到您的目标，请按照[上的指南操作，了解如何将受众激活到流式目标](../destinations/ui/activate-segment-streaming-destinations.md)。

## 验证受众激活 {#verify}

有关如何监视流向目标的数据流的详细信息，请查看[目标监视文档](../dataflows/ui/monitor-destinations.md)。
