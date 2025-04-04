---
title: Adobe Experience Platform 发行说明（2021 年 10 月）
description: Adobe Experience Platform 的 2021 年 10 月发行说明。
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 25%

---

# Adobe Experience Platform 发行说明

**发行日期： 2021年10月27日**

## Experience Platform的更新

Experience Platform的更新。

### 用户界面 {#ui}

用户界面已更新，进行了以下更改：

| 功能 | 描述 |
| --- | --- |
| 深色主题 | 在Experience Platform界面中，使用深色主题开关在浅色和深色主题之间切换。 交换机位于用户名和电子邮件下的用户配置文件中。 |
| 切换左侧导航 | 使用应用程序标题顶部的改进导航切换开关，可显示或隐藏显示Experience Platform功能的菜单。 系统将记住您最后的选择，并仅显示您有权访问的功能。 |
| 访问可见性 | 左侧导航栏仅显示您可以访问的功能。 在Adobe Experience Platform的早期版本中，即使您无法访问不可用的项目，也会显示这些项目。 |

请参阅[Experience Platform UI指南](../../landing/ui-guide.md)以了解详情。

## 现有功能的更新

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [源](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]允许数据工程师映射、转换和验证与Experience Data Model (XDM)之间的数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| `contains_key`函数 | 已引入`contains_key`函数，该函数允许您检查源中是否存在该对象。 此函数替换`is_set`函数，该函数现已弃用。 |
| 错误消息 | 数据准备API中`/mappingSets/preview`端点返回的错误消息现在与运行时生成的错误消息一致。 |

请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)了解有关此服务的更多信息。

### 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| [!DNL Amazon S3]源增强功能 | 您现在可以使用`s3SessionToken`参数使用临时安全凭据将您的[!DNL Amazon S3]帐户连接到Experience Platform。 此令牌允许您向不受信任环境中的用户提供对[!DNL Amazon S3]资源的短期临时访问。 有关详细信息，请参阅[[!DNL Amazon S3] 文档](../../sources/connectors/cloud-storage/s3.md#prerequisites)。 |
| [!DNL Generic REST API] (Beta) | 您现在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md)创建[!DNL Generic REST API]源连接，将数据从通用REST应用程序引入Experience Platform。 有关详细信息，请参阅[[!DNL Generic REST API] 概述](../../sources/connectors/protocols/generic-rest.md)。 |
| [!DNL Zoho CRM] (Beta) | 您现在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md)或[用户界面](../../sources/tutorials/ui/create/crm/zoho.md)创建[!DNL Zoho CRM]源连接，将数据从[!DNL Zoho CRM]帐户引入Experience Platform。 有关详细信息，请参阅[[!DNL Zoho CRM] 概述](../../sources/connectors/crm/zoho.md)。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
