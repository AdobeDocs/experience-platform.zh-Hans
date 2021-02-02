---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service和Experience Cloud应用程序
topic: overview
description: 此文档提供有关如何为隐私相关操作配置不同Experience Cloud应用程序的参考。
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 19%

---


# [!DNL Privacy Service] 和应 [!DNL Experience Cloud] 用

Adobe Experience Platform[!DNL Privacy Service]专为支持Adobe Experience Cloud多个应用程序的隐私请求而构建。 每个应用程序都支持不同的产品值和ID，用于识别数据主体。

此文档可用作[!DNL Experience Cloud]应用程序文档的参考，其中概述了如何配置该应用程序以进行与隐私相关的操作。 这包括如何格式化和标记数据。 涵盖两类别应用程序：

* [与Privacy Service集成的应用程序](#integrated):能够向其发送访问、删除或选择退出请求的应用程序 [!DNL Privacy Service]。
* [自助应用程序](#self-serve):必须在内部管理其隐私请求且不能直接与之通信的 [!DNL Privacy Service] 应用程序。

请查阅[!DNL Experience Cloud]应用程序的文档，了解如何设置隐私请求的格式以及这些请求支持哪些值。

## 与[!DNL Privacy Service]{#integrated}集成的应用程序

以下是与[!DNL Privacy Service]集成的[!DNL Experience Cloud]应用程序的列表，包括它们兼容的[!DNL Privacy Service]功能，以及指向文档的链接以获取详细信息。

| 应用程序 | 访问／删除 | 选择退出销售 | 文档和注意事项 |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | 选定 | 选定 | <ul><li>[访问／删除GDPR文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[CCPA的访问／删除文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的退出销售文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | 选定 | 选定 | <ul><li>[访问／删除文档](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] 使用隐私报告变量处 [理退出请求](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | 选定 | 选定 | <ul><li>[访问／删除文档](https://docs.adobe.com/content/help/zh-Hans/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[退出文档](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | 选定 | 选定 | <ul><li>[访问／删除文档](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[退出文档](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe客户属性(CRS) | 选定 | 不适用 | <ul><li>[访问／删除GDPR文档](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/customer-attributes/gdpr.html)</li><li>[CCPA的访问／删除文档](https://docs.adobe.com/content/help/zh-Hans/core-services/interface/customer-attributes/ccpa.html)</li><li>客户属性无法传输数据，因此不适用退出销售请求。</li></ul> |
| Adobe Experience Platform | 选定 | 选定 | <ul><li>[访问／删除数据湖文档](../catalog/privacy.md)</li><li>[访问／删除实时客户用户档案文档](../profile/privacy.md)</li><li>[!DNL Experience Platform] 接受 [受众区段的退出请求](../segmentation/honoring-opt-outs.md)。</li></ul> |
| Adobe Primetime认证 | 选定 | 不适用 | <ul><li>[访问／删除文档](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 无法传输数据，因此不适用退出销售请求。</li></ul> |
| Adobe Target | 选定 | 不适用 | <ul><li>[访问／删除文档](https://docs.adobe.com/content/help/zh-Hans/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 无法传输数据，因此不适用退出销售请求。</li></ul> |


## 自助服务应用程序{#self-serve}

以下是未与[!DNL Privacy Service]集成的[!DNL Experience Cloud]应用程序的列表，必须在内部管理其隐私问题。 提供了指向每个应用程序文档的链接以及文档内容的说明。

| 应用程序 | 文档说明 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Adobe Campaign ClassicGDPR功能概述。 |
| [Adobe动态标签管理器](https://docs.adobe.com/content/help/zh-Hans/dtm/using/tools/opt-in.html) | 防止Adobe标签在获得同意前激发的步骤。 |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | 概述客户隐私管理员或AEM管理员如何处理GDPR请求。 |
| [Adobe Experience ManagerLivefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre进行GDPR访问和删除请求的步骤。 |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | 介绍开发人员如何使用扩展功能和规则生成器，来定义“选择加入”和“选择退出”解决方案。 |
