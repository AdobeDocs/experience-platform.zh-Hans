---
keywords: Experience Platform；主页；热门主题；Pinterest广告；
title: Pinterest广告源概述
description: 了解如何使用API或用户界面将Pinterest Ads连接到Adobe Experience Platform。
badge: "Beta"
hide: true
hidefromtoc: true
source-git-commit: a16264da68d9e5e9aeac86b1a3083c701407febb
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>的 [!DNL Pinterest Ads] 来源为测试版。 阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

Experience Platform支持从第三方广告系统摄取数据。 对广告提供商的支持包括 [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) 是一个可视发现引擎，可在Web上查找配方、家居装饰、风格灵感和其他创意。 这些内容使用插板格式的图像、动画GIF和视频以小规模呈现。 [[!DNL Pinterest Ads]](https://ads.pinterest.com/) 使您能够扩展业务，并使用 [!DNL Pinterest].

使用 [!DNL Pinterest Ads]，则可以通过有针对性的广告联系用户以发现和购买您的产品。 针脚 [!DNL Pinterest Ads] 会在相关搜索结果中获得额外曝光。 订阅的用户 [!DNL Pinterest Business] 可以选择提升现有性能最佳的针脚，创建新图像或视频，甚至提升已从网站固定的图像。 [!DNL Pinterest Ads] 提供多种广告格式，帮助您实现特定的营销活动目标。

## [!DNL Pinterest] API {#pinterest-apis}

的 [!DNL Pinterest Ads] 来源利用 [!DNL Pinterest] 用于检索 [!DNL Pinterest Ads] 数据，以及所有性能和量度。 支持的API端点包括：

* [促销活动分析](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [广告组分析](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [广告分析](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

使用 [!DNL Pinterest Ads] 源，将数据从 [!DNL Pinterest] Experience Platform时，您可以执行数据分析。 从摄取日期开始，在90天的回溯范围内返回数据。 [!DNL Pinterest Ads] 使用承载令牌作为与通信的验证机制 [!DNL Pinterest] API。

## 先决条件 {#prerequisites}

创建 [!DNL Pinterest Ads] 源连接是为了确保您拥有Pinterest开发人员帐户。 如果您还没有该活动，请访问 [注册](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) 页面以注册和创建帐户。

### 设置 [!DNL Pinterest] 应用程序和生成访问令牌 {#create-app-and-generate-token}

>[!IMPORTANT]
>
>建议使用 [!DNL Pinterest] 用于生成访问令牌的API，因为在UI中生成访问令牌提供的访问权限有限。 通过UI，您将只能访问以下范围： `pins:read`, `boards:read` 和 `user_accounts:read`. 此限制不适合在 [!DNL Pinterest] API。

要生成访问令牌，请阅读 [!DNL Pinterest] 指南 [设置应用程序](https://developers.pinterest.com/docs/getting-started/set-up-app/) 和 [使用OAuth 2.0进行身份验证](https://developers.pinterest.com/docs/getting-started/authentication/).

### 收集所需的凭据 {#gather-required-credentials}

为了连接 [!DNL Pinterest Ads] 对于平台，必须为以下连接属性提供值：

| 凭据 | 描述 |
| --- | --- |
| 访问令牌 | 的 [!DNL Pinterest Ads] 您用户帐户的访问令牌。 令牌的用户帐户必须是指定 [!DNL Pinterest Ad] 帐户，或通过业务访问向他们授予其一个必要角色：管理员、分析师或营销活动管理员。 有关访问令牌的更多信息，请参阅 [[!DNL Pinterest] 有关生成访问令牌的指南](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| 广告帐户ID | 相关 [!DNL Pinterest Ads] 您的业务部门的广告帐户ID。 有关检索广告帐户ID的信息。 访问 [[!DNL Pinterest] 有关在广告管理器中查找ID的指南](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| 促销活动、广告组或广告ID | 的 `campaign`, `ad group`或 `ad` 与您的广告帐户ID对应的ID。 要获取所需的ID，请导航到 [!DNL Pinterest] 页面 **Pinterest业务中心** > **广告帐户摘要** > **促销活动** / **广告组** / **广告** 并复制每个用户名正下方提及的所需ID。 |

>[!NOTE]
>
>的 [!DNL Pinterest] API提供单个API以检索与每个ID关联的数据。 因此，您只需为您感兴趣的ID类型传递相应的ID。

## 护栏 {#guardrails}

以下部分提供了有关 [!DNL Pinterest].

### [!DNL Pinterest] 日期范围 {#pinterest-date-range}

的 [!DNL Pinterest] API支持 `start_date` 和 `end_date` 用于在给定日期范围之间检索analytics数据的参数。

* 的 `start_date` 最长为当前日期之前的90天。
* 的 `end_date` 不能超过 `start_date`.

在计划数据流时，必须配置以下频率和间隔设置之一：

| 频度 | 间隔 |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

例如，如果在2023年3月15日设置了摄取，且其频度和间隔设置配置为 `Day=1` 或 `Hour=24`，则 [!DNL Pinterest] API将仅从2022年12月15日之前检索数据，因为计算的时间回溯了90天。

### [!DNL Pinterest] 时间范围 {#pinterest-time-range}

的 [!DNL Pinterest] API支持用于检索数据的不同时间粒度：

| 时间粒度 | 描述 |
| --- | --- |
| **合计** | 数据量度在指定的日期范围内汇总。 |
| **日** | 数据量度每天进行划分。 |
| **小时** | 数据量度会按小时划分。 |
| **每周** | 每周对数据量度进行划分。 |
| **每月** | 数据量度按月划分。 |

对于平台， [!DNL Pinterest Ads] 源内部配置为 `Day`，这意味着每天都会汇总数据。 例如，使用 `impressions recorded` 作为量度，因为粒度配置为 `DAY`，则 `xx` 展示次数 `day 1`, `yy` 展示次数 `day 2` 等等。

>[!IMPORTANT]
>
>Pinterest对其API施加了每日1000个API调用的速率限制，以从广告、广告组或广告营销活动中读取信息。 有关适用于基础API调用的速率限制的信息，请参阅 [[!DNL Pinterest] 费率限制文档](https://developers.pinterest.com/docs/reference/ratelimits/).

## 连接 [!DNL Pinterest Ads] 到平台 {#connect-to-platform}

以下文档提供了有关如何连接的信息 [!DNL Pinterest Ads] 要使用API或用户界面实现平台，请执行以下操作：

### 连接 [!DNL Pinterest Ads] 到使用API的平台 {#connect-to-platform-using-api}

* [使用流服务API创建Pinterest基本连接](../../tutorials/api/create/advertising/pinterest-ads.md)
* [使用流量服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流量服务API为广告源创建数据流](../../tutorials/api/collect/advertising.md)

### 连接 [!DNL Pinterest Ads] 到使用UI的平台 {#connect-to-platform-using-ui}

* [在UI中创建Pinterest源连接](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [在UI中为广告源连接创建数据流](../../tutorials/ui/dataflow/advertising.md)
