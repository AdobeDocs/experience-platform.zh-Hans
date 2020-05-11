---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform源连接器概述
topic: overview
translation-type: tm+mt
source-git-commit: 492adad9b38c8850130931d3d393f28c67057d07
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---


# 源连接器概述

Adobe Experience Platform允许从外部源摄取数据，同时提供使用平台服务构建、标记和增强传入数据的能力。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)收集数据。

Experience Platform提供REST风格的API和交互式UI，让您轻松设置与各种数据提供商的源连接。 这些源连接使您能够验证您的第三方系统，设置摄取运行的时间并管理数据摄取吞吐量。

借助Experience Platform，您可以集中从不同来源收集的数据，并利用从中获得的洞察完成更多工作。

## 源类型

Experience Platform中的源分为以下类别:

### Adobe应用程序

Experience Platform允许从其他Adobe应用程序(包括Adobe Analytics、Adobe受众管理器和Experience Platform Launch)中摄取数据。 有关更多信息，请参阅以下相关文档:

- [Adobe受众管理器连接器概述](connectors/adobe-applications/audience-manager.md)
- [在UI中创建Adobe受众管理器源连接器](./tutorials/ui/create/adobe-applications/audience-manager.md)
- [Adobe Analytics数据连接器概述](connectors/adobe-applications/analytics.md)
- [在UI中创建Adobe Analytics源连接器](./tutorials/ui/create/adobe-applications/analytics.md)
- [在UI中创建客户属性源连接器](./tutorials/ui/create/adobe-applications/customer-attributes.md)

### 广告

Experience Platform支持从第三方广告系统接收数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [Google Ads连接器](connectors/advertising/ads.md)

### 云存储

云存储源可以将您自己的数据导入平台，而无需下载、格式化或上传。 摄取的数据可格式化为XDM JSON、XDM镶木地板或分隔。 该过程的每个步骤都使用用户界面集成到源工作流中。 有关更多信息，请参阅以下相关文档:

- [Azure Data Lake存储Gen2连接器](connectors/cloud-storage/adls-gen2.md)
- [Azure Blob和Amazon S3连接器](connectors/cloud-storage/blob-s3.md)
- [Azure文件存储连接器](connectors/cloud-storage/azure-file-storage.md)
- [FTP和SFTP连接器](connectors/cloud-storage/ftp-sftp.md)
- [Google Cloud存储连接器](connectors/cloud-storage/google-cloud-storage.md)

### 客户关系管理(CRM)

CRM系统提供的数据有助于建立客户关系，进而创造忠诚度并推动客户保留。 Experience Platform提供从Microsoft Dynamics 365和Salesforce获取CRM数据的支持。 有关更多信息，请参阅以下相关文档:

- [Microsoft Dynamics连接器](connectors/crm/ms-dynamics.md)
- [Salesforce连接器](connectors/crm/salesforce.md)

### 客户成功

Experience Platform支持从第三方客户成功应用程序中获取数据。 有关更多信息，请参阅以下相关文档:

- [Salesforce Service Cloud连接器](connectors/customer-success/salesforce-service-cloud.md)
- [ServiceNow连接器](connectors/customer-success/servicenow.md)

### 数据库

Experience Platform支持从第三方数据库中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [Amazon Redshift连接器](connectors/databases/redshift.md)
- [Azure HDInsights连接器上的Apache Hive](connectors/databases/hive.md)
- [Azure HDInsights连接器上的Apache Spark](connectors/databases/spark.md)
- [Azure Data Explorer连接器](connectors/databases/data-explorer.md)
- [Azure Synapse Analytics连接器](connectors/databases/synapse-analytics.md)
- [Azure表存储连接器](connectors/databases/ats.md)
- [Google BigQuery连接器](connectors/databases/bigquery.md)
- [IBM DB2连接器](connectors/databases/ibm-db2.md)
- [MariaDB连接器](connectors/databases/mariadb.md)
- [Microsoft SQL Server连接器](connectors/databases/sql-server.md)
- [MySQL连接器](connectors/databases/mysql.md)
- [Oracle连接器](connectors/databases/oracle.md)
- [菲尼克斯连接器](connectors/databases/phoenix.md)
- [PostgreSQL连接器](connectors/databases/postgres.md)

### 营销自动化

Experience Platform支持从第三方营销自动化系统中获取数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [HubSpot连接器](connectors/marketing-automation/hubspot.md)

### 付款

Experience Platform支持从第三方支付系统接收数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [PayPal连接器](connectors/payments/paypal.md)

### 协议

Experience Platform支持从第三方协议系统接收数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [通用OData连接器](connectors/protocols/odata.md)

## 访问控制数据获取中的源

可以在Adobe Admin Console中管理数据获取中的源的权限。 您可以通过特定产品用户档案 *中的* “权限”选项卡访问权限。 从“编 **辑权限** ”面板中，可以通过数据获取菜单条目访问与 *源相关的* 权限。 “ **视图源** ”权限授予对“目录”选项卡中可用源的只读访问权，并在“浏览”选项卡中通过身份验证的源 *，而“管理源******* ”权限则授予对读取、创建、编辑和禁用源的完全访问权限。

下表概述了UI根据这些权限的不同组合而表现的方式：

| 权限级别 | 描述 |
| ---- | ----|
| **视图源** On | 授予对“目录”选项卡中每个源类型以及“浏览”、“帐户”和“ *DataFlow******* ”选项卡中的源的只读访问权限。 |
| **管理源** On | 除了视图源中包含的功 **能**，还授予对目录中 *的Connect Source* (连接源 *)选项和* Select DataOption( ****&#x200B;在浏览中)的访问权限。 **“管理源** ”还允许您启用或禁用 *数据流* ，并编辑其计划。 |
| **视图源** Off和 **管理源** Off | 撤销对源的所有访问权限。 |

有关通过Admin Console授予的可用权限（包括这四个来源）的详细信息，请参阅 [访问控制概述](../access-control/home.md)。
