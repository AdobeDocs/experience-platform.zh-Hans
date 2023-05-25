---
title: Adobe Experience Platform发行说明2021年10月
description: Adobe Experience Platform 2021年10月版发行说明。
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 10 月 27 日**

## Experience Platform更新

Experience Platform更新。

### 用户界面 {#ui}

更新了用户界面，进行了以下更改：

| 功能 | 描述 |
| --- | --- |
| 深色主题 | 在Platform界面中，使用深色主题开关在浅色和深色主题之间切换。 交换机位于用户名和电子邮件下的用户配置文件中。 |
| 切换左侧导航 | 使用应用程序标题顶部的改进导航切换开关可显示或隐藏显示Experience Platform功能的菜单。 系统会记住您最后的选择，并仅显示您有权访问的功能。 |
| 访问可见性 | 左侧导航栏仅显示您可以访问的功能。 在Adobe Experience Platform的早期版本中，即使您无法访问不可用的项目，也会显示这些项目。 |

请参阅 [Platform UI指南](../../landing/ui-guide.md) 了解更多信息。

## 现有功能的更新

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [源](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师映射、转换和验证数据到/传出体验数据模型(XDM)。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| `contains_key` 函数 | 此 `contains_key` 函数中，用于检查源中是否存在该对象。 此函数将 `is_set` 函数，现已弃用。 |
| 错误消息 | 返回的错误消息 `/mappingSets/preview` 数据准备API中的端点现在与运行时生成的错误消息一致。 |

请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md) 以了解有关此服务的更多信息。

### 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

| 功能 | 描述 |
| --- | --- |
| [!DNL Amazon S3] 源增强功能 | 您现在可以使用 `s3SessionToken` 用于连接 [!DNL Amazon S3] 使用临时安全凭据连接到Platform的帐户。 此令牌允许您提供对的短期临时访问 [!DNL Amazon S3] 资源提供给不受信任的环境中的用户。 有关详细信息，请参阅[[!DNL Amazon S3] 文档](../../sources/connectors/cloud-storage/s3.md#prerequisites)。 |
| [!DNL Generic REST API] (Beta) | 您现在可以创建 [!DNL Generic REST API] 源连接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) 将数据从通用REST应用程序引入平台。 请参阅 [[!DNL Generic REST API] 概述](../../sources/connectors/protocols/generic-rest.md) 了解更多信息。 |
| [!DNL Zoho CRM] (Beta) | 您现在可以创建 [!DNL Zoho CRM] 源连接使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) 或 [用户界面](../../sources/tutorials/ui/create/crm/zoho.md) 以从您的 [!DNL Zoho CRM] Platform帐户。 请参阅 [[!DNL Zoho CRM] 概述](../../sources/connectors/crm/zoho.md) 了解更多信息。 |

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
