---
title: 标记和事件转发的发行说明
description: 有关 Adobe Experience Platform 中的标记和事件转发的最新发行说明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 15%

---

# 标记和事件转发的发行说明

>[!IMPORTANT]
>
>往后看，此页面上将不再提供标记和事件转发发行说明。 请参阅最新的 [Adobe Experience Platform发行说明](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=en#data-collection) 了解详细的标记和事件转发更新。

## 2023 年 4 月 26 日

* **OAuth JWT密码**：和 [OAuth JWT密码](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 允许客户使用Adobe和Google服务令牌在事件转发中支持服务器到服务器交互。

已发布以下新扩展：

* **[!DNL Pinterest Conversions API]扩展**：和 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 事件转发扩展允许您利用Adobe Experience Platform Edge Network中捕获的数据并将其发送至 [!DNL Pinterest] 以服务器端事件的形式使用 [!DNL Pinterest Conversions API].

## 2023 年 3 月 29 日

**Quick Stark工作流（测试版）**

从数据收集主屏幕访问“开始使用”下新的快速启动工作流程！以下工作流现已作为公共测试版提供给客户。
* **[元转化API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start)**：事件转发客户只需几个简单的步骤，即可快速收集并转发事件数据、服务器端到元以进行广告转化。
* **[移动SDK](https://developer.adobe.com/client-sdks/documentation/)**：客户只需几个简单的步骤，即可快速实施Mobile SDK并验证基本移动事件。

已发布新扩展：

* **[!DNL Braze]事件转发扩展**：和 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件转发扩展允许您利用Adobe Experience Platform Edge Network中捕获的数据并将其发送至 [!DNL Braze] 以服务器端事件的形式使用 [!DNL Braze] 用户跟踪API。
* **[Epsilon事件API] 事件转发扩展**：和 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 扩展允许您利用事件转发来捕获Adobe Experience Platform Edge Network中的事件信息并将其发送给 [!DNL Epsilon] 使用 [!DNL Epsilon] 事件API。
* **[!DNL Mixpanel]事件转发扩展**：和 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 扩展允许您利用事件转发来捕获Adobe Experience Platform Edge Network中的事件信息并将其发送给 [!DNL Mixpanel] 使用跟踪事件API。

## 2023 年 1 月 25 日

* **新主屏幕**：数据收集UI主页已更新，包含有用的载入信息和简化生产力的链接。 这包括：
   1. 入门文档和推荐的工作流程
   1. 最近的属性、规则和数据元素
   1. 热门扩展
   1. 具有快速安装功能的新扩展更新
* **将数据发送到 [!DNL Google Ads] 使用事件转发**：您现在可以使用 [[!DNL Google Ads Enhanced Conversions] API扩展](../extensions/server/google-ads-enhanced-conversions/overview.md) 用于事件转发，与 [Google Oauth 2机密](../ui/event-forwarding/secrets.md#google-oauth2)，以将服务器端数据安全地发送到 [!DNL Google Ads] 实时。

## 2022 年 11 月 23 日

* **[!DNL AWS]事件转发的扩展**：您现在可以将数据发送到 [!DNL Amazon Web Services] ([!DNL AWS])使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL AWS] 扩展概述](../../tags/extensions/server/aws/overview.md) 以了解更多信息。
* **[!DNL Google Ads Enhanced Conversions]事件转发的扩展**：您现在可以将转化数据发送至 [!DNL Google Ads] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Google Ads Enhanced Conversions] 扩展概述](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 以了解更多信息。
* **[!DNL Microsoft Azure]事件转发的扩展**：您现在可以将数据发送到 [!DNL Microsoft Azure] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Microsoft Azure] 扩展概述](../../tags/extensions/server/azure/overview.md) 以了解更多信息。

## 2022 年 10 月 26 日

* **数据流的敏感数据处理**：数据流现在利用多种平台技术适当处理由健康保险便携性和责任法案(HIPAA)等法规强制执行的敏感数据。 请参阅以下部分 [处理数据流中的敏感数据](../../datastreams/overview.md#sensitive) 以了解更多信息。
* **[!DNL Splunk]事件转发的扩展**：您现在可以将数据发送到 [!DNL Splunk] 使用 [事件转发](../ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Splunk] 扩展概述](../extensions/server/splunk/overview.md) 以了解更多信息。
* **[!DNL Zendesk]事件转发的扩展**：您现在可以将数据发送到 [!DNL Zendesk] 使用 [事件转发](../ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Zendesk] 扩展概述](../extensions/server/zendesk/overview.md) 以了解更多信息。

## 2022 年 9 月 28 日

* **Adobe Experience Platform左侧导航集成**：之前数据收集UI独有的所有功能（包括标记和事件转发）现在也可通过左侧导航在Experience PlatformUI的类别下使用 **[!UICONTROL 数据收集]**. 当在Platform中使用数据收集功能时，无需在UI之间进行切换。
* **标记中的用户归因和事件转发**：现在，在标记和事件转发中列出可用属性时，每个列出的属性都会显示上次更新时间以及由谁更新。
* **[[!DNL Snap Conversions API] 扩展](https://exchange.adobe.com/apps/ec/108550) 用于事件转发**：您现在可以将数据发送到 [!DNL Snapchat Conversions API] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 有关如何验证和使用API的更多信息，请参阅 [[!DNL Snapchat Marketing API] 文档](https://marketingapi.snapchat.com/docs/conversion.html).

## 2022 年 7 月 27 日

* 现在，通过Adobe Experience Platform数据收集信息卡下的Adobe Admin Console，可管理对标记和事件转发功能的访问。 请参阅指南，网址为 [数据收集权限](../../collection/permissions.md) 以了解更多信息。
* 支持Internet Explorer 10和11 [已弃用](../ie-deprecation.md).

## 2022 年 6 月 22 日

已发布新扩展：

* [Google数据层标记扩展](../extensions/client/google-data-layer/overview.md)：允许您在标记实施中使用Google数据层。
* [Google Ads增强型转化事件转发扩展](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html)：用于实时增强Google广告转化。
* [Mailchimp事件转发扩展](../extensions/server/mailchimp/overview.md)：将事件发送到Mailchimp营销API，这可以触发Mailchimp营销活动、历程或交易的电子邮件。