---
title: (Beta)使用合作伙伴提供的属性补充第一方用户档案
description: 了解如何使用来自受信任数据合作伙伴的属性来补充第一方配置文件以改进数据基础、获得对客户群的新洞察以及更好的受众优化。
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 019ebe0c1cf11a7fb30dced1e10b511bab9b5100
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---

# 使用合作伙伴提供的属性补充第一方配置文件

>[!AVAILABILITY]
>
>* 此测试版功能适用于已获得许可的Real-Time CDP（应用程序服务）、Adobe Experience Platform Activation、Real-time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate的客户。 有关这些软件包的更多信息，请参阅 [产品描述](https://helpx.adobe.com/legal/product-descriptions.html) 有关更多信息，请与您的Adobe代表联系。

使用来自受信任数据合作伙伴的属性来补充第一方配置文件，以改进您的数据基础，获得有关您的客户群的新洞察信息并获得更好的受众优化。

![使用合作伙伴提供的属性丰富用户档案用例高级可视化概述。](/help/rtcdp/assets/partner-data/enrichment-use-case-overview.png)

## 先决条件和规划 {#prerequisites-and-planning}

在考虑使用数据合作伙伴的属性补充您自己的第一方配置文件时，您应该与数据合作伙伴讨论并解决有关数据扩充循环的以下详细信息：

* 考虑将受众列表从Real-Time CDP导出并与数据供应商共享的位置。 此位置需要支持文件导出。
* 数据供应商希望使用哪些标识符来栈叠其他属性？
* 如何将包含合作伙伴提供的属性的文件引入回Real-time CDP？ 例如，可以通过云存储源连接器(例如 [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) 或 [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* 您希望合作伙伴提供的属性以何种节奏返回到Real-Time CDP并进行刷新？

>[!WARNING]
>
>Real-Time CDP中摄取的其他合作伙伴提供的属性会影响 *平均配置文件丰富度*. 阅读 [Real-time Customer Data Platform产品描述](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 以了解有关配置文件丰富度的更多信息。

## 如何实现用例：高级概述 {#achieve-the-use-case-high-level}

![使用合作伙伴提供的属性丰富用户档案用例高级可视化概述。](/help/rtcdp/assets/partner-data/enrichment-use-case-steps.png)

1. As a **客户**，您可从以下位置许可属性 **数据合作伙伴**.
2. As a **客户**，您可以扩展配置文件数据和治理模型以适应 **合作伙伴**&#x200B;提供的属性。
3. As a **客户**，您载入了希望通过数据合作伙伴进行扩充的受众。 通常，这些受众会切断个人身份信息(PII)元素（如电子邮件、姓名、地址或其他内容）等输入标识符的键值。
4. 此 **合作伙伴** 为能够匹配的用户档案附加许可属性。 （可选）一个 [合作伙伴ID](/help/identity-service/namespaces.md) 可以包含并摄取到合作伙伴作用域ID命名空间中。
5. As a **客户**，即可将属性从data partner加载到Real-Time CDP中的客户配置文件中。

## 如何实现用例：分步说明 {#step-by-step-instructions}

请阅读以下部分（包括指向更多文档的链接），以完成上述高级概述中的每个步骤。

### 合作伙伴的许可证属性 {#license-attributes-from-partner}

此步骤在 [先决条件](#prerequisites-and-planning) 和Adobe假定您与受信任的数据供应商签订了适当的合同协议，以扩充您的第一方配置文件。

### 扩展您的配置文件数据和治理模型，以适应合作伙伴提供的属性。 {#extend-governance-model}

此时，您需要在Real-Time CDP中扩展数据管理框架，以适应合作伙伴提供的属性。

您可以选择为以下项创建新架构： **[!UICONTROL XDM个人资料]** 类，或扩展相同类型的现有架构以包含合作伙伴提供的属性。 Adobe强烈建议使用最能代表数据供应商的其他属性的新字段组集创建新架构。 这可确保您的数据架构是干净的，并且可以相互独立地演进。

要在架构中包含合作伙伴提供的属性，您可以使用所需的属性创建新字段组，也可以使用Adobe提供的预配置字段组之一。

有关详细信息，请阅读下面的文档页面：

* [模式组合的基础知识](/help/xdm/schema/composition.md)
* [概述 [!UICONTROL XDM个人资料] 类](/help/xdm/classes/individual-profile.md)
* [在UI中创建和编辑架构](/help/xdm/ui/resources/schemas.md)
* [在UI中创建和编辑架构字段组](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

此外，在此步骤中，请思考数据管理模型如何随着您扩展数据管理策略以包含合作伙伴提供的第三方数据而发生变化。 探索以下文档链接中的注意事项：

* (**即将推出**)将第三方数据保留在单独的数据集中，以便轻松删除和撤消集成。
* (**即将推出**)使用 [数据集过期](/help/hygiene/ui/dataset-expiration.md) 数据集上的功能，适用于购买了数据卫生加载项的客户。
* (**即将推出**)创建提取第三方数据的派生数据集时请务必谨慎，因为一旦混合在一起，删除第三方数据的唯一解决方案是删除整个派生数据集。

>[!TIP]
>
>如果您选择使用数据供应商提供的基于人员的标识符来补充客户配置文件，则可以创建该类型的新标识类型 **[[!UICONTROL 合作伙伴ID]](/help/identity-service/namespaces.md)**.
>
>有关合作伙伴ID的更多信息，请参阅 [身份类型部分](/help/identity-service/namespaces.md).
>阅读关于 [如何定义标识字段](/help/xdm/ui/fields/identity.md) 在Experience Platform用户界面中。

### 导出在输入个人可识别信息(PII)或经过哈希处理的PII后希望扩充的受众 {#export-audiences}

导出您希望合作伙伴扩充的受众。 使用Real-time CDP提供的云存储目标，如Amazon S3或SFTP。 请阅读以下文档页面以完成此步骤：

* [Amazon S3目标](/help/destinations/catalog/cloud-storage/amazon-s3.md) 文档页面
* [SFTP目标](/help/destinations/catalog/cloud-storage/sftp.md) 文档页面
* 操作方法 [连接到目标](/help/destinations/ui/connect-destination.md)
* 操作方法 [将数据导出到云存储目标](/help/destinations/ui/activate-batch-profile-destinations.md)

### 您的数据合作伙伴会为能够匹配的用户档案附加许可属性 {#partner-appends-attributes}

在此步骤中，您的数据合作伙伴会为导出的受众附加许可属性。 输出通常可作为平面文件使用，并可引入回Real-Time CDP中。 详细了解 [将文件摄取到Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP会将扩充的属性附加到客户个人资料中 {#ingest-data}

您现在需要通过源连接器从合作伙伴中摄取数据，以将扩充的数据恢复到Real-Time CDP中，并使用合作伙伴提供的数据补充您的用户档案。

为此，建议使用的一些源连接器可能包括：

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## 限制和疑难解答 {#limitations-and-troubleshooting}

在探索此页面上描述的用例时，请注意以下限制：

* 如果您选择使用合作伙伴ID，请注意，在构建您的 [身份图](/help/identity-service/ui/identity-graph-viewer.md).

## 通过合作伙伴数据支持实现的其他用例 {#other-use-cases}

探索通过Real-Time CDP中的合作伙伴数据支持启用的更多用例：

* (**即将推出**) [!BADGE 测试版]{type=Informative}**利用合作伙伴提供的认可度** 用于在访问期间个性化现场体验，以及在访问后进行非现场重新定位，而无需用户进行身份验证或者没有品牌历史。
* (**即将推出**) [!BADGE 测试版]{type=Informative}**扩展的激活** 使用合作伙伴ID发布不接受PII或哈希处理PII的生态系统。