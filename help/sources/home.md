---
keywords: Experience Platform；主页；热门主题；源连接器；源连接器；源；数据源；数据源；数据源连接
solution: Experience Platform
title: Source连接器概述
description: Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 9bc7d372eba9ffcfe64f90d2d58a532411e5f1ce
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 3%

---

# Source连接器概述

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源中摄取数据，如 Adobe 应用程序、基于云的存储、数据库和许多其他源。

[!DNL Flow Service]用于收集和集中Experience Platform中各种不同来源的客户数据。 该服务提供了一个用户界面和RESTful API，可让您轻松设置到各种数据提供商的源连接。 通过这些源连接，您可以验证第三方系统、设置摄取运行的时间，以及管理数据摄取吞吐量。

借助Experience Platform，您可以集中从不同来源收集的数据，并利用从中获得的见解做更多工作。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 高级企业源 {#advanced-enterprise-sources}

以下源仅供[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)客户使用。

- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md) [!BADGE 正在流式传输]{type=Positive}
- [[!DNL Amazon Redshift]](connectors/databases/redshift.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md) [!BADGE 正在流式传输]{type=Positive}
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md) [!BADGE 批次]{type=Informative}
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md) [!BADGE 批次]{type=Informative}
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md) [!BADGE 正在流式传输]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake-streaming.md) [!BADGE 正在流式传输]{type=Positive}
- [[!DNL Snowflake]](connectors/databases/snowflake.md) [!BADGE 批次]{type=Informative}

## Adobe构建和合作伙伴构建的源 {#adobe-and-partner-built-sources}

Experience Platform源目录中的某些连接器是由Adobe构建和维护的，而其他连接器是由合作伙伴公司使用[源SDK](/help/sources/sources-sdk/overview.md)构建和维护的。 如果合作伙伴创建并维护了源，则每个合作伙伴构建的连接器在文档页面顶部的注释会标出。 例如，[Amazon S3连接器](/help/sources/connectors/cloud-storage/s3.md)由Adobe创建，而[RainFocus连接器](/help/sources/connectors/analytics/rainfocus.md)由RainFocus团队创建和维护。

对于合作伙伴创作并维护的连接器，这意味着连接器问题可能需要由合作伙伴团队解决（文档页面注释中提供的联系方法）。 有关Adobe创作和维护的连接器出现的问题，请联系您的Adobe代表或客户关怀。

## 源类别

Experience Platform中的源分为以下类别：

### Adobe 应用程序 {#adobe-applications}

Experience Platform允许从其他Adobe应用程序(包括Adobe Analytics和Adobe Audience Manager)中摄取数据。 有关更多信息，请参阅以下相关文档：

- [Adobe Audience Manager源概述](connectors/adobe-applications/audience-manager.md)
   - [在UI中创建Adobe Audience Manager源连接](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分类数据源概述](connectors/adobe-applications/classifications.md)
   - [在UI中创建Adobe Analytics分类数据源连接](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics报表包数据源概述](connectors/adobe-applications/analytics.md)
   - [在UI中创建Adobe Analytics源连接](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe Campaign Managed Cloud Services源概述](connectors/adobe-applications/campaign.md)
   - [在UI中创建Adobe Campaign Managed Cloud Services源连接](./tutorials/ui/create/adobe-applications/campaign.md)
- [Adobe Commerce源概述](connectors/adobe-applications/commerce.md)
- [Adobe数据收集源概述](connectors/adobe-applications/data-collection.md)
   - [在UI中创建客户属性源连接](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage]源概述](connectors/adobe-applications/marketo/marketo.md)
   - [在UI中创建 [!DNL Marketo Engage] 源连接](./tutorials/ui/create/adobe-applications/marketo.md)
   - [为自定义活动数据创建 [!DNL Marketo Engage] 源连接和数据流](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)

### Advertising {#advertising}

Experience Platform支持从第三方广告系统中提取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [Google广告](connectors/advertising/ads.md) [!BADGE 批次]{type=Informative}

### Analytics {#analytics}

Experience Platform支持从第三方Analytics平台引入数据。 有关详细信息，请阅读以下相关文档：

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md) [!BADGE 批次]{type=Informative}
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md) [!BADGE 正在流式传输]{type=Positive}
- [[!DNL RainFocus]](connectors/analytics/rainfocus.md) [!BADGE 正在流式传输]{type=Positive}

### 云存储 {#cloud-storage}

云存储源可以将您自己的数据导入Experience Platform，而无需下载、设置格式或上传。 引入的数据可以格式化为XDM JSON、XDM Parquet或分隔。 该过程的每个步骤都使用用户界面集成到源工作流中。 有关更多信息，请参阅以下相关文档：

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md) [!BADGE 批次]{type=Informative}
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md) [!BADGE 批次]{type=Informative}
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md) [!BADGE 批次]{type=Informative}
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md) [!BADGE 批次]{type=Informative}
- [[!DNL FTP]](connectors/cloud-storage/ftp.md) [!BADGE 批次]{type=Informative}
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md) [!BADGE 批次]{type=Informative}
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md) [!BADGE 批次]{type=Informative}
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md) [!BADGE 批次]{type=Informative}

