---
keywords: Experience Platform；主页；热门主题；源连接器；源连接器；源；数据源；数据源；数据源；数据源；数据源；数据源；数据源连接
solution: Experience Platform
title: 源连接器概述
topic-legacy: overview
description: Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
source-git-commit: 365e36351bf18864c677f53dffbc30b47f29b074
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# 源连接器概述

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

[!DNL Flow Service] 用于从平台内各种不同来源收集客户数据并将其集中在一起。 该服务提供了用户界面和RESTful API，可让您轻松设置与各种数据提供商的源连接。 通过这些源连接，您可以验证第三方系统、设置摄取运行的时间，以及管理数据摄取吞吐量。

通过Experience Platform，您可以集中从不同来源收集的数据，并利用从中获得的分析完成更多工作。

## 源类型

Experience Platform中的源分为以下类别：

### Adobe应用程序 {#adobe-applications}

Experience Platform允许从其他Adobe应用程序(包括Adobe Analytics和Adobe Audience Manager)摄取数据。 有关更多信息，请参阅以下相关文档：

- [Adobe Audience Manager connector概述](connectors/adobe-applications/audience-manager.md)
- [在UI中创建Adobe Audience Manager源连接](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分类数据源连接概述](connectors/adobe-applications/classifications.md)
- [在UI中创建Adobe Analytics分类数据源连接](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics报表包数据源连接概述](connectors/adobe-applications/analytics.md)
- [在UI中创建Adobe Analytics源连接](./tutorials/ui/create/adobe-applications/analytics.md)
- [Adobe数据收集](connectors/adobe-applications/data-collection.md)
- [在UI中创建客户属性源连接](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 连接器概述](connectors/adobe-applications/marketo/marketo.md)
- [创建 [!DNL Marketo Engage] UI中的源连接](./tutorials/ui/create/adobe-applications/marketo.md)

### 广告 {#advertising}

Experience Platform支持从第三方广告系统摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Google AdWords]](connectors/advertising/ads.md) 连接器

### 云存储 {#cloud-storage}

云存储源可以将您自己的数据引入平台，而无需下载、设置或上传。 摄取的数据可以格式为XDM JSON、XDM Parquet或分隔。 流程的每个步骤均使用用户界面集成到源工作流中。 有关更多信息，请参阅以下相关文档：

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

### 同意和首选项 {#consent}

Experience Platform支持从第三方同意和首选项管理平台摄取数据。 有关更多信息，请参阅以下相关文档：

- [[!DNL OneTrust Integration]](connectors/consent-and-preferences/onetrust.md)


### 客户关系管理(CRM) {#customer-relationship-management}

CRM系统提供的数据有助于建立客户关系，这反过来又可以创造忠诚度并促进客户维系。 Experience Platform支持从 [!DNL Microsoft Dynamics 365] 和 [!DNL Salesforce]. 有关更多信息，请参阅以下相关文档：

- [[!DNL Microsoft Dynamics]](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce]](connectors/crm/salesforce.md)
- [[!DNL Veeva CRM]](connectors/crm/veeva.md)
- [[!DNL Zoho CRM]](connectors/crm/zoho.md)

### 客户成功 {#customer-success}

Experience Platform支持从第三方客户成功应用程序摄取数据。 有关更多信息，请参阅以下相关文档：

- [[!DNL Salesforce Service Cloud]](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow]](connectors/customer-success/servicenow.md)

### 数据库 {#database}

Experience Platform支持从第三方数据库摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

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
- [[!DNL Snowflake]](connectors/databases/snowflake.md)

### 电子商务 {#ecommerce}

Experience Platform支持从第三方电子商务系统摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### 本地系统 {#local-system}

Experience Platform支持从本地系统摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [本地文件上传](connectors/local-system/local-file-upload.md)

### 营销自动化 {#marketing-automation}

Experience Platform支持从第三方营销自动化系统摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL HubSpot]](connectors/marketing-automation/hubspot.md)
- [[!DNL Mailchimp]](connectors/marketing-automation/mailchimp.md)
- [[!DNL Oracle Eloqua]](connectors/marketing-automation/oracle-eloqua.md)
- [[!DNL Salesforce Marketing Cloud]](connectors/marketing-automation/salesforce-marketing-cloud.md)

### 支付 {#payments}

Experience Platform支持从第三方支付系统摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL PayPal]](connectors/payments/paypal.md)
- [[!DNL Square]](connectors/payments/square.md)

### 流 {#streaming}

Experience Platform支持从流源摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL HTTP API]](connectors/streaming/http.md)

### 协议 {#protocols}

Experience Platform支持从第三方协议系统摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档：

- [[!DNL Generic OData]](connectors/protocols/odata.md)
- [[!DNL Generic REST API]](connectors/protocols/generic-rest.md)

## 数据摄取中源的访问控制

可以在Adobe Admin Console中管理数据摄取中源的权限。 您可以通过 **[!UICONTROL 权限]** 选项卡。 从 **[!UICONTROL 编辑权限]** 面板中，您可以通过 **[!UICONTROL 数据摄取]** 菜单目录访问Advertising Cloud帮助。 的 **[!UICONTROL 查看源]** 权限授予对 **[!UICONTROL 目录]** 选项卡和已验证的源 **[!UICONTROL 浏览]** ，而 **[!UICONTROL 管理源]** 权限授予对读取、创建、编辑和禁用源的完全访问权限。

下表概述了基于这些权限的不同组合，UI的行为方式：

| 权限级别 | 描述 |
| ---- | ----|
| **[!UICONTROL 查看源]** 开 | 授予对“目录”选项卡中每种源类型以及“浏览”、“帐户”和“数据流”选项卡中源的只读访问权限。 |
| **[!UICONTROL 管理源]** 开 | 除了 **[!UICONTROL 查看源]**，授予访问权限 **[!UICONTROL 连接源]** 选项 **[!UICONTROL 目录]** 和 **[!UICONTROL 选择数据]** 选项 **[!UICONTROL 浏览]**. **[!UICONTROL 管理源]** 还允许您启用或禁用 **[!UICONTROL 数据流]** 并编辑其计划。 |
| **[!UICONTROL 查看源]** 关闭和 **[!UICONTROL 管理源]** 关闭 | 撤消对源的所有访问权限。 |

有关通过Admin Console授予的可用权限（包括这四个来源）的更多信息，请参阅 [访问控制概述](../access-control/home.md).

## 条款和条件 {#terms-and-conditions}

通过使用任何标记为测试版（“测试版”）的源，您特此确认已提供测试版 ***“按原样”，不提供任何担保***.

Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持测试版。 建议您谨慎使用，切勿以任何方式依赖此类测试版和/或随附材料的正确功能或性能。 测试版被视为Adobe的机密信息。

“您”向Adobe提供的任何“反馈”（有关测试版的信息，包括但不限于您在使用测试版、建议、改进和建议时遇到的问题或缺陷），现将分配给Adobe，包括对此反馈的所有权利、标题和兴趣以及对此反馈的关注。

提交开放反馈或创建支持票证以共享您的建议或报告错误，寻求功能增强。
