---
title: Adobe Experience Platform发行说明2022年9月
description: 2022年9月版Adobe Experience Platform发行说明。
source-git-commit: 1890bd9dbce6a217951c28fc2fb3fec2634e714d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 7%

---


# Adobe Experience Platform 发行说明

**发布日期：2022 年 9 月 28 日**

Adobe Experience Platform 现有功能的更新包括：

- [Identity Service](#identity-service)
- [源](#sources)

## Identity Service {#identity-service}

提供相关的数字体验需要全面了解您的客户。 当客户数据在不同的系统中分散，导致每个客户似乎具有多个“身份”时，这会使操作愈发困难。

Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 支持删除数据集 | 现在，在通过 [目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)、用户界面或数据卫生。 阅读 [删除UI中的数据集](../../catalog/datasets/user-guide.md#delete-a-dataset) 以了解更多信息。 |

要了解有关Identity Service的更多信息，请阅读 [Identity Service概述](../../identity-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| Audience Manager区段人口对实时客户资料的影响 | 首次使用Audience Manager源将Audience Manager区段发送到Platform时，大量Audience Manager区段人口的摄取会直接影响用户档案总数。 这意味着选择所有区段可能会导致用户档案计数超过您的许可证使用权限。 有关更多信息，请阅读 [Audience Manager源概述](../../sources/connectors/adobe-applications/audience-manager.md). 有关许可证使用情况的信息，请阅读 [使用许可证使用功能板](../../dashboards/guides/license-usage.md). |

要进一步了解来源，请阅读 [源概述](../../sources/home.md).