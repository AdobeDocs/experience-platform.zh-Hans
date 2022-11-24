---
title: 标记和事件转发发行说明
description: 有关 Adobe Experience Platform 中的标记和事件转发的最新发行说明。
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 6%

---

# 标记和事件转发的发行说明

## 2022 年 10 月 26 日

* **数据流的敏感数据处理**:数据流现在利用多种平台技术适当地处理受法规(如健康保险流通和责任法案(HIPAA))强制实施的敏感数据。 请参阅 [处理数据流中的敏感数据](../../edge/datastreams/overview.md#sensitive) 以了解更多信息。
* **[!DNL Splunk]事件转发扩展**:您现在可以将数据发送到 [!DNL Splunk] 使用 [事件转发](../ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Splunk] 扩展概述](../extensions/server/splunk/overview.md) 以了解更多信息。
* **[!DNL Zendesk]事件转发扩展**:您现在可以将数据发送到 [!DNL Zendesk] 使用 [事件转发](../ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Zendesk] 扩展概述](../extensions/server/zendesk/overview.md) 以了解更多信息。

## 2022 年 9 月 28 日

* **Adobe Experience Platform左导航集成**:以前只有数据收集UI才能使用的所有功能（包括标记和事件转发）现在也可以通过Experience PlatformUI的左侧导航中类别下的方式使用 **[!UICONTROL 数据收集]**. 使用Platform中的数据收集功能时，无需在UI之间切换。
* **标记和事件转发中的用户归因**:现在，在标记和事件转发中列出可用属性时，每个列出的属性都会显示上次更新时间以及更新者。
* **[[!DNL Snap Conversions API] 扩展](https://exchange.adobe.com/apps/ec/108550) 用于事件转发**:您现在可以将数据发送到 [!DNL Snapchat Conversions API] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 有关如何验证和使用API的更多信息，请参阅 [[!DNL Snapchat Marketing API] 文档](https://marketingapi.snapchat.com/docs/conversion.html).

## 2022 年 7 月 27 日

* 现在，可通过Adobe Admin Console中Adobe Experience Platform数据收集卡下的管理对标记和事件转发功能的访问。 请参阅 [数据收集权限](../../collection/permissions.md) 以了解更多信息。
* 已支持Internet Explorer 10和11 [已弃用](../ie-deprecation.md).

## 2022 年 6 月 22 日

已发布新扩展：

* [Google Data Layer标记扩展](../extensions/client/google-data-layer/overview.md):用于在标记实施中使用Google数据层。
* [Google Ads Enhanced Conversions事件转发扩展](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html):允许您实时提高Google广告转化。
* [Mailchimp事件转发扩展](../extensions/server/mailchimp/overview.md):将事件发送到Mailchimp营销API，该API可以触发Mailchimp营销活动、历程或交易的电子邮件。
