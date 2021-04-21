---
keywords: Experience Platform；主页；热门主题；源连接器；源连接器；源；数据源；数据源；数据源；数据源连接
solution: Experience Platform
title: 源连接器概述
topic-legacy: overview
description: Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用平台服务构建、标记和增强传入数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、数据库和许多其他来源。
exl-id: efdbed4d-5697-43ef-a47a-a8bcf0f13237
translation-type: tm+mt
source-git-commit: 412d7c247353bfd30e134656140ba13f55d2ca07
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# 源连接器概述

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用平台服务构建、标记和增强传入数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、数据库和许多其他资源。

[!DNL Flow Service] 用于收集和集中平台内不同来源的客户数据。该服务提供了用户界面和RESTful API，使您能够轻松设置与各种数据提供者的源连接。 这些源连接使您能够验证您的第三方系统，设置摄取运行的时间，并管理数据摄取吞吐量。

利用Experience Platform，您可以集中从不同来源收集的数据，并利用从中获得的洞察完成更多工作。

## 源类型

Experience Platform中的源分为以下类别:

### Adobe应用程序

Experience Platform允许从其他Adobe应用程序(包括Adobe Analytics、Adobe Audience Manager和[!DNL Experience Platform Launch])中摄取数据。 有关更多信息，请参阅以下相关文档:

- [Adobe Audience Manager connector概述](connectors/adobe-applications/audience-manager.md)
- [在UI中创建Adobe Audience Manager源连接](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分类数据连接器概述](connectors/adobe-applications/classifications.md)
- [在UI中创建Adobe Analytics分类数据源连接](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics数据连接器概述](connectors/adobe-applications/analytics.md)
- [在UI中创建Adobe Analytics源连接](./tutorials/ui/create/adobe-applications/analytics.md)
- [在UI中创建客户属性源连接](./tutorials/ui/create/adobe-applications/customer-attributes.md)
- [[!DNL Marketo Engage] 连接器概述](connectors/adobe-applications/marketo/marketo.md)
- [在UI [!DNL Marketo Engage] 中创建资源连接](./tutorials/ui/create/adobe-applications/marketo.md)

### 广告

Experience Platform支持从第三方广告系统中摄取数据。 有关特定源连接器的详细信息，请参阅以下相关文档:

- [[!DNL Google AdWords]](connectors/advertising/ads.md) 连接器

### 云存储

云存储源可以将您自己的数据导入平台，而无需下载、格式化或上传。 收录的数据可以格式化为XDM JSON、XDM Perface或分隔。 该过程的每个步骤都使用用户界面集成到源工作流中。 有关更多信息，请参阅以下相关文档:

- [[!DNL Azure Data Lake Storage Gen2] 连接器](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] 连接器](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] 连接器](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] 连接器](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] 连接器](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] 连接器](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] 连接器](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP] 连接器](connectors/cloud-storage/ftp.md)
- [[!DNL Google Cloud Storage] 连接器](connectors/cloud-storage/google-cloud-storage.md)
- [[!DNL Google PubSub] 连接器](connectors/cloud-storage/google-pubsub.md)
- [[!DNL Oracle Object Storage] 连接器](connectors/cloud-storage/oracle-object-storage.md)
- [[!DNL SFTP] 连接器](connectors/cloud-storage/sftp.md)

### 客户关系管理(CRM)

CRM系统提供的数据有助于建立客户关系，进而创造忠诚度并推动客户保留。 Experience Platform支持从[!DNL Microsoft Dynamics 365]和[!DNL Salesforce]获取CRM数据。 有关更多信息，请参阅以下相关文档:

- [[!DNL Microsoft Dynamics] 连接器](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] 连接器](connectors/crm/salesforce.md)

### 客户成功

Experience Platform支持从第三方客户成功应用程序中获取数据。 有关更多信息，请参阅以下相关文档:

- [[!DNL Salesforce Service Cloud] 连接器](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] 连接器](connectors/customer-success/servicenow.md)

### 数据库

Experience Platform支持从第三方数据库中摄取数据。 有关特定源连接器的详细信息，请参阅以下相关文档:

