---
title: 元像素扩展概述
description: 了解Adobe Experience Platform中的Meta Pixel标记扩展。
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# [!DNL Meta Pixel]扩展概述

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/)是一种基于JavaScript的分析工具，它允许您跟踪网站上的访客活动。 您跟踪的访客操作（称为转化）会被发送到[[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager)，您可以在其中使用它们来衡量广告、促销活动、转化漏斗等的有效性。

[!DNL Meta Pixel]标记扩展允许您在客户端标记库中利用[!DNL Pixel]功能。 本文档介绍如何安装扩展并在[规则](../../../ui/managing-resources/rules.md)中使用其功能。

## 先决条件

若要使用扩展，您必须拥有有效的[!DNL Meta]帐户，并且有权访问[!DNL Ads Manager]。 具体来说，您必须[创建一个新的 [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755)并复制其[!DNL Pixel ID]，以便将扩展配置为您的帐户。 如果您已有[!DNL Meta Pixel]，则可以改用其ID。

强烈建议将[!DNL Meta Pixel]与[!DNL Meta Conversions API]结合使用，以分别从客户端和服务器端共享和发送相同的事件，因为这有助于恢复[!DNL Meta Pixel]未提取的事件。 请参阅[[!DNL Meta Conversions API] 扩展指南，了解事件转发](../../client/meta/overview.md)中有关如何将其集成到服务器端实施中的步骤。 请注意，您的组织必须有权访问[事件转发](../../../ui/event-forwarding/overview.md)，才能使用服务器端扩展。

## 安装扩展

要安装[!DNL Meta Pixel]扩展，请导航到数据收集UI或Experience PlatformUI，然后从左侧导航中选择&#x200B;**[!UICONTROL 标记]**。 在此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的属性后，在左侧导航中选择&#x200B;**[!UICONTROL 扩展]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。 搜索[!UICONTROL Meta Pixel]卡，然后选择&#x200B;**[!UICONTROL 安装]**。

![正在为数据收集UI中的[!UICONTROL Meta Pixel]扩展选择[!UICONTROL 安装]按钮。](../../../images/extensions/client/meta/install.png)

在显示的配置视图中，必须提供您之前复制的[!DNL Pixel] ID以将扩展关联到您的帐户。 您可以将ID直接粘贴到输入中，也可以选择现有数据元素。

>[!TIP]
>
>使用数据元素，您可以选择根据其他因素（如生成环境）动态更改使用的[!DNL Pixel] ID。 有关详细信息，请参阅[中针对不同环境使用不同的 [!DNL Pixel] ID](#id-data-element)的附录部分。

您还可以选择提供要与扩展关联的事件ID。 这用于删除[!DNL Meta Pixel]和[!DNL Meta Conversions API]之间的相同事件。 有关详细信息，请参阅[!DNL Conversions API]扩展的概述中有关[事件去重](../../server/meta/overview.md#event-deduplication)的部分。

完成后，选择&#x200B;**[!UICONTROL 保存]**

![在扩展配置视图中作为数据元素提供的[!DNL Pixel] ID。](../../../images/extensions/client/meta/configure.png)

扩展已安装，您现在可以在标记规则中使用其各种操作。

## 配置标记规则 {#rule}

[!DNL Meta Pixel]接受一组预定义的[标准事件](https://www.facebook.com/business/help/402791146561655)，每个事件都有自己的上下文和接受的属性。 [!DNL Pixel]扩展提供的规则操作与这些事件类型相关联，允许您根据发送给[!DNL Meta]的事件类型轻松分类和配置该事件。

出于演示目的，本节将演示如何构建一个将页面查看事件发送到[!DNL Meta]的规则。

开始创建新标记规则，并根据需要配置其条件。 为规则选择操作时，请为扩展选择&#x200B;**[!UICONTROL Meta Pixel]**，然后为操作类型选择&#x200B;**[!UICONTROL 发送页面视图]**。

![正在为数据收集UI中的规则选择[!UICONTROL 发送页面视图]操作类型。](../../../images/extensions/client/meta/select-action.png)

[!UICONTROL 发送页面视图]操作不需要进一步的配置。 选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以将操作添加到规则配置。 如果对规则满意，请选择&#x200B;**[!UICONTROL 保存到库]**。

最后，发布新标记[生成](../../../ui/publishing/builds.md)以启用对库的更改。

## 确认[!DNL Meta]正在接收数据

将更新的内部版本部署到您的网站后，您可以在浏览器中生成一些转化事件并检查这些事件是否显示在[[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180)中，从而确认数据是否按预期发送。

## 后续步骤

本指南介绍了如何使用[!DNL Meta Pixel]标记扩展将数据发送到[!DNL Meta]。 如果您还计划向[!DNL Meta]发送服务器端事件，则现在可以继续安装和配置[[!DNL Conversions API] 事件转发扩展](../../server/meta/overview.md)。

有关Experience Platform中标记的详细信息，请参阅[标记概述](../../../home.md)。

## 附录：为不同的环境使用不同的[!DNL Pixel] ID {#id-data-element}

如果要在开发或暂存环境中测试实施，同时保持生产[!DNL Meta Pixel]分析不变，则可以使用数据元素根据正在使用的环境动态选择适当的[!DNL Pixel] ID。

通过将[!UICONTROL 自定义代码]数据元素（由[[!UICONTROL Core]扩展](../core/overview.md)提供）与[`turbine`自由变量](../../../extension-dev/turbine.md)结合使用，可以实现此目的。 在数据元素的JavaScript代码中，使用`turbine`对象查找当前环境阶段，然后根据结果返回相应的[!DNL Pixel] ID。

以下示例在生产环境中使用时返回虚假的生产ID `exampleProductionKey`，在使用任何其他环境时返回不同的ID `exampleTestKey`。 实施此代码时，请将每个值替换为您实际的生产和测试[!DNL Pixel] ID。

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
