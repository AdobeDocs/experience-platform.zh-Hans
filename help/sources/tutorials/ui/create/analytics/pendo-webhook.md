---
title: 在UI中创建Pendo Source连接
description: 了解如何使用Adobe Experience Platform UI创建Pendo源连接。
badge: Beta 版
exl-id: defdec30-42af-43c8-b2eb-7ce98f7871e3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 1%

---

# 在UI中创建[!DNL Pendo]源连接数据流和

>[!NOTE]
>
>[!DNL Pendo]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了使用Adobe Experience Platform用户界面创建[!DNL Pendo]源连接和数据流的步骤。

## 快速入门 {#getting-started}

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

## 先决条件 {#prerequisites}

以下部分提供了在创建[!DNL Pendo]源连接之前需要完成的先决条件的信息。

### 用于为[!DNL Pendo]定义源架构的JSON示例 {#prerequisites-json-schema}

在创建[!DNL Pendo]源连接之前，您需要提供源架构。 您可以使用下面的JSON。

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

有关详细信息，请阅读webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks)上的[[!DNL Pendo] 指南。

### 为[!DNL Pendo]创建Experience Platform架构 {#create-platform-schema}

您还必须确保首先创建一个Experience Platform架构以用于您的源。 有关如何创建架构的完整步骤，请参阅有关[创建Experience Platform架构](../../../../../xdm/schema/composition.md)的教程。

![Experience Platform UI显示Pendo的示例架构。](../../../../images/tutorials/create/analytics-pendo-webhook/schema.png)

## 连接您的[!DNL Pendo]帐户 {#connect-account}

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区，并查看Experience Platform中可用的源目录。

使用&#x200B;*[!UICONTROL 类别]*&#x200B;菜单按类别筛选源。 或者，在搜索栏中输入源名称，以从目录查找特定源。

转到[!UICONTROL Analytics]类别以查看[!DNL Pendo]源卡。 要开始，请选择&#x200B;**[!UICONTROL 添加数据]**。

![带有Pendo卡的Experience Platform UI源目录。](../../../../images/tutorials/create/analytics-pendo-webhook/catalog.png)

## 选择数据 {#select-data}

此时将显示&#x200B;**[!UICONTROL 选择数据]**&#x200B;步骤，该步骤为您提供了一个界面以选择要带入Experience Platform的数据。

* 界面的左侧是一个浏览器，允许您查看帐户内的可用数据流；
* 界面的右侧部分允许您预览JSON文件中最多100行数据。

选择&#x200B;**[!UICONTROL 上载文件]**&#x200B;以从本地系统上载JSON文件。 或者，您也可以将要上传的JSON文件拖放到[!UICONTROL 拖放文件]面板。

![源工作流的添加数据步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/add-data.png)

上传文件后，预览界面会更新，以显示您上传的架构预览。 预览界面允许您检查文件的内容和结构。 您还可以使用[!UICONTROL 搜索字段]实用工具访问架构中的特定项目。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的预览步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/preview.png)

## 数据流详细信息 {#dataflow-detail}

此时将显示&#x200B;**数据流详细信息**&#x200B;步骤，该步骤为您提供了使用现有数据集或为数据流建立新数据集的选项，以及提供数据流名称和描述的机会。 在此步骤中，您还可以配置配置文件摄取、错误诊断、部分摄取和警报的设置。

完成后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的数据流详细信息步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/dataflow-detail.png)

## 映射 {#mapping}

此时将显示[!UICONTROL 映射]步骤，该步骤为您提供了一个接口，用于将源架构中的源字段映射到目标架构中相应的目标XDM字段。

Experience Platform根据您选择的目标架构或数据集，为自动映射的字段提供智能推荐。 您可以手动调整映射规则以适合您的用例。 根据需要，您可以选择直接映射字段，或使用数据准备函数转换源数据以派生计算值或计算值。 有关使用映射器界面和计算字段的全面步骤，请参阅[数据准备UI指南](../../../../../data-prep/ui/mapping.md)。

下面列出的映射是强制性的，应在继续执行[!UICONTROL 审阅]阶段之前进行设置。

| 目标字段 | 描述 |
| --- | --- |
| `uniqueId` | 事件的[!DNL Pendo]标识符。 |

成功映射源数据后，选择&#x200B;**[!UICONTROL 下一步]**。

![源工作流的映射步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/mapping.png)

## 审查 {#review}

将显示&#x200B;**[!UICONTROL 审核]**&#x200B;步骤，允许您在创建新数据流之前对其进行审核。 详细信息分为以下类别：

