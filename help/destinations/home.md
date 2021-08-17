---
keywords: 目标；adobe experience platform；平台；目标概述；激活数据；激活
title: 目标概述
seo-title: 目标概述
description: 了解如何将Adobe Experience Platform数据激活到跨渠道营销活动、电子邮件、定向广告等的目标。
seo-description: 目标是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用Adobe Experience Platform中的目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: f73598224d527535aaf9ecb2aa1c26786cae2d82
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 1%

---

# [!DNL Destinations] 概述 {#overview}

![目标概述横幅](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]** 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

## 目标和来源 {#destinations-and-sources}

Platform的核心功能之一是摄取第一方数据并根据业务需求对其进行激活。 使用[sources](../sources/home.md)将数据摄取到平台和目标以从平台导出数据。

## 目标步骤 {#steps}

* 从[自助服务目录](./catalog/overview.md)中选择平台中所有可用目标。
* 使用目标[activate](./ui/activate-destinations.md)并将用户档案或区段发送到营销自动化平台、数字广告平台等。
* 计划定期向首选目标导出数据。

## 控件 {#controls}

[目标工作区](./ui/destinations-workspace.md)中的控件允许您：

* 浏览可激活数据的目标平台目录；
* 创建、编辑、激活和禁用数据流到目录中目标的数据流；
* 在存储位置创建帐户或将平台链接到目标平台中的帐户；
* 选择应激活到目标的区段；
* 选择在将区段激活到电子邮件营销目标时要导出的[体验数据模型(XDM)字段](../xdm/home.md)。

## 目标类型和类别 {#types-and-categories}

有关详细信息，请参阅[目标类型和类别概述](./destination-types.md)。

## 目标和访问控制 {#access-controls}

Platform中的目标功能可与Adobe Experience Platform访问控制权限配合使用。 根据用户的权限级别，您可以查看、管理和激活目标。 有关各个权限的信息，请参阅Adobe Experience Platform](../access-control/home.md)中的[访问控制，然后向下滚动到页面底部。

有关访问控制的更多信息，请参阅[访问控制用户指南](../access-control/ui/overview.md)。

## [!DNL Data Governance] 将数据激活到目标的限制 {#data-governance}

通过以下方式为Platform目标强制实施数据管理：

* *营销* 活动，您可以在创建目标工作流中选择这些活动；
* *数据使* 用策略，将包含某些使用标签的数据限制为通过特定营销操作激活到目标。

有关[营销操作](../data-governance/policies/overview.md)和[解决数据策略违规](../data-governance/enforcement/auto-enforcement.md)的详细信息，请参阅Platform文档中的[!DNL Data Governance]。

有关在创建目标工作流中选择营销操作的更多信息，请参阅Platform中不同目标类型的以下页面：

* [广告目标 — Google Ad Manager ](./catalog/advertising/google-ad-manager.md)
* [广告目标 — Google Ads](./catalog/advertising/google-ads-destination.md)
* [广告目标 — Google Display &amp; Video 360 ](./catalog/advertising/google-dv360.md)
* [云存储目标](./catalog/cloud-storage/overview.md)
* [电子邮件营销目标](./catalog/email-marketing/overview.md)
* [社交目标](./catalog/social/overview.md)

有关区段激活工作流中违反数据策略的详细信息，请参阅[激活用户档案和区段到目标](./ui/activate-destinations.md#review)中的查看步骤。
