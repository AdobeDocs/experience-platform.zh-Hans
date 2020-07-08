---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 10%

---


# Adobe Experience Platform Privacy Service概述

为了提供更好的客户体验，您需要收集和存储客户的个人数据。 使用这些数据时，了解和尊重客户的隐私非常重要。 新的法律和组织法规授予用户根据请求从数据存储中访问或删除其个人数据的权利。

Adobe Experience Platform Privacy Service提供RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 通过Privacy Service，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

## 为什么是Privacy Service?

Privacy Service是为应对企业管理其客户个人数据的方式的根本性转变而开发的。 Privacy Service的核心目的是自动遵守数据隐私规定，如果违反这些规定，可能会对您的业务造成重大罚款和中断数据操作。

### Privacy Service与GDPR

[](https://eugdpr.org/)《通用数据保护条例》(GDPR) 为欧盟成员国引入了几项新的数据隐私权，其中包括&#x200B;**访问权**&#x200B;和&#x200B;**被遗忘权**。这意味着被企业收集了个人数据的任何欧盟公民都可以随时请求访问或删除其数据。如果在30天内不遵守这些要求，您的组织将面临数百万美元的罚款。

Privacy Service支持访问和删除GDPR请求，并根据CCPA条例单独跟踪这些请求和请求。 有关更多 [信息，请参](gdpr/faq.md) 阅 [GDPR常](gdpr/terminology.md) 见问题解答和术语文档。

### Privacy Service和CCPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. CCPA为加州居民提供了新的数据隐私权，包括访问和删除其个人数据、了解其个人数据是否被出售或披露（以及向谁）的权利，以及将其数选择退出据出售给第三方的权利。

Privacy Service支持CCPA条例的访问和删除请求，并与GDPR请求分开跟踪这些请求。 Privacy Service还支持为支持Experience Cloud应用程序发送选择退出销售请求。 有关更多 [信息，请参](ccpa/faq.md) 阅CCPA常见问题解答。

## 如何使用Privacy Service管理隐私作业请求

Privacy Service提供RESTful API和用户界面，允许您管理客户访问／删除其私有数据或选择退出销售的请求(也称为隐 **私作业**)。 该服务还提供一个中央审计和记录机制，允许您视图涉及Experience Cloud应用程序的隐私作业的状态和结果。

>[!NOTE]
>
>选择退出请求当前仅受Privacy ServiceAPI支持。

### 使用API

Privacy Service [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) 允许您使用RESTful API调用创建和管理隐私工作，允许您以编程方式为Experience Cloud应用程序遵循隐私法规。 有关如何使用API的详细步骤，请参阅 [Privacy ServiceAPI开发人员指南](api/getting-started.md)。

### 使用UI

Privacy ServiceUI允许您使用图形界面创建和监视隐私作业。 UI包括状态 **报告构件** ，它提供所有活动请求状态的可视表示形式，并允许您通过使用内置的Request Builder或通过上传JSON文件创建 **新请求** 。 有关使用UI的详细信息，请参阅 [Privacy Service用户指南](ui/overview.md)。