---
title: 元转换API扩展概述
description: 了解Adobe Experience Platform中用于事件转发的Meta Conversions API扩展。
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: e7d63ff86cdc1718129d0a8e4861b6a8c4631f75
workflow-type: tm+mt
source-wordcount: '2565'
ht-degree: 0%

---

# [!DNL Meta Conversions API] 扩展概述

此 [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) 允许您将服务器端营销数据连接到 [!DNL Meta] 技术，以优化广告定位、降低每次操作的成本并衡量结果。 事件链接到 [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID和的处理方式与客户端事件类似。

使用 [!DNL Meta Conversions API] 扩展上，您可以利用API在 [事件转发](../../../ui/event-forwarding/overview.md) 将数据发送到的规则 [!DNL Meta] 来自Adobe Experience Platform Edge Network。 本文档介绍如何安装扩展并在事件转发中使用其功能 [规则](../../../ui/managing-resources/rules.md).

## 先决条件

强烈建议使用 [!DNL Meta Pixel] 和 [!DNL Conversions API] 以分别从客户端和服务器端共享和发送相同的事件，因为这有助于恢复未提取的事件 [!DNL Meta Pixel]. 安装之前 [!DNL Conversions API] 扩展上，请参阅 [[!DNL Meta Pixel] 扩展](../../client/meta/overview.md) 以了解如何将其集成到客户端标记实施中的步骤。

>[!NOTE]
>
>上的部分 [事件去重](#deduplication) 本文档稍后将介绍确保同一事件不被使用两次的步骤，因为从浏览器和服务器都可能会收到该事件。

要使用 [!DNL Conversions API] 扩展上，您必须有权访问事件转发并具有有效的 [!DNL Meta] 具有访问权限的帐户 [!DNL Ad Manager] 和 [!DNL Event Manager]. 具体而言，您必须复制现有 [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (或 [新建 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) 相反)，以便可以为您的帐户配置扩展。

>[!INFO]
>
>如果您计划将此扩展与移动应用程序数据一起使用，或者如果您还在 [!DNL Meta] 营销活动，您将需要通过现有应用程序创建数据集并选择 **从像素ID创建** 出现提示时。 请参阅文章 [确定适合您的企业的数据集创建选项](https://www.facebook.com/business/help/5270377362999582?id=490360542427371) 以了解详细信息。 请参阅 [应用程序事件的转化API](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) 提供了有关所有必需和可选应用程序跟踪参数的文档。

## 安装扩展

安装 [!DNL Meta Conversions API] 扩展中，导航到数据收集UI或Experience PlatformUI并选择 **[!UICONTROL 事件转发]** 从左侧导航栏中。 在此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的属性后，选择 **[!UICONTROL 扩展]** 在左侧导航中，然后选择 **[!UICONTROL 目录]** 选项卡。 搜索 [!UICONTROL 元转化API] 信息卡，然后选择 **[!UICONTROL 安装]**.

![此 [!UICONTROL 安装] 为选择的选项 [!UICONTROL 元转化API] 数据收集UI中的扩展。](../../../images/extensions/server/meta/install.png)

在显示的配置视图中，您必须提供 [!DNL Pixel] 您之前复制的ID用于将扩展关联到您的帐户。 您可以将ID直接粘贴到输入中，也可以改用数据元素。

您还需要提供访问令牌以使用 [!DNL Conversions API] 具体来说。 请参阅 [!DNL Conversions API] 文档 [生成访问令牌](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) 以获取有关如何获取此值的步骤。

完成后，选择 **[!UICONTROL 保存]**

![此 [!DNL Pixel] 在扩展配置视图中作为数据元素提供的ID。](../../../images/extensions/server/meta/configure.png)

扩展已安装，您现在可以在事件转发规则中使用该扩展的功能。

## 与元业务扩展(MBE)集成 {#mbe}

与元业务扩展(MBE)增强功能的集成允许您快速向元业务帐户进行身份验证。 然后，这会自动填充 [!UICONTROL 像素Id] 和元转化API [!UICONTROL 访问令牌]，更轻松地安装和配置元转化API。

安装时，会出现在MBE中进行身份验证的对话框提示 [!UICONTROL 元转化API] 扩展。

![此 [!UICONTROL 元转化API扩展] 安装页面突出显示 [!UICONTROL 连接到元].](../../../images/extensions/server/meta/mbe-extension-install.png)

在事件转发的快速启动工作流UI中，还会显示在MBE中进行身份验证的对话框提示。

![快速入门工作流UI高亮显示 [!UICONTROL 连接到元].](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## 与事件质量匹配分数(EMQ)集成 {#emq}

与事件质量匹配分数(EMQ)集成允许您通过显示EMQ分数来轻松查看实施的有效性。 此集成最大限度地减少了上下文切换，并帮助您提高元转换API实施的成功。 这些事件得分显示在 [!UICONTROL 元转化API扩展] 配置屏幕。

![此 [!UICONTROL 元转化API扩展] 配置页面突出显示 [!UICONTROL 查看EMQ得分].](../../../images/extensions/server/meta/emq-score.png)

## 与LiveRamp(Alpha)集成 {#alpha}

[!DNL LiveRamp] 客户具有 [!DNL LiveRamp]其网站上部署的经过身份验证的流量解决方案(ATS)可能会选择将RampID作为客户信息参数共享。 请与您的 [!DNL Meta] 客户团队，加入此功能的Alpha计划。

![元事件转发 [!UICONTROL 规则] 配置页面突出显示 [!UICONTROL 合作伙伴名称(alpha)] 和 [!UICONTROL 合作伙伴ID (alpha)].](../../../images/extensions/server/meta/live-ramp.png)

## 配置事件转发规则 {#rule}

本节介绍如何使用 [!DNL Conversions API] 扩展中相同的事件转发规则。 实际上，您应该配置多个规则以发送所有已接受的规则 [标准事件](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] 和 [!DNL Conversions API]. 有关移动应用程序数据，请参阅必填字段、应用程序数据字段、客户信息参数和自定义数据详细信息 [此处](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events).

>[!NOTE]
>
>事件应为 [实时发送](https://www.facebook.com/business/help/379226453470947?id=818859032317965) 或尽可能接近实时以更好地优化广告活动。

开始创建新的事件转发规则，并根据需要配置其条件。 为规则选择操作时，选择 **[!UICONTROL 元转化API扩展]** 对于扩展，然后选择 **[!UICONTROL 发送转化API事件]** 操作类型的。

![此 [!UICONTROL 发送页面查看] 为数据收集UI中的规则选择的操作类型。](../../../images/extensions/server/meta/select-action.png)

显示的控件允许您配置将发送到的事件数据 [!DNL Meta] 通过 [!DNL Conversions API]. 这些选项可以直接输入到提供的输入中，也可以选择现有数据元素来表示值。 配置选项分为四个主要部分，如下所述。

| 配置区域 | 描述 |
| --- | --- |
| [!UICONTROL 服务器事件参数] | 有关事件的常规信息，包括发生时间和触发该事件的源操作。 请参阅 [!DNL Meta] 开发人员文档，以了解有关 [标准事件参数](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) 已接受 [!DNL Conversions API].<br><br>如果您同时使用两者 [!DNL Meta Pixel] 和 [!DNL Conversions API] 要发送事件，请确保同时包含 **[!UICONTROL 事件名称]** (`event_name`)和 **[!UICONTROL 事件ID]** (`event_id`)，因为这些值用于 [事件去重](#deduplication).<br><br>您还可以选择 **[!UICONTROL 启用有限数据使用]** 以帮助遵守客户选择退出的要求。 请参阅 [!DNL Conversions API] 文档 [数据处理选项](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) 以了解有关此功能的详细信息。 |
| [!UICONTROL 客户信息参数] | 用于将事件归因于客户的用户身份数据。 在将某些值发送到API之前，必须对它们进行哈希处理。<br><br>为确保良好的通用API连接和高事件匹配质量(EMQ)，建议您发送所有 [接受的客户信息参数](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) 以及服务器事件。 这些参数还应 [根据它们对EMQ的重要性和影响确定优先级](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL 自定义数据] | 用于广告投放优化的附加数据，以JSON对象的形式提供。 请参阅 [[!DNL Conversions API] 文档](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) 以了解有关该对象接受的属性的更多信息。<br><br>如果要发送购买事件，则必须使用此部分提供所需的属性 `currency` 和 `value`. |
| [!UICONTROL 测试事件] | 此选项用于验证您的配置是否导致接收服务器事件 [!DNL Meta] 如预期。 要使用此功能，请选择 **[!UICONTROL 作为测试事件发送]** 复选框，然后在以下输入中提供您选择的测试事件代码。 部署事件转发规则后，如果您正确配置了扩展和操作，则您应该会看到活动出现在 **[!DNL Test Events]** 在中查看 [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

完成后，选择 **[!UICONTROL 保留更改]** 将操作添加到规则配置。

![[!UICONTROL 保留更改] 操作配置处于选中状态。](../../../images/extensions/server/meta/keep-changes.png)

如果对规则满意，请选择 **[!UICONTROL 保存到库]**. 最后，发布新的事件转发 [生成](../../../ui/publishing/builds.md) 以启用对库所做的更改。

## 事件去重 {#deduplication}

如 [“先决条件”部分](#prerequisites)，建议您同时使用 [!DNL Meta Pixel] 标记扩展和 [!DNL Conversions API] 事件转发扩展，用于在冗余设置中从客户端和服务器发送相同事件。 这有助于恢复一个扩展或其他扩展未拾取的事件。

如果您从客户端和服务器发送不同的事件类型，且两者之间没有重叠，则无需进行重复数据删除。 但是，如果任何单个事件由两者共享 [!DNL Meta Pixel] 和 [!DNL Conversions API]中，您必须确保为这些冗余事件去重，以免对报表造成负面影响。

发送共享事件时，请确保包括事件ID和名称，以及您从客户端和服务器发送的每个事件。 接收到具有相同ID和名称的多个事件时， [!DNL Meta] 自动采用多种策略来消除重复并保留最相关的数据。 请参阅 [!DNL Meta] 文档 [删除重复项 [!DNL Meta Pixel] 和 [!DNL Conversions API] 事件](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) 以了解有关该过程的详细信息。

## 快速入门工作流：Meta Conversions API扩展（测试版） {#quick-start}

>[!IMPORTANT]
>
>* 已购买Real-Time CDP Prime和Ultimate包的客户可以使用快速入门功能。 请联系您的Adobe代表以获取更多信息。
>* 此功能适用于全新实施，当前不支持在现有标记和事件转发属性上自动安装扩展和配置。

>[!NOTE]
>
>任何现有客户端都可以使用快速入门工作流创建可用于以下项目的参考实施：
>* 使用它作为全新实施的开始。
>* 将其用作参考实施，您可以检查该实施，以了解其配置方式，然后将其复制到当前生产实施中。

快速入门功能可帮助您通过元转化API和元像素扩展轻松高效地完成设置。 此工具可自动执行在Adobe标签和事件转发中执行的多个步骤，从而显着缩短设置时间。

此功能会在新自动生成的标记上自动安装和配置元转化API和元像素扩展，并使用必要的规则和数据元素来配置事件转发属性。 此外，它还会自动安装和配置Experience PlatformWeb SDK和数据流。 最后，快速启动功能会自动将库发布到开发环境中的指定URL中，从而支持通过事件转发和Experience Platform边缘网络实时进行客户端数据收集和服务器端事件转发。

以下视频介绍了快速入门功能。

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### 安装快速入门功能

>[!NOTE]
>
>此功能旨在帮助您开始实施事件转发。 它不会提供可容纳所有用例的端到端、完全正常的实施。

此设置会自动安装元转化API和元像素扩展。 Meta建议使用此混合实施来收集和转发事件转换。
快速设置功能旨在帮助客户开始事件转发实施，而不是提供可适应所有用例的端到端、功能齐全的实施。

要安装该功能，请选择 **[!UICONTROL 开始使用]** 对象 **[!DNL Send Conversions Data to Meta]** 关于Adobe Experience Platform数据收集 **[!UICONTROL 主页]** 页面。

![数据收集主页，其中显示到元数据的转化数据](../../../images/extensions/server/meta/conversion-data-to-meta.png)

输入您的 **[!UICONTROL 域]**，然后选择 **[!UICONTROL 下一个]**. 此域将用作自动生成的标记和事件转发属性、规则、数据元素、数据流等的命名约定。

![请求域名的欢迎屏幕](../../../images/extensions/server/meta/welcome.png)

在 **[!UICONTROL 初始设置]** 对话框输入您的 **[!UICONTROL 元像素ID]**， **[!UICONTROL 元转换API访问令牌]**、和 **[!UICONTROL 数据层路径]**，然后选择 **[!UICONTROL 下一个]**.

![初始设置对话框](../../../images/extensions/server/meta/initial-setup.png)

等待几分钟以完成初始设置过程，然后选择 **[!UICONTROL 下一个]**.

![初始设置完成确认屏幕](../../../images/extensions/server/meta/setup-complete.png)

从 **[!UICONTROL 在您的网站上添加代码]** 对话框复制使用复制提供的代码 ![复制](../../../images/extensions/server/meta/copy-icon.png) 函数并将其粘贴到 `<head>` 源网站的。 实施后，选择 **[!UICONTROL 开始验证]**

![在站点对话框中添加代码](../../../images/extensions/server/meta/add-code-on-your-site.png)

此 [!UICONTROL 验证结果] 对话框显示元扩展实施结果。 选择 **[!UICONTROL 下一个]**. 您还可以通过选择 **[!UICONTROL Assurance]** 链接。

![显示实施结果的测试结果对话框](../../../images/extensions/server/meta/test-results.png)

此 **[!UICONTROL 后续步骤]** 屏幕显示确认设置完成。 在此处，您可以选择通过添加新事件来优化实施，下一部分将显示这些事件。

如果不想添加其他事件，请选择 **[!UICONTROL 关闭]**.

![后续步骤对话框](../../../images/extensions/server/meta/next-steps.png)

#### 添加其他事件

要添加新事件，请选择 **[!UICONTROL 编辑标记Web属性]**.

![显示编辑标记Web属性的后续步骤对话框](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

选择与要编辑的元事件对应的规则。 例如， **MetaConversion_AddToCart**.

>[!NOTE]
>
>如果没有事件，则此规则将不会运行。 这适用于所有规则，包括 **MetaConversion_PageView** 规则是例外。

要添加事件，请选择 **[!UICONTROL 添加]** 在 [!UICONTROL 活动] 标题。

![标记属性页面未显示任何事件](../../../images/extensions/server/meta/edit-rule.png)

选择 [!UICONTROL 事件类型]. 在此示例中，我们已选择 [!UICONTROL 单击] 事件并将其配置为在 **.add-to-cart-button** 已选中。 选择&#x200B;**[!UICONTROL 保留更改]**。

![显示点击事件的事件配置屏幕](../../../images/extensions/server/meta/event-configuration.png)

已保存新事件。 选择 **[!UICONTROL 选择工作库]** 并选择要生成到的库。

![选择工作库下拉列表](../../../images/extensions/server/meta/working-library.png)

接下来，选择旁边的下拉菜单 **[!UICONTROL 保存到库]** 并选择 **[!UICONTROL 保存到库并生成]**. 这会将更改发布到库中。

![选择save to library and build](../../../images/extensions/server/meta/save-and-build.png)

对要配置的任何其他元转化事件重复这些步骤。

#### 数据层配置 {#configuration}

>[!IMPORTANT]
>
>更新此全局数据层的方式取决于您的网站架构。 单页应用程序将与服务器端渲染应用程序不同。 另外，您可能将完全负责在Tags产品中创建和更新此数据。 在所有情况下，在运行每个 `MetaConversion_* rules`. 如果不更新规则之间的数据，您还可能会遇到发送上次使用的过时数据的情况 `MetaConversion_* rule` 在当前的 `MetaConversion_* rule`.

在配置过程中，系统会询问您数据层的存放位置。 默认情况下，这将 `window.dataLayer.meta`，并在内部 `meta` 对象，您的数据应如下所示。

![数据层元数据](../../../images/extensions/server/meta/data-layer-meta.png)

这一点很重要，因为 `MetaConversion_*` 规则使用此数据结构将相关的数据段传递到 [!DNL Meta Pixel] 扩展和 [!DNL Meta Conversions API]. 请参阅有关以下内容的文档 [标准事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) 有关不同元事件需要哪些数据的更多信息。

例如，如果要使用 `MetaConversion_Subscribe` 规则，您需要更新 `window.dataLayer.meta.currency`， `window.dataLayer.meta.predicted_ltv`、和 `window.dataLayer.meta.value` 根据上的文档所述的对象属性 [标准事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events).

以下是在执行规则之前需要在网站上运行以更新数据层的示例。

![更新数据层元信息](../../../images/extensions/server/meta/update-data-layer-meta.png)

默认情况下， `<datalayerpath>.conversionData.eventId` “生成新事件ID”操作将随机生成的任何事件 `MetaConversion_* rules`.

要获取数据层外观的本地参考，您可以在 `MetaConversion_DataLayer` 资产上的数据元素。

## 后续步骤

本指南介绍了如何将服务器端事件数据发送到 [!DNL Meta] 使用 [!DNL Meta Conversions API] 扩展。 在此处，建议通过连接更多来扩展您的集成 [!DNL Pixels] 并在适用的情况下共享更多事件。 执行以下任一操作均有助于进一步改善广告性能：

* 连接任何其他 [!DNL Pixels] 尚未连接到 [!DNL Conversions API] 集成。
* 如果您专门通过发送某些事件 [!DNL Meta Pixel] 在客户端，将这些相同的事件发送到 [!DNL Conversions API] 服务器端。

请参阅 [!DNL Meta] 文档 [的最佳实践 [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 以获取有关如何有效实施集成的更多指导。 有关Adobe Experience Cloud中标记和事件转发的更多常规信息，请参阅 [标记概述](../../../home.md).