### 同意和偏好设置 {#consent}

Experience Platform支持从第三方同意和偏好设置管理平台中摄取数据。 有关更多信息，请参阅以下相关文档：

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md) [!BADGE 批次]{type=Informative}

### 客户关系管理(CRM) {#customer-relationship-management}

CRM系统提供的数据可帮助建立客户关系，进而创建忠诚度并促进客户维系。 Experience Platform支持从[!DNL Microsoft Dynamics 365]和[!DNL Salesforce]摄取CRM数据。 有关更多信息，请参阅以下相关文档：

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md) [!BADGE 批次]{type=Informative}
- [[!DNL Salesforce]](connectors/crm/salesforce.md) [!BADGE 批次]{type=Informative}
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md) [!BADGE 批次]{type=Informative}
- [[!DNL Veeva CRM]](connectors/crm/veeva.md) [!BADGE 批次]{type=Informative}
- [[!DNL Zoho CRM]](connectors/crm/zoho.md) [!BADGE 批次]{type=Informative}

### 客户成功 {#customer-success}

Experience Platform支持从第三方客户成功应用程序中摄取数据。 有关更多信息，请参阅以下相关文档：

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md) [!BADGE 批次]{type=Informative}
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md) [!BADGE 批次]{type=Informative}
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md) [!BADGE 批次]{type=Informative}
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md) [!BADGE 批次]{type=Informative}

### 数据库 {#database}

Experience Platform支持从第三方数据库引入数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md) [!BADGE 批次]{type=Informative}
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Databricks]](connectors/databases/databricks.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md) [!BADGE 批次]{type=Informative}
- [[!DNL Azure Table Storage]](connectors/databases/ats.md) [!BADGE 批次]{type=Informative}
- [[!DNL Couchbase]](connectors/databases/couchbase.md) [!BADGE 批次]{type=Informative}
- [[!DNL GreenPlum]](connectors/databases/greenplum.md) [!BADGE 批次]{type=Informative}
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md) [!BADGE 批次]{type=Informative}
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md) [!BADGE 批次]{type=Informative}
- [[!DNL MariaDB]](connectors/databases/mariadb.md) [!BADGE 批次]{type=Informative}
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md) [!BADGE 批次]{type=Informative}
- [[!DNL MySQL]](connectors/databases/mysql.md) [!BADGE 批次]{type=Informative}
- [[!DNL Oracle]](connectors/databases/oracle.md) [!BADGE 批次]{type=Informative}
- [[!DNL Phoenix]](connectors/databases/phoenix.md) [!BADGE 批次]{type=Informative}
- [[!DNL PostgreSQL]](connectors/databases/postgres.md) [!BADGE 批次]{type=Informative}
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md) [!BADGE 批次]{type=Informative}

### 数据和身份标识合作伙伴 {#data-partner}

Experience Platform支持从数据和身份合作伙伴中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Acxiom Data Ingestion]](connectors/data-partners/acxiom-data-ingestion.md) [!BADGE 批次]{type=Informative}
- [[!DNL Acxiom Prospecting Data Import]](connectors/data-partners/acxiom-prospecting-data-import.md) [!BADGE 批次]{type=Informative}
- [[!DNL Algolia User Profiles]](connectors/data-partners/algolia-user-profiles.md)
- [[!DNL Bombora Intent]](connectors/data-partners/bombora.md) [!BADGE 批次]{type=Informative}
- [[!DNL Demandbase Intent]](connectors/data-partners/demandbase.md) [!BADGE 批次]{type=Informative}
- [[!DNL Merkury Enterprise Identity Resolution]](connectors/data-partners/merkury.md) [!BADGE 批次]{type=Informative}

### 电子商务 {#ecommerce}

Experience Platform支持从第三方电子商务系统中引入数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL SAP Commerce]](connectors/ecommerce/sap-commerce.md) [!BADGE 批次]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify.md) [!BADGE 批次]{type=Informative}
- [[!DNL Shopify]](connectors/ecommerce/shopify-streaming.md) [!BADGE 正在流式传输]{type=Positive}

### 本地系统 {#local-system}

Experience Platform支持从本地系统中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [本地文件上载](connectors/local-system/local-file-upload.md)

### 营销自动化 {#marketing-automation}

Experience Platform支持从第三方营销自动化系统中提取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Braze]](connectors/marketing-automation/braze.md) [!BADGE 正在流式传输]{type=Positive}
- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md) [!BADGE 正在流式传输]{type=Positive}
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md) [!BADGE 正在流式传输]{type=Positive}
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md) [!BADGE 批次]{type=Informative}
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md) [!BADGE 批次]{type=Informative}
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md) [!BADGE 批次]{type=Informative}
- [[!DNL Oracle NetSuite]](connectors/marketing-automation/oracle-netsuite.md) [!BADGE 批次]{type=Informative}
- [[!DNL PathFactory]](connectors/marketing-automation/pathfactory.md) [!BADGE 批次]{type=Informative}
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md) [!BADGE 批次]{type=Informative}
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### 付款 {#payments}

