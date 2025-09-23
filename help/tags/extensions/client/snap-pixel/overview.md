---
title: 快照像素扩展概述
description: 了解如何使用Snap Pixel标记扩展在Adobe Experience Platform中捕获宝贵的用户交互。
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# [!DNL Snap Pixel]扩展概述

[[!DNL Snap Pixel]](https://businesshelp.snapchat.com/s/article/snap-pixel-about)是一个基于JavaScript的分析工具，它使您能够捕获网站上的重要用户交互。 重要访客操作（如购买、注册或其他转化）会自动发送到[广告管理器](http://ads.snapchat.com/)，从而允许您衡量和优化广告、促销活动、转化路径等的效果。

[!DNL Snap Pixel]标记扩展允许您将[!DNL Snap Pixel]功能直接集成到客户端标记库中。 本文档概述如何安装该扩展，并在标记管理规则中实施其功能。

[!DNL Snap Pixel]标记扩展简化了[!DNL Snap Pixel]功能与现有客户端标记库的集成。 本文档概述了如何在标签管理[规则](../../../ui/managing-resources/rules.md)中安装扩展并配置其功能。

## 先决条件 {#prerequisites}

若要使用该扩展，您需要一个有效的[!DNL Snap]帐户，该帐户具有访问[!DNL Ads Manager]的权限。 您必须[创建一个新的 [!DNL Snap Pixel]](https://forbusiness.snapchat.com/advertising/snap-pixel#about)并复制其像素ID以配置您帐户的扩展。 如果您现有[!DNL Snap Pixel]，则只需使用其ID即可。

建议将[!DNL Snap Pixel]与[!DNL Snap Conversions API]一起使用以从客户端和服务器端发送相同的事件。 此方法有助于恢复仅由[!DNL Snap Pixel]无法捕获的事件。 有关如何将其集成到服务器端实施中的步骤，请参阅事件转发的[[!DNL Snap] Conversions API扩展](../../server/snap/overview.md)。 请注意，您的组织必须有权访问[事件转发](../../../ui/event-forwarding/overview.md)，才能使用服务器端扩展。

## 安装扩展 {#install}

要安装[!DNL Snap Pixel]扩展，请导航到数据收集UI或Experience Platform UI，然后从左侧导航中选择&#x200B;**[!UICONTROL 标记]**。 在此处，选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的属性后，在左侧导航中选择&#x200B;**[!UICONTROL 扩展]**，然后选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。 搜索[!UICONTROL Snap Pixel]卡，然后选择&#x200B;**[!UICONTROL 安装]**。

![正在为数据收集UI中的[!UICONTROL Snap Pixel]扩展选择[!UICONTROL 安装]按钮。](./images/install.png)

在显示的配置视图中，您必须提供之前复制的像素ID，以将扩展关联到您的帐户。 您可以将ID直接粘贴到输入中，也可以选择现有数据元素。

完成后，选择&#x200B;**[!UICONTROL 保存]**。

![在扩展配置视图中作为数据元素提供的[!DNL Pixel] ID。](./images/configure.png)

扩展已安装，您现在可以在标记规则中使用其各种操作。

## 配置标记规则 {#rule}

[!DNL Snap Pixel]支持一组预定义的标准事件，每个事件都有特定的上下文和接受的参数。 [!DNL Snap Pixel]扩展中可用的规则操作与这些事件类型一致，从而可轻松根据发送到[!DNL Snap]的事件类型对事件进行分类和配置。

出于演示目的，本节将演示如何构建一个将购买事件发送到[!DNL Snap]的规则。

要开始，请创建新标记规则并根据需要定义条件。 设置规则的操作时，选择[!DNL Snap Pixel]作为扩展，然后选择&#x200B;**[!UICONTROL 发送购买事件]**&#x200B;作为操作类型。

配置完[!UICONTROL 发送购买事件]操作后，选择&#x200B;**[!UICONTROL 保留更改]**&#x200B;以将其添加到规则设置。

![为数据收集UI中的规则选择的[!UICONTROL 发送购买事件]操作类型。](./images/action-type.png)

如果对整体规则配置满意，请选择&#x200B;**[!UICONTROL 保存到库]**。

要应用更新，请发布新标记[内部版本](../../../ui/publishing/builds.md)以启用对库的更改。

## 确认[!DNL Snap]正在接收数据 {#confirm}

将更新的内部版本部署到您的网站后，您可以在浏览器中触发转化事件并检查这些事件是否出现在[[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager)中，从而验证数据是否按预期发送。

## 后续步骤 {#next-steps}

本指南介绍如何使用[!DNL Snap]标记扩展将数据发送到[!DNL Snap Pixel]。 如果您还计划将服务器端事件发送到[!DNL Snap]，则可以继续安装和配置[[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md)。
