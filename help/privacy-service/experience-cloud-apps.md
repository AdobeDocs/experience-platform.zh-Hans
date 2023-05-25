---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service和Experience Cloud应用程序
description: 本文档提供了有关如何为与隐私相关的操作配置各种Experience Cloud应用程序的参考。
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 16985d285cf181547f3692c5ed1910eebe8df210
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 12%

---

# [!DNL Privacy Service] 和 [!DNL Experience Cloud] 应用程序

Adobe Experience Platform [!DNL Privacy Service] 构建用于支持多个Adobe Experience Cloud应用程序的隐私请求。 每个应用程序支持不同的产品值和ID，用于标识数据主体。

本文档可作为参考 [!DNL Experience Cloud] 应用程序文档，其中概述了如何配置该应用程序以进行与隐私相关的操作。 这包括如何设置数据的格式和标签。 其中涉及两类应用程序：

* [与Privacy Service集成的应用程序](#integrated)：能够向发送访问、删除或选择退出请求的应用程序 [!DNL Privacy Service].
* [自助应用程序](#self-serve)：必须在内部管理其隐私请求，并且无法与之通信的应用程序 [!DNL Privacy Service] 直接。

请查看文档，以了解 [!DNL Experience Cloud] 应用程序以了解如何设置隐私请求的格式，以及这些请求支持哪些值。

## 与集成的应用程序 [!DNL Privacy Service] {#integrated}

以下是以下列表 [!DNL Experience Cloud] 与集成的应用程序 [!DNL Privacy Service]，包括 [!DNL Privacy Service] 它们兼容的功能、处理删除请求的协议以及指向文档的链接以了解更多信息。

>[!NOTE]
>
>所有集成产品均可在30天或更短的时间内响应隐私请求。

| 应用程序 | 访问/删除 | 选择退出销售 | 删除行为 | 文档和其他注意事项 |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ “ ”标签 | ✓ | 数据主体的Cookie ID或设备ID以及与Cookie相关的所有成本、点击和收入数据都将从系统中删除。 | <ul><li>[访问/删除GDPR文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[访问/删除CCPA文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA的选择退出销售文档](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics 根据数据的敏感性和合同限制提供了数据标签设置工具。标签是执行以下操作的重要步骤：<ol><li>识别数据主体。</li><li>确定作为访问请求的一部分返回哪些数据。</li><li>确定必须在删除请求过程中删除的数据字段。</li></ol> | <ul><li>[隐私工作流程](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Analytics标签](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[Analytics选择退出](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | 与请求中包含的Audience Manager标识符关联的所有特征和区段都会被删除。 此外，个人的相应标识符被选择退出进一步的数据收集并且相应的ID映射被移除。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[选择退出文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | 从系统中删除数据主体的存储数据。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hans)</li><li>[选择退出文档](../segmentation/consents.md)</li></ul> |
| Adobe客户属性(CRS) | ✓ | 不适用 | 数据主体的属性将从系统中删除。 | <ul><li>[访问/删除GDPR文档](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[访问/删除CCPA文档](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>客户属性无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | 当Experience Platform收到来自Privacy Service的删除请求时，平台会向Privacy Service发送确认，确认已收到请求并且已将受影响的数据标记为删除。 隐私作业完成后，记录将从Data Lake或配置文件存储中删除。 在作业完成之前，数据会被软删除，因此任何Platform服务都无法访问。 | <ul><li>[访问/删除数据湖文档](../catalog/privacy.md)</li><li>[访问/删除Identity Service文档](../identity-service/privacy.md)</li><li>[访问/删除Real-time Customer Profile的文档](../profile/privacy.md)</li><li>[!DNL Experience Platform] 荣誉 [受众区段的选择退出请求](../segmentation/consents.md).</li></ul> |
| Adobe Primetime身份验证 | ✓ | 不适用 | 从系统中删除数据主体的存储数据。 | <ul><li>[访问/删除文档](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Adobe Target | ✓ | 不适用 | 与数据主体ID关联的所有数据都会从其访客配置文件中删除。 不识别个人或其他不相关的汇总或匿名数据（例如内容数据）不适用于删除请求。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 无法传输数据，因此选择退出销售请求不适用。</li></ul> |
| Marketo Engage | ✓ | 不适用 | 从系统中删除数据主体的存储数据。 | <ul><li>[访问/删除文档](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] 无法传输数据，因此选择退出销售请求不适用。</li></ul> |

{style="table-layout:auto"}

## 自助应用程序 {#self-serve}

以下是以下列表 [!DNL Experience Cloud] 未与集成的应用程序 [!DNL Privacy Service] 并且必须在内部管理其隐私问题。 提供了指向每个应用程序文档的链接，以及文档内容的描述。

| 应用程序 | 文档描述 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=zh-Hans) | Adobe Campaign Classic的GDPR功能概述。 |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 概述客户隐私管理员或AEM管理员如何处理GDPR请求。 |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | 使用Livefyre发出GDPR访问和删除请求的步骤。 |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | 确保您的Magento Commerce安装符合特定隐私法规的要求。 |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | 了解隐私法规如何应用于Marketo。 |
| [Adobe Experience Platform 中的标记](../tags/ui/client-side/consent.md) | 介绍开发人员如何使用扩展功能和规则生成器，来定义“选择加入”和“选择退出”解决方案。 |
| [Workfront](https://www.workfront.com/privacy-notice) | 了解Workfront如何收集个人数据，以及数据主体如何通过表单提交隐私请求。 |

{style="table-layout:auto"}
