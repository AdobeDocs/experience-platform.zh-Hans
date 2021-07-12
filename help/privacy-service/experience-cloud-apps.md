---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service和Experience Cloud应用程序
topic-legacy: overview
description: 本文档提供了有关如何为隐私相关操作配置不同Experience Cloud应用程序的参考。
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 55d6d8ad7b0fc5457dc0fdc981aaa92717adbe68
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 12%

---

# [!DNL Privacy Service] 和应用程 [!DNL Experience Cloud] 序

Adobe Experience Platform [!DNL Privacy Service]旨在支持多个Adobe Experience Cloud应用程序的隐私请求。 每个应用程序都支持不同的产品值和ID来识别数据主体。

本文档作为[!DNL Experience Cloud]应用程序文档的参考，其中概述了如何配置该应用程序以执行与隐私相关的操作。 这包括如何设置数据的格式和标签。 包括两类应用程序：

* [与Privacy Service集成的应用程序](#integrated):能够向发送访问、删除或选择退出请求的应用程 [!DNL Privacy Service]序。
* [自助式应用程序](#self-serve):必须在内部管理其隐私请求且不能直接与之通信的应 [!DNL Privacy Service] 用程序。

请查看[!DNL Experience Cloud]应用程序的文档，了解如何设置隐私请求的格式，以及这些请求支持哪些值。

## 与[!DNL Privacy Service]集成的应用程序 {#integrated}

以下是与[!DNL Privacy Service]集成的[!DNL Experience Cloud]应用程序列表，包括它们兼容的[!DNL Privacy Service]功能，以及指向文档的链接以获取更多信息。

| 应用程序 | 访问/删除 | 选择退出销售 | 文档和注意事项 |
| --- | :---: | :---: | --- |
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[访问/删除GDPR文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[CCPA的访问/删除文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的选择退出销售文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=zh-Hans)</li><li>[!DNL Analytics] 使用隐私报表变量处理 [选择退出请求](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[选择退出文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hans)</li><li>[选择退出文档](../segmentation/consents.md)</li></ul> |
| Adobe客户属性(CRS) | ✓ | 不适用 | <ul><li>[访问/删除GDPR文档](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[CCPA的访问/删除文档](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>客户属性无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[数据湖的访问/删除文档](../catalog/privacy.md)</li><li>[实时客户资料的访问/删除文档](../profile/privacy.md)</li><li>[!DNL Experience Platform] 执行 [受众区段的选择退出请求](../segmentation/consents.md)。</li></ul> |
| Adobe Primetime身份验证 | ✓ | 不适用 | <ul><li>[访问/删除文档](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Adobe Target | ✓ | 不适用 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 无法传输数据，因此选择退出销售请求不适用。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 自助式应用程序 {#self-serve}

以下是未与[!DNL Privacy Service]集成且必须在内部管理其隐私问题的[!DNL Experience Cloud]应用程序列表。 此外，还提供了指向每个应用程序文档的链接以及文档内容的描述。

| 应用程序 | 文档描述 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html) | 概述适用于Adobe Campaign Classic的GDPR功能。 |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 概述客户隐私管理员或AEM管理员如何处理GDPR请求。 |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre发出GDPR访问和删除请求的步骤。 |
| [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/client-side-info/deploy-javascript-tags-to-opt-in-to-launch.html) | 介绍开发人员如何使用扩展功能和规则生成器，来定义“选择加入”和“选择退出”解决方案。 |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | 确保您的Magento Commerce安装符合特定隐私法规的要求。 |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | 了解隐私法规如何应用于Marketo。 |
| [Workfront](https://www.workfront.com/privacy-notice) | 了解Workfront如何收集个人数据，以及数据主体如何通过表单提交隐私请求。 |

{style=&quot;table-layout:auto&quot;}
