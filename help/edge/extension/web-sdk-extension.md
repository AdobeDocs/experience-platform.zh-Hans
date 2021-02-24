---
title: Adobe Experience Platform Web SDK 扩展 概述
description: 了解Adobe Experience Platform Web SDK扩展for Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 53%

---


# Adobe Experience Platform Web SDK扩展概述

Adobe Experience Platform Web SDK扩展通过Adobe Experience Platform Edge Network从Web属性将数据发送到Adobe Experience Cloud。 Adobe Experience Platform Web SDK 扩展允许将数据流式传输到平台、同步身份、选择加入和自动收集上下文数据。

## 配置扩展

此部分提供有关配置 Adobe Experience Platform Web SDK 扩展时可用的选项的参考。

如果尚未安装Adobe Experience Platform Web SDK扩展，请打开您的属性，然后选择&#x200B;**[!UICONTROL 扩展>目录]**，将指针悬停在Adobe Experience Platform Web SDK扩展上，然后选择&#x200B;**[!UICONTROL 安装]**。

要配置扩展，请打开&#x200B;**[!UICONTROL 扩展]**&#x200B;选项卡，将指针悬停在扩展上，然后选择&#x200B;**[!UICONTROL 配置]**。

![](./assets/ext-aep-config.png)

### 实例名称

Adobe Experience Platform Web SDK扩展支持页面上的多个实例。 可以利用这一点来通过单个 Adobe Experience Platform Launch 配置向多个组织发送数据。**[!UICONTROL 名称]**&#x200B;默认为合金。 但是，您可以将实例名称更改为任何有效的 JavaScript 对象名称。Adobe Experience Platform扩展要求每个实例具有不同的&#x200B;**[!UICONTROL 配置ID]**&#x200B;和不同的&#x200B;**[!UICONTROL 组织ID]**。

## **[!UICONTROL 配置ID]**

**[!UICONTROL 配置ID]**&#x200B;告诉Adobe Experience Platform数据应路由的位置以及服务器上应使用的配置。 这是 Adobe Experience Platform 扩展正常工作所必需的。您可以联系客户关怀获取配置 ID。


### **[!UICONTROL Organization ID]**

**[!UICONTROL 组织ID]**&#x200B;是您希望在Adobe发送数据的组织。 大多数情况下，您应使用自动填充的默认值。当页面上有多个实例时，使用要向其发送数据的第二个组织的值填充该实例。

### **[!UICONTROL 边缘域]**

**[!UICONTROL 边缘域]**&#x200B;是Adobe Experience Platform扩展发送和接收数据的域。 该扩展要求您对生产流量使用第一方 CNAME。默认的第三方域适用于开发环境，但不适合生产环境。[此处](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/ec-cookies/cookies-first-party.html)列出了有关如何设置第一方 CNAME 的说明。

### **[!UICONTROL 启用错误]**

默认情况下，如果该扩展存在错误，它会将错误记录到控制台。如果要隐藏生产环境中的错误，可取消选中&#x200B;**[!UICONTROL 启用错误]**&#x200B;复选框。 在 Platform Launch 中打开调试时，仍会输出错误。

### **[!UICONTROL 启用选择加入]**

如果&#x200B;**[!UICONTROL 启用选择加入]**，则扩展可保持点击，直到收到选择加入。 此扩展会显示用于设置选择加入首选项的操作。

### **[!UICONTROL 启用迁移ECID]**

平台Web SDK扩展使用新的cookie存储ECID。 出于迁移目的，此设置支持新 Cookie 与旧 Cookie 之间的兼容性。Adobe 强烈建议启用此功能，除非您的现有访客均未使用 ECID。

### **[!UICONTROL 使用第三方Cookie]**

Adobe Experience Platform 将始终在第一方域中存储 Cookie。此选项使您除了使用第一方域中的 Cookie 之外，还能够使用在 demdex.net 上设置的第三方 Cookie。当用户在多个域之间移动时，此选项会很有用。这将禁用对 demdex.net 的调用。

### **[!UICONTROL 上下文]**

此扩展会自动收集有关请求上下文的信息（例如，有关 URL 和浏览器的详细信息）。可通过取消选择特定上下文来禁用此选项。

- **[!UICONTROL web]**  — 有关网页的详细信息，如url、推荐人等。
- **[!UICONTROL device]**  — 有关设备的详细信息，如屏幕方向、屏幕高度和屏幕宽度。
- **[!UICONTROL 环境]**  — 有关计算环境（浏览器、连接等）的信息
- **[!UICONTROL location]**  — 有关用户位置的有限信息

## 下一步

1. 设置[操作类型](action-types.md)。
2. 设置[数据元素类型](data-element-types.md)。
