---
title: 在UI中创建Shopify流连接和数据流
description: 了解如何使用Platform用户界面创建Shopify流源连接和数据流
badge: 测试版
exl-id: 3368ecf6-0c61-49ce-bc9c-29ee50b3f037
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# 为创建源连接和数据流 [!DNL Shopify Streaming] 使用UI的数据

本教程提供了用于创建 [!DNL Shopify Streaming] 源连接和数据流。

## 快速入门 {#getting-started}

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

>[!IMPORTANT]
>
>本教程要求您完成先决条件设置 [!DNL Shopify Streaming] 帐户。 有关设置帐户的步骤，请阅读 [[!DNL Shopify Streaming] 概述](../../../../connectors/ecommerce/shopify-streaming.md).

## 连接您的 [!DNL Shopify Streaming] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 以访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **电子商务** 类别，选择 [!DNL Shopify Streaming]，然后选择 **[!UICONTROL 添加数据]**.

![Experience Platform源目录](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## 选择数据

此 **[!UICONTROL 选择数据]** 步骤随即显示，为您提供了一个界面来选择要带到Platform的数据。

* 界面的左侧是一个浏览器，允许您查看帐户内的可用数据流；
* 界面的右侧部分允许您预览来自JSON文件的最多100行数据。

选择 **[!UICONTROL 上传文件]** 以从本地系统上传JSON文件。 或者，您也可以将要上传的JSON文件拖放到 [!UICONTROL 拖放文件] 面板。

![源工作流的添加数据步骤。](../../../../images/tutorials/create/shopify-streaming/select-data.png)

上传文件后，预览界面会更新以显示您上传的架构预览。 预览界面允许您检查文件的内容和结构。 您还可以使用 [!UICONTROL 搜索字段] 用于从架构中访问特定项目的实用程序。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的预览步骤。](../../../../images/tutorials/create/shopify-streaming/preview.png)

## 数据流详细信息

此 **数据流详细信息** 此时会显示步骤，为您提供使用现有数据集或为数据流建立新数据集的选项，并提供为数据流提供名称和描述的机会。 在此步骤中，您还可以配置配置文件提取、错误诊断、部分提取和警报的设置。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的数据流详细信息步骤。](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## 映射

此 [!UICONTROL 映射] 步骤随即显示，为您提供了一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的综合步骤，请参阅 [数据准备UI指南](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![源工作流的映射步骤。](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## 请查看

此 **[!UICONTROL 审核]** 步骤，允许您在创建新数据流之前对其进行查看。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源文件的相关路径以及源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括该数据集所遵循的架构。

查看数据流后，选择 **[!UICONTROL 完成]** 并留出一些时间来创建数据流。

![源工作流的审核步骤。](../../../../images/tutorials/create/shopify-streaming/review.png)

## 获取您的流端点URL

创建流数据流后，您现在可以检索流端点URL。 此端点将用于订阅您的webhook，允许您的流源与Experience Platform通信。

要检索您的流端点，请转到 [!UICONTROL 数据流活动] 之前创建的数据流页面，并从 [!UICONTROL 属性] 面板。

![数据流活动中的流端点。](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## 后续步骤

通过学习本教程，您已建立了与的源连接和数据流 [!DNL Shopify Streaming] 帐户。 有关如何连接 [!DNL Shopify Streaming] 帐户使用API，请阅读以下教程： [创建要流处理的源连接和数据流 [!DNL Shopify] 使用流服务API的数据](../../../api/create/ecommerce/shopify-streaming.md).
