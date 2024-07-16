---
keywords: 事件转发扩展；Braze；Braze事件转发扩展
title: Braze事件转发扩展
description: 此Adobe Experience Platform事件转发扩展可将Edge Network事件发送到Braze。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 2%

---

# [!DNL Braze Track Events API] 事件转发扩展

[[!DNL Braze]](https://www.braze.com)是一个客户参与平台，可实时支持消费者和品牌之间以客户为中心的互动。 使用[!DNL Braze]，您可以执行以下操作：

- 根据用户的语言偏好、位置偏好等，向目标用户交付数据（例如营销消息），以提高转化率并支持关键业务目标。
- 在适当的时间以客户的首选语言跨多个渠道向客户发送个性化消息，包括电子邮件、推送通知和应用程序内消息。
- 定位特定用户进行营销和促销活动，以增加常客的数量。
- 研究用户行为和模式，通过自定义消息定位特定受众，这可能有助于增加收入。

[!DNL Braze Track Events API] [事件转发](../../../ui/event-forwarding/overview.md)扩展允许您利用Adobe Experience PlatformEdge Network中捕获的数据，并使用[[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API以服务器端事件的形式将其发送到[!DNL Braze]。

本文档介绍了扩展的用例，如何在事件转发库中安装扩展，以及如何在事件转发[规则](../../../ui/managing-resources/rules.md)中运用扩展的功能。

## 用例

如果要使用[!DNL Braze]中Edge Network的数据以利用其客户分析和定位功能，应使用此扩展。

例如，假定某个零售组织具有多渠道存在（网站和移动设备），并且从其网站和移动平台捕获事务性或对话性输入作为事件数据。 使用各种[标记](../../../home.md)规则，实时将此数据发送给Edge Network。 在此处，[!DNL Braze]事件转发扩展会自动将相关事件从服务器端发送到[!DNL Braze]。

发送数据后，组织的分析团队可以利用[!DNL Braze's]功能处理数据集并获取业务见解以生成图形、功能板或其他可视化图表来通知业务利益相关者。 有关该平台各种用例的更多详细信息，请参阅[[!DNL Braze] 客户](https://www.braze.com/customers)页面。

## [!DNL Braze]先决条件和护栏 {#prerequisites}

您必须拥有[!DNL Braze]帐户才能使用其技术。 如果您没有帐户，请导航到[!DNL Braze]上的[开始页面](https://www.braze.com/get-started/)以连接到[!DNL Braze Sales]并启动帐户创建过程。

### API护栏

该扩展使用[!DNL Braze]的两个API，其限制概述如下：

| API | 速率限制 |
| --- | --- |
| [!DNL User Track] | 每分钟50,000个请求。 <br>有关详细信息，请参阅[[!DNL User Track] API文档](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit)。 |
| [!DNL User Identify] | 每分钟20,000个请求。 <br>有关详细信息，请参阅[[!DNL User Identify] API文档](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit)。 |

>[!NOTE]
>
> 请参阅[[!DNL Braze] API限制](https://www.braze.com/docs/api/api_limits/)指南，了解有关这些限制的详细信息。

### 可记帐数据点

向[!DNL Braze]发送其他自定义属性可能会增加您的[!DNL Braze]数据点消耗。 在发送其他自定义属性之前，请咨询您的[!DNL Braze]帐户管理员。 有关详细信息，请参阅有关[计费数据点](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable)的[!DNL Braze]文档。

### 收集所需的配置详细信息 {#configuration-details}

要将Edge Network连接到[!DNL Braze]，需要以下输入：

| 键类型 | 描述 | 示例 |
| --- | --- | --- |
| [!DNL Braze]实例 | 与[!DNL Braze]帐户关联的REST终结点。 有关指导，请参阅有关[实例](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints)的[!DNL Braze]文档。 | `https://rest.iad-03.braze.com` |
| API密钥 | 与[!DNL Braze]帐户关联的[!DNL Braze] API密钥。 <br/>有关指导，请参阅有关[REST API密钥](https://www.braze.com/docs/api/basics/#rest-api-key)的[!DNL Braze]文档。 | `YOUR-BRAZE-REST-API-KEY` |

### 创建密钥

创建新的[事件转发密码](../../../ui/event-forwarding/secrets.md)并将值设置为您的[[!DNL Braze] API密钥](#configuration-details)。 这将用于验证与您的帐户的连接，同时保持值的安全。

## 安装和配置[!DNL Braze]扩展 {#install}

若要安装该扩展，请[创建事件转发属性](../../../ui/event-forwarding/overview.md#properties)或选择现有属性进行编辑。

在左侧导航中选择&#x200B;**[!UICONTROL 扩展]**。 在&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中，在[!DNL Braze]扩展的卡片中选择&#x200B;**[!UICONTROL 安装]**。

![安装[!DNL Braze]扩展。](../../../images/extensions/server/braze/install-extension.png)

在下一个屏幕上，输入您之前从[!DNL Braze]收集的以下[配置值](#configuration-details)：

- **[!UICONTROL Braze Rest终结点URL]**：您可以在提供的输入中输入[!DNL Braze] Rest终结点URL的纯文本值。
- **[!UICONTROL API密钥]**：选择您之前创建的[机密数据元素](#create-a-secret)，该元素包含您的[!DNL Braze] API密钥。

完成后选择&#x200B;**[!UICONTROL 保存]**。

![扩展配置页面[!DNL Braze]。](../../../images/extensions/server/braze/configure-extension.png)

## 创建[!DNL Send Event]规则 {#tracking-rule}

安装扩展后，创建新的事件转发[规则](../../../ui/managing-resources/rules.md)并根据需要配置其条件。 配置规则的操作时，请选择&#x200B;**[!UICONTROL Braze]**&#x200B;扩展，然后为操作类型选择&#x200B;**[!UICONTROL 发送事件]**。

![添加事件转发规则操作配置。](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL 用户标识]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 外部用户ID] | 长、随机和分布良好的UUID或GUID。 如果您选择不同的方法来命名用户ID，则这些用户ID还必须很长且是随机的、分布良好的。 了解有关[建议的用户ID命名约定](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention)的更多信息。 |
| [!UICONTROL Braze用户ID] | Braze用户标识符。 |
| [!UICONTROL 用户别名] | 别名用作替代的唯一用户标识符。 使用别名标识与核心用户ID沿不同维度的用户。 <br><br>用户别名对象由两部分组成：标识符本身的alias_name和指示别名类型的alias_label。 用户可以有多个具有不同标签的别名，但每个alias_label只能有一个别名。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 要将事件与用户绑定，您需要填写[!UICONTROL 外部用户ID]字段、[!UICONTROL Braze用户标识符]字段或[!UICONTROL 用户别名]部分。

**[!UICONTROL 事件数据]**

| 输入 | 描述 | 必需 |
| --- | --- | --- |
| [!UICONTROL 事件名称{&#x200B;1}] | 事件的名称。 | 是 |
| [!UICONTROL 事件时间] | ISO 8601或`yyyy-MM-dd'T'HH:mm:ss:SSSZ`格式字符串形式的日期时间。 | 是 |
| [!UICONTROL 应用程序标识符] | 应用程序标识符或<strong>app_id</strong>是将活动与应用程序组中的特定应用程序关联的参数。 它可指定您正在与应用程序组中的哪个应用程序进行交互。 了解有关[API标识符类型](https://www.braze.com/docs/api/identifier_types/)的更多信息。 | |
| [!UICONTROL 事件属性{1&#x200B;}] | 包含事件的自定义属性的JSON对象。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> **[!UICONTROL Braze Send Event]**&#x200B;操作只需要指定&#x200B;**[!UICONTROL 事件名称]**&#x200B;和&#x200B;**[!UICONTROL 事件时间]**，但您应在自定义属性字段中包含尽可能多的信息。 有关[!DNL Braze]事件对象的详细信息，请参阅[官方文档](https://www.braze.com/docs/api/objects_filters/event_object/)。

**[!UICONTROL 用户属性]**

用户属性可以是JSON对象，其中包含相应的字段，这些字段将在指定的用户配置文件上使用提供的名称和值创建或更新属性。 支持以下属性：

| 用户属性 | 描述 |
| --- | --- |
| [!UICONTROL 名字] | |
| [!UICONTROL 姓氏] | |
| [!UICONTROL 电话] | |
| [!UICONTROL 电子邮件] | |
| [!UICONTROL 性别] | 以下字符串之一：“M”、“F”、“O”（其他）、“N”（不适用）、“P”（不愿意说）。 |
| [!UICONTROL 城市] | |
| [!UICONTROL 国家/地区] | [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)格式的国家/地区字符串。 |
| [!UICONTROL 语言] | [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)格式的字符串语言。 |
| [!UICONTROL 出生日期] | “YYYY-MM-DD”格式的字符串（例如，1980-12-21）。 |
| [!UICONTROL 时区] | 来自[IANA时区数据库](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)的时区名称(例如，“美洲/纽约”或“东部时间（美国和加拿大）”)。 |
| [!UICONTROL Facebook] | 散列包含任意ID（字符串）、like（字符串数组）、num_friends（整数）。 |
| [!UICONTROL Twitter] | 包含ID （整数）、screen_name (字符串、Twitter句柄)、followers_count （整数）、friends_count （整数）、statuses_count （整数）的任意哈希值。 |

{style="table-layout:auto"}

## 创建[!DNL Send Purchase Event]规则 {#purchase-rule}

安装扩展后，创建新的事件转发[规则](../../../ui/managing-resources/rules.md)并根据需要配置其条件。 配置规则的操作时，请选择&#x200B;**[!UICONTROL Braze]**&#x200B;扩展，然后为操作类型选择&#x200B;**[!UICONTROL 发送购买事件]**。

![添加Braze Purchase操作类型事件转发规则操作配置。](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL 用户标识]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 外部用户ID] | 长、随机和分布良好的UUID或GUID。 如果您选择不同的方法来命名用户ID，则这些用户ID还必须很长且是随机的、分布良好的。 了解有关[建议的用户ID命名约定](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention)的更多信息。 |
| [!UICONTROL Braze用户ID] | Braze用户标识符。 |
| [!UICONTROL 用户别名] | 别名用作替代的唯一用户标识符。 使用别名标识与核心用户ID沿不同维度的用户。 <br><br>用户别名对象由两部分组成：标识符本身的alias_name和指示别名类型的alias_label。 用户可以有多个具有不同标签的别名，但每个alias_label只能有一个别名。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 若要将事件链接到用户，必须填写[!UICONTROL 外部用户ID]字段、[!UICONTROL 钎焊用户标识符]字段或[!UICONTROL 用户别名]部分。

**[!UICONTROL 购买数据]**

| 输入 | 描述 | 必需 |
| --- | --- | --- |
| [!UICONTROL 产品ID &#x200B;] | 购买的标识符。 （例如，产品名称或产品类别） | 是 |
| [!UICONTROL 购买时间] | ISO 8601或`yyyy-MM-dd'T'HH:mm:ss:SSSZ`格式字符串形式的日期时间。 | 是 |
| [!UICONTROL 货币{&#x200B;1}] | 货币作为[ISO 4217](https://en.wikipedia.org/wiki/ISO_4217)字母货币代码格式的字符串。 | 是 |
| [!UICONTROL 价格&#x200B;] | 价格。 | 是 |
| [!UICONTROL 数量&#x200B;] | 如果未提供，则默认值为1。 最大值必须小于100。 | |
| [!UICONTROL 应用程序标识符] | 应用程序标识符或<strong>app_id</strong>是将活动与应用程序组中的特定应用程序关联的参数。 它可指定您正在与应用程序组中的哪个应用程序进行交互。 了解有关[API标识符类型](https://www.braze.com/docs/api/identifier_types/)的更多信息。 | |
| [!UICONTROL 购买属性&#x200B;] | 包含购买的自定义属性的JSON对象。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> **[!UICONTROL Braze Send Event]**&#x200B;操作只需要指定&#x200B;**[!UICONTROL 事件名称]**&#x200B;和&#x200B;**[!UICONTROL 事件时间]**，但您应在自定义属性字段中尽可能多地包含信息。 有关[!DNL Braze]事件对象的详细信息，请参阅[官方文档](https://www.braze.com/docs/api/objects_filters/event_object/)。

**[!UICONTROL 用户属性]**

用户属性可以是JSON对象，其中包含相应的字段，这些字段将在指定的用户配置文件上使用提供的名称和值创建或更新属性。 支持以下属性：

| 用户属性 | 描述 |
| --- | --- |
| [!UICONTROL 名字] | |
| [!UICONTROL 姓氏] | |
| [!UICONTROL 电话] | |
| [!UICONTROL 电子邮件] | |
| [!UICONTROL 性别] | 以下字符串之一：“M”、“F”、“O”（其他）、“N”（不适用）、“P”（不愿意说）。 |
| [!UICONTROL 城市] | |
| [!UICONTROL 国家/地区] | [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)格式的国家/地区字符串。 |
| [!UICONTROL 语言] | [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)格式的字符串语言。 |
| [!UICONTROL 出生日期] | “YYYY-MM-DD”格式的字符串（例如，1980-12-21）。 |
| [!UICONTROL 时区] | 来自[IANA时区数据库](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)的时区名称(例如，“美洲/纽约”或“东部时间（美国和加拿大）”)。 |
| [!UICONTROL Facebook] | 散列包含任意ID（字符串）、like（字符串数组）、num_friends（整数）。 |
| [!UICONTROL Twitter] | 包含ID （整数）、screen_name (字符串、Twitter句柄)、followers_count （整数）、friends_count （整数）、statuses_count （整数）的任意哈希值。 |

{style="table-layout:auto"}

## 验证[!DNL Braze]中的数据 {#validate}

如果事件收集和[!DNL Adobe Experience Platform]集成成功，则在[查看用户配置文件](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/)时，您将在[!DNL Braze]控制台中看到事件。 具体来说，发送到[!DNL Braze]的新事件数据反映在特定用户的[概述选项卡](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab)的[!DNL Purchases]部分中。

## 后续步骤

本指南介绍了如何使用事件转发将转化事件发送到[!DNL Braze]。 有关发送至[!DNL Braze]的事件数据的下游应用程序的更多详细信息，请参阅[官方文档](https://www.braze.com/docs)。

有关Experience Platform中事件转发功能的详细信息，请参阅[事件转发概述](../../../ui/event-forwarding/overview.md)。
