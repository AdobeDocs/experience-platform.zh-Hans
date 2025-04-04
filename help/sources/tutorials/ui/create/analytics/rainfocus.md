---
title: 使用UI将RainFocus帐户连接到Experience Platform
description: 了解如何使用UI将您的RainFocus帐户连接到Experience Platform。
badge: Beta 版
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 1%

---

# 使用UI将您的[!DNL RainFocus]帐户连接到Experience Platform

>[!NOTE]
>
>[!DNL RainFocus]源为测试版。 有关使用测试版标记源的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了有关如何将您的[!DNL RainFocus]帐户连接并将事件管理和分析数据流式传输到Adobe Experience Platform的步骤。

>[!IMPORTANT]
>
>此源连接器和文档页面由[!DNL RainFocus]团队创建和维护。 如有任何查询或更新请求，请直接通过clientcare<span>@rainfocus.com联系他们，或访问[[!DNL RainFocus] 帮助中心](https://help.rainfocus.com/hc/en-us)

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

### 先决条件

在将[!DNL RainFocus]帐户连接到Experience Platform之前，必须首先完成以下先决任务：

* [收集所需的凭据](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [创建XDM架构并定义标识字段](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [在RainFocus中创建集成配置文件](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

完成先决条件设置后，您可以继续执行下面列出的步骤。

## 将您的RainFocus帐户连接到Experience Platform

在Experience Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问源工作区。 *[!UICONTROL Catalog]*&#x200B;屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;*[!UICONTROL Analytics]*&#x200B;类别下，选择&#x200B;**[!UICONTROL RainFocus体验]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![已选择RainFocus源的Experience Platform UI上的源目录。](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## 选择数据

此时会显示选择数据步骤，提供一个界面以供您选择将导入Experience Platform的数据。

* 界面的左侧是一个浏览器，允许您查看帐户内的可用数据流；
* 界面的右侧部分允许您预览JSON文件中最多100行数据。

选择&#x200B;**[!UICONTROL 上载文件]**&#x200B;以从本地系统上载JSON文件。 或者，您也可以将要上传的JSON文件拖放到拖放文件面板。

上载从&#x200B;**RainFocus**&#x200B;下载的示例JSON有效负载。

![源工作流中的选择数据步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

上传文件后，预览界面会更新，以显示您上传的架构预览。 预览界面允许您检查文件的内容和结构。 您还可以使用搜索字段实用程序从架构中访问特定项目。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流程的数据预览步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## 数据流详细信息

此时将显示&#x200B;**数据流详细信息**&#x200B;步骤，该步骤为您提供了使用现有数据集或为数据流建立新数据集的选项，以及提供数据流名称和描述的机会。 在此步骤中，您还可以配置配置文件摄取、错误诊断、部分摄取和警报的设置。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的数据流详细信息步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## 映射 {#mapping}

此时会显示映射步骤，为您提供了一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Experience Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的全面步骤，请参阅[数据准备UI指南](../../../../../data-prep/ui/mapping.md)。

成功映射源数据后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的映射步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## 审查

将显示&#x200B;**审核**&#x200B;步骤，允许您在创建新数据流之前对其进行审核。 详细信息分为以下类别：

* **连接**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **分配数据集和映射字段**：显示要将源数据摄取到哪个数据集，包括数据集所遵循的架构。

查看数据流后，选择&#x200B;**完成**，然后等待一些时间来创建数据流。

![源工作流的审核步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## 获取您的流端点URL {#get-your-streaming-endpoint-url}

创建流数据流后，您现在可以检索流端点URL。 此端点将用于订阅您的webhook，允许您的流源与Experience Platform通信。

要检索您的流端点，请转到刚刚创建的数据流的&#x200B;*[!UICONTROL 数据流活动]*&#x200B;页面，并从&#x200B;*[!UICONTROL 属性]*&#x200B;面板的底部复制端点。

![源工作区中的数据流活动页面，流终结点URL突出显示。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## 在RainFocus中激活集成配置文件

数据流完成并检索到流式处理终结点URL后，您现在可以在[!DNL RainFocus]中激活[!DNL Integration Profile]。

* 登录到[[!DNL RainFocus] 平台](https://app.rainfocus.com)。 在主导航中，选择&#x200B;**[!DNL Libraries]**&#x200B;和&#x200B;**[!DNL Integration Profiles]**
* 打开您之前作为[先决条件](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)的一部分创建的[!DNL Integration Profile]。
* 粘贴从Experience Platform中的数据流复制的&#x200B;**数据流ID**&#x200B;和&#x200B;**流式端点**，然后选择&#x200B;**保存**

## 后续步骤

通过学习本教程，您已为[!DNL RainFocus]源建立连接，从而允许您将事件管理和分析数据流式传输到Experience Platform。

## 其他资源

以下文档提供了有关[!DNL RainFocus]源的细微差别的其他指南。

* [RainFocus帮助中心](https://help.rainfocus.com/hc/en-us)
* [在Adobe Developer门户中创建Adobe服务帐户(JWT)](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [在API中创建架构](../../../../../xdm/tutorials/create-schema-api.md)
* [在UI中创建架构](../../../../../xdm/tutorials/create-schema-ui.md)
* [在UI中定义标识字段](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
