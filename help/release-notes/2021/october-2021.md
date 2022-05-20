---
title: Adobe Experience Platform发行说明2021年10月
description: 2021年10月版Adobe Experience Platform发行说明。
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 10 月 27 日**

## Experience Platform更新

更新了Experience Platform。

### 用户界面 {#ui}

用户界面已更新，更改如下：

| 功能 | 描述 |
| --- | --- |
| 深色主题 | 使用深色主题开关可在平台界面中的浅色主题和深色主题之间进行切换。 交换机位于用户名和电子邮件下方的用户配置文件中。 |
| 切换左侧导航 | 使用应用程序标题顶部的改进导航切换开关，可显示或隐藏显示Experience Platform功能的菜单。 系统会记住您的上次选择，并仅显示您有权访问的功能。 |
| 访问可见性 | 左侧导航栏仅显示您能够访问的功能。 在Adobe Experience Platform的早期版本中，即使您无法访问不可用项目，它们也是可见的。 |

请参阅 [平台UI指南](../../landing/ui-guide.md) 以了解更多。

## 现有功能的更新

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [源](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| `contains_key` 函数 | 的 `contains_key` 函数，用于检查对象是否存在于源中。 此函数将 `is_set` 函数，现已弃用。 |
| 错误消息 | 返回的错误消息 `/mappingSets/preview` 数据准备API中的端点现在与运行时生成的错误消息一致。 |

请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md) 了解有关此服务的更多信息。

### 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| [!DNL Amazon S3] 源增强功能 | 您现在可以使用 `s3SessionToken` 连接 [!DNL Amazon S3] 帐户到Platform的临时安全凭据。 此令牌允许您提供对 [!DNL Amazon S3] 资源。 有关详细信息，请参阅[[!DNL Amazon S3] 文档](../../sources/connectors/cloud-storage/s3.md#prerequisites)。 |
| [!DNL Generic REST API] （测试版） | 您现在可以创建 [!DNL Generic REST API] 源连接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) 将数据从通用REST应用程序引入平台。 请参阅 [[!DNL Generic REST API] 概述](../../sources/connectors/protocols/generic-rest.md) 以了解更多信息。 |
| [!DNL Zoho CRM] （测试版） | 您现在可以创建 [!DNL Zoho CRM] 源连接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) 或 [用户界面](../../sources/tutorials/ui/create/crm/zoho.md) 从 [!DNL Zoho CRM] 帐户到平台。 请参阅 [[!DNL Zoho CRM] 概述](../../sources/connectors/crm/zoho.md) 以了解更多信息。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
