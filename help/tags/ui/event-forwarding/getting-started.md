---
title: 事件转发快速入门
description: 按照此分步教程进行操作，以开始在Adobe Experience Platform中使用事件转发。
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 30%

---

# 事件转发快速入门

>[!NOTE]
>
>事件转发是一项付费功能，包含在Adobe Real-Time Customer Data Platform连接、Prime或Ultimate产品中。

要在Adobe Experience Platform中使用事件转发，必须使用以下三个选项中的一个或多个将数据发送到Adobe Experience Platform Edge Network：

* [Adobe Experience Platform Web SDK](../../extensions/client/web-sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)

>[!NOTE]
>Experience Platform Web SDK和Experience Platform Mobile SDK不需要通过Adobe Experience Platform中的标记进行部署。 但是，推荐使用标记来部署这些SDK。

将数据发送到 Edge Network 后，可打开 Adobe 解决方案以在相应的位置发送数据。要将数据发送到非Adobe解决方案，请在事件转发中设置。

## 先决条件

* Adobe Real-Time CDP Connections、Prime或Ultimate(有关定价，请联系您的Adobe客户团队)
* Adobe Experience Platform中的事件转发
* Adobe Experience Platform Web SDK、Mobile SDK或Edge Network API配置为将数据发送到Edge Network
* 将数据映射到Experience Data Model (XDM)（此映射可以使用标记完成）

## 创建 XDM 架构

在 Adobe Experience Platform 中，创造您的架构。

1. 选择&#x200B;**[!UICONTROL Schemas]**>**[!UICONTROL Create Schema]**&#x200B;并选择&#x200B;**[!UICONTROL XDM ExperienceEvent]**&#x200B;选项以创建架构。

1. 为架构命名并提供简短描述。

1. 您可以通过选择&#x200B;**[!UICONTROL Add]**&#x200B;旁边的&#x200B;**[!UICONTROL Field Groups]**&#x200B;来添加“ExperienceEvent Web详细信息”字段组。

   >[!NOTE]
   >
   >如果需要，可以添加多个字段组。

1. 保存架构并记下您提供的名称。

有关架构的更多信息，请参阅 [Experience Data Model (XDM) 系统帮助](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)。

## 创建事件转发属性

在&#x200B;**[!UICONTROL Tags]**&#x200B;工作区中，创建&#x200B;**[!UICONTROL Edge]**&#x200B;类型的属性。

1. 选择 **[!UICONTROL New Property]**。

1. 命名资产。

1. 选择“Edge”平台类型。

1. 选择 **[!UICONTROL Save]**。

创建资产后，转到新资产的 **[!UICONTROL Environments]** 选项卡，并记下
环境 ID。如果数据流中使用的Adobe组织不同于事件转发中使用的Adobe组织，则可以从&#x200B;**[!UICONTROL Environments]**&#x200B;选项卡复制环境ID，并在创建数据流时粘贴它。 您也可以从下拉菜单中选择环境。

## 创建数据流

要在Adobe Experience Platform中创建数据流，请使用在创建事件转发属性时生成的环境ID。

1. 在左侧导航中选择&#x200B;**[!UICONTROL Datastreams]**。

1. 对配置进行命名并提供描述（可选）。
该描述有助于在包含多个配置的列表中识别配置。

1. 选择 **[!UICONTROL Save]**。

## 启用事件转发 {#enable-event-forwarding}

接下来，配置Edge Network以将数据发送到事件转发和其他Adobe产品。

1. 在&#x200B;**[!UICONTROL Datastreams]**&#x200B;工作区中，选择您创建的属性。

1. 选择 Development、Production 或 Staging 环境。

   或者，若要将数据发送到Adobe组织外的事件转发环境，请选择&#x200B;**[!UICONTROL Switch to Advanced Mode]**&#x200B;并粘贴到ID中。 此ID是您在创建事件转发属性时提供的ID。

1. 打开必要的工具并根据需要进行配置。

   * Adobe Analytics 需要一个报表包 ID。

   * Adobe Experience Platform中的事件转发需要一个资产ID和环境ID。 这是事件转发属性的发布路径。

配置后，记下新资产的环境 ID。

## 配置Experience Platform Web SDK扩展，以将数据发送到之前创建的数据流

在&#x200B;**[!UICONTROL Tags]**&#x200B;工作区中创建属性，然后导航到&#x200B;**[!UICONTROL Extensions]**&#x200B;并从目录中选择Experience Platform Web SDK扩展以对其进行配置和安装。

有关配置选项的详细信息，请参阅[Web SDK扩展文档](../../extensions/client/web-sdk/overview.md)。

## 创建标记规则以将数据发送到Experience Platform Web SDK

完成上述操作后，即可构建数据定义、规则等，它们使用事件转发和标记，但只需要从页面中发出单个请求。

使用Experience Platform Web SDK扩展和“发送事件”操作类型创建页面加载规则：

1. 打开 **[!UICONTROL Rules]** 选项卡，然后选择 **[!UICONTROL Create New Rule]**。

1. 命名规则。

1. 选择 **[!UICONTROL Events Add]**。

1. 通过选择扩展以及该扩展可用的事件类型之一来添加事件，然后配置该事件的设置。例如，选择 **[!UICONTROL Core - Window Loaded]**。

1. 使用Experience Platform Web SDK扩展添加操作。 从 **[!UICONTROL Action Type]** 列表中选择 **[!UICONTROL Send Event]**，选择所需的实例（以前配置的 Alloy 实例），然后选择要添加到 Alloy 点击的 XDM 数据块的数据元素。

1. 对于本示例，请将其余设置保留为默认设置，然后选择 **[!UICONTROL Save]**。

再举一个示例，如果用户将鼠标悬停在指定的按钮上，您可以创建一项将数据层发送到 Edge 的规则。

## 概要

设置完各项内容后，您现在可以创建事件转发规则，以将数据转发到非Adobe目标。

* Experience Data Model架构（请注意您为其指定的名称。）
* 事件转发属性（跟踪属性ID和环境ID。）
* 数据流（请注意环境ID，切勿与事件转发的环境ID混淆。）
* 标记属性
