---
keywords: 目标；adobe experience platform；平台；目标概述；激活数据；激活；
title: 目标概述
seo-title: 目标概述
description: 了解如何将Adobe Experience Platform数据激活到跨渠道营销活动、电子邮件、定向广告等目标。
seo-description: 目标是预建的与目标平台集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用Adobe Experience Platform中的目标来激活您已知和未知的跨渠道营销活动、电子邮件活动、定向广告和许多其他使用案例的数据。
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# [!DNL Destinations]概述{#overview}

![目标概述横幅](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是预建的与目标平台的集成，允许从Adobe Experience Platform无缝激活数据。您可以使用目标来激活已知和未知的跨渠道营销活动、电子邮件活动、定向广告和许多其他用例的数据。

## 目标和源{#destinations-and-sources}

平台的核心功能之一是获取第一方数据，并根据您的业务需要对其进行激活。 使用[sources](../sources/home.md)将数据引入平台和目标，以从平台导出数据。

## 目标步骤{#steps}

* 从[自助服务目录](./catalog/overview.md)中选择平台中所有可用目标。
* 使用目标[激活](./ui/activate-destinations.md)，并将用户档案或细分发送到营销自动化平台、数字广告平台等。
* 计划数据会定期导出到您的首选目标。

## 控件{#controls}

[目标工作区](./ui/destinations-workspace.md)中的控件允许您：

* 浏览可激活数据的目标平台目录；
* 创建、编辑、激活和禁用流向目录中目标的数据；
* 在存储位置创建帐户或将平台链接到目标平台中的帐户；
* 选择应将哪些区段激活到目标；
* 选择要在将区段激活到电子邮件营销目标时导出的[体验数据模型(XDM)字段](../xdm/home.md)。

## 目标类型和类别{#types-and-categories}

有关详细信息，请参阅[目标类型和类别概述](./destination-types.md)。

## 目标和访问控制{#access-controls}

平台中的目标功能与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以视图、管理和激活目标。 有关各个权限的信息，请参阅Adobe Experience Platform](../access-control/home.md)中的[访问控制，然后向下滚动到页面底部。

有关访问控制的详细信息，请参阅[访问控制用户指南](../access-control/ui/overview.md)。

## [!DNL Data Governance] 将数据激活到目标的限制  {#data-governance}

通过以下方式为平台目标实施数据管理：

* *您可* 以在创建目标工作流中选择的营销活动；
* *数据使用策* 略，可限制包含某些使用标签的数据不能被激活到具有某些营销操作的目标。

有关[营销操作](../data-governance/policies/overview.md)和[解决数据策略违规问题](../data-governance/enforcement/auto-enforcement.md)的详细信息，请参阅平台文档中的[!DNL Data Governance]。

有关在创建目标工作流中选择营销操作的详细信息，请参阅平台中不同目标类型的以下页面：

* [广告目的地 — Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [广告目的地 — Google Ads](./catalog/advertising/google-ads-destination.md)
* [广告目的地 — Google Display &amp; Video 360  ](./catalog/advertising/google-dv360.md)
* [云存储目标](./catalog/cloud-storage/workflow.md)
* [电子邮件营销目标](./catalog/email-marketing/overview.md)
* [社交网络目标](./catalog/social/workflow.md)

有关区段激活工作流中违反用户档案策略的详细信息，请参阅[将数据和区段激活到目标](./ui/activate-destinations.md#review)中的查看步骤。