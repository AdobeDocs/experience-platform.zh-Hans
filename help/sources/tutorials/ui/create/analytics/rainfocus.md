---
title: 使用UI将RainFocus帐户连接到Experience Platform
description: 了解如何使用UI将RainFocus帐户连接到Experience Platform。
badge: Beta 版
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 1%

---

# 连接您的 [!DNL RainFocus] 要使用UIExperience Platform的帐户

>[!NOTE]
>
>此 [!DNL RainFocus] 源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

本教程提供了有关如何连接 [!DNL RainFocus] 帐户并将事件管理和分析数据流式传输到Adobe Experience Platform。

>[!IMPORTANT]
>
>此源连接器和文档页面由 [!DNL RainFocus] 团队。 如有任何查询或更新请求，请直接通过客户关怀部门联系<span>@rainfocus.com或访问 [[!DNL RainFocus] 帮助中心](https://help.rainfocus.com/hc/en-us)

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

### 先决条件

在连接之前， [!DNL RainFocus] Experience Platform时，您必须先完成以下先决任务：

* [收集所需的凭据](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [创建XDM架构并定义标识字段](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [在RainFocus中创建集成配置文件](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

完成先决条件设置后，您可以继续执行下面列出的步骤。

## 将您的RainFocus帐户连接到Experience Platform

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问“源”工作区。 此 *[!UICONTROL 目录]* 屏幕显示了多种来源，您可以使用这些来源创建帐户。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 *[!UICONTROL 分析]* 类别，选择 **[!UICONTROL RainFocus体验]**，然后选择 **[!UICONTROL 添加数据]**.

![选择了RainFocus源的Experience PlatformUI上的源目录。](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## 选择数据

此时会显示选择数据步骤，提供一个界面供您选择要Experience Platform的数据。

* 界面的左侧是一个浏览器，允许您查看帐户内的可用数据流；
* 界面的右侧部分允许您预览JSON文件中最多100行数据。

选择 **[!UICONTROL 上载文件]** 以从本地系统上传JSON文件。 或者，您也可以将要上传的JSON文件拖放到拖放文件面板。

上传从下载的JSON有效负载示例 **RainFocus**.

![源工作流中的选择数据步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

上传文件后，预览界面会更新，以显示您上传的架构预览。 预览界面允许您检查文件的内容和结构。 您还可以使用搜索字段实用程序从架构中访问特定项目。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的数据预览步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## 数据流详细信息

此 **数据流详细信息** 此时会显示步骤，为您提供使用现有数据集或为数据流建立新数据集的选项，以及提供数据流名称和描述的机会。 在此步骤中，您还可以配置配置文件摄取、错误诊断、部分摄取和警报的设置。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的数据流详细信息步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## 映射 {#mapping}

此时会显示映射步骤，为您提供了一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Experience Platform根据您选择的Target架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的全面步骤，请参阅 [数据准备UI指南](../../../../../data-prep/ui/mapping.md).

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![源工作流的映射步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## 请查看

此 **审核** 此时会显示步骤，允许您在创建新数据流之前对其进行查看。 详细信息分为以下类别：

* **连接**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **分配数据集和映射字段**：显示要将源数据摄取到哪个数据集，包括数据集所遵循的架构。

查看数据流后，选择 **完成** 留出一段时间来创建数据流。

![源工作流的审核步骤。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## 获取您的流端点URL {#get-your-streaming-endpoint-url}

创建流数据流后，您现在可以检索流端点URL。 此端点将用于订阅您的webhook，允许您的流源与Experience Platform通信。

要检索您的流端点，请转到 *[!UICONTROL 数据流活动]* 之前创建的数据流页面，并从 *[!UICONTROL 属性]* 面板。

![源工作区中的“数据流活动”页面，其中突出显示了流端点URL。](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## 在RainFocus中激活集成配置文件

数据流完成并检索到流端点URL后，您现在可以激活 [!DNL Integration Profile] 在 [!DNL RainFocus].

* 登录 [[!DNL RainFocus] 平台](https://app.rainfocus.com). 在主导航中，选择 **[!DNL Libraries]** 和 **[!DNL Integration Profiles]**
* 打开 [!DNL Integration Profile] 您之前创建的，作为 [先决条件](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* 粘贴 **数据流ID** 和 **流端点** 从Experience Platform中的数据流复制并选择 **保存**

## 后续步骤

通过学习本教程，您已为建立了连接 [!DNL RainFocus] 源，允许您流式传输事件管理和Experience Platform数据。

## 其他资源

以下文档提供了有关 [!DNL RainFocus] 源。

* [RainFocus帮助中心](https://help.rainfocus.com/hc/en-us)
* [在Adobe Developer门户中创建Adobe服务帐户(JWT)](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [在API中创建架构](../../../../../xdm/tutorials/create-schema-api.md)
* [在UI中创建架构](../../../../../xdm/tutorials/create-schema-ui.md)
* [在UI中定义标识字段](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
