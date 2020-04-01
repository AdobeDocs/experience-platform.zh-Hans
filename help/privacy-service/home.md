---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform隐私服务
topic: overview
translation-type: tm+mt
source-git-commit: 66fef5b98d2c21d1ac8b272e2c8557d26daa3364

---


# Adobe Experience Platform隐私服务概述

为了提供更好的客户体验，您需要收集和存储客户的个人数据。 使用这些数据时，了解和尊重客户的隐私非常重要。 新的法律和组织法规授予用户根据请求从数据存储中访问或删除其个人数据的权利。

Adobe Experience Platform Privacy Service提供RESTful API和用户界面，帮助您管理来自客户的这些数据请求。 通过隐私服务，您可以提交从Adobe Experience Cloud应用程序访问和删除私人或个人客户数据的请求，从而促进自动遵守法律和组织隐私法规。

## 为什么选择隐私服务？

隐私服务是为了应对企业管理客户个人数据方式的根本转变而开发的。 隐私服务的核心目的是自动遵守数据隐私权规定，如果违反这些规定，可能会对您的业务造成重大罚款和中断数据操作。

### 隐私服务和GDPR

一般 [数据保护规定](https://eugdpr.org/) (GDPR)为欧洲合并成员引入了若干新的数据隐私权，包括访问权和被遗 **忘权******。 这意味着，您的企业已收集个人数据的任何欧盟公民均可请求随时访问或删除其数据。 如果在30天内不遵守这些要求，您的组织将面临数百万美元的罚款。

隐私服务支持访问和删除GDPR请求，并根据CCPA规定单独跟踪这些请求和请求。 有关更多 [信息，请参阅GDPR常见问题](gdpr/faq.md)[解答](gdpr/terminology.md) 和术语文档。

### 隐私服务和CCPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. CCPA为加利福尼亚州居民提供了新的数据隐私权，包括访问和删除其个人数据、了解其个人数据是出售还是披露（以及向谁）的权利，以及将其数据出售给第选择退出三方的权利。

隐私服务支持访问和删除CCPA规定的请求，并单独跟踪它们与GDPR请求。 隐私服务还支持发送针对支持Experience Cloud应用程序的选择退出请求。 有关更多信 [息，请参阅CCPA常见问题](ccpa/faq.md) 。

## 如何使用隐私服务管理隐私作业请求

隐私服务提供RESTful API和用户界面，允许您管理客户访问／删除其私有数据或选择退出销售的请求(也称为隐 **私作业**)。 该服务还提供了集中审核和记录机制，允许您视图涉及Experience Cloud应用程序的隐私作业的状态和结果。

>[!NOTE] 选择退出请求当前仅受Privacy Service API支持。

### 使用API

隐私 [服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) 允许您使用RESTful API调用创建和管理隐私工作，从而使您能够有计划地为Experience Cloud应用程序遵循隐私法规。 有关如何使用API的详细步骤，请参阅 [Privacy Service API开发人员指南](api/getting-started.md)。

### 使用UI

隐私服务UI允许您使用图形界面创建和监视隐私作业。 UI包括一个状 **态报告构件** ，它提供所有活动请求状态的可视表示形式，并允许您通过使用内置的 **Request Builder** 或通过上传JSON文件创建新请求。 有关使用UI的详细信息，请参阅隐 [私服务用户指南](ui/overview.md)。