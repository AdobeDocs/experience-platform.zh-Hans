---
keywords: Experience Platform；主页；热门主题；本地系统；文件上传；映射csv；映射csv文件；将csv文件映射到xdm；将csv映射到xdm；用户界面指南；
solution: Experience Platform
title: 在UI中创建本地文件上传Source连接器
type: Tutorial
description: 了解如何为本地系统创建源连接，以将本地文件带入Experience Platform
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# 在UI中创建本地文件上传源连接器

本教程提供了使用用户界面创建本地文件上传源连接器以将本地文件摄取到Experience Platform的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

## 将本地文件上传到Experience Platform

在Experience Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL 目录]屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL 本地系统]类别下，选择&#x200B;**[!UICONTROL 本地文件上传]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/local/catalog.png)

### 使用现有数据集

[!UICONTROL 数据流详细信息]页面允许您选择是将CSV数据摄取到现有数据集，还是新数据集。

要将CSV数据摄取到现有数据集，请选择&#x200B;**[!UICONTROL 现有数据集]**。 您可以使用[!UICONTROL 高级搜索]选项或通过滚动下拉菜单中的现有数据集列表来检索现有数据集。

选择数据集后，为数据流提供名称和可选描述。

在此过程中，您还可以启用[!UICONTROL 错误诊断]和[!UICONTROL 部分摄取]。 [!UICONTROL 错误诊断]允许为数据流中发生的任何错误记录生成详细的错误消息，而[!UICONTROL 部分摄取]允许您摄取包含错误的数据，摄取阈值为您手动定义的某个阈值。 有关详细信息，请参阅[部分批次摄取概述](../../../../../ingestion/batch-ingestion/partial.md)。

![现有数据集](../../../../images/tutorials/create/local/existing-dataset.png)

### 使用新数据集

要将CSV数据摄取到新数据集中，请选择&#x200B;**[!UICONTROL 新数据集]**，然后提供输出数据集名称和可选描述。 接下来，使用[!UICONTROL 高级搜索]选项或通过滚动下拉菜单中的现有架构列表来选择要映射到的架构。

选择架构后，为数据流提供名称和可选描述，然后为数据流应用所需的[!UICONTROL 错误诊断]和[!UICONTROL 部分摄取]设置。 完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![新数据集](../../../../images/tutorials/create/local/new-dataset.png)

### 选择数据

此时将显示[!UICONTROL 选择数据]步骤，该步骤为您提供了一个用于上载本地文件并预览其结构和内容的界面。 选择&#x200B;**[!UICONTROL 选择文件]**&#x200B;以从本地系统上传CSV文件。 或者，您也可以将要上载的CSV文件拖放到[!UICONTROL 拖放文件]面板。

>[!TIP]
>
>本地文件上传当前仅支持CSV文件。 每个文件的最大文件大小为1 GB。

![choose-files](../../../../images/tutorials/create/local/choose-files.png)

上传文件后，预览界面会更新以显示文件的内容和结构。

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

根据您的文件，可以为源数据选择列分隔符，例如制表符、逗号、管道或自定义列分隔符。 选择&#x200B;**[!UICONTROL 分隔符]**&#x200B;下拉箭头，然后从菜单中选择相应的分隔符。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![分隔符](../../../../images/tutorials/create/local/delimiter.png)

## 映射

此时将显示[!UICONTROL 映射]步骤，该步骤为您提供了一个接口，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射界面的完整步骤，请参阅[数据准备UI指南](../../../../../data-prep/ui/mapping.md)。

映射集准备就绪后，选择&#x200B;**[!UICONTROL 完成]**，等待片刻再创建新数据流。

![映射](../../../../images/tutorials/create/local/mapping.png)

## 监测数据摄取

映射和创建CSV文件后，您可以使用监视仪表板监视通过该文件摄取的数据。 有关详细信息，请参阅有关UI[&#128279;](../../../../../dataflows/ui/monitor-sources.md)中监视源数据流的教程。

## 后续步骤

通过遵循本教程，您已成功将平面CSV文件映射到XDM架构并将其引入到Experience Platform中。 此数据现在可以由下游[!DNL Experience Platform]服务（如[!DNL Real-Time Customer Profile]）使用。 有关详细信息，请参阅[[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)的概述。
