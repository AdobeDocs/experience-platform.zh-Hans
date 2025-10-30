---
title: 标记和事件转发发行说明
description: 有关 Adobe Experience Platform 中的标记和事件转发的最新发行说明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 88%

---

# 标记和事件转发发行说明

>[!IMPORTANT]
>
>今后，此页面将不再提供标记和事件转发发行说明。请参阅最新的 [Adobe Experience Platform 发行说明](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=zh-Hans#data-collection)，了解有关标记和事件转发的详细更新。

## 2023 年 4 月 26 日

* **OAuth JWT 机密**：[OAuth JWT 机密](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=zh-Hans)客户可以使用 Adobe 和 Google 服务令牌在事件转发中支持服务器到服务器的交互。

以下新扩展已发布：

* **[!DNL Pinterest Conversions API]扩展**：通过使用 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=zh-Hans) 事件转发扩展功能，可利用在 Adobe Experience Platform Edge Network 中捕获的数据，并使用 [!DNL Pinterest Conversions API] 以服务器端事件的形式将数据发送到 [!DNL Pinterest]。

## 2023 年 3 月 29 日

**快速 Stark 工作流 (Beta)**

从数据收集主屏幕访问“开始使用”下新的快速启动工作流！以下工作流现在以公开 Beta 版的形式提供给客户。

* **[Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=zh-Hans#quick-start)**：事件转发客户可以快速收集事件数据并将其从服务器端转发到 Meta，只需几个简单的步骤即可实现广告转换。
* **[移动 SDK](https://developer.adobe.com/client-sdks/documentation/)**：客户只需几个简单的步骤即可快速实施移动 SDK 并验证基本的移动事件。

已发布新扩展：

* **[!DNL Braze]事件转发扩展**：[[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=zh-Hans) 事件转发扩展允许您利用 Adobe Experience Platform Edge Network 中捕获的数据，并使用 [!DNL Braze] User Track API 以服务器端事件的形式将其发送到 [!DNL Braze]。
* **[Epsilon 事件 API] 事件转发扩展**：[[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=zh-Hans) 扩展允许您利用事件转发功能在 Adobe Experience Platform Edge Network 中捕获事件信息，并使用 [!DNL Epsilon] Event API 将其发送给 [!DNL Epsilon]。
* **[!DNL Mixpanel]事件转发扩展**：[[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=zh-Hans) 扩展允许您利用事件转发功能在 Adobe Experience Platform Edge Network 中捕获事件信息，并使用 Track Events API 将其发送给 [!DNL Mixpanel]。

## 2023 年 1 月 25 日

* **新的主屏幕**：数据收集 UI 的主页已更新，其中包含有用的入门信息和可提高生产力的链接。这包括：
   1. 入门文档和推荐的工作流
   1. 最近的属性、规则和数据元素
   1. 热门扩展
   1. 具有快速安装功能的新扩展更新
* **使用事件转发功能将数据发送至 [!DNL Google Ads]**：您现在可以使用 [[!DNL Google Ads Enhanced Conversions] API 扩展](../extensions/server/google-ads-enhanced-conversions/overview.md)进行事件转发，结合 [Google Oauth 2 机密](../ui/event-forwarding/secrets.md#google-oauth2)，安全地实时将服务器端数据发送到 [!DNL Google Ads]。

## 2022 年 11 月 23 日

* **[!DNL AWS]事件转发的** 扩展：您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到 [!DNL Amazon Web Services] ([!DNL AWS])。有关更多信息，请参阅[[!DNL AWS] 扩展概述](../../tags/extensions/server/aws/overview.md)。
* 事件转发的 **[!DNL Google Ads Enhanced Conversions]扩展**：您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将转化数据发送到 [!DNL Google Ads]。有关更多信息，请参阅[[!DNL Google Ads Enhanced Conversions] 扩展概述](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)。
* 事件转发的 **[!DNL Microsoft Azure]扩展**：您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到 [!DNL Microsoft Azure]。有关更多信息，请参阅[[!DNL Microsoft Azure] 扩展概述](../../tags/extensions/server/azure/overview.md)。

## 2022 年 10 月 26 日

* **数据流的敏感数据处理**：数据流现在利用几种Experience Platform技术适当地处理由健康保险可移植性和责任法案(HIPAA)等法规强制执行的敏感数据。 有关详细信息，请参阅[处理数据流中的敏感数据](../../datastreams/overview.md#sensitive)部分。
* 事件转发的 **[!DNL Splunk]扩展**：您现在可以使用[事件转发](../ui/event-forwarding/overview.md)扩展将数据发送到 [!DNL Splunk]。有关更多信息，请参阅[[!DNL Splunk] 扩展概述](../extensions/server/splunk/overview.md)。
* 事件转发的 **[!DNL Zendesk]扩展**：您现在可以使用[事件转发](../ui/event-forwarding/overview.md)扩展将数据发送到 [!DNL Zendesk]。有关更多信息，请参阅[[!DNL Zendesk] 扩展概述](../extensions/server/zendesk/overview.md)。

## 2022 年 9 月 28 日

* **Adobe Experience Platform左侧导航集成**：之前专用于数据收集UI的所有功能（包括标记和事件转发）现在也可以通过Experience Platform UI的左侧导航在类别&#x200B;**[!UICONTROL Data Collection]**&#x200B;下使用。 当在Experience Platform中使用数据收集功能时，无需在UI之间进行切换。
* **标记和事件转发中的用户归因**：在标记和事件转发中列出可用属性时，每个列出的属性现在都会显示最后更新的时间和更新者。
* 事件转发的 **[[!DNL Snap Conversions API] 扩展](https://exchange.adobe.com/apps/ec/108550)**：您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到 [!DNL Snapchat Conversions API]。有关如何验证和使用 API 的更多信息，请参阅此[[!DNL Snapchat Marketing API] 文档](https://marketingapi.snapchat.com/docs/conversion.html)。

## 2022 年 7 月 27 日

* 现在，通过 Adobe Experience Platform 数据收集信息卡下的 Adobe Admin Console 管理对标记和事件转发功能的访问。请参阅指南[数据收集权限](../../collection/permissions.md)，以了解更多信息。
* 对 Internet Explorer 10 和 11 的支持[已弃用](../ie-deprecation.md)。

## 2022 年 6 月 22 日

已发布新扩展：

* [Google 数据层标记扩展](../extensions/client/google-data-layer/overview.md)：允许您在标记实施中使用 Google 数据层。
* [Google Ads 增强型转化事件转发扩展](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html)：允许您实时增强 Google Ads 转化率。
* [Mailchimp 事件转发扩展](../extensions/server/mailchimp/overview.md)：可将事件发送到 Mailchimp 营销 API，从而触发 Mailchimp 营销活动、历程或交易的电子邮件。