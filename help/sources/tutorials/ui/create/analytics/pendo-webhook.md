---
title: 在UI中创建Pendo源连接
description: 了解如何使用Adobe Experience Platform UI创建Pendo源连接。
badge: "Beta"
source-git-commit: 5a199262acd517516b1e5313a25ddff8f1b11959
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 1%

---

# 创建 [!DNL Pendo] 源连接数据流和UI中的

>[!NOTE]
>
>的 [!DNL Pendo] 来源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

本教程提供了创建 [!DNL Pendo] 源连接和数据流。

## 快速入门 {#getting-started}

本教程需要对Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

## 先决条件 {#prerequisites}

以下部分提供了在创建 [!DNL Pendo] 源连接。

### 用于定义源架构的JSON示例 [!DNL Pendo] {#prerequisites-json-schema}

在创建 [!DNL Pendo] 源连接时，您需要提供源架构。 您可以使用下面的JSON。

```
{
  "accountId": "58f79ee324d3f",
  "timestamp": 1673372516,
  "visitorId": "test@test.com",
  "uniqueId": "166e50cdf40930fe1367e4d44795c9c74d88b83a",
  "properties": {
    "guideProperties": {
  "name": "Guide Conversion Test"
  }
}
}
```

有关更多信息，请阅读 [[!DNL Pendo] webhooks指南](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### 为创建平台模式 [!DNL Pendo] {#create-platform-schema}

您还必须确保首先创建要用于源的平台架构。 请参阅 [创建平台模式](../../../../../xdm/schema/composition.md) 有关如何创建架构的完整步骤。

![Platform UI显示了Pendo的模式示例。](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## 连接 [!DNL Pendo] 帐户 {#connect-account}

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区，并查看Experience Platform中可用的源目录。

使用 *[!UICONTROL 类别]* 菜单来按类别筛选源。 或者，在搜索栏中输入源名称，以从目录中查找特定源。

转到 [!UICONTROL Analytics] 类别以查看 [!DNL Pendo] 源卡。 要开始，请选择 **[!UICONTROL 添加数据]**.

![带有Pendo卡的Platform UI源目录。](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## 选择数据 {#select-data}

的 **[!UICONTROL 选择数据]** 步骤，为您提供一个界面以选择要引入平台的数据。

* 界面的左侧是一个浏览器，用于查看您帐户中的可用数据流；
* 界面的右侧部分允许您从JSON文件预览多达100行数据。

选择 **[!UICONTROL 上传文件]** 从本地系统上传JSON文件。 或者，您也可以将要上传的JSON文件拖放到 [!UICONTROL 拖放文件] 的上界。

![源工作流的添加数据步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

上传文件后，预览界面会随之发生更新，以显示您上传的架构的预览。 预览界面允许您检查文件的内容和结构。 您还可以使用 [!UICONTROL 搜索字段] 用于从架构中访问特定项目的实用程序。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的预览步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## 数据流详细信息 {#dataflow-detail}

的 **数据流详细信息** 此步骤将显示，为您提供使用现有数据集或为数据流建立新数据集的选项，以及提供数据流名称和描述的机会。 在此步骤中，您还可以配置用于配置文件摄取、错误诊断、部分摄取和警报的设置。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的数据流详细信息步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## 映射 {#mapping}

的 [!UICONTROL 映射] 此时会显示步骤，为您提供一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据您的需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以导出计算值或计算值。 有关使用映射器界面和计算字段的完整步骤，请参阅 [数据准备UI指南](../../../../../data-prep/ui/mapping.md).

下面列出的映射是必选的，在继续到 [!UICONTROL 审阅] 舞台。

| 目标字段 | 描述 |
| --- | --- |
| `uniqueId` | 的 [!DNL Pendo] 事件的标识符。 |

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![源工作流的映射步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## 请查看 {#review}

的 **[!UICONTROL 审阅]** 步骤，允许您在创建新数据流之前查看新数据流。 详细信息按以下类别分组：

* **[!UICONTROL 连接]**:显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**:显示源数据被摄取到的数据集，包括该数据集附加的架构。

审核数据流后，选择 **[!UICONTROL 完成]** 并为创建数据流留出一些时间。

![源工作流的审核步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## 获取流端点URL {#get-streaming-endpoint-url}

创建流数据流后，您现在可以检索流端点URL。 此端点将用于订阅您的Webhook，从而允许您的流源与Experience Platform通信。

以构建用于在上配置Webhook的URL [!DNL Pendo] 您必须检索以下内容：

* **[!UICONTROL 数据流ID]**
* **[!UICONTROL 流端点]**

检索 **[!UICONTROL 数据流ID]** 和 **[!UICONTROL 流端点]**，转到 [!UICONTROL 数据流活动] 数据流的页面，并从 [!UICONTROL 属性] 的上界。

![数据流活动中的流端点。](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

在检索到流端点和数据流ID后，请根据以下模式构建URL: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. 例如，构建的Webhook URL可能如下所示： ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## 在中设置Webhook [!DNL Pendo] {#set-up-webhook}

接下来，登录您的帐户 [[!DNL Pendo]](https://pendo.io/) 并创建网钩。 有关如何使用创建网页挂接的步骤 [!DNL Pendo] 用户界面，请参阅 [[!DNL Pendo] 创建webhook指南](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

创建Webhook后，导航到 [!DNL Pendo] webhook并在 [!DNL URL] 字段。

![Pendo UI屏幕截图，显示Webhook端点字段](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>您可以订阅各种不同的事件类别，以确定要从 [!DNL Pendo] 实例到平台。 有关不同事件的更多信息，请参阅 [[!DNL Pendo] 文档](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## 后续步骤 {#next-steps}

在本教程之后，您已成功配置了流数据流以将 [!DNL Pendo] Experience Platform。 要监视正在摄取的数据，请参阅 [使用Platform UI监控流数据流](../../monitor-streaming.md).

## 其他资源 {#additional-resources}

以下部分提供了在使用 [!DNL Pendo] 来源。

### 验证 {#validation}

验证是否已正确设置源和 [!DNL Pendo] 正在摄取消息，请执行以下步骤：

* 您可以检查 [!DNL Pendo] **[!UICONTROL 报表]** > **[!UICONTROL 聊天历史记录]** 页面以标识捕获的事件 [!DNL Pendo].

![Pendo UI屏幕截图显示聊天历史记录](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* 在平台UI中，选择 **[!UICONTROL 查看数据流]** 旁边 [!DNL Pendo] 源目录的卡片菜单。 接下来，选择 **[!UICONTROL 预览数据集]** 验证为您在 [!DNL Pendo].

![显示摄取事件的Platform UI屏幕截图](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### 错误和疑难解答 {#errors-and-troubleshooting}

检查数据流运行时，您可能会遇到以下错误消息： `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![显示错误的平台UI屏幕截图。](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

要修复此错误，您必须验证 *uniqueID* 映射已设置。 有关其他指导，请参阅 [Mmpping](#mapping) 中。

有关更多信息，请访问 [[!DNL Pendo] 帮助中心](https://www.pendo.io/help-center/).