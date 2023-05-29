---
title: 在UI中创建Pendo源连接
description: 了解如何使用Adobe Experience Platform UI创建Pendo源连接。
badge: 测试版
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 1%

---

# 创建 [!DNL Pendo] 源连接数据流和UI中

>[!NOTE]
>
>此 [!DNL Pendo] 源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记源的更多信息。

本教程提供了用于创建 [!DNL Pendo] 源连接和数据流(使用Adobe Experience Platform用户界面)。

## 快速入门 {#getting-started}

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

## 先决条件 {#prerequisites}

以下部分提供了在创建之前，需要完成的先决条件的信息 [!DNL Pendo] 源连接。

### 用于定义源架构的JSON示例 [!DNL Pendo] {#prerequisites-json-schema}

创建之前 [!DNL Pendo] 源连接，则需要提供源架构。 您可以使用下面的JSON。

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

有关详细信息，请阅读 [[!DNL Pendo] webhook指南](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks).

### 为创建平台架构 [!DNL Pendo] {#create-platform-schema}

您还必须确保首先创建一个用于源的Platform架构。 请参阅上的教程 [创建平台架构](../../../../../xdm/schema/composition.md) 以了解有关如何创建架构的全面步骤。

![显示示例Pendo架构的平台UI。](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## 连接您的 [!DNL Pendo] 帐户 {#connect-account}

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 并查看Experience Platform中可用的源目录。

使用 *[!UICONTROL 类别]* 菜单，用于按类别筛选源。 或者，在搜索栏中输入源名称，以从目录查找特定源。

转到 [!UICONTROL 分析] 类别以查看 [!DNL Pendo] 源卡。 要开始，请选择 **[!UICONTROL 添加数据]**.

![带有Pendo卡的Platform UI源目录。](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## 选择数据 {#select-data}

此 **[!UICONTROL 选择数据]** 步骤，为您提供了一个界面来选择要带到Platform的数据。

* 界面的左侧是一个浏览器，允许您查看帐户内的可用数据流；
* 界面的右侧部分允许您预览来自JSON文件的最多100行数据。

选择 **[!UICONTROL 上传文件]** 以从本地系统上传JSON文件。 或者，您也可以将要上传的JSON文件拖放到 [!UICONTROL 拖放文件] 面板。

![源工作流的添加数据步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

上传文件后，预览界面会更新以显示您上传的架构预览。 预览界面允许您检查文件的内容和结构。 您还可以使用 [!UICONTROL 搜索字段] 用于从架构中访问特定项目的实用程序。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的预览步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## 数据流详细信息 {#dataflow-detail}

此 **数据流详细信息** 此时会显示步骤，为您提供使用现有数据集或为数据流建立新数据集的选项，并提供为数据流提供名称和描述的机会。 在此步骤中，您还可以配置配置文件提取、错误诊断、部分提取和警报的设置。

完成后，选择 **[!UICONTROL 下一个]**.

![源工作流的数据流详细信息步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## 映射 {#mapping}

此 [!UICONTROL 映射] 步骤随即显示，为您提供了一个界面，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的综合步骤，请参阅 [数据准备UI指南](../../../../../data-prep/ui/mapping.md).

下面列出的映射是强制性的，应在继续执行 [!UICONTROL 审核] 暂存。

| 目标字段 | 描述 |
| --- | --- |
| `uniqueId` | 此 [!DNL Pendo] 事件的标识符。 |

成功映射源数据后，选择 **[!UICONTROL 下一个]**.

![源工作流的映射步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## 请查看 {#review}

此 **[!UICONTROL 审核]** 步骤，允许您在创建新数据流之前对其进行查看。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括该数据集所遵循的架构。

查看数据流后，选择 **[!UICONTROL 完成]** 并留出一些时间来创建数据流。

![源工作流的审核步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## 获取您的流端点URL {#get-streaming-endpoint-url}

创建流数据流后，您现在可以检索流端点URL。 此端点将用于订阅您的webhook，允许您的流源与Experience Platform通信。

要构建用于在上配置webhook的URL [!DNL Pendo] 必须检索以下内容：

* **[!UICONTROL 数据流ID]**
* **[!UICONTROL 流端点]**

检索您的 **[!UICONTROL 数据流ID]** 和 **[!UICONTROL 流端点]**，转到 [!UICONTROL 数据流活动] 创建的数据流页面，并从页面底部复制详细信息 [!UICONTROL 属性] 面板。

![数据流活动中的流端点。](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

在检索到流端点和数据流ID后，请基于以下模式构建URL： ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```. 例如，构建的webhook URL可能如下所示： ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## 在中设置Webhook [!DNL Pendo] {#set-up-webhook}

接下来，登录到您的帐户，网址为 [[!DNL Pendo]](https://pendo.io/) 并创建一个webhook。 有关如何使用创建webhook的步骤 [!DNL Pendo] 用户界面，请参阅 [[!DNL Pendo] 创建webhook指南](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

创建webhook后，导航到 [!DNL Pendo] webhook并将您的webhook URL输入 [!DNL URL] 字段。

![显示webhook端点字段的Pendo UI屏幕截图](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>您可以订阅各种不同的事件类别，以确定要从发送何种事件 [!DNL Pendo] 实例到Platform。 欲知不同事件的详情，请参阅 [[!DNL Pendo] 文档](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4).

## 后续步骤 {#next-steps}

按照本教程，您已成功配置了一个流数据流，将 [!DNL Pendo] Experience Platform数据。 要监视正在摄取的数据，请参阅上的指南 [使用Platform UI监控流数据流](../../monitor-streaming.md).

## 其他资源 {#additional-resources}

以下各节提供了在使用时，您可以参考的其他资源 [!DNL Pendo] 源。

### 验证 {#validation}

验证是否已正确设置源和 [!DNL Pendo] 正在摄取消息，请执行以下步骤：

* 您可以检查 [!DNL Pendo] **[!UICONTROL 报告]** > **[!UICONTROL 聊天历史记录]** 用于标识所捕获的事件的页面 [!DNL Pendo].

![显示聊天历史记录的Pendo UI屏幕快照](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* 在Platform UI中，选择 **[!UICONTROL 查看数据流]** 在 [!DNL Pendo] 源目录中的卡菜单。 接下来，选择 **[!UICONTROL 预览数据集]** 验证为您在中配置的Webhook摄取的数据 [!DNL Pendo].

![显示已摄取事件的平台UI屏幕截图](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### 错误和疑难解答 {#errors-and-troubleshooting}

在检查数据流运行时，您可能会遇到以下错误消息： `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![平台UI屏幕截图显示错误。](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

要修复此错误，您必须验证 *唯一标识符* 已设置映射。 有关其他指导，请参阅 [Mmping](#mapping) 部分。

欲知更多信息，请访问 [[!DNL Pendo] 帮助中心](https://www.pendo.io/help-center/).
