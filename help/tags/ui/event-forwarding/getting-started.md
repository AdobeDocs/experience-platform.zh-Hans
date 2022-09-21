---
title: 事件转发入门
description: 请按照此分步教程，开始使用Adobe Experience Platform中的事件转发。
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 26%

---

# 事件转发入门

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

要在Adobe Experience Platform中使用事件转发，必须使用以下三个选项中的一个或多个选项将数据发送到Adobe Experience Platform边缘网络：

* [Adobe Experience Platform Web SDK](../../extensions/web/sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [服务器到服务器API](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>Platform Web SDK和Platform Mobile SDK不需要在Adobe Experience Platform中通过标记进行部署。 但是，建议使用标记来部署这些SDK。

将数据发送到 Edge Network 后，可打开 Adobe 解决方案以在相应的位置发送数据。要将数据发送到非Adobe解决方案，请在事件转发中设置。

## 先决条件

* Adobe Experience Platform Collection Enterprise（请联系您的客户经理以了解定价信息）
* Adobe Experience Platform中的事件转发
* Adobe Experience Platform Web 或 Mobile SDK，配置为将数据发送到 Edge Network
* 将数据映射到体验数据模型(XDM)（此映射可以使用标记完成）

## 创建 XDM 架构

在 Adobe Experience Platform 中，创造您的架构。

1. 通过选择 **[!UICONTROL 模式]**>**[!UICONTROL 创建架构]** 选择 **[!UICONTROL XDM ExperienceEvent]** 选项。

1. 为架构命名并提供简短描述。

1. 您可以通过选择 **[!UICONTROL 添加]** 下一页 **[!UICONTROL 字段组]**.

   >[!NOTE]
   >
   >如果需要，可以添加多个字段组。

1. 保存架构，并记下您为其提供的名称。

有关架构的更多信息，请参阅 [Experience Data Model (XDM) 系统帮助](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)。

## 创建事件转发属性

在 **[!UICONTROL 标记]** 工作区，创建类型的属性 **[!UICONTROL Edge]**.

1. 选择 **[!UICONTROL 新建资产]**.

1. 命名资产。

1. 选择“Edge”平台类型。

1. 选择&#x200B;**[!UICONTROL 保存]**。

创建资产后，转到 **[!UICONTROL 环境]** 选项卡，并记下环境ID。 如果数据流中使用的Adobe组织与事件转发中使用的Adobe组织不同，则可以从 **[!UICONTROL 环境]** 选项卡，并在创建数据流时粘贴它。 您也可以从下拉菜单中选择环境。

## 创建数据流

要在Adobe Experience Platform中创建数据流，请使用在创建事件转发属性时生成的环境ID。

1. 选择 **[!UICONTROL 数据流]** 中。

1. 对配置进行命名并提供描述（可选）。
该描述有助于在包含多个配置的列表中识别配置。

1. 选择&#x200B;**[!UICONTROL 保存]**。

## 启用事件转发

接下来，配置边缘网络以将数据发送到事件转发和其他Adobe产品。

1. 在 **[!UICONTROL 数据流]** 工作区中，选择您创建的属性。

1. 选择 Development、Production 或 Staging 环境。

   或者，要将数据发送到Adobe组织以外的事件转发环境，请选择 **[!UICONTROL 切换到高级模式]** 并粘贴ID。 在创建事件转发属性时，会提供该ID。

1. 打开必要的工具并根据需要进行配置。

   * Adobe Analytics 需要一个报表包 ID。

   * Adobe Experience Platform中的事件转发需要属性ID和环境ID。 这是事件转发属性的发布路径。

配置后，记下新资产的环境 ID。

## 配置Platform Web SDK扩展，以将数据发送到之前创建的数据流

在 **[!UICONTROL 标记]** 工作区，然后导航到 **[!UICONTROL 扩展]** ，然后从目录中选择Experience PlatformWeb SDK扩展以对其进行配置和安装。

请参阅 [Web SDK扩展文档](../../extensions/web/sdk/overview.md) 以了解有关配置选项的详细信息。

## 创建标记规则以将数据发送到Platform Web SDK

在实施上述功能后，构建使用事件转发和标记的数据定义、规则等，但只需从页面中发出一个请求。

使用Platform Web SDK扩展和“Send Event”操作类型创建页面加载规则：

1. 打开 **[!UICONTROL 规则]** 选项卡，然后选择 **[!UICONTROL 创建新规则]**.

1. 命名规则。

1. 选择 **[!UICONTROL 事件添加]**.

1. 通过选择扩展以及该扩展可用的事件类型之一来添加事件，然后配置该事件的设置。例如，选择 **[!UICONTROL 核心 — 已加载窗口]**.

1. 使用 Platform Web SDK 扩展添加操作。选择 **[!UICONTROL 发送事件]** 从 **[!UICONTROL 操作类型]** 列表中，选择所需的实例（之前配置的Alloy实例），然后选择要添加到Alloy点击中XDM数据块的数据元素。

1. 将其余设置保留为此示例的默认设置，然后选择 **[!UICONTROL 保存]**.

再举一个示例，如果用户将鼠标悬停在指定的按钮上，您可以创建一项将数据层发送到 Edge 的规则。

## 概要

现在，通过实施以下功能，您可以创建事件转发规则以将数据转发到非Adobe目标。

* 体验数据模型架构（请注意您为其提供的名称。）
* 事件转发属性（保留对属性ID和环境ID的跟踪。）
* 数据流（请注意环境ID，切勿将其与事件转发中的环境ID混淆。）
* 标记属性
