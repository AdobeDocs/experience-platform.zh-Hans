---
title: (Beta) 使用合作伙伴提供的属性补充第一方配置文件
description: 了解如何使用可信赖的数据合作伙伴的属性来补充第一方配置文件，以改善您的数据基础，获得对客户群的全新见解，并提升受众优化。
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 019ebe0c1cf11a7fb30dced1e10b511bab9b5100
workflow-type: ht
source-wordcount: '1082'
ht-degree: 100%

---

# 使用合作伙伴提供的属性补充第一方配置文件

>[!AVAILABILITY]
>
>* 此 Beta 功能可供已获得 Real-Time CDP（应用程序服务）、Adobe Experience Platform 激活、Real-time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate 许可的客户使用。阅读[产品说明](https://helpx.adobe.com/legal/product-descriptions.html)中关于这些软件包的详细信息，并联系您的 Adobe 代表了解更多信息。

使用可信赖的数据合作伙伴的属性来补充第一方配置文件，以改善您的数据基础，获得对客户群的全新见解，并提升受众优化。

![利用合作伙伴提供的属性扩充配置文件用例高级视觉概述。](/help/rtcdp/assets/partner-data/enrichment-use-case-overview.png)

## 先决条件和规划 {#prerequisites-and-planning}

当您考虑使用数据合作伙伴的属性来补充您自己的第一方配置文件时，您应该与数据合作伙伴讨论并解决有关数据扩充循环的以下详细信息：

* 考虑要从 Real-Time CDP 中导出受众列表的位置，以便与数据供应商共享该信息。该位置需要支持文件导出。
* 数据供应商希望您提供哪些标识符，以便分层附加属性？
* 包含合作伙伴提供的属性的文件会如何被引入 Real-time CDP 中？例如，可以通过云存储源连接器引入文件，例如 [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) 或 [SFTP](/help/sources/connectors/cloud-storage/sftp.md)。
* 您希望合作伙伴提供的属性返回 Real-Time CDP 并进行刷新的节奏是什么？

>[!WARNING]
>
>Real-Time CDP 中包含的其他由合作伙伴提供的属性会影响您的&#x200B;*平均配置文件丰富程度*。有关配置文件丰富程度的更多信息，请阅读[ Real-Time Customer Data Platform 产品说明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)。

## 如何实现该用例：高级概述 {#achieve-the-use-case-high-level}

![利用合作伙伴提供的属性扩充配置文件用例高级视觉概述。](/help/rtcdp/assets/partner-data/enrichment-use-case-steps.png)

1. 作为&#x200B;**客户**，您许可&#x200B;**数据合作伙伴**&#x200B;的属性。
2. 作为&#x200B;**客户**，您可以扩展您的配置文件数据和治理模型，以适应&#x200B;**合作伙伴**&#x200B;提供的属性。
3. 作为&#x200B;**客户**，您加入希望通过数据合作伙伴扩充的受众。一般来说，这些受众去除了输入标识符，例如电子邮件、姓名、地址或其他个人身份信息 (PII) 元素。
4. **合作伙伴**&#x200B;为他们能够匹配的配置文件附加许可属性。可以选择将[合作伙伴 ID ](/help/identity-service/namespaces.md)包含在合作伙伴范围的 ID 命名空间中。
5. 作为&#x200B;**客户**，您可以在 Real-Time CDP 中将数据合作伙伴的属性加载到客户配置文件中。

## 如何实现用例：分步说明 {#step-by-step-instructions}

通读以下部分（其中包括指向更多文档的链接），以完成上面高级概述中的每个步骤。

### 合作伙伴的许可属性 {#license-attributes-from-partner}

这一步骤包含在[先决条件](#prerequisites-and-planning)中，Adobe 假设您与可信赖的数据供应商签订了恰当的合同协议，以增强您的第一方配置文件。

### 扩展您的配置文件数据和治理模型，以适应合作伙伴提供的属性。 {#extend-governance-model}

目前，您正在扩展 Real-Time CDP 中的数据管理框架，以适应合作伙伴提供的属性。

您可以选择创建&#x200B;**[!UICONTROL XDM 单个配置文件]**&#x200B;类的新架构，或者扩展相同类型的现有架构，以包括合作伙伴提供的属性。Adobe 强烈建议使用一组新的字段组创建新架构，这些字段组最能代表数据供应商的附加属性。这可以确保您的数据架构是干净的，并且可以相互独立地发展。

要在架构中包含合作伙伴提供的属性，您可以使用所需的属性创建新字段组，也可以使用 Adobe 提供的预配置字段组之一。

有关更多信息，请阅读以下的文档页面：

* [架构组成基础](/help/xdm/schema/composition.md)
* [对 [!UICONTROL XDM 单个配置文件]类的概述](/help/xdm/classes/individual-profile.md)
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
>如果您选择使用数据供应商提供的基于个人的标识符来补充您的客户配置文件，您可以创建类型为&#x200B;**[[!UICONTROL 合作伙伴 ID]](/help/identity-service/namespaces.md)** 的新身份类型。
>
>阅读[身份类型部分](/help/identity-service/namespaces.md)，了解有关合作伙伴 ID 的更多信息。
>阅读 Experience Platform 用户界面中有关[如何定义身份字段](/help/xdm/ui/fields/identity.md)的内容。

### 在除去个人身份信息 (PII) 或哈希 PII 时导出您想要扩充的受众 {#export-audiences}

导出您希望合作伙伴进行扩充的受众。使用 Real-time CDP 提供的云存储目标，例如 Amazon S3 或 SFTP。阅读以下文档页面以完成此步骤：

* [Amazon S3 目标](/help/destinations/catalog/cloud-storage/amazon-s3.md)文档页面
* [SFTP 目标](/help/destinations/catalog/cloud-storage/sftp.md)文档页面
* 如何[连接目标](/help/destinations/ui/connect-destination.md)
* 如何[将数据导出到云存储目标](/help/destinations/ui/activate-batch-profile-destinations.md)

### 您的数据合作伙伴为他们能够匹配的配置文件附加许可属性 {#partner-appends-attributes}

在此步骤中，您的数据合作伙伴会为导出的受众附加许可属性。输出通常以平面文件形式提供，并且可以重新将其引入 Real-Time CDP。阅读更多关于[将文件引入 Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file) 中的信息。

### Real-Time CDP 将扩充的属性附加到客户配置文件中 {#ingest-data}

现在，您需要通过源连接器从合作伙伴那里引入数据，将扩充的数据带回到 Real-Time CDP 中，并使用合作伙伴提供的数据补充您的配置文件。

为此，建议使用以下源连接器：

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## 限制和故障排除 {#limitations-and-troubleshooting}

在探索本页中描述的用例时，请注意以下限制：

* 如果您选择使用合作伙伴 ID，请注意在构建您的[身份图](/help/identity-service/ui/identity-graph-viewer.md)时不会使用这些 ID。

## 由合作伙伴数据支持实现的其他用例 {#other-use-cases}

探索通过 Real-Time CDP 中的合作伙伴数据支持实现的更多用例：

* （**即将推出**）[!BADGE Beta]{type=Informative}**利用合作伙伴辅助的认可**&#x200B;在访问期间提供个性化现场体验，以及在访问后异地重新定位，而无需用户进行身份验证或之前使用过您的品牌。
* （**即将推出**）[!BADGE Beta]{type=Informative}**扩大激活**&#x200B;使用合作伙伴 ID 发布不接受 PII 或哈希 PII 的生态系统。