Experience Platform支持从第三方支付系统中提取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL PayPal]](connectors/payments/paypal.md) [!BADGE 批次]{type=Informative}
- [[!DNL Square]](connectors/payments/square.md) [!BADGE 批次]{type=Informative}
- [[!DNL Stripe]](connectors/payments/stripe.md) [!BADGE 批次]{type=Informative}

### 流式处理 {#streaming}

Experience Platform支持从流来源摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL HTTP API]](connectors/streaming/http.md) [!BADGE 正在流式传输]{type=Positive}

### 协议 {#protocols}

Experience Platform支持从第三方协议系统中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Generic OData]](connectors/protocols/odata.md) [!BADGE 批次]{type=Informative}
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md) [!BADGE 批次]{type=Informative}

## 数据摄取中源的访问控制

数据摄取中源的权限可在Adobe Admin Console中管理。 您可以通过特定产品配置文件中的&#x200B;**[!UICONTROL 权限]**&#x200B;选项卡来访问权限。 从&#x200B;**[!UICONTROL 编辑权限]**&#x200B;面板中，您可以通过&#x200B;**[!UICONTROL 数据摄取]**&#x200B;菜单项访问与源相关的权限。 **[!UICONTROL 查看源]**&#x200B;权限授予对&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中的可用源和&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中的已验证源的只读访问权限，而&#x200B;**[!UICONTROL 管理源]**&#x200B;权限授予读取、创建、编辑和禁用源的完全访问权限。

下表概述了UI基于这些权限的不同组合的行为方式：

| 权限级别 | 描述 |
| ---- | ----|
| **[!UICONTROL 查看源]** | 授予对“目录”选项卡中每种源类型以及“浏览”、“帐户”和“数据流”选项卡中的源的只读访问权限。 |
| **[!UICONTROL 管理源]**&#x200B;时间 | 除了&#x200B;**[!UICONTROL 查看源]**&#x200B;中包含的功能外，还授予对&#x200B;**[!UICONTROL 目录]**&#x200B;中的&#x200B;**[!UICONTROL 连接Source]**&#x200B;选项和&#x200B;**[!UICONTROL 浏览]**&#x200B;中的&#x200B;**[!UICONTROL 选择数据]**&#x200B;选项的访问权限。 **[!UICONTROL 管理源]**&#x200B;还允许您启用或禁用&#x200B;**[!UICONTROL DataFlow]**&#x200B;并编辑其计划。 |
| 关闭&#x200B;**[!UICONTROL 查看源]**&#x200B;并关闭&#x200B;**[!UICONTROL 管理源]** | 撤销对源的所有访问权限。 |

有关通过Adobe权限授予的可用权限的详细信息，请阅读[访问控制概述](../access-control/home.md)。

### 基于属性的访问控制

Adobe Experience Platform中基于属性的访问控制允许管理员根据属性控制对特定对象和/或权能的访问。

通过基于属性的访问控制，您可以将映射配置应用到您拥有权限的字段。 此外，如果您无权访问数据集中的所有字段，则无法将数据摄取到数据集。

#### 支持源中基于属性的访问控制

>[!TIP]
>
>基于属性的访问控制的工作方式如下：**角色**&#x200B;的创建用于对与Experience Platform实例交互的用户类型进行分类。 **标签**&#x200B;应用于&#x200B;**角色**&#x200B;以指定该给定角色的访问权限。 **标签**&#x200B;也应用于架构字段和区段等资源。 为了使用户能够访问某些架构字段和区段，必须将其添加到&#x200B;*角色，该角色具有分配给查询资源的相同标签*。 有关详细信息，请阅读[基于属性的访问控制端到端指南](../access-control/abac/end-to-end-guide.md)。

- 将标签应用于架构字段以定义对组织中特定架构字段的访问权限。 一旦建立了对特定架构字段的访问权限，用户将只能为他们有权访问的字段创建映射。
- 不具有相应角色的用户将无法创建或更新包含包含无法访问架构字段的映射的数据流。 此外，未经授权的用户无法更新、删除、启用或禁用具有无法访问架构字段的现有数据流。
- 此外，数据流在其映射、目标数据集和目标连接中必须具有完全相同的架构ID和版本。

有关基于属性的访问控制的详细信息，请阅读[基于属性的访问控制概述](../access-control/abac/overview.md)。

## 条款和条件 {#terms-and-conditions}

通过使用标记为Beta的任何源(“Beta”)，您在此确认Beta按“原样”提供，不提供任何形式的担保&#x200B;***。***

Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持Beta。 建议您使用信息性的，切勿依赖此类Beta和/或随附材料的正确功能或性能。 Beta被视为Adobe的机密信息。

您向Beta提供的任何“反馈”(有关Beta的信息，包括但不限于您在使用Adobe时遇到的问题或缺陷、建议、改进和推荐)均会分配给Adobe，其中包括针对该反馈的所有权利、标题和兴趣。

提交开放反馈或创建支持工单以共享您的建议或报告错误，寻求功能改进。
