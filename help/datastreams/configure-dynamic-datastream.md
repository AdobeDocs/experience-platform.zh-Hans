---
title: 创建动态数据流配置
description: 了解如何根据规则创建动态数据流配置，以将数据路由到各种Experience Cloud服务。
hide: true
hidefromtoc: true
badge: label="Beta 版" type="Informative"
exl-id: 528ddf89-ad87-4021-b5a6-8e25b4469ac4
source-git-commit: 39e65f1f74b95fffffb3c5400ce1b7e60aa81bad
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 1%

---

# 创建动态数据流配置

>[!AVAILABILITY]
>
>* 定义动态数据流配置的选项当前存在于Beta中，并且仅供有限数量的客户使用。 要获得此功能的访问权限，请联系您的Adobe代表。 文档和功能可能会发生变化。

默认情况下，Experience PlatformEdge Network会将到达数据流的所有事件发送到您为数据流启用的所有Experience Cloud[服务](configure.md#add-services)。 根据您的用例，这可能并不总是您的理想工作流程。

动态数据流配置通过用户可配置的规则集解决了这一问题，这些规则集可为为数据流启用的每个服务定义，并规定了哪些Experience Cloud解决方案应接收每种类型的数据。

## 先决条件 {#prerequisites}

要为数据流创建动态配置，您必须满足两个条件：

* 您必须已创建&#x200B;*至少*&#x200B;个要处理的数据流。 有关详细信息，请参阅有关如何[创建数据流](configure.md)的文档。
* 您必须向数据流中添加至少&#x200B;*个* Experience Cloud服务。 有关详细信息，请参阅有关如何将服务[添加到数据流](configure.md#add-services)的文档。

创建数据流并向其中添加Experience Cloud服务后，您可以[创建动态配置](#create-dynamic-configuration)。

## 动态数据流配置与数据流配置覆盖 {#dynamic-versus-overrides}

动态数据流配置和[数据流配置覆盖](overrides.md)是互斥功能。

这意味着您不能将动态数据流配置与数据流配置覆盖一起使用。 你必须选择一个或另一个。

如果同时启用动态数据流配置和数据流配置覆盖，则配置覆盖将优先，并且动态数据流配置规则将被忽略。

## 创建动态数据流配置 {#create-dynamic-configuration}

在您[创建了数据流](configure.md)并[向其添加了服务](configure.md#add-services)之后，请按照以下步骤向该服务添加动态配置。

1. 转到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 数据流]**&#x200B;页面并选择您创建的数据流。

   ![显示数据流列表的数据流用户界面的图像。](assets/configure-dynamic-datastream/select-datastream.png)

1. 选择要为其定义动态配置的服务上的&#x200B;**[!UICONTROL 编辑]**&#x200B;选项。

   ![数据流用户界面的图像，显示添加到数据流的服务。](assets/configure-dynamic-datastream/select-service.png)

1. 在&#x200B;**[!UICONTROL 配置]**&#x200B;页面中，选择&#x200B;**[!UICONTROL 保存并编辑动态配置]**。

   ![显示数据流配置页的数据流用户界面的图像。](assets/configure-dynamic-datastream/save-and-edit.png)

1. 选择&#x200B;**[!UICONTROL 添加动态配置]**。

   ![数据流用户界面的图像，显示未添加规则的动态配置消息。](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. 从&#x200B;**[!UICONTROL 资源]**&#x200B;面板中，将要用于构建规则的项拖放到窗口的右侧。 您可以合并多个资源以构建复杂的规则。

   使用每个资源的选项（如&#x200B;**[!UICONTROL 等于]**、**[!UICONTROL 不等于]**、**[!UICONTROL 存在]**&#x200B;等）来优化规则。

   ![显示动态配置规则的数据流用户界面的图像。](assets/configure-dynamic-datastream/drag-resources.png)

1. 在&#x200B;**[!UICONTROL 配置]**&#x200B;部分中，根据是否希望将数据发送到每个服务，切换要为每个规则启用或禁用的服务。 如果关闭切换开关，服务路由将禁用，*不会向上游服务发送任何数据*。

   ![显示动态配置规则的数据流用户界面的图像。](assets/configure-dynamic-datastream/enable-service.png)

1. 配置完规则后，选择&#x200B;**[!UICONTROL 保存]**。

## 规则优先级注意事项 {#considerations}

您可以为每个动态数据流配置定义多个规则。 但是，如果数据与多个规则的条件匹配，则只考虑列表中的第一个匹配规则，并忽略所有其他匹配规则。

要获得所需的数据路由行为，请注意规则的排列顺序。

要配置规则顺序，您可以按所需的顺序拖放规则窗口。

![显示如何通过拖放更改GIF顺序的规则。](assets/configure-dynamic-datastream/move-rules.gif)
