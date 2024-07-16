---
title: 标记和事件转发的发行说明
description: 有关 Adobe Experience Platform 中的标记和事件转发的最新发行说明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 7%

---

# 标记和事件转发的发行说明

>[!IMPORTANT]
>
>往后看，此页面上将不再提供标记和事件转发发行说明。 有关详细的标记和事件转发更新，请参阅最新的[Adobe Experience Platform发行说明](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection)。

## 2023年4月26日

* **OAuth JWT密码**： [OAuth JWT密码](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html)允许客户使用Adobe和Google服务令牌在事件转发中支持服务器到服务器交互。

已发布以下新扩展：

* **[!DNL Pinterest Conversions API]扩展**： [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html)事件转发扩展允许您利用Adobe Experience PlatformEdge Network中捕获的数据，并使用[!DNL Pinterest Conversions API]以服务器端事件的形式将其发送到[!DNL Pinterest]。

## 2023年3月29日

**Quick Stark工作流(Beta)**

从数据收集主屏幕访问“开始使用”下新的快速启动工作流程！以下工作流现已作为公共Beta提供给客户。
* **[Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**：事件转发客户只需几个简单的步骤，即可快速收集和转发事件数据，从服务器端到元进行广告转换。
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**：客户只需几个简单的步骤，即可快速实施Mobile SDK并验证基本移动事件。

已发布新扩展：

* **[!DNL Braze]事件转发扩展**： [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html)事件转发扩展允许您利用Adobe Experience PlatformEdge Network中捕获的数据，并使用[!DNL Braze]用户跟踪API以服务器端事件的形式将其发送到[!DNL Braze]。
* **[Epsilon Events API]事件转发扩展**： [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html)扩展允许您利用事件转发捕获Adobe Experience PlatformEdge Network中的事件信息，并使用[!DNL Epsilon]事件API将其发送到[!DNL Epsilon]。
* **[!DNL Mixpanel]事件转发扩展**： [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html)扩展允许您利用事件转发捕获Adobe Experience PlatformEdge Network中的事件信息，并使用跟踪事件API将其发送到[!DNL Mixpanel]。

## 2023年1月25日

* **新主屏幕**：数据收集UI的主页已更新，包含有用的入门信息和简化生产力的链接。 这包括：
   1. 入门文档和推荐的工作流程
   1. 最近的属性、规则和数据元素
   1. 热门扩展
   1. 具有快速安装功能的新扩展更新
* **使用事件转发将数据发送到[!DNL Google Ads]**：您现在可以使用[[!DNL Google Ads Enhanced Conversions] API扩展](../extensions/server/google-ads-enhanced-conversions/overview.md)进行事件转发，并结合[Google Oauth 2密钥](../ui/event-forwarding/secrets.md#google-oauth2)，以便安全地实时将服务器端数据发送到[!DNL Google Ads]。

## 2022年11月23日

* 用于事件转发的&#x200B;**[!DNL AWS]扩展**：您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到[!DNL Amazon Web Services] ([!DNL AWS])。 有关详细信息，请参阅[[!DNL AWS] 扩展概述](../../tags/extensions/server/aws/overview.md)。
* 用于事件转发的&#x200B;**[!DNL Google Ads Enhanced Conversions]扩展**：您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将转换数据发送到[!DNL Google Ads]。 有关详细信息，请参阅[[!DNL Google Ads Enhanced Conversions] 扩展概述](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)。
* 用于事件转发的&#x200B;**[!DNL Microsoft Azure]扩展**：您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到[!DNL Microsoft Azure]。 有关详细信息，请参阅[[!DNL Microsoft Azure] 扩展概述](../../tags/extensions/server/azure/overview.md)。

## 2022年10月26日

* **数据流的敏感数据处理**：数据流现在利用多种平台技术正确处理健康保险便携性和责任法案(HIPAA)等法规强制执行的敏感数据。 有关详细信息，请参阅有关[处理数据流中的敏感数据](../../datastreams/overview.md#sensitive)的部分。
* 用于事件转发的&#x200B;**[!DNL Splunk]扩展**：您现在可以使用[事件转发](../ui/event-forwarding/overview.md)扩展将数据发送到[!DNL Splunk]。 有关详细信息，请参阅[[!DNL Splunk] 扩展概述](../extensions/server/splunk/overview.md)。
* 用于事件转发的&#x200B;**[!DNL Zendesk]扩展**：您现在可以使用[事件转发](../ui/event-forwarding/overview.md)扩展将数据发送到[!DNL Zendesk]。 有关详细信息，请参阅[[!DNL Zendesk] 扩展概述](../extensions/server/zendesk/overview.md)。

## 2022年9月28日

* **Adobe Experience Platform左侧导航集成**：以前专用于数据收集UI的所有功能（包括标记和事件转发）现在也可通过左侧导航在Experience PlatformUI的类别&#x200B;**[!UICONTROL 数据收集]**&#x200B;下使用。 当在Platform中使用数据收集功能时，无需在UI之间进行切换。
* **标记和事件转发中的用户归因**：在标记和事件转发中列出可用属性时，现在每个列出的属性都会显示上次更新时间以及由谁更新。
* 用于事件转发的&#x200B;**[[!DNL Snap Conversions API] 扩展](https://exchange.adobe.com/apps/ec/108550)**：您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到[!DNL Snapchat Conversions API]。 有关如何验证和使用API的更多信息，请参阅[[!DNL Snapchat Marketing API] 文档](https://marketingapi.snapchat.com/docs/conversion.html)。

## 2022 年 7 月 27 日

* 现在，通过Adobe Experience Platform数据收集信息卡下的Adobe Admin Console，可管理对标记和事件转发功能的访问。 有关详细信息，请参阅[数据收集权限](../../collection/permissions.md)指南。
* 对Internet Explorer 10和11的支持已[弃用](../ie-deprecation.md)。

## 2022年6月22日

已发布新扩展：

* [Google数据层标记扩展](../extensions/client/google-data-layer/overview.md)：允许您在标记实施中使用Google数据层。
* [Google Ads增强转化事件转发扩展](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html)：允许您实时增强Google Ads转化。
* [Mailchimp事件转发扩展](../extensions/server/mailchimp/overview.md)：将事件发送到Mailchimp营销API，这可以触发Mailchimp营销活动、历程或交易的电子邮件。