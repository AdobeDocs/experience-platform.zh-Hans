---
title: 使用合作伙伴提供的属性补充第一方轮廓
description: 了解如何使用可信赖的数据合作伙伴的属性来补充第一方轮廓，以改善您的数据基础，获得对客户群的全新洞察，并提升受众优化。
feature: Use Cases, Profile Enrichment
exl-id: ee21b988-88f9-4c8e-bd82-7fc55c37ec24
source-git-commit: 7ee472294e8f255d9de3c15982a6f5d2d3654755
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 73%

---

# 使用合作伙伴提供的属性补充第一方轮廓

>[!AVAILABILITY]
>
>* 已获得许可Real-Time CDP（应用程序服务）、Adobe Experience Platform Activation、Real-Time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate的客户可以使用此功能。 阅读[产品说明](https://helpx.adobe.com/cn/legal/product-descriptions.html)中关于这些软件包的详细信息，并联系您的 Adobe 代表了解更多信息。

使用可信赖的数据合作伙伴的属性来补充第一方轮廓，以改善您的数据基础，获得对客户群的全新洞察，并提升受众优化。

![利用合作伙伴提供的属性扩充轮廓用例高级视觉概述。](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## 为什么考虑此用例 {#why-this-use-case}

大多数品牌（甚至那些拥有第一方数据的品牌）都可从简化数据以及更细致地了解客户、其行为、模式和偏好中受益。

Adobe Real-time Customer Data Platform可以帮助品牌商通过来自一个或多个可信合作伙伴的重要见解、标识符和属性，负责任地补充其第一方数据。

Adobe知道没有一种放之四海而皆准的方法，它允许与数据和身份合作伙伴进行无缝的互操作性，从而在客户生命周期的各个阶段促进个性化、深思熟虑的互动。 这些功能由受信任的数据治理框架提供支持，允许对使用合作伙伴数据的位置和方式进行细微控制。 例如，您可能希望使用合作伙伴提供的分析进行分段，而不是进行个性化。

例如，当您需要使用人口统计和意图信号扩充客户记录时，请按照此用例中描述的步骤操作。

## 先决条件和规划

当您考虑使用数据合作伙伴的属性来补充您自己的第一方轮廓时，您应该与数据合作伙伴讨论并解决有关数据扩充循环的以下详细信息：

* 考虑要从 Real-Time CDP 中导出受众列表的位置，以便与数据供应商共享该信息。该位置需要支持文件导出。
* 数据供应商希望您提供哪些标识符，以便分层附加属性？
* 如何将包含合作伙伴提供的属性的文件引入回Real-Time CDP？ 例如，可以通过云存储源连接器引入文件，例如 [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) 或 [SFTP](/help/sources/connectors/cloud-storage/sftp.md)。
* 您希望合作伙伴提供的属性返回 Real-Time CDP 并进行刷新的节奏是什么？

>[!WARNING]
>
>摄取到Real-Time CDP中的其他合作伙伴提供的属性会影响您的&#x200B;*总数据量*。 阅读[Real-Time Customer Data Platform产品说明](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform.html)以了解有关总数据量的详细信息。

## 视频演练 {#video-walkthrough}

查看下面的视频教程，了解如何使用合作伙伴提供的属性来补充第一方受众：

>[!VIDEO](https://video.tv.adobe.com/v/3452471/?captions=chi_hans&learn=on)

## 如何实现该用例：大致概述 {#achieve-the-use-case-high-level}

![利用合作伙伴提供的属性扩充轮廓用例高级视觉概述。](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. 作为&#x200B;**客户**，您许可&#x200B;**数据合作伙伴**&#x200B;的属性。
2. 作为&#x200B;**客户**，您可以扩展您的轮廓数据和治理模型，以适应&#x200B;**合作伙伴**&#x200B;提供的属性。
3. 作为&#x200B;**客户**，您加入希望通过数据合作伙伴扩充的受众。一般来说，这些受众去除了输入标识符，例如电子邮件、姓名、地址或其他个人身份信息 (PII) 元素。
4. **合作伙伴**&#x200B;为他们能够匹配的轮廓附加许可属性。可以选择将[合作伙伴 ID &#x200B;](/help/identity-service/features/namespaces.md)包含在合作伙伴范围的 ID 命名空间中。
5. 作为&#x200B;**客户**，您可以在 Real-Time CDP 中将数据合作伙伴的属性加载到客户轮廓中。

## 如何实现用例：分步说明 {#step-by-step-instructions}

通读以下部分（其中包括指向更多文档的链接）以完成上方大致概述中的每个步骤。

### 合作伙伴的许可属性 {#license-attributes-from-partner}

这一步骤包含在[先决条件](#prerequisites-and-planning)中，Adobe 假设您与可信赖的数据供应商签订了恰当的合同协议，以增强您的第一方轮廓。

### 扩展您的轮廓数据和治理模型，以适应合作伙伴提供的属性。 {#extend-governance-model}

目前，您正在扩展 Real-Time CDP 中的数据管理框架，以适应合作伙伴提供的属性。

您可以选择创建&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;类的新架构，或者扩展相同类型的现有架构以包含合作伙伴提供的属性。 Adobe 强烈建议使用一组新的字段组创建新架构，这些字段组最能代表数据供应商的附加属性。这可以确保您的数据架构是干净的，并且可以相互独立地发展。

要在架构中包含合作伙伴提供的属性，您可以使用所需的属性创建新字段组，也可以使用 Adobe 提供的预配置字段组之一。

有关更多信息，请阅读以下的文档页面：

* [架构构成基础](/help/xdm/schema/composition.md)
* [[!UICONTROL XDM Individual Profile]类概述](/help/xdm/classes/individual-profile.md)
* [在 UI 中创建和编辑架构](/help/xdm/ui/resources/schemas.md)
* [在 UI 中创建和编辑架构字段组](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

此外，在此步骤中，请考虑当您通过扩展数据管理策略来加入合作伙伴提供的第三方数据时，您的数据治理模型会如何变化。探索以下文档链接中的注意事项：

* （**即将推出**）将第三方数据保存在单独的数据集中，以便轻松地删除它并撤消集成。
* (**即将推出**）购买数据卫生附加组件的客户可在数据集上使用[数据集过期](/help/hygiene/ui/dataset-expiration.md)功能。
* （**即将推出**）创建引入第三方数据的派生数据集时请务必小心，因为一旦混合在一起，删除第三方数据的唯一解决方案是删除整个派生数据集。

>[!TIP]
>
>如果您选择使用数据供应商提供的基于人员的标识符补充您的客户配置文件，则可以创建类型为&#x200B;**[[!UICONTROL Partner ID]](/help/identity-service/features/namespaces.md)**&#x200B;的新标识类型。
>
>阅读[身份标识类型部分](/help/identity-service/features/namespaces.md)，了解有关合作伙伴 ID 的更多信息。
>阅读 Experience Platform 用户界面中有关[如何定义身份标识字段](/help/xdm/ui/fields/identity.md)的内容。

### 在除去个人身份信息 (PII) 或哈希 PII 时导出您想要扩充的受众 {#export-audiences}

导出您希望合作伙伴进行扩充的受众。使用Real-Time CDP提供的云存储目标，如Amazon S3或SFTP。 阅读以下文档页面以完成此步骤：

* [Amazon S3 目标](/help/destinations/catalog/cloud-storage/amazon-s3.md)文档页面
* [SFTP 目标](/help/destinations/catalog/cloud-storage/sftp.md)文档页面
* 如何[连接目标](/help/destinations/ui/connect-destination.md)
* 如何[将数据导出到云存储目标](/help/destinations/ui/activate-batch-profile-destinations.md)

### 您的数据合作伙伴为他们能够匹配的轮廓附加许可属性 {#partner-appends-attributes}

在此步骤中，您的数据合作伙伴会为导出的受众附加许可属性。输出通常以平面文件形式提供，并且可以重新将其引入 Real-Time CDP。阅读更多关于[将文件引入 Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file) 中的信息。

### Real-Time CDP 将扩充的属性附加到客户轮廓中 {#ingest-data}

现在，您需要通过源连接器从合作伙伴那里引入数据，将扩充的数据带回到 Real-Time CDP 中，并使用合作伙伴提供的数据补充您的轮廓。

为此，建议使用以下源连接器：

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## 限制和故障排除 {#limitations-and-troubleshooting}

在探索本页中描述的用例时，请注意以下限制：

* 如果您选择使用合作伙伴 ID，请注意在构建您的[身份标识图](/help/identity-service/features/identity-graph-viewer.md)时不会使用这些 ID。

## 由合作伙伴数据支持实现的其他用例 {#other-use-cases}

探索通过 Real-Time CDP 中的合作伙伴数据支持实现的更多用例：

* 使用 Real-Time CDP 中的第三方数据支持，[通过数据合作伙伴提供的潜在客户轮廓扩充您的轮廓基础并与其交流以获取或接触新客户](/help/rtcdp/partner-data/prospecting.md)。
* [在访问期间使用合作伙伴帮助的访客识别](/help/rtcdp/partner-data/onsite-personalization.md)为未知访客提供个性化现场体验，用户无需进行身份验证或没有您的品牌历史记录。
* [扩大了潜在客户轮廓和潜在客户受众的激活范围](/help/destinations/ui/activate-prospect-audiences.md)，以选择目标。
