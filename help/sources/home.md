---
keywords: Experience Platform;home;popular topics;source connectors;source connector;sources;data sources;data source;data source connection
solution: Experience Platform
title: Adobe Experience Platform源连接器概述
topic: overview
description: Adobe Experience Platform允许从外部来源摄取数据，同时使您能够使用平台服务构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)收集数据。
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---


# 源连接器概述

Adobe Experience Platform允许从外部来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松设置与各种数据提供者的源连接。 这些源连接使您能够验证您的第三方系统，设置摄取运行的时间并管理数据摄取吞吐量。

利用 [!DNL Experience Platform]该功能，您可以集中从不同来源收集的数据，并利用从中获得的洞察做更多工作。

## 源类型

中的源 [!DNL Experience Platform] 分为以下类别:

### Adobe应用程序

[!DNL Experience Platform] 允许从其他Adobe应用程序(包括Adobe Analytics、Adobe Audience Manager和)中摄取数据 [!DNL Experience Platform Launch]。 有关更多信息，请参阅以下相关文档:

- [Adobe Audience Manager连接器概述](connectors/adobe-applications/audience-manager.md)
- [在UI中创建Adobe Audience Manager源连接器](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics分类数据连接器概述](connectors/adobe-applications/classifications.md)
- [在UI中创建Adobe Analytics分类数据源连接器](./tutorials/ui/create/adobe-applications/classifications.md)
- [Adobe Analytics数据连接器概述](connectors/adobe-applications/analytics.md)
- [在UI中创建Adobe Analytics源连接器](./tutorials/ui/create/adobe-applications/analytics.md)
- [在UI中创建客户属性源连接器](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### 广告

[!DNL Experience Platform] 支持从第三方广告系统中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [[!DNL Google AdWords]连接器](connectors/advertising/ads.md)

### 云存储

云存储源无需下载、格式化 [!DNL Platform] 或上传即可将您自己的数据导入其中。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 该过程的每个步骤都使用用户界面集成到源工作流中。 有关更多信息，请参阅以下相关文档:

- [[!DNL Azure Data Lake Storage Gen2] 连接器](connectors/cloud-storage/adls-gen2.md)
- [[!DNL Azure Blob] 连接器](connectors/cloud-storage/blob.md)
- [[!DNL Amazon Kinesis] 连接器](connectors/cloud-storage/kinesis.md)
- [[!DNL Amazon S3] 连接器](connectors/cloud-storage/s3.md)
- [[!DNL Apache HDFS] 连接器](connectors/cloud-storage/hdfs.md)
- [[!DNL Azure Event Hubs] 连接器](connectors/cloud-storage/eventhub.md)
- [[!DNL Azure File Storage] 连接器](connectors/cloud-storage/azure-file-storage.md)
- [[!DNL FTP and SFTP] 连接器](connectors/cloud-storage/ftp-sftp.md)
- [[!DNL Google Cloud Storage] 连接器](connectors/cloud-storage/google-cloud-storage.md)

### 客户关系管理(CRM)

CRM系统提供的数据有助于建立客户关系，进而创造忠诚度并推动客户保留。 [!DNL Experience Platform] 支持从和中获取 [!DNL Microsoft Dynamics 365] CRM数 [!DNL Salesforce]据 有关更多信息，请参阅以下相关文档:

- [[!DNL Microsoft Dynamics] 连接器](connectors/crm/ms-dynamics.md)
- [[!DNL Salesforce] 连接器](connectors/crm/salesforce.md)

### 客户成功

[!DNL Experience Platform] 支持从第三方客户成功应用程序中获取数据。 有关更多信息，请参阅以下相关文档:

- [[!DNL Salesforce Service Cloud] 连接器](connectors/customer-success/salesforce-service-cloud.md)
- [[!DNL ServiceNow] 连接器](connectors/customer-success/servicenow.md)

### 数据库

[!DNL Experience Platform] 支持从第三方数据库中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

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
- [[!DNL Microsoft SQL Server] 连接器](connectors/databases/sql-server.md)
- [[!DNL MySQL] 连接器](connectors/databases/mysql.md)
- [[!DNL Oracle] 连接器](connectors/databases/oracle.md)
- [[!DNL Phoenix] 连接器](connectors/databases/phoenix.md)
- [[!DNL PostgreSQL] 连接器](connectors/databases/postgres.md)

### 营销自动化

[!DNL Experience Platform] 支持从第三方营销自动化系统中获取数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [[!DNL HubSpot] 连接器](connectors/marketing-automation/hubspot.md)

### 付款

[!DNL Experience Platform] 支持从第三方支付系统中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [[!DNL PayPal] 连接器](connectors/payments/paypal.md)

### 协议

[!DNL Experience Platform] 支持从第三方协议系统接收数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [[!DNL Generic OData] 连接器](connectors/protocols/odata.md)

## 访问控制数据获取中的源

可在Adobe Admin Console内管理数据获取来源的权限。 您可以通过特定产品用户档案 **[!UICONTROL 中的]** “权限”选项卡访问权限。 从“编 **[!UICONTROL 辑权限]** ”面板中，可以通过数据获取菜单条目访问与 **[!UICONTROL 源相关的]** 权限。 “ **[!UICONTROL 视图源]** ”权限授予对“目录”选项卡中可用源的只读访问权，并在“浏览”选项卡中通过身份验证的源 **[!UICONTROL ，而“管理源]********** ”权限则授予对读取、创建、编辑和禁用源的完全访问权限。

下表概述了UI根据这些权限的不同组合表现的方式：

| 权限级别 | 描述 |
| ---- | ----|
| **[!UICONTROL 视图源]** On | 授予对“目录”选项卡中每个源类型以及“浏览”、“帐户”和“数据流”选项卡中的源的只读访问权限。 |
| **[!UICONTROL 管理源]** On | 除了视图源中包含的功 **[!UICONTROL 能]**，还授予对目录中 **[!UICONTROL 的Connect Source]** (连接源 **[!UICONTROL )选项和]** Select DataOption( ********&#x200B;在浏览中)的访问权限。 **[!UICONTROL “管理源]** ”还允许您启用或禁用 **[!UICONTROL 数据流]** ，并编辑其计划。 |
| **[!UICONTROL 视图源]** Off和 **[!UICONTROL 管理源]** Off | 撤销对源的所有访问权限。 |

有关通过Admin Console授予的可用权限（包括这四个来源）的详细信息，请参阅 [访问控制概述](../access-control/home.md)。

## 条款和条件 {#terms-and-conditions}

通过使用任何标为测试版（“测试版”）的来源，您特此确认测试版按“原样”提 ***供，不作任何形式的担保***。

Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持测试版。 建议您务必小心，不要以任何方式依赖此类测试版和／或随附材料的正确功能或性能。 测试版被视为Adobe的机密信息。

您向Adobe提供的任何“反馈”（有关测试版的信息，包括但不限于您在使用测试版时遇到的问题或缺陷、建议、改进和建议），现将分配给Adobe，包括该反馈中和该反馈的所有权利、所有权和兴趣。

提交开放式反馈或创建支持票证以共享您的建议或报告错误，寻求功能增强。
