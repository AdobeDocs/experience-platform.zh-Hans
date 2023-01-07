---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service和Experience Cloud应用程序
description: 本文档提供了有关如何为隐私相关操作配置不同Experience Cloud应用程序的参考。
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 11%

---

# [!DNL Privacy Service] 和 [!DNL Experience Cloud] 应用程序

Adobe Experience Platform [!DNL Privacy Service] 旨在支持多个Adobe Experience Cloud应用程序的隐私请求。 每个应用程序都支持不同的产品值和ID来识别数据主体。

本文档作为 [!DNL Experience Cloud] 应用程序文档，其中概述了如何配置该应用程序以执行与隐私相关的操作。 这包括如何设置数据的格式和标签。 包括两类应用程序：

* [与Privacy Service集成的应用程序](#integrated):能够向发送访问、删除或选择退出请求的应用程序 [!DNL Privacy Service].
* [自助式应用程序](#self-serve):必须在内部管理其隐私请求且无法与通信的应用程序 [!DNL Privacy Service] 直接。

请查看您的 [!DNL Experience Cloud] 应用程序以了解如何设置隐私请求的格式，以及这些请求支持哪些值。

## 与集成的应用程序 [!DNL Privacy Service] {#integrated}

以下是 [!DNL Experience Cloud] 与 [!DNL Privacy Service]，包括 [!DNL Privacy Service] 与兼容的功能、用于处理删除请求的协议，以及指向文档的链接以获取更多信息。

>[!NOTE]
>
>所有集成产品会在30天内响应隐私请求。

| 应用程序 | 访问/删除 | 选择退出销售 | 删除行为 | 文档和其他注意事项 |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | 数据主体的Cookie ID或设备ID将从系统中删除，以及与Cookie关联的所有成本、点击和收入数据也将一起删除。 | <ul><li>[访问/删除GDPR文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[CCPA的访问/删除文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的选择退出销售文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | 如果 `analyticsDeleteMethod` 忽略或设置为 `anonymize` 在发出隐私请求时，给定用户ID集合引用的所有数据都将设为匿名。 如果 `analyticsDeleteMethod` 设置为 `purge`，则所有数据都将被完全删除。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=zh-Hans)</li><li>[!DNL Analytics] 使用 [隐私报表变量](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html?lang=zh-Hans)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | 与请求中包含的Audience Manager标识符关联的所有特征和区段都将被删除。 此外，个人的相应标识符被选择退出进一步的数据收集，并且相应的ID映射被移除。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[选择退出文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | 数据主体所存储的数据将从系统中删除。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hans)</li><li>[选择退出文档](../segmentation/consents.md)</li></ul> |
| Adobe客户属性(CRS) | ✓ | 不适用 | 数据主体的属性将从系统中删除。 | <ul><li>[访问/删除GDPR文档](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[CCPA的访问/删除文档](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>客户属性无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | 当Experience Platform收到来自Privacy Service的删除请求时，Platform会向Privacy Service发送确认，确认该请求已被接收，且受影响的数据已被标记为删除。 隐私作业完成后，将从数据湖或配置文件存储中删除记录。 作业完成前，数据会被软删除，因此任何平台服务都无法访问。 | <ul><li>[数据湖的访问/删除文档](../catalog/privacy.md)</li><li>[Identity Service的访问/删除文档](../identity-service/privacy.md)</li><li>[实时客户资料的访问/删除文档](../profile/privacy.md)</li><li>[!DNL Experience Platform] 荣誉 [受众区段的选择退出请求](../segmentation/consents.md).</li></ul> |
| Adobe Primetime身份验证 | ✓ | 不适用 | 数据主体所存储的数据将从系统中删除。 | <ul><li>[访问/删除文档](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Adobe Target | ✓ | 不适用 | 与数据主体的ID关联的所有数据都会从其访客配置文件中删除。 未识别个人或其他无关的聚合或匿名数据（如内容数据）不适用于删除请求。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Marketo Engage | ✓ | 不适用 | 数据主体所存储的数据将从系统中删除。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] 无法传输数据，因此选择退出销售请求不适用。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 自助式应用程序 {#self-serve}

以下是 [!DNL Experience Cloud] 未与集成的应用程序 [!DNL Privacy Service] 必须在内部管理他们的隐私问题。 此外，还提供了指向每个应用程序文档的链接以及文档内容的描述。

| 应用程序 | 文档描述 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hans) | 概述适用于Adobe Campaign Classic的GDPR功能。 |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 概述客户隐私管理员或AEM管理员如何处理GDPR请求。 |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre发出GDPR访问和删除请求的步骤。 |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | 确保您的Magento Commerce安装符合特定隐私法规的要求。 |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | 了解隐私法规如何应用于Marketo。 |
| [Adobe Experience Platform 中的标记](../tags/ui/client-side/consent.md) | 介绍开发人员如何使用扩展功能和规则生成器，来定义“选择加入”和“选择退出”解决方案。 |
| [Workfront](https://www.workfront.com/privacy-notice) | 了解Workfront如何收集个人数据，以及数据主体如何通过表单提交隐私请求。 |

{style=&quot;table-layout:auto&quot;}
