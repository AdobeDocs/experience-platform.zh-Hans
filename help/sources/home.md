---
keywords: Experience Platform；主页；热门主题；源连接器；源连接器；源；数据源；数据源；数据源连接
solution: Experience Platform
title: 源连接器概述
description: Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 6e663e428eebcea92f94111708686d80cf63a988
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 2%

---

# 源连接器概述

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源中摄取数据，如 Adobe 应用程序、基于云的存储、数据库和许多其他源。

[!DNL Flow Service] 用于收集并集中Platform内各种不同来源的客户数据。 该服务提供了一个用户界面和RESTful API，可让您轻松设置到各种数据提供商的源连接。 通过这些源连接，您可以对第三方系统进行身份验证、设置摄取运行的时间，以及管理数据摄取吞吐量。

借助Experience Platform，您可以集中从不同来源收集的数据，并利用从中获得的见解做更多事情。

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 源类型

Experience Platform中的源分为以下几类：

### Adobe应用程序 {#adobe-applications}

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
- [[!DNL Marketo Engage] 源概述](connectors/adobe-applications/marketo/marketo.md)
   - [创建 [!DNL Marketo Engage] UI中的源连接](./tutorials/ui/create/adobe-applications/marketo.md)
   - [创建 [!DNL Marketo Engage] 自定义活动数据的源连接和数据流](./tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
- [Adobe Workfront源概述](connectors/adobe-applications/workfront.md)
   - [在UI中创建Workfront源连接](./tutorials/ui/create/adobe-applications/workfront.md)

### Advertising {#advertising}

Experience Platform支持从第三方广告系统中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [Google Ads](connectors/advertising/ads.md)

### Analytics {#analytics}

Experience Platform支持从第三方Analytics平台引入数据。 有关更多信息，请参阅以下相关文档：

- [[!DNL Mixpanel]](connectors/analytics/mixpanel.md)
- [[!DNL Pendo]](connectors/analytics/pendo-webhook.md)

### 云存储 {#cloud-storage}

云存储源可以将您自己的数据引入Platform，而无需下载、格式化或上传。 引入的数据可以格式化为XDM JSON、XDM Parquet或分隔。 该过程的每个步骤都使用用户界面集成到源工作流中。 有关更多信息，请参阅以下相关文档：

- [[!DNL Azure Data Lake Storage Gen2]](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob]](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis]](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3]](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS]](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs]](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage]](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL Data Landing Zone]](connectors/cloud-storage/data-landing-zone.md)
- [[!DNL FTP]](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage]](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub]](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage]](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP]](connectors/cloud-storage/sftp.md)

### 同意和偏好设置 {#consent}

Experience Platform支持从第三方同意和偏好管理平台摄取数据。 有关更多信息，请参阅以下相关文档：

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)

### 客户关系管理(CRM) {#customer-relationship-management}

CRM系统提供的数据可帮助建立客户关系，进而创建忠诚度并促进客户维系。 Experience Platform支持从提取CRM数据 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce]. 有关更多信息，请参阅以下相关文档：

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL SugarCRM]](connectors/crm/sugarcrm.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### 客户成功 {#customer-success}

Experience Platform支持从第三方客户成功应用程序中摄取数据。 有关更多信息，请参阅以下相关文档：

- [[!DNL Oracle Service Cloud]](connectors/customer-success/oracle-service-cloud.md)
- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)
- [[!DNL Zendesk]](connectors/customer-success/zendesk.md)

### 数据库 {#database}

Experience Platform支持从第三方数据库引入数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Amazon Redshift]](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights]](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights]](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer]](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics]](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage]](connectors/databases/ats.md)
- [[!DNL Couchbase]](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery]](connectors/databases/bigquery.md)
- [[!DNL GreenPlum]](connectors/databases/greenplum.md)
- [[!DNL HP Vertica]](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2]](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB]](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server]](connectors/databases/sql-server.md)
- [[!DNL MySQL]](connectors/databases/mysql.md)
- [[!DNL Oracle]](connectors/databases/oracle.md)
- [[!DNL Phoenix]](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL]](connectors/databases/postgres.md)
- [[!DNL Snowflake Streaming]](connectors/databases//snowflake-streaming.md)
- [[!DNL Snowflake]](connectors/databases/snowflake.md)
- [[!DNL Teradata Vantage]](connectors/databases/teradata-vantage.md)

### 电子商务 {#ecommerce}

Experience Platform支持从第三方电子商务系统中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)
- [[!DNL Shopify Streaming]](connectors/ecommerce/shopify-streaming.md)

### 本地系统 {#local-system}

