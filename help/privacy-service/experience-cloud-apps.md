---
keywords: Experience Platform；首页；热门话题
solution: Experience Platform
title: Privacy Service和Experience Cloud应用程序
description: 本文档提供了有关如何为隐私相关操作配置各种Experience Cloud应用程序的参考。
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: b8b862a2134d4901e45f5dce82ac4de457ed6db6
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 8%

---

# [!DNL Privacy Service]和[!DNL Experience Cloud]应用程序

Adobe Experience Platform [!DNL Privacy Service]构建用于支持多个Adobe Experience Cloud应用程序的隐私请求。 每个应用程序支持不同的产品值和ID，以便识别数据主体。

本文档可作为[!DNL Experience Cloud]应用程序文档的参考，该文档概述了如何配置该应用程序以进行与隐私相关的操作。 这包括如何格式化数据和为数据设置标签。 其中涵盖了两种类型的应用程序：

* [与Privacy Service集成的应用程序](#integrated)：能够向[!DNL Privacy Service]发送访问、删除或选择退出请求的应用程序。
* [自助应用程序](#self-serve)：必须在内部管理其隐私请求的应用程序，不能直接与[!DNL Privacy Service]通信。

请查看[!DNL Experience Cloud]应用程序的文档，了解如何设置隐私请求的格式，以及这些请求支持哪些值。

## 与[!DNL Privacy Service]集成的应用程序 {#integrated}

以下是与[!DNL Experience Cloud]集成的[!DNL Privacy Service]应用程序的列表，包括它们兼容的[!DNL Privacy Service]功能、它们处理删除请求的协议以及指向文档的链接以了解更多信息。

>[!NOTE]
>
>所有集成产品均可在30天或更短时间内响应隐私请求。

| 应用程序 | 访问/删除 | 选择禁用销售 | 删除行为 | 文档和其他注意事项 |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising | ✓ | ✓ | 数据主体的Cookie ID或设备ID以及与Cookie关联的所有成本、点击和收入数据都会从系统中删除。 | <ul><li>[访问/删除GDPR文档](https://experienceleague.adobe.com/en/docs/advertising/privacy/gdpr)</li><li>[访问/删除CCPA文档](https://experienceleague.adobe.com/en/docs/advertising/privacy/ccpa/ccpa-access-delete)</li><li>[CCPA的选择退出销售文档](https://experienceleague.adobe.com/en/docs/advertising/privacy/ccpa/ccpa-opt-out-of-sale)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics提供了用于根据其敏感性和合同限制来标记数据的工具。 标签是执行以下操作的重要步骤：<ol><li>识别数据主体。</li><li>确定作为访问请求的一部分返回哪些数据。</li><li>确定删除请求中必须删除的数据字段。</li></ol> | <ul><li>[隐私工作流](https://experienceleague.adobe.com/en/docs/analytics/technotes/privacy/gdpr)</li><li>[Analytics标签](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/privacy-labeling/labels)</li><li>[Analytics选择退出](https://experienceleague.adobe.com/en/docs/analytics/components/dimensions/cm-opt-out)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | 与请求中包含的Audience Manager标识符关联的所有特征和区段都会被删除。 此外，个人相应的标识符被选择退出进一步的数据收集并且相应的ID映射被移除。 | <ul><li>[访问](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests#access-data) / [删除](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests#delete-data)文档</li><li>[选择退出文档](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/declared-ids#opt-out-calls)</li><li>[选择退出请求](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | 从系统中删除数据主体的存储数据。 | <ul><li>[隐私管理](https://experienceleague.adobe.com/en/docs/campaign-classic/using/getting-started/privacy/privacy-management)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | 从系统中删除数据主体的存储数据。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/en/docs/campaign-standard/using/getting-started/privacy/privacy-management#right-access-forgotten)</li><li>[选择退出文档](https://experienceleague.adobe.com/en/docs/campaign-standard/using/profiles-and-audiences/understanding-opt-in-and-opt-out-processes/about-opt-in-and-opt-out-in-campaign)</li></ul> |
| Adobe客户属性(CRS) | ✓ | 不适用 | 从系统中删除数据主体的属性。 | <ul><li>[访问/删除GDPR文档](https://experienceleague.adobe.com/en/docs/core-services/interface/services/customer-attributes/gdpr)</li><li>[访问/删除CCPA文档](https://experienceleague.adobe.com/en/docs/core-services/interface/services/customer-attributes/ccpa)</li><li>客户属性无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | 当Experience Platform收到来自Privacy Service的删除请求时，Experience Platform会向Privacy Service发送确认，确认已收到该请求并且已将受影响的数据标记为删除。 隐私作业完成后，记录将从数据湖或配置文件存储中删除。 在作业完成之前，数据会被软删除，因此任何Experience Platform服务都无法访问。 | <ul><li>[访问/删除数据湖的文档](../catalog/privacy.md)</li><li>[访问/删除Identity服务的文档](../identity-service/privacy.md)</li><li>[访问/删除实时客户个人资料的文档](../profile/privacy.md)</li><li>[!DNL Experience Platform]执行受众区段的[选择退出请求](../segmentation/tutorials/consents.md)。</li></ul> |
| Adobe Journey Optimizer | ✓ | 不适用 | 从系统中删除数据主体的存储数据。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Adobe Pass 身份验证 | ✓ | 不适用 | 从系统中删除数据主体的存储数据。 | <ul><li>[访问/删除文档](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Pass无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Adobe Target | ✓ | 不适用 | 与数据主体ID关联的所有数据都会从其访客配置文件中删除。 无法识别个人或无其他关联的聚合或匿名数据（例如内容数据）不适用于删除请求。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/en/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation)</li><li>[!DNL Target]没有传输数据的功能，因此选择退出销售请求不适用。</li></ul> |
| Commerce (Personalization) | ✓ | 不适用 | Privacy Service出于营销目的删除存储在Commerce SaaS服务中的[!DNL Commerce]数据，这意味着数据主体的配置文件和订单不再发送到Adobe营销应用程序以用于营销活动和客户历程。 但是，Privacy Service不会删除[!DNL Commerce]应用程序中的数据，因为商家事务型需求可能仍需要这些数据。 商家负责[!DNL Commerce]应用程序中的任何数据删除/访问请求。 | <ul><li>[访问/删除Commerce的文档](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/handle-privacy-request)</li></ul> |
| Marketo Engage | ✓ | 不适用 | 从系统中删除数据主体的存储数据。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests)</li><li>[!DNL Marketo]没有传输数据的功能，因此选择退出销售请求不适用。</li></ul> |

## 自助应用程序 {#self-serve}

以下是[!DNL Experience Cloud]应用程序的列表，这些应用程序未与[!DNL Privacy Service]集成，必须在内部管理其隐私问题。 提供了指向每个应用程序文档的链接，以及文档内容的描述。

| 应用程序 | 文档描述 |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy) | 概述客户隐私管理员或AEM管理员如何处理GDPR请求。 |
| [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/overview) | 确保您的Adobe Commerce安装符合特定隐私法规的要求。 |
| Adobe Experience Platform中的[标记](../tags/ui/client-side/consent.md) | 介绍开发人员如何使用扩展功能和规则生成器，来定义“选择加入”和“选择退出”解决方案。 |
| [Workfront](https://www.workfront.com/privacy-notice) | 了解Workfront如何收集个人数据，以及数据主体如何通过表单提交隐私请求。 |
