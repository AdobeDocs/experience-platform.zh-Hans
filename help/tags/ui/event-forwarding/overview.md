---
title: 事件转发概述
description: 了解Adobe Experience Platform中的事件转发，该功能允许您使用平台边缘网络执行任务，而无需更改标签实施。
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 42%

---

# 事件转发概述

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

Adobe Experience Platform中的事件转发使用Adobe Experience Platform边缘网络执行在客户端上正常完成的任务，从而减少网页和应用程序重量。 事件转发规则可以转换数据并将其发送到新目标，而无需更改客户端实施。

事件转发与Adobe Experience Platform Web SDK和Mobile SDK相结合，可以：

* 从包含数据有效负载的页面中进行单个调用。 然后，数据会联合到服务器端，以减少客户端网络流量，并为客户提供更快的体验。
* 缩短加载网页所占用的时间，让您的站点在性能方面符合行业最佳实践。
* 提高透明度并控制在所有标记属性中发送哪些数据类型。
* 创建事件转发规则以将之前跟踪的数据发送到新目标。

## 改进性能

在竞争日益激烈的环境下，企业必须优先考虑性能，以维护并扩大市场份额。事件转发可跨移动设备、IoT和OTT设备提高网站和应用程序性能。 由于缩短了加载时间，网站转换率有所提升；移动设备应用程序不再像以往一样快速耗尽电池电量，并且 OTT 应用程序与运行在移动设备上的相同应用程序相比，具有类似的响应速度。正是因为性能的改进，转换率也随之普遍提升。

## 更好的数据管理

随着技术堆栈不断发展以及数据被发往越来越多的目的地，控制“应该将怎样的数据类型发往何方”的挑战变得日益艰巨。GDPR和CCPA等法规的正常化，迫使企业对越来越难的数据问题施加更多控制。

事件转发有助于营销团队在控制数据的同时实现业务增长。 它减少了营销人员进入目标市场并向非 Adobe 目的地发送数据时所需使用的客户端技术的数量。这使得实施团队能够更轻松地管理从客户端流向不同目的地的数据。

## 事件转发和标记之间的差异

请务必注意事件转发和标记之间的以下差异：

* 数据元素标记化

   * 标记：在规则中，数据元素在数据元素名称的开头和结尾使用`%`进行标记。 例如：`%viewportHeight%`。

   * 事件转发：在规则中，数据元素的标记为：数据元素名称的开头为`{{`，末尾为`}}`。 例如，`{{viewportHeight}}`。

* 数据引用方式

   要引用来自 Edge Network 的数据，数据元素路径必须为 `arc.event._<element>_`。

   其中，`arc` 表示 Adobe 响应上下文。

   例如：`arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >如果此路径指定不正确，则不会收集数据。


* 规则的操作顺序

   在规则的“操作”部分中，事件转发规则始终按顺序执行。 您在保存规则时，应确保操作顺序正确。无法像使用标记一样选择此执行序列。

* 自定义代码 JavaScript 版本

   标记使用JavaScript版本es5。 事件转发使用的是版本es6。

<!--doc Adobe Cloud Connector extension, get from Jon-->
