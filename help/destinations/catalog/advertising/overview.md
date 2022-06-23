---
keywords: 广告目标；目标；平台目标
title: 广告目标概述
seo-title: Advertising destinations overview
description: 将Adobe Experience Platform连接到第三方广告平台(例如DSP、广告网络、SSP)，并将假名受众共享到这些平台。
seo-description: Connect Adobe Experience Platform to a 3rd-party advertising platform (e.g. DSP, ad network, SSP) and share pseudonymous audiences to these platforms.
exl-id: 072743a4-fc62-4a61-92ec-8f9640a47ab2
source-git-commit: 74b3c6f24486d8b18750932f1268f0da7f5fa034
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 1%

---

# 广告目标概述 {#advertising-destinations}

## 概述 {#overview}

将Adobe Experience Platform连接到第三方广告平台，例如需求方平台(DSP)、供应方平台(SSP)、广告网络，并将假名受众共享到这些平台。

连接到广告目标时，您的受众将作为ID发送到目标平台，然后这些受众会映射到目标平台已知的ID。

## 支持的广告目标 {#supported-destinations}

目前，Experience Platform支持下面列出的广告目标。

要了解连接和扩展之间的差异，请参阅 [连接](../../destination-types.md#connections) （在目标类型和类别页面中）。

### 连接

* [(Beta)Criteo连接](criteo.md)
* [Google Display &amp; Video 360连接](google-dv360.md)
* [Google Ads连接](google-ads-destination.md)
* [Google Ad Manager连接](google-ad-manager.md)
* [（测试版）Google Ad Manager 360连接](google-ad-manager-360-connection.md)
* [Google客户匹配连接](google-customer-match.md)
* [Microsoft Bing连接](bing.md)
* [Pinterest客户列表连接](pinterest.md)
* [交易台连接](tradedesk.md)
* [Yahoo/Verizon DataX](datax.md)

### 扩展

* [Adobe Advertising Cloud扩展](adobe-advertising-cloud.md)
* [Awin广告转化标记扩展](awin-conversiontag.md)
* [Awin Advertising Mastertag扩展](awin-mastertag.md)
* [Bing Ads通用事件跟踪扩展](bing-ads.md)
* [分支扩展](branch.md)
* [DoubleClick Floodlight扩展](doubleclick-floodlight.md)
* [Facebook Pixel扩展](facebook-pixel.md)
* [Flashtalking OneTag扩展](flashtalking.md)
* [Google Ads扩展](google-ads-extension.md)
* [Google扩展](gtag-advertising.md)
* [linkedIn Insight Tag扩展](linkedin.md)
* [Pinterest转化跟踪扩展](pinterest-extension.md)
* [Twitter通用网站标记扩展](twitter-uwt.md)

## 连接到新的广告目标 {#connect-destination}

要将区段发送到营销活动的广告目标，Platform必须先连接到该目标。 请参阅 [目标创建教程](../../ui/connect-destination.md) 以了解有关设置新目标的详细信息。
