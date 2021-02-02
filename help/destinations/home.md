---
keywords: 目标；adobe experience platform；平台；目标概述；激活数据；激活；
title: 目标概述
seo-title: 目标概述
description: 将平台数据激活到跨渠道营销活动、电子邮件、定向广告等的目标。
seo-description: 目标是预建的与目标平台集成，实现来自Adobe Experience Platform的无缝激活。 您可以使用Adobe Experience Platform的目标来激活您已知和未知的跨渠道营销活动、电子邮件活动、定向广告和许多其他使用案例的数据。
translation-type: tm+mt
source-git-commit: 32eae2ed782e46941bb21e3aca62c6bce68cde1e
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 3%

---


# [!DNL Destinations]概述{#overview}

![目标概述横幅](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是预建的与目标平台的集成，允许从Adobe Experience Platform无缝激活数据。您可以使用目标来激活已知和未知的跨渠道营销活动、电子邮件活动、定向广告和许多其他用例数据。

## 目标和源{#destinations-and-sources}

平台的一个核心功能是接收第一方数据并根据业务需求激活它。 使用源将数据引入平台和目标，以从平台导出数据。

## 目标步骤{#steps}

* 从[自助服务目录](./catalog/overview.md)中选择平台中可用的所有目标。
* 使用&#x200B;**[!UICONTROL 目标]**[activate](./ui/activate-destinations.md)将用户档案或细分发送到营销自动化平台、数字广告平台等。
* 计划定期导出到首选目标。

## 控件{#controls}

[目标工作区](./ui/destinations-workspace.md)中的控件允许您：

* 浏览可激活数据的目标平台目录；
* 创建、编辑、激活和禁用数据流至目录中的目标；
* 在存储位置创建帐户或将平台链接到目标平台中的帐户；
* 选择应将哪些区段激活到目标；
* 选择在将区段激活到电子邮件营销目标时要导出的[体验数据模型(XDM)字段](../xdm/home.md)。

## 目标类型和类别{#types-and-categories}

有关详细信息，请参阅[目标类型和类别概述](./destination-types.md)。

## 目标和访问控制{#access-controls}

平台中的目标功能与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以视图、管理和激活目标。 有关各个权限的信息，请参阅Adobe Experience Platform的[访问控制](../access-control/home.md)并向下滚动到页面底部。

有关访问控制的详细信息，请参阅[访问控制用户指南](../access-control/ui/overview.md)。

## [!DNL Data Governance] 将数据激活到目标的限制  {#data-governance}

通过以下方式为平台目标实施数据管理：

* *营销使* 用您可以在创建目标工作流中选择的案例；
* *数据使用策* 略，其限制包含某些使用标签的数据被激活到具有某些市场营销用例的目标。

有关[市场营销用例](../data-governance/policies/overview.md)和[解决数据策略违规问题的详细信息，请参阅平台文档中的[!DNL Data Governance]。](../data-governance/enforcement/auto-enforcement.md)

有关在创建目标工作流中选择市场营销用例的详细信息，请参阅平台中不同目标类型的以下页面：

* [广告目标-Google Ad Manager  ](./catalog/advertising/google-ad-manager.md)
* [广告目的地- Google广告](./catalog/advertising/google-ads-destination.md)
* [广告目标- Google Display &amp; Video 360  ](./catalog/advertising/google-dv360.md)
* [云存储目标](./catalog/cloud-storage/workflow.md)
* [电子邮件营销目标](./catalog/email-marketing/overview.md)
* [社交网络目标](./catalog/social/workflow.md)

有关区段激活工作流中违反数据策略的详细信息，请参阅[将用户档案和区段激活到目标](./ui/activate-destinations.md#review)中的检查步骤。