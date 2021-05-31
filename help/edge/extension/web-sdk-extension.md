---
title: Adobe Experience Platform Web SDK扩展概述
description: 了解适用于Adobe Experience Platform Launch的Adobe Experience Platform Web SDK扩展
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 12%

---

# Adobe Experience Platform Web SDK扩展概述

Adobe Experience Platform Web SDK扩展通过Adobe Experience Platform Edge Network从Web属性向Adobe Experience Cloud发送数据。 该扩展允许您将数据流式传输到平台、同步身份、处理客户同意信号并自动收集上下文数据。

本文档介绍如何在Adobe Experience Platform Launch用户界面中配置扩展。

## 配置扩展

如果已经为资产安装了Platform Web SDK扩展，请在Platform launchUI中打开该资产，然后选择&#x200B;**[!UICONTROL Extensions]**&#x200B;选项卡。 在Platform Web SDK下，选择&#x200B;**[!UICONTROL 配置]**。

![](../images/extension/overview/configure.png)

如果尚未安装该扩展，请选择&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡。 从可用扩展列表中，找到Platform Web SDK扩展，然后选择&#x200B;**[!UICONTROL Install]**。

![](../images/extension/overview/install.png)

在这两种情况下，您都会到达Platform Web SDK的配置页面。 以下部分介绍扩展的配置选项。

![](../images/extension/overview/config-screen.png)

## 常规配置选项

页面顶部的配置选项告知Adobe Experience Platform要将数据路由到何处以及要在服务器上使用的配置。

### [!UICONTROL 名称]

Adobe Experience Platform Web SDK扩展支持页面上的多个实例。 该名称用于通过单个Platform launch配置向多个组织发送数据。

扩展的名称默认为“[!DNL alloy]”。 但是，您可以将实例名称更改为任何有效的 JavaScript 对象名称。

### **[!UICONTROL IMS 组织 ID]**

[!UICONTROL IMS组织ID]是您希望在Adobe时将数据发送到的组织。 大多数情况下，会使用自动填充的默认值。 当页面上有多个实例时，使用要向其发送数据的第二个组织的值填充此字段。

### **[!UICONTROL 边缘域]**

[!UICONTROL Edge Domain]是Adobe Experience Platform扩展发送和接收数据的域。 该扩展要求您对生产流量使用第一方 CNAME。默认的第三方域适用于开发环境，但不适合生产环境。[此处](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hans)列出了有关如何设置第一方 CNAME 的说明。

## [!UICONTROL 数据流]

将请求发送到Adobe Experience Platform边缘网络时，会使用数据流ID引用服务器端配置。 您无需在网站上进行代码更改即可更新配置。

有关更多信息，请参阅[datastreams](../fundamentals/datastreams.md)指南。


## [!UICONTROL 隐私]

[!UICONTROL Privacy]部分允许您配置SDK如何处理来自您网站的用户同意信号。 具体而言，如果未提供其他明确的同意首选项，则允许您选择用户假定的默认同意级别。 默认同意级别不会保存到用户的配置文件中。 下表分析了每个选项的要求：

| [!UICONTROL 默认同意级别] | 描述 |
| --- | --- |
| [!UICONTROL 在] | 收集在用户提供同意首选项之前发生的事件。 |
| [!UICONTROL 输出] | 放弃在用户提供同意首选项之前发生的事件。 |
| [!UICONTROL 待定] | 在用户提供同意首选项之前发生的队列事件。 提供同意首选项后，将根据提供的首选项收集或丢弃事件。 |
| [!UICONTROL 由数据元素提供] | 默认同意级别由您定义的单独数据元素决定。 使用此选项时，必须使用提供的下拉菜单指定数据元素。 |

如果您需要明确的用户同意您的业务操作，请使用“禁用”或“待定”。
