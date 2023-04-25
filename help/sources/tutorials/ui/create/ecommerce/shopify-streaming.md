---
title: 在Ui中创建Shopify流连接和数据流
description: 了解如何使用Platform用户界面创建Shopify流源连接和数据流
badge: Beta
exl-id: 3368ecf6-0c61-49ce-bc9c-29ee50b3f037
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# 为创建源连接和数据流 [!DNL Shopify Streaming] 使用UI的数据

本教程提供了创建 [!DNL Shopify Streaming] 源连接和数据流。

## 快速入门 {#getting-started}

本教程需要对Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

>[!IMPORTANT]
>
>本教程要求您完成 [!DNL Shopify Streaming] 帐户。 有关设置帐户的步骤，请阅读 [[!DNL Shopify Streaming] 概述](../../../../connectors/ecommerce/shopify-streaming.md).

## 连接 [!DNL Shopify Streaming] 帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 **电子商务** 类别，选择 [!DNL Shopify Streaming]，然后选择 **[!UICONTROL 添加数据]**.

![Experience Platform源目录](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## 选择数据

的 **[!UICONTROL 选择数据]** 步骤，为您提供一个界面以选择引入到平台的数据。

* 界面的左侧是一个浏览器，用于查看您帐户中的可用数据流；
* 界面的右侧部分允许您从JSON文件预览多达100行数据。

选择 **[!UICONTROL 上传文件]** 从本地系统上传JSON文件。 或者，您也可以将要上传的JSON文件拖放到 [!UICONTROL 拖放文件] 的上界。

![源工作流的添加数据步骤。](../../../../images/tutorials/create/shopify-streaming/select-data.png)

上传文件后，预览界面会随之发生更新，以显示您上传的架构的预览。 预览界面允许您检查文件的内容和结构。 您还可以使用 [!UICONTROL 搜索字段] 用于从架构中访问特定项目的实用程序。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的预览步骤。](../../../../images/tutorials/create/shopify-streaming/preview.png)

## 数据流详细信息

的 **数据流详细信息** 此步骤将显示，为您提供使用现有数据集或为数据流建立新数据集的选项，以及提供数据流名称和描述的机会。 在此步骤中，您还可以配置用于配置文件摄取、错误诊断、部分摄取和警报的设置。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的数据流详细信息步骤。](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## 映射

的 [!UICONTROL 映射] 此时会显示步骤，为您提供一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关使用映射器界面和计算字段的完整步骤，请参阅 [数据准备UI指南](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![源工作流的映射步骤。](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## 请查看

的 **[!UICONTROL 审阅]** 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。

审核数据流后，选择 **[!UICONTROL 完成]** 并为创建数据流留出一些时间。

![源工作流的审核步骤。](../../../../images/tutorials/create/shopify-streaming/review.png)

## 获取流端点URL

创建流数据流后，您现在可以检索流端点URL。 此端点将用于订阅您的Webhook，从而允许您的流源与Experience Platform通信。

要检索流端点，请转到 [!UICONTROL 数据流活动] 数据流的页面，并从 [!UICONTROL 属性] 的上界。

![数据流活动中的流端点。](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## 后续步骤

通过阅读本教程，您已经为 [!DNL Shopify Streaming] 帐户。 有关如何连接 [!DNL Shopify Streaming] 帐户，请阅读 [创建源连接和数据流到流 [!DNL Shopify] 使用流量服务API的数据](../../../api/create/ecommerce/shopify-streaming.md).