* **[!UICONTROL 连接]**：显示源类型、所选源文件的相关路径以及该源文件中的列数。
* **[!UICONTROL 分配数据集和映射字段]**：显示要将源数据摄取到哪个数据集，包括数据集所遵循的架构。

查看数据流后，选择&#x200B;**[!UICONTROL 完成]**，然后等待一些时间来创建数据流。

![源工作流的审核步骤。](../../../../images/tutorials/create/analytics-pendo-webhook/review.png)

## 获取您的流端点URL {#get-streaming-endpoint-url}

创建流数据流后，您现在可以检索流端点URL。 此端点将用于订阅您的webhook，允许您的流源与Experience Platform通信。

要构造用于在[!DNL Pendo]上配置webhook的URL，您必须检索以下内容：

* **[!UICONTROL 数据流ID]**
* **[!UICONTROL 流式处理终结点]**

要检索&#x200B;**[!UICONTROL 数据流ID]**&#x200B;和&#x200B;**[!UICONTROL 流式处理终结点]**，请转到刚刚创建的数据流的[!UICONTROL 数据流活动]页面，并从[!UICONTROL 属性]面板的底部复制详细信息。

![数据流活动中的流终结点。](../../../../images/tutorials/create/analytics-pendo-webhook/endpoint-test.png)

在检索到流端点和数据流ID后，请基于以下模式构建URL： ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```。 例如，构建的webhook URL可能如下所示： ```https://dcs.adobedc.net/collection/0c61859cc71939a0caf01123f91b2fc52589018800ad46b6c76c2dff3595ee95```

## 在[!DNL Pendo]中设置Webhook {#set-up-webhook}

接下来，在[[!DNL Pendo]](https://pendo.io/)上登录您的帐户并创建webhook。 有关如何使用[!DNL Pendo]用户界面创建webhook的步骤，请参阅有关创建webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4)的[[!DNL Pendo] 指南。

创建webhook后，导航到[!DNL Pendo] webhook的设置页面，并在[!DNL URL]字段中输入webhook URL。

![显示webhook终结点字段的Pendo UI屏幕截图](../../../../images/tutorials/create/analytics-pendo-webhook/webhook.png)

>[!TIP]
>
>您可以订阅各种不同的事件类别，以确定要从[!DNL Pendo]实例发送到Experience Platform的事件类型。 有关不同事件的详细信息，请参阅[[!DNL Pendo] 文档](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks#create-a-webhook-0-4)。

## 后续步骤 {#next-steps}

通过完成本教程，您已成功配置流式数据流以将您的[!DNL Pendo]数据引入Experience Platform。 要监视正在摄取的数据，请参阅关于使用Experience Platform UI监视流式数据流的[指南](../../monitor-streaming.md)。

## 其他资源 {#additional-resources}

以下各节提供了在使用[!DNL Pendo]源时可以参考的其他资源。

### 验证 {#validation}

要验证您是否已正确设置源，并且正在摄取[!DNL Pendo]条消息，请执行以下步骤：

* 您可以检查[!DNL Pendo] **[!UICONTROL 报告]** > **[!UICONTROL 聊天历史记录]**&#x200B;页面以识别[!DNL Pendo]正在捕获的事件。

![Pendo UI屏幕截图显示聊天历史记录](../../../../images/tutorials/create/analytics-pendo-webhook/pendo-events.png)

* 在Experience Platform UI中，选择源目录上[!DNL Pendo]卡片菜单旁边的&#x200B;**[!UICONTROL 查看数据流]**。 接下来，选择&#x200B;**[!UICONTROL 预览数据集]**&#x200B;以验证为您在[!DNL Pendo]中配置的Webhook摄取的数据。

![Experience Platform UI屏幕截图显示摄取的事件](../../../../images/tutorials/create/analytics-pendo-webhook/platform-dataset.png)

### 错误和故障排除 {#errors-and-troubleshooting}

检查数据流运行时，您可能会遇到以下错误消息： `The message can't be validated ... uniqueID:expected minLength:1, actual 0].`

![Experience Platform UI屏幕快照显示错误。](../../../../images/tutorials/create/analytics-pendo-webhook/error.png)

要修复此错误，必须验证是否已设置&#x200B;*uniqueID*&#x200B;映射。 有关其他指导，请参阅[Mmping](#mapping)部分。

有关详细信息，请访问[[!DNL Pendo] 帮助中心](https://www.pendo.io/help-center/)。