Experience Platform支持从本地系统中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [本地文件上传](connectors/local-system/local-file-upload.md)

### 营销自动化 {#marketing-automation}

Experience Platform支持从第三方营销自动化系统中引入数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Chatlio]](connectors/marketing-automation/chatlio-webhook.md)
- [[!DNL Customer.io]](connectors/marketing-automation/customerio-webhook.md)
- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)
<!-- 
- [[!DNL Oracle Responsys]](connectors/marketing-automation/oracle-responsys.md)
-->

### 支付 {#payments}

Experience Platform支持从第三方支付系统中提取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### 流 {#streaming}

Experience Platform支持从流源摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL HTTP API]](connectors/streaming/http.md)

### 协议 {#protocols}

Experience Platform支持从第三方协议系统中引入数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## 数据摄取中源的访问控制

数据摄取中源的权限可在Adobe Admin Console中管理。 您可以通过 **[!UICONTROL 权限]** 选项卡。 从 **[!UICONTROL 编辑权限]** 面板中，您可以通过，访问与源相关的权限 **[!UICONTROL 数据摄取]** 菜单项。 此 **[!UICONTROL 查看源]** 权限授予对中的可用源的只读访问权限 **[!UICONTROL 目录]** 选项卡和经过验证的源 **[!UICONTROL 浏览]** 选项卡，而 **[!UICONTROL 管理源]** 权限授予读取、创建、编辑和禁用源的完全访问权限。

下表概述了UI基于这些权限的不同组合的行为方式：

| 权限级别 | 描述 |
| ---- | ----|
| **[!UICONTROL 查看源]** 日期 | 授予对“目录”选项卡中每种源类型以及“浏览”、“帐户”和“数据流”选项卡中的源的只读访问权限。 |
| **[!UICONTROL 管理源]** 日期 | 除了包含的函数外， **[!UICONTROL 查看源]**，授予对的访问权限 **[!UICONTROL 连接源]** 中的选项 **[!UICONTROL 目录]** 和 **[!UICONTROL 选择数据]** 中的选项 **[!UICONTROL 浏览]**. **[!UICONTROL 管理源]** 还允许您启用或禁用 **[!UICONTROL 数据流]** 并编辑其时间表。 |
| **[!UICONTROL 查看源]** 关闭和 **[!UICONTROL 管理源]** 关闭 | 撤销对源的所有访问权限。 |

有关通过Adobe权限授予的可用权限的更多信息，请阅读 [访问控制概述](../access-control/home.md).

### 基于属性的访问控制

Adobe Experience Platform中基于属性的访问控制允许管理员根据属性控制对特定对象和/或功能的访问。

通过基于属性的访问控制，您可以将映射配置应用到您拥有权限的字段。 此外，如果您无权访问数据集中的所有字段，则无法将数据摄取到数据集。

#### 在源中支持基于属性的访问控制

>[!TIP]
>
>基于属性的访问控制的工作方式如下： **角色** 创建用于对与您的Platform实例交互的用户类型进行分类。 **标签** 应用于 **角色** 指定该给定角色的访问权限。 **标签** 也会应用于架构字段和区段等资源。 用户要访问某些架构字段和区段，必须将其添加到 *具有分配给查询资源的相同标签的角色*. 有关详细信息，请阅读 [基于属性的访问控制端到端指南](../access-control/abac/end-to-end-guide.md).

- 将标签应用于架构字段以定义对组织中特定架构字段的访问权限。 一旦建立了对特定架构字段的访问权限，用户将只能为他们有权访问的字段创建映射。
- 不具有相应角色的用户将无法创建或更新包含不可访问架构字段的映射的数据流。 此外，未经授权的用户无法更新、删除、启用或禁用具有无法访问架构字段的现有数据流。
- 此外，数据流在其映射、目标数据集和目标连接中必须具有完全相同的架构ID和版本。

有关基于属性的访问控制的详细信息，请阅读 [基于属性的访问控制概述](../access-control/abac/overview.md).

## 条款和条件 {#terms-and-conditions}

使用标记为Beta(“Beta”)的任何源，即表示您确认已提供Beta ***“原样”，无任何形式的担保***.

Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持Beta。 建议您谨慎使用，不要依赖此测试版和/或随附材料的正确功能或性能。 Beta版被视为Adobe的机密信息。

您向Adobe提供的任何“反馈”（关于Beta版的信息，包括但不限于您在使用Beta版时遇到的问题或缺陷、建议、改进和建议）将分配给Adobe，包括在该反馈中的所有权利、标题和兴趣。

提交开放反馈或创建支持工单以分享您的建议或报告错误，寻求功能增强。
