---
title: “常用Analytics扩展”概述
description: 了解Adobe Experience Platform中的“常用Analytics标记”扩展。
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 62%

---

# “常用Analytics插件”扩展概述

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

使用本文的参考信息可了解有关配置“常用 Analytics 插件”扩展，以及使用此扩展增强 [!DNL Adobe Analytics] 扩展时可用选项的信息。

## 配置“常用 Analytics 插件”扩展

此部分提供有关配置“常用 Analytics 插件”扩展时可用选项的参考。

>[!IMPORTANT]
>
>“常用 Analytics 插件”扩展是对 [!DNL Adobe Analytics] 扩展的充实和增强。必须在您的资产上安装 [!DNL Adobe Analytics] 扩展才能使其正常工作。此外，您必须将跟踪器设置为在 [!DNL Adobe Analytics] 扩展中可全局访问。

在扩展级别不需要任何其他配置。

## 将插件添加到 [!DNL Adobe Analytics] 扩展

要使用此扩展中提供的插件，您必须首先在插件自己的规则中，初始化要使用的插件。

1. 创建新规则。
1. 添加“Core - Library Loaded (Page Top)”事件。
1. 使用以下任一初始化方法。

## “常用 Analytics 插件”扩展操作类型

此部分介绍“常用 Analytics 插件”扩展中可用的操作类型。

“常用 Analytics 插件”扩展提供了以下操作：

* [初始化](#initialize)
* [初始化插件](#initialize-plugin)

### 初始化

>[!IMPORTANT]
>
>虽然此操作更易于实施，但 Adobe 咨询服务团队不建议您使用此操作，因为它会增加插件的负担。

在此操作中，您可以选择要包含在实施中的每个插件并保存更改。您可以按照自己的需要，选择任意数量的、要在实施过程中使用的插件。在 Analytics [插件概述](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html)中，提供了如何使用每个插件的文档链接和简要说明。

### 初始化插件

这些操作可以分别初始化要使用的特定插件。若要初始化您打算在资产中使用的所有插件，只需将相应的操作添加到规则并保存规则即可。虽然这种方式在配置扩展方面需要的工作量稍大一些，但它的代码效率更高。因此，Adobe 建议采用此方法。

## “常用Analytics插件”扩展数据元素

此部分介绍“常用Analytics插件”扩展中可用的数据元素。

### getGeoCoordinates

允许用户利用Adobe Experience Platform中的本机数据收集UI来设置和配置getGeoCoordinates插件。

### getNewRepeat

允许用户利用本机数据收集UI来设置和配置getNewRepeat插件。

### getPageName

允许用户利用本机数据收集UI来设置和配置getPageName插件。

### getResponsiveLayout

允许用户利用本机数据收集UI来设置和配置getResponsiveLayout插件。

### getTimeParting

允许用户利用本机数据收集UI来设置和配置getTimeParting插件。

### getTimeSinceLastVisit

允许用户利用本机数据收集UI来设置和配置getTimeSinceLastVisit插件。

### getVisitDuration

允许用户利用本机数据收集UI来设置和配置getVisitDuration插件。

### getVisitNum

允许用户利用本机数据收集UI来设置和配置getVisitNum插件。
