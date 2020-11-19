---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;destinations;destination;rtcdp
title: 目标概述
seo-title: 目标概述
description: 将平台数据激活到跨渠道营销活动、电子邮件、定向广告等的目标。
seo-description: 目标是预建的与目标平台集成，允许从实时客户数据平台无缝激活数据。 您可以在实时客户数据平台中使用目标来激活已知和未知的跨渠道营销活动、电子邮件活动、定向广告和许多其他用例数据。
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 3%

---


# [!DNL Destinations]概述{#overview}

![目标概述横幅](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**[!DNL Destinations]** 是预建的与目标平台的集成，允许从实时客户数据平台无缝激活数据。 您可以使用目标来激活已知和未知的跨渠道营销活动、电子邮件活动、定向广告和许多其他用例数据。

## 目标和来源 {#destinations-and-sources}

实时CDP的一个核心功能是接收第一方数据并根据业务需求激活它。 使用源将数据引入实时CDP中，并使用目标从实时CDP中导出数据。

## 目标步骤 {#steps}

* 从实时 [CDP中提供](/help/rtcdp/destinations/destinations-catalog.md) 的所有目标的自助服务目录中进行选择。
* 使 **[!UICONTROL 用目]** 的地 [激活用户档案](/help/rtcdp/destinations/activate-destinations.md) 或细分，并将其发送到营销自动化平台、数字广告平台等。
* 计划定期导出到首选目标。

## 控件 {#controls}

“目标”工作区 [中的控件](/help/rtcdp/destinations/destinations-workspace.md) ，允许您：

* 浏览可激活数据的目标平台目录；
* 创建、编辑、激活和禁用数据流至目录中的目标；
* 在存储位置创建帐户或将实时CDP链接到目标平台中的帐户；
* 选择应将哪些区段激活到目标；
* 在将区段 [激活到电子邮件营销目标时](../../xdm/home.md) ，选择要导出的体验数据模型(XDM)字段。

## Destination types and categories {#types-and-categories}

有关详细信息，请参 [阅目标类型和类别概述](/help/rtcdp/destinations/destination-types.md)。

## 目标和访问控制 {#access-controls}

实时CDP中的目标功能与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以视图、管理和激活目标。 有关各个权限的信息，请参 [阅Adobe Experience Platform的访问控制](../../access-control/home.md) ，然后向下滚动到页面底部。

有关访问控制的详细信息，请参阅 [访问控制用户指南](../../access-control/ui/overview.md)。

## [!DNL Data Governance] 将数据激活到目标的限制 {#data-governance}

通过以下方式为实时CDP目标实施数据管理：

* *您可以在创建* 、目标工作流中选择的营销用例；
* *数据使用策略* ，该策略限制包含某些使用标签的数据被激活到具有某些市场营销用例的目标。

有关营销 [!DNL Data Governance] 用例和解决违反数据策略的情况的更 [多信息](/help/rtcdp/privacy/data-governance-overview.md#destinations) ，请 [参见实时CDP文档](/help/rtcdp/privacy/data-governance-overview.md#enforcement)。

有关在创建目标工作流中选择营销用例的详细信息，请参阅实时CDP中不同目标类型的以下页面：

* [广告目标-Google Ad Manager ](/help/rtcdp/destinations/google-ad-manager-destination.md)
* [广告目的地- Google广告](/help/rtcdp/destinations/google-ads-destination.md)
* [广告目标- Google Display &amp; Video 360 ](/help/rtcdp/destinations/google-dv360-destination.md)
* [云存储目标](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)
* [电子邮件营销目标](/help/rtcdp/destinations/email-marketing-destinations.md)
* [社交网络目标](/help/rtcdp/destinations/social-network-destinations-workflow.md)

有关区段激活工作流中违反数据策略的详细信息，请参阅将和区段 [激活到目标用户档案中的审核步骤](/help/rtcdp/destinations/activate-destinations.md#review)。