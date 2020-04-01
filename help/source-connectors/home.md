---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Source Connectors概述
topic: overview
translation-type: tm+mt
source-git-commit: 291d669cc0f5b009b23dc2771688ee54b53d08db

---


# 源连接器概述

Adobe Experience Platform允许从外部源中摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)获取数据。

Experience Platform提供RESTful API和交互式UI，使您能轻松设置与各种数据提供商的源连接。 这些源连接使您能够验证第三方系统的身份、设置摄取运行的时间以及管理数据摄取吞吐量。

通过Experience Platform，您可以集中从不同来源收集的数据，并利用从中获得的洞察完成更多工作。

## 来源类型

Experience Platform中的源分为以下类别:

### Adobe应用程序

Experience Platform允许从其他Adobe应用程序(包括Adobe Analytics、Adobe受众管理器和Experience Platform Launch)中摄取数据。 有关详细信息，请参阅以下相关文档:

- [Adobe受众管理器连接器概述](./ui/adobe-applications/audience-manager.md)
- [在UI中创建Adobe受众管理器源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/aam-ui-tutorial.md)
- [Adobe Analytics数据连接器概述](./ui/adobe-applications/analytics.md)
- [在UI中创建Adobe Analytics源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/adobe-applications/adobe-analytics-ui-tutorial.md)

### 云存储

云存储源可以将您自己的数据导入平台，而无需下载、格式化或上传。 该过程的每个步骤都使用用户界面集成到源工作流中。 对云存储提供商的支持包括Amazon S3、Azure Blob、FTP服务器和SFTP服务器。 有关详细信息，请参阅以下相关文档:

- [在UI中创建Azure Blob或Amazon S3源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/amazon-s3-ui-tutorial.md)
- [在UI中创建Azure Data Lake存储Gen2源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/adls-gen2-ui-tutorial.md)
- [在UI中创建FTP或SFTP源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/ftp-sftp-ui-tutorial.md)
- [在UI中创建Google Cloud存储源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/cloud-storages/google-cloud-storage-ui-tutorial.md)

### 客户关系管理(CRM)

CRM系统提供的数据有助于建立客户关系，进而创造忠诚度并推动客户保留。 Experience Platform支持从Microsoft Dynamics 365和Salesforce中摄取CRM数据。 有关详细信息，请参阅以下相关文档:

- [在UI中创建Microsoft Dynamics 365或Salesforce源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/dynamics-salesforce-ui-tutorial.md)
- [在UI中创建PayPal源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/crm/paypal-tutorial.md)

### 客户成功(CS)

Experience Platform支持从第三方客户成功应用程序中获取数据。 有关详细信息，请参阅以下相关文档:

- [在UI中创建Salesforce Service Cloud源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/salesforce-service-cloud-tutorial.md)
- [在UI中创建ServiceNow源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/customer-success/servicenow-ui-tutorial.md)

### 数据库

Experience Platform支持从第三方数据库中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [在UI中创建AWS Redshift源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/amazon-redshift-ui-tutorial.md)
- [在UI中创建Azure突触分析源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/azure-synapse-analytics-ui-tutorial.md)
- [在UI中创建Google BigQuery源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/google-big-query-ui-tutorial.md)
- [在UI中创建MariaDB源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/database-nosql/mariadb-api-tutorial.md)
- [在UI中创建Microsoft SQL Server源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/sql-server-ui-tutorial.md)
- [在UI中创建MySQL源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/mysql-ui-tutorial.md)
- [在UI中创建PostgreSQL源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/databases/postgresql-tutorial.md)

### 营销自动化

Experience Platform支持从第三方营销自动化系统中摄取数据。 有关特定源连接器的更多信息，请参阅以下相关文档:

- [在UI中创建HubSpot源连接器](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-ui-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/ui/marketing-automation/hubspot-tutorial.md)

## API教程

您可以使用Flow Service API创建源连接器。 有关详细信息，请参阅 [源API教程文档](https://www.adobe.io/apis/experienceplatform/home/tutorials/sources-api-tutorials.html#!api-specification/markdown/narrative/tutorials/sources_tutorial/api/sources-api-tutorial.md)。

## 访问控制数据摄取中的源

可以在Adobe Admin Console中管理数据获取中源的权限。 您可以通过特定产品用户档案中 *的* “权限”选项卡访问权限。 从“编 **辑权限** ”面板中，可以通过数据获取菜单条目访问与 *源相关的权限* 。 “ **视图源********** ”权限授予对“目录”选项卡中可用源的只读访问权限，并在“浏览”选项卡中通过身份验证的源，而“管理源”权限则授予对读取、创建、编辑和禁用源的完全访问权限。

下表概述了UI根据这些权限的不同组合而表现的方式：

| 权限级别 | 描述 |
| ---- | ----|
| **视图来源** On | 授予对 *Catalog* （目录）选项卡中每个源类型以及 *Counts*（帐户）、Accounts（帐户）和 **** DataFlow（流）选项卡中的源的只读访问权限。 |
| **在上管理源** | 除了包含在 **视图源中之外**，还授予对Catalog *中的Connect Source* （连接源）选项的访问权，以及对Browse Connect Sources（浏览）中 ******&#x200B;的Select Connect Source（选择数据）选项的访问权。 **Manage Sources** 还允许您启用或禁用 *DataFlow* ，并编辑其计划。 |
| **视图源** Off（关闭）和 **管理源** Off（关闭） | 撤销对源的所有访问权。 |

有关通过Admin Console授予的可用权限（包括这四个来源）的详细信息，请参阅 [访问控制概述](../access-control/home.md)。
