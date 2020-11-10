---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service和Experience Cloud应用程序
topic: overview
translation-type: tm+mt
source-git-commit: 4cd7b9d3ca542c2fba83d066197b92775c053729
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 20%

---


# [!DNL Privacy Service] 和应 [!DNL Experience Cloud] 用

Adobe Experience Platform [!DNL Privacy Service] 的设计初衷是支持Adobe Experience Cloud多个应用程序的隐私请求。 每个应用程序都支持不同的产品值和ID，用于识别数据主体。

此文档可作为应用程序文 [!DNL Experience Cloud] 档的参考，其中概述了如何配置该应用程序进行与隐私相关的操作。 这包括如何格式化和标记数据。 涵盖两类别应用程序：

* [与Privacy Service集成的应用程序](#integrated):能够向其发送访问、删除或选择退出请求的应用程序 [!DNL Privacy Service]。
* [自助应用程序](#self-serve):必须在内部管理其隐私请求且不能直接与之通信的应 [!DNL Privacy Service] 用程序。

请查阅您的应用程序 [!DNL Experience Cloud] 的文档，了解如何设置隐私请求的格式以及这些请求支持哪些值。

## 与 [!DNL Privacy Service] {#integrated}

以下是与之集成的 [!DNL Experience Cloud] 应用程序列表, [!DNL Privacy Service]包括它们 [!DNL Privacy Service] 兼容的功能，以及指向文档的链接以获取更多信息。

| 应用程序 | 访问／删除 | 选择退出销售 | 文档和注意事项 |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[访问／删除GDPR文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[CCPA的访问／删除文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的退出销售文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[访问／删除文档](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] 使用隐私报告变量处 [理退出请求](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[访问／删除文档](https://docs.adobe.com/content/help/zh-Hans/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[退出文档](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[访问／删除文档](https://docs.campaign.adobe.com/doc/standard/getting_started/cn/ACS_GDPR.html)</li><li>[退出文档](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe客户属性(CRS) | ✓ | 不适用 | <ul><li>[访问／删除GDPR文档](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/customer-attributes/gdpr.html)</li><li>[CCPA的访问／删除文档](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/customer-attributes/ccpa.html)</li><li>客户属性无法传输数据，因此不适用退出销售请求。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[访问／删除数据湖文档](../catalog/privacy.md)</li><li>[访问／删除实时客户用户档案文档](../profile/privacy.md)</li><li>[!DNL Experience Platform] 接受 [受众区段的退出请求](../segmentation/honoring-opt-outs.md)。</li></ul> |
| Adobe Primetime认证 | ✓ | 不适用 | <ul><li>[访问／删除文档](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 无法传输数据，因此不适用退出销售请求。</li></ul> |
| Adobe Target | ✓ | 不适用 | <ul><li>[访问／删除文档](https://docs.adobe.com/content/help/zh-Hans/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 无法传输数据，因此不适用退出销售请求。</li></ul> |


## 自助应用程序 {#self-serve}

以下是未与其集成 [!DNL Experience Cloud] 并必须在内部管理其隐 [!DNL Privacy Service] 私问题的应用程序列表。 提供了指向每个应用程序文档的链接以及文档内容的说明。

| 应用程序 | 文档说明 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Adobe Campaign ClassicGDPR功能概述。 |
| [Adobe动态标签管理器](https://docs.adobe.com/content/help/zh-Hans/dtm/using/tools/opt-in.html) | 防止Adobe标签在获得同意前激发的步骤。 |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | 概述客户隐私管理员或AEM管理员如何处理GDPR请求。 |
| [Adobe Experience ManagerLivefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre进行GDPR访问和删除请求的步骤。 |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | 介绍开发人员如何使用扩展功能和规则生成器，来定义“选择加入”和“选择退出”解决方案。 |
