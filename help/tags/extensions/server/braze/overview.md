---
keywords: 事件转发扩展；布雷；阻止事件转发扩展
title: Braze事件转发扩展
description: 此Adobe Experience Platform事件转发扩展会将Adobe Experience Edge Network事件发送到Braze。
source-git-commit: 6815b5eb0426efd1dde901db1e8b86e86615530a
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 4%

---


# [!DNL Braze Track Events API] 事件转发扩展

[[!DNL Braze]](https://www.braze.com) 是一个客户参与平台，可实时支持消费者和品牌之间以客户为中心的交互。 使用 [!DNL Braze]，您可以执行以下操作：

- 根据目标用户的语言偏好、位置偏好等向其提供数据（如营销消息），以提高转化率并支持关键业务目标。
- 在适当的时间以客户首选的语言，跨多个渠道向客户发送个性化的消息，包括电子邮件、推送通知和应用程序内消息。
- 为营销和促销活动定位特定用户，以增加回访客户数量。
- 研究用户行为和模式以通过自定义消息定向特定受众，这有助于增加收入。

的 [!DNL Braze Track Events API] [事件转发](../../../ui/event-forwarding/overview.md) 扩展允许您利用在Adobe Experience Platform边缘网络中捕获的数据，并将其发送到 [!DNL Braze] 以服务器端事件的形式使用 [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API。

本文档介绍扩展的用例、如何在事件转发库中安装该扩展，以及如何在事件转发中使用其功能 [规则](../../../ui/managing-resources/rules.md).

## 用例

如果要在 [!DNL Braze] 以利用其客户分析和定位功能。

例如，假设零售组织拥有多渠道业务（网站和移动设备），并且从其网站和移动平台中捕获作为事件数据的事务性或对话式输入。 使用各种 [标记](../../../home.md) 规则，此数据会实时发送到边缘网络。 从此处， [!DNL Braze] 事件转发扩展会自动将相关事件发送到 [!DNL Braze] 从服务器端。

发送数据后，组织的分析团队便可以利用 [!DNL Braze's] 用于处理数据集和获取业务分析的功能，以生成图形、功能板或其他可视化图表，从而通知业务利益相关方。 请参阅 [[!DNL Braze] 客户](https://www.braze.com/customers) 页面，以了解有关该平台各种用例的更多详细信息。

## [!DNL Braze] 先决条件和防护 {#prerequisites}

您必须具有 [!DNL Braze] 以便使用其技术。 如果您没有帐户，请导航到 [开始页面](https://www.braze.com/get-started/) on [!DNL Braze] 连接到 [!DNL Braze Sales] 并启动帐户创建过程。

### API护栏

扩展使用 [!DNL Braze]的API及其限制如下所述：

| API | 速率限制 |
| --- | --- |
| [!DNL User Track] | 每分钟50,000个请求。 <br>请参阅 [[!DNL User Track] API文档](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) 以了解详细信息。 |
| [!DNL User Identify] | 每分钟20,000个请求。 <br>请参阅 [[!DNL User Identify] API文档](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) 以了解详细信息。 |

>[!NOTE]
>
> 请参阅 [[!DNL Braze] API限制](https://www.braze.com/docs/api/api_limits/) 有关这些限制的更多细节。

### 计费数据点

将其他自定义属性发送到 [!DNL Braze] 可以增加 [!DNL Braze] 数据点使用情况。 咨询您的 [!DNL Braze] 帐户管理器。 请参阅 [!DNL Braze] 文档 [计费数据点](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) 以了解更多信息。

### 收集所需的配置详细信息 {#configuration-details}

将边缘网络连接到 [!DNL Braze]，则需要输入以下数据：

| 键类型 | 描述 | 示例 |
| --- | --- | --- |
| [!DNL Braze] 实例 | 与 [!DNL Braze] 帐户。 请参阅 [!DNL Braze] 文档 [实例](https://www.braze.com/docs/user_guide/administrative/access_braze/braze_instances) 以获取指导。 | `https://rest.iad-03.braze.com` |
| API 密钥 | 的 [!DNL Braze] 与 [!DNL Braze] 帐户。 <br/>请参阅 [!DNL Braze] 文档位于 [REST API密钥](https://www.braze.com/docs/api/basics/#rest-api-key) 以获取指导。 | `YOUR-BRAZE-REST-API-KEY` |

### 创建密钥

新建 [事件转发密钥](../../../ui/event-forwarding/secrets.md) 并将值设置为 [[!DNL Braze] API密钥](#configuration-details). 这将用于验证与帐户的连接，同时保持值的安全性。

## 安装和配置 [!DNL Braze] 扩展 {#install}

要安装扩展，请 [创建事件转发属性](../../../ui/event-forwarding/overview.md#properties) 或选择要编辑的现有属性。

选择 **[!UICONTROL 扩展]** 中。 在 **[!UICONTROL 目录]** 选项卡，选择 **[!UICONTROL 安装]** 在 [!DNL Braze] 扩展。

![安装 [!DNL Braze] 扩展。](../../../images/extensions/server/braze/install-extension.png)

在下一个屏幕上，输入以下内容 [配置值](#configuration-details) 之前从 [!DNL Braze]:

- **[!UICONTROL Braze Rest端点URL]**:您可以输入 [!DNL Braze] rest端点URL作为提供的输入中的纯文本。
- **[!UICONTROL API密钥]**:选择 [秘密数据元素](#create-a-secret) 之前创建的，其中包含 [!DNL Braze] API密钥。

选择 **[!UICONTROL 保存]** 完成。

![的 [!DNL Braze] 扩展配置页面。](../../../images/extensions/server/braze/configure-extension.png)

## 创建 [!DNL Send Event] 规则 {#tracking-rule}

安装扩展后，创建新的事件转发 [规则](../../../ui/managing-resources/rules.md) 并根据需要配置其条件。 为规则配置操作时，选择 **[!UICONTROL 布雷兹]** 扩展，然后选择 **[!UICONTROL 发送事件]** （对于操作类型）。

![添加事件转发规则操作配置。](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL 用户标识]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 外部用户ID] | 长、随机且分布良好的UUID或GUID。 如果您选择其他方法来命名用户ID，则这些ID还必须长、随机且分布良好。 详细了解 [建议的用户ID命名约定](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze用户ID] | 使用户标识符更新。 |
| [!UICONTROL 用户别名] | 别名用作替代的唯一用户标识符。 使用别名来标识与核心用户ID具有不同维度的用户。 <br><br> 用户别名对象由两部分组成：标识符本身的alias_name，以及指示别名类型的alias_label。 用户可以具有多个具有不同标签的别名，但每个别名标签只能有一个别名。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 要将事件与用户绑定，您需要填写 [!UICONTROL 外部用户ID] 字段，或 [!UICONTROL Braze用户标识符] 字段或 [!UICONTROL 用户别名] 中。

**[!UICONTROL 事件数据]**

| 输入 | 描述 | 必需 |
| --- | --- | --- |
| [!UICONTROL 活动名称 &#x200B;] | 事件的名称。 | 是 |
| [!UICONTROL 事件时间 ] | 在ISO 8601或 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 格式。 | 是 |
| [!UICONTROL 应用程序标识符] | 应用程序标识符或 <strong>app_id</strong> 是将活动与应用程序组中的特定应用程序关联的参数。 它可指定您与之交互的应用程序组中的哪个应用程序。 进一步了解 [API标识符类型](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL 事件属&#x200B;性] | 包含事件自定义属性的JSON对象。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> 的 **[!UICONTROL 阻止发送事件]** 操作只需要 **[!UICONTROL 事件名称]** 和 **[!UICONTROL 事件时间]** ，但您应在自定义属性字段中尽可能多地包含信息。 有关 [!DNL Braze] 事件对象，请参阅 [官方文档](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL 用户属性]**

用户属性可以是JSON对象，其中包含将使用指定用户配置文件中提供的名称和值创建或更新属性的字段。 支持以下属性：

| 用户属性 | 描述 |
| --- | --- |
| [!UICONTROL 名字] |  |
| [!UICONTROL 姓氏] |  |
| [!UICONTROL Phone] |  |
| [!UICONTROL 电子邮件] |  |
| [!UICONTROL 性别] | 以下字符串之一：“M”、“F”、“O”（其他）、“N”（不适用）、“P”（宁可不说）。 |
| [!UICONTROL 城市] |  |
| [!UICONTROL 国家/地区] | 国家/地区： [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 格式。 |
| [!UICONTROL 语言] | 语言作为字符串 [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 格式。 |
| [!UICONTROL 出生日期] | 格式为“YYYY-MM-DD”的字符串(例如，1980-12-21)。 |
| [!UICONTROL 时区] | 时区名称来源 [IANA时区数据库](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (例如，“America/New_York”或“Eastern Time(Us &amp; Canada)”)。 |
| [!UICONTROL Facebook] | 包含任意id（字符串）、称赞（字符串数组）、num_friends（整数）的哈希。 |
| [!UICONTROL Twitter] | 包含以下任一项的哈希： id（整数）、screen_name(字符串，Twitter句柄)、followers_count（整数）、friends_count（整数）、statusstages_count(integer)。 |

{style="table-layout:auto"}

## 创建 [!DNL Send Purchase Event] 规则 {#purchase-rule}

安装扩展后，创建新的事件转发 [规则](../../../ui/managing-resources/rules.md) 并根据需要配置其条件。 为规则配置操作时，选择 **[!UICONTROL 布雷兹]** 扩展，然后选择 **[!UICONTROL 发送购买事件]** （对于操作类型）。

![添加“品牌购买”操作类型事件转发规则操作配置。](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL 用户标识]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 外部用户ID] | 长、随机且分布良好的UUID或GUID。 如果您选择其他方法来命名用户ID，则这些ID还必须长、随机且分布良好。 详细了解 [建议的用户ID命名约定](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze用户ID] | 使用户标识符更新。 |
| [!UICONTROL 用户别名] | 别名用作替代的唯一用户标识符。 使用别名来标识与核心用户ID具有不同维度的用户。 <br><br> 用户别名对象由两部分组成：标识符本身的alias_name，以及指示别名类型的alias_label。 用户可以具有多个具有不同标签的别名，但每个别名标签只能有一个别名。 |

{style="table-layout:auto"}

>[!NOTE]
>
> 要将事件链接到用户，您必须完成 [!UICONTROL 外部用户ID] 字段， [!UICONTROL Braze用户标识符] 字段，或 [!UICONTROL 用户别名] 中。

**[!UICONTROL 购买数据]**

| 输入 | 描述 | 必需 |
| --- | --- | --- |
| [!UICONTROL 产品 ID &#x200B;] | 购买的标识符。 （例如，产品名称或产品类别） | 是 |
| [!UICONTROL 购买时间 ] | 在ISO 8601或 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 格式。 | 是 |
| [!UICONTROL 货币 &#x200B;] | 货币作为 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 字母货币代码格式。 | 是 |
| [!UICONTROL 价格 &#x200B;] | 价格. | 是 |
| [!UICONTROL 数量 &#x200B;] | 如果未提供，则默认值为1。 最大值必须小于100。 |  |
| [!UICONTROL 应用程序标识符] | 应用程序标识符或 <strong>app_id</strong> 是将活动与应用程序组中的特定应用程序关联的参数。 它可指定您与之交互的应用程序组中的哪个应用程序。 进一步了解 [API标识符类型](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL 购买属&#x200B;性] | 包含购买的自定义属性的JSON对象。 |  |

{style="table-layout:auto"}

>[!NOTE]
>
> 的 **[!UICONTROL 阻止发送事件]** 操作只需要 **[!UICONTROL 事件名称]** 和 **[!UICONTROL 事件时间]** ，但您应在自定义属性字段中尽可能多地包含信息。 有关 [!DNL Braze] 事件对象，请参阅 [官方文档](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL 用户属性]**

用户属性可以是JSON对象，其中包含将使用指定用户配置文件中提供的名称和值创建或更新属性的字段。 支持以下属性：

| 用户属性 | 描述 |
| --- | --- |
| [!UICONTROL 名字] |  |
| [!UICONTROL 姓氏] |  |
| [!UICONTROL Phone] |  |
| [!UICONTROL 电子邮件] |  |
| [!UICONTROL 性别] | 以下字符串之一：“M”、“F”、“O”（其他）、“N”（不适用）、“P”（宁可不说）。 |
| [!UICONTROL 城市] |  |
| [!UICONTROL 国家/地区] | 国家/地区： [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) 格式。 |
| [!UICONTROL 语言] | 语言作为字符串 [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 格式。 |
| [!UICONTROL 出生日期] | 格式为“YYYY-MM-DD”的字符串(例如，1980-12-21)。 |
| [!UICONTROL 时区] | 时区名称来源 [IANA时区数据库](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (例如，“America/New_York”或“Eastern Time(Us &amp; Canada)”)。 |
| [!UICONTROL Facebook] | 包含任意id（字符串）、称赞（字符串数组）、num_friends（整数）的哈希。 |
| [!UICONTROL Twitter] | 包含以下任一项的哈希： id（整数）、screen_name(字符串，Twitter句柄)、followers_count（整数）、friends_count（整数）、statusstages_count(integer)。 |

{style="table-layout:auto"}

## 在中验证数据 [!DNL Braze] {#validate}

如果事件集合和 [!DNL Adobe Experience Platform] 集成成功后，您将在 [!DNL Braze] 控制台 [查看用户配置文件](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). 具体而言，发送到的新事件数据 [!DNL Braze] 反映在 [!DNL Purchases] 特定用户的部分 [“概述”选项卡](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## 后续步骤

本指南介绍了如何将转化事件发送到 [!DNL Braze] 使用事件转发。 有关下游应用程序的更多详细信息，请参阅 [!DNL Braze]，请参阅 [官方文档](https://www.braze.com/docs).

有关Experience Platform中事件转发功能的更多信息，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
