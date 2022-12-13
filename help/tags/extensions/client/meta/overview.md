---
title: 元像素扩展概述
description: 了解Adobe Experience Platform中的Meta Pixel标记扩展。
source-git-commit: 87376172f89858bfa883084461544a2c50ba5009
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# [!DNL Meta Pixel] 扩展概述

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) 是一个基于JavaScript的分析工具，允许您跟踪网站上的访客活动。 您跟踪的访客操作（称为转化）将发送到 [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) 可用于衡量广告、促销活动、转化漏斗等内容的有效性。

的 [!DNL Meta Pixel] 标记扩展允许您利用 [!DNL Pixel] 功能。 本文档介绍如何在 [规则](../../../ui/managing-resources/rules.md).

<!-- (To include when Conversions API extension doc is published)
>[!NOTE]
>
>If you are trying to send server-side events to [!DNL Meta] rather than from the client side, use the [[!DNL Meta Conversions API] extension](../../server/meta/overview.md) instead.
-->

## 先决条件

要使用该扩展，您必须具有 [!DNL Meta] 有权访问的帐户 [!DNL Ads Manager]. 具体而言，您必须 [新建 [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) 复制 [!DNL Pixel ID] 以便可以将扩展配置为您的帐户。 如果您已经有 [!DNL Meta Pixel]，则可以改用其ID。

## 安装扩展

安装 [!DNL Meta Pixel] 扩展中，导航到数据收集UI或Experience PlatformUI，然后选择 **[!UICONTROL 标记]** 的上界。 从此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的资产后，请选择 **[!UICONTROL 扩展]** 在左侧导航中，选择 **[!UICONTROL 目录]** 选项卡。 搜索 [!UICONTROL 元像素] 卡片，然后选择 **[!UICONTROL 安装]**.

![的 [!UICONTROL 安装] 按钮 [!UICONTROL 元像素] 扩展。](../../../images/extensions/client/meta/install.png)

在显示的配置视图中，必须提供 [!DNL Pixel] 您之前复制的ID，用于将扩展关联到您的帐户。 您可以将ID直接粘贴到输入中，也可以改为选择现有数据元素。

>[!TIP]
>
>通过使用数据元素，您可以选择动态更改 [!DNL Pixel] ID的使用取决于其他因素，例如构建环境。 请参阅 [使用不同 [!DNL Pixel] 不同环境的ID](#id-data-element) 以了解更多信息。

您还可以选择提供要与扩展关联的事件ID。 用于删除与 [!DNL Meta Pixel] 和 [!DNL Meta Conversions API]. 请参阅 [!DNL Meta] 文档 [处理重复项 [!DNL Pixel] 和 [!DNL Conversions API] 事件](https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/) 以了解详细信息。

完成后，选择 **[!UICONTROL 保存]**

![的 [!DNL Pixel] 作为扩展配置视图中的数据元素提供的ID。](../../../images/extensions/client/meta/configure.png)

扩展已安装，您现在可以在标记规则中使用其各种操作。

## 配置标记规则 {#rule}

[!DNL Meta Pixel] 接受一组预定义的 [标准事件](https://www.facebook.com/business/help/402791146561655)，每个资产具有自己的上下文和接受的属性。 提供的规则操作 [!DNL Pixel] 扩展会与这些事件类型关联，从而允许您轻松地对要发送到的事件进行分类和配置 [!DNL Meta] 根据其类型。

出于演示目的，此部分将演示如何构建规则以将页面查看事件发送到 [!DNL Meta].

开始创建新标记规则，并根据需要配置其条件。 为规则选择操作时，选择 **[!UICONTROL 元像素]** 对于扩展，选择 **[!UICONTROL 发送页面查看]** （对于操作类型）。

![的 [!UICONTROL 发送页面查看] 在数据收集UI中为规则选择的操作类型。](../../../images/extensions/client/meta/select-action.png)

无需进一步配置 [!UICONTROL 发送页面查看] 操作。 选择 **[!UICONTROL 保留更改]** 将操作添加到规则配置。 如果您对规则满意，请选择 **[!UICONTROL 保存到库]**.

最后，发布新标记 [构建](../../../ui/publishing/builds.md) 以启用对库的更改。

## 确认 [!DNL Meta] 正在接收数据

将更新的内部版本部署到您的网站后，您可以通过在浏览器上生成一些转化事件并检查这些事件是否显示在中，来确认数据是否按预期发送 [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## 后续步骤

本指南介绍了如何将数据发送到 [!DNL Meta] 使用 [!DNL Meta Pixel] 标记扩展。 有关Experience Platform中标记的更多信息，请参阅 [标记概述](../../../home.md).

## 附录：使用不同 [!DNL Pixel] 不同环境的ID {#id-data-element}

如果您希望在开发或暂存环境中测试实施，同时保留生产环境 [!DNL Meta Pixel] analytics完整无缺，您可以使用数据元素动态选择适当的 [!DNL Pixel] ID，具体取决于所使用的环境。

您可以使用 [!UICONTROL 自定义代码] 数据元素(由 [[!UICONTROL 核心] 扩展](../core/overview.md))与 [`turbine` 自由变量](../../../extension-dev/turbine.md). 在数据元素的JavaScript代码中，使用 `turbine` 对象来查找当前环境阶段，然后返回相应的 [!DNL Pixel] 基于结果的ID。

以下示例返回假的生产ID `exampleProductionKey` 在生产环境中使用时， `exampleTestKey` 使用任何其他环境时。 实施此代码时，请将每个值替换为实际的生产和测试 [!DNL Pixel] ID。

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```