- [[!DNL Amazon Redshift] 连接器](connectors/databases/redshift.md)
- [[!DNL Apache Hive on Azure HDInsights] 连接器](connectors/databases/hive.md)
- [[!DNL Apache Spark on Azure HDInsights] 连接器](connectors/databases/spark.md)
- [[!DNL Azure Data Explorer] 连接器](connectors/databases/data-explorer.md)
- [[!DNL Azure Synapse Analytics] 连接器](connectors/databases/synapse-analytics.md)
- [[!DNL Azure Table Storage] 连接器](connectors/databases/ats.md)
- [[!DNL Couchbase] 连接器](connectors/databases/couchbase.md)
- [[!DNL Google BigQuery] 连接器](connectors/databases/bigquery.md)
- [[!DNL GreenPlum] 连接器](connectors/databases/greenplum.md)
- [[!DNL HP Vertica] 连接器](connectors/databases/hp-vertica.md)
- [[!DNL IBM DB2] 连接器](connectors/databases/ibm-db2.md)
- [[!DNL MariaDB] 连接器](connectors/databases/mariadb.md)
- [[!DNL Microsoft SQL Server] 连接器](connectors/databases/sql-server.md)
- [[!DNL MySQL] 连接器](connectors/databases/mysql.md)
- [[!DNL Oracle] 连接器](connectors/databases/oracle.md)
- [[!DNL Phoenix] 连接器](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] 连接器](connectors/databases/postgres.md)

### 电子商务

Experience Platform支持从第三方电子商务系统中摄取数据。 有关特定源连接器的详细信息，请参阅以下相关文档:

- [[!DNL Shopify]](connectors/ecommerce/shopify.md)

### 营销自动化

Experience Platform支持从第三方营销自动化系统中获取数据。 有关特定源连接器的详细信息，请参阅以下相关文档:

- [[!DNL HubSpot] 连接器](connectors/marketing-automation/hubspot.md)

### 付款

Experience Platform支持从第三方支付系统中摄取数据。 有关特定源连接器的详细信息，请参阅以下相关文档:

- [[!DNL PayPal] 连接器](connectors/payments/paypal.md)

### 协议

Experience Platform支持从第三方协议系统中摄取数据。 有关特定源连接器的详细信息，请参阅以下相关文档:

- [[!DNL Generic OData] 连接器](connectors/protocols/odata.md)

## 访问控制数据获取中的源

可以在Adobe Admin Console中管理数据获取中源的权限。 您可以通过特定产品用户档案中的&#x200B;**[!UICONTROL Permissions]**&#x200B;选项卡访问权限。 从&#x200B;**[!UICONTROL Edit Permissions]**&#x200B;面板中，可通过&#x200B;**[!UICONTROL data ingestion]**&#x200B;菜单条目访问与源相关的权限。 **[!UICONTROL View Sources]**&#x200B;权限授予对&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡中可用源和&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡中已验证源的只读访问权限，而&#x200B;**[!UICONTROL Manage Sources]**&#x200B;权限授予对读取、创建、编辑和禁用源的完全访问权限。

下表概述了UI根据这些权限的不同组合而表现的方式：

| 权限级别 | 描述 |
| ---- | ----|
| **[!UICONTROL View Sources]** 开 | 授予对“目录”选项卡中每个源类型以及“浏览”、“帐户”和“数据流”选项卡中的源的只读访问权限。 |
| **[!UICONTROL Manage Sources]** 开 | 除了&#x200B;**[!UICONTROL View Sources]**&#x200B;中包含的函数外，还授予对&#x200B;**[!UICONTROL Catalog]**&#x200B;中的&#x200B;**[!UICONTROL Connect Source]**&#x200B;选项和&#x200B;**[!UICONTROL Browse]**&#x200B;中的&#x200B;**[!UICONTROL Select Data]**&#x200B;选项的访问权。 **[!UICONTROL Manage Sources]** 还允许您启用或禁用和 **[!UICONTROL DataFlows]** 编辑其计划。 |
| **[!UICONTROL View Sources]** 关/ **[!UICONTROL Manage Sources]** 关 | 撤销对源的所有访问权。 |

有关通过Admin Console授予的可用权限（包括这四个来源）的详细信息，请参阅[访问控制概述](../access-control/home.md)。

## 条款和条件{#terms-and-conditions}

通过使用任何标为测试版（“测试版”）的源，您特此确认测试版按&#x200B;***“原样”提供，不提供任何类型的担保***。

Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持测试版。 建议您务必小心，切勿以任何方式依赖此类测试版和/或随附材料的正确功能或性能。 测试版被视为Adobe的机密信息。

您向Adobe提供的任何“反馈”（有关测试版的信息，包括但不限于您在使用测试版时遇到的问题或缺陷、建议、改进和建议）现已指派给Adobe，包括此类反馈的所有权利、所有权和兴趣。

提交开放反馈或创建支持票证以共享您的建议或报告错误、寻求功能增强。
