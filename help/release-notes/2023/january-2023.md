---
title: Adobe Experience Platform发行说明2023年1月
description: 2023年1月版Adobe Experience Platform发行说明。
source-git-commit: 01c220147312108649e036d93288823df5389235
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 9%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 1 月 25 日**

Adobe Experience Platform 现有功能的更新包括：

- [源](#sources)

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| 允许用户访问云存储源的子文件夹 | 现在，您可以在创建新帐户时定义对云存储源特定子文件夹的访问权限。 创建后，用户将只能从允许的子文件夹访问数据。 此功能适用于以下云存储源： [Azure Blob存储](../../sources/connectors/cloud-storage/blob.md), [Google云存储](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)和 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 测试版可用性 [!DNL SugarCRM] | [!DNL SugarCRM] 源现在在测试版中可用。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 从 [!DNL SugarCRM] 帐户Experience Platform。 有关更多信息，请阅读 [[!DNL SugarCRM] 概述](../../sources/connectors/crm/sugarcrm.md). |