---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
source-git-commit: 0c507a26f551af1eb17889e8e77a036e3c106240
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 10%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 10 月 27 日**

Adobe Experience Platform 现有功能的更新包括：

- [源](#sources)

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| [!DNL Amazon S3] 源增强功能 | 您现在可以使用 `s3SessionToken` 连接 [!DNL Amazon S3] 帐户到Platform的临时安全凭据。 此令牌允许您提供对 [!DNL Amazon S3] 资源。 请参阅 [[!DNL Amazon S3] 文档](../../sources/connectors/cloud-storage/s3.md#prerequisites) 以了解更多信息。 |
| [!DNL Generic REST API] （测试版） | 您现在可以创建 [!DNL Generic REST API] 源连接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) 或 [用户界面](../../sources/tutorials/ui/create/protocols/generic-rest.md) 将数据从通用REST应用程序引入平台。 请参阅 [[!DNL Generic REST API] 概述](../../sources/connectors/protocols/generic-rest.md) 以了解更多信息。 |
| [!DNL Zoho CRM] （测试版） | 您现在可以创建 [!DNL Zoho CRM] 源连接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) 或 [用户界面](../../sources/tutorials/ui/create/crm/zoho.md) 从 [!DNL Zoho CRM] 帐户到平台。 请参阅 [[!DNL Zoho CRM] 概述](../../sources/connectors/crm/zoho.md) 以了解更多信息。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
