---
title: 元像素扩展概述
description: 了解Adobe Experience Platform中的Meta Pixel标记扩展。
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] 扩展概述

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) 是一个基于JavaScript的分析工具，可用于跟踪网站上的访客活动。 您跟踪的访客操作（称为转化）将发送至 [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) 在中，它们可用于衡量广告、促销活动、转化漏斗等项的有效性。

此 [!DNL Meta Pixel] 标记扩展允许您利用 [!DNL Pixel] 客户端标记库中的功能。 本文档介绍了如何安装扩展以及如何在中使用扩展的功能。 [规则](../../../ui/managing-resources/rules.md).

## 先决条件

要使用扩展，您必须具有有效的 [!DNL Meta] 有权访问的帐户 [!DNL Ads Manager]. 具体而言，您必须 [新建 [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) 并复制 [!DNL Pixel ID] 以便可以为您的帐户配置该扩展。 如果您已经拥有 [!DNL Meta Pixel]，您可以改用其ID。

强烈建议使用 [!DNL Meta Pixel] 与 [!DNL Meta Conversions API] 以分别从客户端和服务器端共享和发送相同的事件，因为这有助于恢复未提取的事件 [!DNL Meta Pixel]. 请参阅 [[!DNL Meta Conversions API] 事件转发的扩展](../../client/meta/overview.md) ，了解如何将其集成到服务器端实施中。 请注意，您的组织必须有权访问 [事件转发](../../../ui/event-forwarding/overview.md) 才能使用服务器端扩展。

## 安装扩展

安装 [!DNL Meta Pixel] 扩展上，导航到数据收集UI或Experience PlatformUI并选择 **[!UICONTROL 标记]** 从左侧导航栏中。 在此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的属性后，选择 **[!UICONTROL 扩展]** 在左侧导航中，然后选择 **[!UICONTROL 目录]** 选项卡。 搜索 [!UICONTROL 元像素] 信息卡，然后选择 **[!UICONTROL 安装]**.

![此 [!UICONTROL 安装] 已为选择按钮 [!UICONTROL 元像素] 数据收集UI中的扩展。](../../../images/extensions/client/meta/install.png)

在显示的配置视图中，您必须提供 [!DNL Pixel] 您之前复制的ID用于将扩展链接到您的帐户。 您可以将ID直接粘贴到输入中，也可以选择现有的数据元素。

>[!TIP]
>
>通过使用数据元素，您可以选择动态更改 [!DNL Pixel] 使用的ID取决于其他因素，例如构建环境。 请参阅附录中关于 [使用不同的 [!DNL Pixel] 不同环境的ID](#id-data-element) 了解更多信息。

您还可以选择提供要与扩展关联的事件ID。 这用于删除以下时间之间的相同事件： [!DNL Meta Pixel] 和 [!DNL Meta Conversions API]. 有关详细信息，请参阅 [事件去重](../../server/meta/overview.md#event-deduplication) 在概述中 [!DNL Conversions API] 扩展。

完成后，选择 **[!UICONTROL 保存]**

![此 [!DNL Pixel] 在扩展配置视图中作为数据元素提供的ID。](../../../images/extensions/client/meta/configure.png)

扩展已安装，您现在可以在标记规则中运用其各种操作。

## 配置标记规则 {#rule}

[!DNL Meta Pixel] 接受一组预定义的 [标准事件](https://www.facebook.com/business/help/402791146561655)，每个页面都有自己的上下文和接受的属性。 规则操作由 [!DNL Pixel] 扩展与这些事件类型相关联，这使您能够轻松分类并配置要发送到的事件 [!DNL Meta] 根据其类型而定。

出于演示目的，此部分将演示如何构建将页面查看事件发送到的规则 [!DNL Meta].

开始创建新标记规则，并根据需要配置其条件。 为规则选择操作时，选择 **[!UICONTROL 元像素]** 对于扩展，然后选择 **[!UICONTROL 发送页面查看]** 操作类型对应的。

![此 [!UICONTROL 发送页面查看] 为数据收集UI中的规则选择的操作类型。](../../../images/extensions/client/meta/select-action.png)

无需进一步配置 [!UICONTROL 发送页面查看] 操作。 选择 **[!UICONTROL 保留更改]** 以将操作添加到规则配置。 如果对规则满意，请选择 **[!UICONTROL 保存到库]**.

最后，发布新标记 [生成](../../../ui/publishing/builds.md) 以启用对库的更改。

## 确认 [!DNL Meta] 正在接收数据

将更新的内部版本部署到您的网站后，您可以在浏览器中生成一些转化事件并检查这些事件是否显示在中，从而确认数据是否按预期发送 [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## 后续步骤

本指南介绍了如何将数据发送到 [!DNL Meta] 使用 [!DNL Meta Pixel] 标记扩展。 如果您还计划向发送服务器端事件 [!DNL Meta]，您现在可以继续安装和配置 [[!DNL Conversions API] 事件转发扩展](../../server/meta/overview.md).

有关Experience Platform中标记的详细信息，请参阅 [标记概述](../../../home.md).

## 附录：使用不同的 [!DNL Pixel] 不同环境的ID {#id-data-element}

如果您希望在开发或暂存环境中测试实施，同时保留生产 [!DNL Meta Pixel] analytics保持不变，您可以使用数据元素动态选择合适的 [!DNL Pixel] ID，具体取决于所使用的环境。

您可以使用实现此目标 [!UICONTROL 自定义代码] 数据元素(由 [[!UICONTROL 核心] 扩展](../core/overview.md))与 [`turbine` 自由变量](../../../extension-dev/turbine.md). 在数据元素的JavaScript代码中，使用 `turbine` 对象以查找当前环境阶段，然后返回相应的 [!DNL Pixel] 基于结果的ID。

以下示例返回一个虚假的生产ID `exampleProductionKey` 在生产环境中使用时，以及不同的ID `exampleTestKey` 当使用任何其他环境时。 实施此代码时，请将每个值替换为实际的生产和测试 [!DNL Pixel] ID。

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
