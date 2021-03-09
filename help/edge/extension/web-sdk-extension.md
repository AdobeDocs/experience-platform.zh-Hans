---
title: Adobe Experience Platform Web SDK 扩展 概述
description: 了解Adobe Experience Platform Web SDK扩展for Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 13%

---


# Adobe Experience Platform Web SDK扩展概述

Adobe Experience Platform Web SDK扩展通过Adobe Experience Platform Edge Network从Web属性向Adobe Experience Cloud发送数据。 该扩展允许您将数据流化到平台、同步身份、处理客户同意信号以及自动收集上下文数据。

本文档介绍如何在Adobe Experience Platform Launch用户界面中配置扩展。

## 配置扩展

如果已为某个属性安装了Platform Web SDK扩展，请在Platform launch UI中打开该属性，然后选择&#x200B;**[!UICONTROL Extensions]**&#x200B;选项卡。 在“平台Web SDK”下，选择&#x200B;**[!UICONTROL 配置]**。

![](../images/extension/overview/configure.png)

如果尚未安装该扩展，请选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。 从可用扩展的列表中，找到Platform Web SDK扩展并选择&#x200B;**[!UICONTROL 安装]**。

![](../images/extension/overview/install.png)

在这两种情况下，您都会到达Platform Web SDK的配置页。 以下部分说明了扩展的配置选项。

![](../images/extension/overview/config-screen.png)

## 常规配置选项

页面顶部的配置选项告诉Adobe Experience Platform将数据路由到何处以及在服务器上使用的配置。

### [!UICONTROL 名称]

Adobe Experience Platform Web SDK扩展支持页面上的多个实例。 该名称用于使用单个Platform launch配置向多个组织发送数据。

扩展名的名称默认为“[!DNL alloy]”。 但是，您可以将实例名称更改为任何有效的 JavaScript 对象名称。

### **[!UICONTROL IMS 组织 ID]**

[!UICONTROL IMS组织ID]是您希望在Adobe发送数据的组织。 大多数情况下，请使用自动填充的默认值。 当页面上有多个实例时，请用要向其发送数据的第二个组织的值填充此字段。

### **[!UICONTROL 边缘域]**

[!UICONTROL 边缘域]是Adobe Experience Platform扩展发送和接收数据的域。 该扩展要求您对生产流量使用第一方 CNAME。默认的第三方域适用于开发环境，但不适合生产环境。[此处](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/ec-cookies/cookies-first-party.html)列出了有关如何设置第一方 CNAME 的说明。

## [!UICONTROL 边缘配置]

向Adobe Experience Platform Edge Network发送请求时，会使用边缘配置ID引用服务器端配置。 您无需在网站上更改代码即可更新配置。

有关详细信息，请参阅[边缘配置](../fundamentals/edge-configuration.md)指南。

## [!UICONTROL 隐私]

通过[!UICONTROL 隐私]部分，可配置SDK如何处理来自您网站的用户同意信号。 具体而言，它允许您选择在未提供其他明确同意首选项的情况下假定用户的默认同意级别。 默认同意级别不会保存到用户的用户档案。 下表分析了每个选项所包含的内容：

| [!UICONTROL 默认同意级别] | 描述 |
| --- | --- |
| [!UICONTROL 入] | 收集在用户提供同意首选项之前发生的事件。 |
| [!UICONTROL 出] | 放弃在用户提供同意首选项之前发生的事件。 |
| [!UICONTROL 待定] | 在用户提供同意首选项之前发生的队列事件。 当提供同意偏好时，将根据提供的偏好收集或丢弃事件。 |
| [!UICONTROL 由数据元素提供] | 默认同意级别由您定义的单独数据元素决定。 使用此选项时，必须使用提供的下拉菜单指定数据元素。 |

如果您要求明确的用户同意您的业务操作，则使用“退出”或“待定”。