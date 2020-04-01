---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隐私服务和Experience Cloud应用程序
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 隐私服务和Experience Cloud应用程序

Adobe Experience Platform隐私服务旨在支持多个Adobe Experience Cloud应用程序的隐私请求。 每个应用程序都支持不同的产品值和ID以识别数据主体。

本文档可作为Experience Cloud应用程序文档的参考，其中概述了如何配置该应用程序以执行与隐私相关的操作。 这包括如何设置数据的格式和标记数据。 涵盖两类别应用程序：

* [与隐私服务集成的应用程序](#integrated):能够向隐私服务发送访问、删除或选择退出请求的应用程序。
* [自助应用程序](#self-serve):必须在内部管理其隐私请求且不能直接与隐私服务通信的应用程序。

请查看Experience Cloud应用程序的文档，了解如何设置隐私请求的格式以及这些请求支持哪些值。

## 与隐私服务集成的应用程序 {#integrated}

以下是与隐私服务集成的Experience Cloud应用程序列表，包括与之兼容的隐私服务功能，以及指向文档的链接以获取更多信息。

| 应用程序 | 访问／删除 | 选择退出销售 | 文档和注意事项 |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[访问／删除文档](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>Advertising Cloud利用Adobe隐私中心提供的现有全球退出功能。 有关详细信息，请 [参阅有关提出数据隐私请求](https://docs.adobe.com/content/help/en/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) 的指南。</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[访问／删除文档](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/index.html)</li><li>Analytics使用隐私报告变量处理退出 [请求](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[访问／删除文档](https://marketing.adobe.com/resources/help/en_US/aam/aam-gdpr.html)</li><li>[退出文档](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[访问／删除文档](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[退出文档](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[访问／删除数据湖文档](../catalog/privacy.md)</li><li>[访问／删除实时客户用户档案文档](../profile/privacy.md)</li><li>Experience Platform支持 [针对受众细分的退出请求](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/honoring-opt-outs.md)。</li></ul> |
| Adobe Primetime身份验证 | ✓ | 不适用 | <ul><li>[访问／删除文档](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Primetime无法传输数据，因此不适用选择退出销售请求。</li></ul> |
| Adobe Target | ✓ | 不适用 | <ul><li>[访问／删除文档](https://marketing.adobe.com/resources/help/en_US/target/target/privacy-and-general-data-protection-regulation.html)</li><li>目标无法传输数据，因此不适用选择退出销售请求。</li></ul> |

<!-- (To include once access/delete documentation is available)
Adobe Customer Attributes (CRS) | ✓ | N/A | <ul><li>Customer Attributes does not have the capability to transfer data, therefore opt-out-of-sale requests are not applicable.</li></ul>
-->

## 自助式应用程序 {#self-serve}

以下是未与隐私服务集成的Experience Cloud应用程序列表，并且必须在内部管理其隐私问题。 提供了指向每个应用程序文档的链接以及文档内容的说明。

| 应用程序 | 文档说明 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Adobe Campaign经典的GDPR功能概述。 |
| [Adobe Dynamic Tag Manager](https://marketing.adobe.com/resources/help/en_US/dtm/opt-in.html) | 防止在获得同意前触发Adobe标记的步骤。 |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | 概述客户隐私管理员或AEM管理员如何处理GDPR请求。 |
| [Adobe Experience Manager Livefyre](https://marketing.adobe.com/resources/help/en_US/livefyre/c_gdpr_compliance.html) | 使用Livefyre进行GDPR访问和删除请求的步骤。 |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | 介绍开发人员如何使用扩展功能和规则生成器，来定义“选择加入”和“选择退出”解决方案。 |
| [Adobe Social](https://marketing.adobe.com/resources/help/en_US/social/c_gdpr-request.html) | 使用GDPR请求表访问或删除Social收集的数据的步骤。 |