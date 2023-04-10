---
title: 元转化API扩展概述
description: 了解用于Adobe Experience Platform中事件转发的元转化API扩展。
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 6538599e10d4980c3890a8fba65c8ef51c24496a
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 0%

---

# [!DNL Meta Conversions API] 扩展概述

的 [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) 允许您将服务器端营销数据连接到 [!DNL Meta] 技术，以优化广告定位、降低每项操作的成本并衡量结果。 事件与 [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID和的处理方式与客户端事件类似。

使用 [!DNL Meta Conversions API] 扩展，您可以在 [事件转发](../../../ui/event-forwarding/overview.md) 将数据发送到的规则 [!DNL Meta] 从Adobe Experience Platform边缘网络。 本文档介绍如何安装扩展并在事件转发中使用其功能 [规则](../../../ui/managing-resources/rules.md).

## 先决条件

强烈建议使用 [!DNL Meta Pixel] 和 [!DNL Conversions API] 共享和发送来自客户端和服务器端的相同事件，因为这可能有助于恢复未被 [!DNL Meta Pixel]. 安装之前 [!DNL Conversions API] 扩展，请参阅 [[!DNL Meta Pixel] 扩展](../../client/meta/overview.md) 以了解如何将其集成到客户端标记实施中的步骤。

>[!NOTE]
>
>上的部分 [事件重复数据删除](#deduplication) 本文档的后面部分介绍了确保同一事件不被使用两次的步骤，因为同一事件可能会从浏览器和服务器收到。

为了使用 [!DNL Conversions API] 扩展中，您必须具有事件转发的访问权限，并且 [!DNL Meta] 有权访问的帐户 [!DNL Ad Manager] 和 [!DNL Event Manager]. 具体而言，您必须复制现有 [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (或 [新建 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) )，以便可以将扩展配置到您的帐户。

## 安装扩展

安装 [!DNL Meta Conversions API] 扩展中，导航到数据收集UI或Experience PlatformUI，然后选择 **[!UICONTROL 事件转发]** 的上界。 从此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的资产后，请选择 **[!UICONTROL 扩展]** 在左侧导航中，选择 **[!UICONTROL 目录]** 选项卡。 搜索 [!UICONTROL 元转化API] 卡片，然后选择 **[!UICONTROL 安装]**.

![的 [!UICONTROL 安装] 按钮 [!UICONTROL 元转化API] 扩展。](../../../images/extensions/server/meta/install.png)

在显示的配置视图中，必须提供 [!DNL Pixel] 您之前复制的ID，用于将扩展关联到您的帐户。 您可以将ID直接粘贴到输入中，也可以改用数据元素。

您还需要提供访问令牌才能使用 [!DNL Conversions API] 具体而言。 请参阅 [!DNL Conversions API] 文档 [生成访问令牌](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) 以了解有关如何获取此值的步骤。

完成后，选择 **[!UICONTROL 保存]**

![的 [!DNL Pixel] 作为扩展配置视图中的数据元素提供的ID。](../../../images/extensions/server/meta/configure.png)

已安装扩展，您现在可以将其功能应用于事件转发规则中。

## 配置事件转发规则 {#rule}

本节介绍如何使用 [!DNL Conversions API] 扩展。 实际上，您应该配置多个规则以发送所有已接受的规则 [标准事件](https://developers.facebook.com/docs/meta-pixel/reference) 通过 [!DNL Meta Pixel] 和 [!DNL Conversions API].

>[!NOTE]
>
>事件应为 [实时发送](https://www.facebook.com/business/help/379226453470947?id=818859032317965) 或尽可能接近实时，以优化广告活动。

开始创建新的事件转发规则，并根据需要配置其条件。 为规则选择操作时，选择 **[!UICONTROL 元转化API扩展]** 对于扩展，选择 **[!UICONTROL 发送转化API事件]** （对于操作类型）。

![的 [!UICONTROL 发送页面查看] 在数据收集UI中为规则选择的操作类型。](../../../images/extensions/server/meta/select-action.png)

此时会显示允许您配置要发送到的事件数据的控件 [!DNL Meta] 通过 [!DNL Conversions API]. 这些选项可以直接输入到提供的输入中，或者您可以选择现有数据元素来表示值。 配置选项分为四个主要部分，如下所述。

| 配置部分 | 描述 |
| --- | --- |
| [!UICONTROL 服务器事件参数] | 有关事件的一般信息，包括事件发生的时间以及触发该事件的源操作。 请参阅 [!DNL Meta] 开发人员文档，以了解有关 [标准事件参数](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) 被接受 [!DNL Conversions API].<br><br>如果您同时使用 [!DNL Meta Pixel] 和 [!DNL Conversions API] 要发送事件，请确保将 **[!UICONTROL 事件名称]** (`event_name`)和 **[!UICONTROL 事件ID]** (`event_id`)，因为这些值用于 [事件重复数据删除](#deduplication).<br><br>您还可以选择 **[!UICONTROL 启用有限数据使用]** 以帮助遵守客户的选择退出。 请参阅 [!DNL Conversions API] 文档 [数据处理选项](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) 有关此功能的详细信息。 |
| [!UICONTROL 客户信息参数] | 用于将事件归因给客户的用户标识数据。 其中某些值必须先经过哈希处理，然后才能发送到API。<br><br>为确保良好的常用API连接和高事件匹配质量(EMQ)，建议您发送所有 [已接受的客户信息参数](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) 与服务器事件一起使用。 这些参数还应为 [根据其重要性和对EMQ的影响确定优先级](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL 自定义数据] | 要用于广告投放优化的其他数据，以JSON对象的形式提供。 请参阅 [[!DNL Conversions API] 文档](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) 有关此对象已接受属性的详细信息。<br><br>如果您发送购买事件，则必须使用此部分提供所需的属性 `currency` 和 `value`. |
| [!UICONTROL 测试事件] | 此选项用于验证您的配置是否导致服务器事件被 [!DNL Meta] 如预期。 要使用此功能，请选择 **[!UICONTROL 作为测试事件发送]** 复选框，然后在以下输入中提供您选择的测试事件代码。 部署事件转发规则后，如果正确配置了扩展和操作，则应会在 **[!DNL Test Events]** 查看 [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

完成后，选择 **[!UICONTROL 保留更改]** 将操作添加到规则配置。

![[!UICONTROL 保留更改] 正在为操作配置选择。](../../../images/extensions/server/meta/keep-changes.png)

如果您对规则满意，请选择 **[!UICONTROL 保存到库]**. 最后，发布新的事件转发 [构建](../../../ui/publishing/builds.md) 以启用对库所做的更改。

## 事件去重 {#deduplication}

如 [先决条件部分](#prerequisites)，建议您同时使用 [!DNL Meta Pixel] 标记扩展和 [!DNL Conversions API] 事件转发扩展，用于在冗余设置中从客户端和服务器发送相同的事件。 这有助于恢复一个扩展或另一个扩展未提取的事件。

如果您从客户端和服务器发送不同的事件类型，但二者之间没有重叠，则无需进行重复数据删除。 但是，如果两者共享任何单个事件 [!DNL Meta Pixel] 和 [!DNL Conversions API]，则必须确保删除这些重复事件，以便不会对报告产生不利影响。

发送共享事件时，请确保包含事件ID和名称，以及从客户端和服务器发送的每个事件。 收到多个ID和名称相同的事件时， [!DNL Meta] 会自动使用多种策略来删除重复项并保留最相关的数据。 请参阅 [!DNL Meta] 文档 [重复数据删除 [!DNL Meta Pixel] 和 [!DNL Conversions API] 事件](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) 以了解此过程的详细信息。

## 快速启动工作流：元转化API扩展（测试版） {#quick-start}

>[!IMPORTANT]
>
>* 快速入门功能适用于已购买Real-Time CDP Prime和Ultimate软件包的客户。 有关更多信息，请联系您的Adobe代表。
>* 此功能适用于新的新实施，当前不支持在现有标记和事件转发属性上自动安装扩展和配置。


快速入门功能可帮助您轻松高效地设置元转化API和元像素扩展。 此工具可自动执行Adobe标记和事件转发中执行的多个步骤，从而显着缩短设置时间。

此功能可使用必要的规则和数据元素，在新自动生成的标记和事件转发属性上自动安装和配置元转化API和元像素扩展。 此外，它还会自动安装和配置Experience PlatformWeb SDK和数据流。 最后，快速入门功能会在开发环境中自动将库发布到指定的URL，从而通过事件转发和Experience Edge实时收集客户端数据和进行服务器端事件转发。

以下视频介绍了快速入门功能。

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### 安装快速入门功能

>[!NOTE]
>
>此功能旨在帮助您开始实施事件转发。 它不会提供适用于所有用例的端到端、功能完备的实施。

此设置会自动安装元转换API和元像素扩展。 Meta建议使用此混合实施来收集和转发事件转化服务器端。
快速设置功能旨在帮助客户开始实施事件转发，而不是旨在提供适用于所有用例的端到端、功能完备的实施。

要安装该功能，请选择 **[!UICONTROL 入门]** 表示 **[!DNL Send Conversions Data to Meta]** 在Adobe Experience Platform数据收集上 **[!UICONTROL 主页]** 页面。

![数据收集主页显示转化数据到元](../../../images/extensions/server/meta/conversion-data-to-meta.png)

输入 **[!UICONTROL 域]**，然后选择 **[!UICONTROL 下一个]**. 此域将用作自动生成的标记和事件转发属性、规则、数据元素、数据流等的命名约定。

![欢迎屏幕请求域名](../../../images/extensions/server/meta/welcome.png)

在 **[!UICONTROL 初始设置]** 对话框输入 **[!UICONTROL 元像素ID]**, **[!UICONTROL 元转换API访问令牌]**&#x200B;和 **[!UICONTROL 数据层路径]**，然后选择 **[!UICONTROL 下一个]**.

![初始设置对话框](../../../images/extensions/server/meta/initial-setup.png)

需要几分钟才能完成初始设置过程，然后选择 **[!UICONTROL 下一个]**.

![初始设置完成确认屏幕](../../../images/extensions/server/meta/setup-complete.png)

从 **[!UICONTROL 在您的网站上添加代码]** 对话框复制使用副本提供的代码 ![复制](../../../images/extensions/server/meta/copy-icon.png) 函数并将其粘贴到 `<head>` 源网站的。 实施后，选择 **[!UICONTROL 开始验证]**

![在网站对话框中添加代码](../../../images/extensions/server/meta/add-code-on-your-site.png)

的 [!UICONTROL 验证结果] 对话框显示元扩展实施结果。 选择&#x200B;**[!UICONTROL 下一步]**。您还可以通过选择 **[!UICONTROL 保证]** 链接。

![显示实施结果的测试结果对话框](../../../images/extensions/server/meta/test-results.png)

的 **[!UICONTROL 后续步骤]** 屏幕显示确认设置已完成。 在此，您可以选择通过添加新事件来优化实施，这些事件将显示在下一节中。

如果不想添加其他事件，请选择 **[!UICONTROL 关闭]**.

![“下一步”对话框](../../../images/extensions/server/meta/next-steps.png)

#### 添加其他事件

要添加新事件，请选择 **[!UICONTROL 编辑标记Web属性]**.

![显示编辑标记Web属性的“下一步”对话框](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

选择与要编辑的元事件对应的规则。 例如， **MetaConversion_AddToCart**.

>[!NOTE]
>
>如果没有事件，则不会运行此规则。 对于所有规则，都是如此， **MetaConversion_PageView** 规则为例外。

添加事件选择 **[!UICONTROL 添加]** 下 [!UICONTROL 事件] 标题。

![“标记属性”页面不显示事件](../../../images/extensions/server/meta/edit-rule.png)

选择 [!UICONTROL 事件类型]. 在本例中，我们选择了 [!UICONTROL 单击] 事件，并将其配置为在 **.add-to-cart-button** 中。 选择&#x200B;**[!UICONTROL 保留更改]**。

![显示点击事件的事件配置屏幕](../../../images/extensions/server/meta/event-configuration.png)

已保存新事件。 选择 **[!UICONTROL 选择工作库]** 并选择要构建到的库。

![选择工作库下拉列表](../../../images/extensions/server/meta/working-library.png)

接下来，选择旁边的下拉菜单 **[!UICONTROL 保存到库]** 选择 **[!UICONTROL 保存到库并构建]**. 这将在库中发布更改。

![选择保存到库并生成](../../../images/extensions/server/meta/save-and-build.png)

对要配置的任何其他元转换事件重复这些步骤。

#### 数据层配置 {#configuration}

>[!IMPORTANT]
>
>更新此全局数据层的方式取决于您的网站架构。 单页应用程序与服务器端渲染应用程序将不同。 您还可能完全负责在标记产品中创建和更新此数据。 在所有情况下，都需要在运行 `MetaConversion_* rules`. 如果不在规则之间更新数据，则还可能会遇到发送最后一个规则的过时数据的情况 `MetaConversion_* rule` 在 `MetaConversion_* rule`.

在配置过程中，系统会询问您数据层的居住位置。 默认情况下，这将为 `window.dataLayer.meta`，和内部 `meta` 对象，则您的数据将会如下所示。

![数据层元信息](../../../images/extensions/server/meta/data-layer-meta.png)

这一点很重要 `MetaConversion_*` 规则使用此数据结构将相关数据段传递到 [!DNL Meta Pixel] 扩展和 [!DNL Meta Conversions API]. 请参阅 [标准事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) 有关不同元事件需要哪些数据的更多信息。

例如，如果您想要使用 `MetaConversion_Subscribe` 规则，您需要更新 `window.dataLayer.meta.currency`, `window.dataLayer.meta.predicted_ltv`和 `window.dataLayer.meta.value` 根据 [标准事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events).

以下示例说明了在执行规则之前需要在网站上运行什么才能更新数据层。

![更新数据层元信息](../../../images/extensions/server/meta/update-data-layer-meta.png)

默认情况下， `<datalayerpath>.conversionData.eventId` 将由任何 `MetaConversion_* rules`.

有关数据层外观的本地引用，您可以在 `MetaConversion_DataLayer` 数据元素。

## 后续步骤

本指南介绍了如何将服务器端事件数据发送到 [!DNL Meta] 使用 [!DNL Meta Conversions API] 扩展。 从此处，建议通过连接更多来扩展您的集成 [!DNL Pixels] 和共享更多事件（如果适用）。 执行以下任一操作可帮助您进一步提高广告性能：

* 连接任何其他 [!DNL Pixels] 尚未与 [!DNL Conversions API] 集成。
* 如果您只通过 [!DNL Meta Pixel] 在客户端，将这些相同的事件发送到 [!DNL Conversions API] 从服务器端。

请参阅 [!DNL Meta] 文档 [最佳实践 [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 有关如何有效实施集成的更多指导。 有关Adobe Experience Cloud中标记和事件转发的更多常规信息，请参阅 [标记概述](../../../home.md).
