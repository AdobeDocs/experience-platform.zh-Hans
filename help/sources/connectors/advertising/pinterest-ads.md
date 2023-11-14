---
keywords: Experience Platform；主页；热门主题；Pinterest Ads；
title: pinterest广告源概述
description: 了解如何使用API或用户界面将Pinterest Ads连接到Adobe Experience Platform。
badge: Beta 版
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>此 [!DNL Pinterest Ads] 源为测试版。 阅读 [源概述](../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方广告系统摄取数据。 对广告提供商的支持包括 [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) 是一个可视化发现引擎，用于在Web上查找食谱、家庭装饰、风格灵感和其他创意。 这些内容使用插接板格式的图像、动画GIF和视频进行小规模呈现。 [[!DNL Pinterest Ads]](https://ads.pinterest.com/) 使您能够扩展业务，使用 [!DNL Pinterest].

替换为 [!DNL Pinterest Ads]，您可以通过定向广告联系用户以发现和购买您的产品。 固定自 [!DNL Pinterest Ads] 获得赞助，以便在相关搜索结果中获取额外的曝光度。 订阅的用户 [!DNL Pinterest Business] 可选择提升现有效果最佳的pin，创建新图像或视频，甚至可提升从网站固定的图像。 [!DNL Pinterest Ads] 提供了多种广告格式，以帮助您实现特定的营销活动目标。

## [!DNL Pinterest] API {#pinterest-apis}

此 [!DNL Pinterest Ads] 源利用 [!DNL Pinterest] 用于检索您的 [!DNL Pinterest Ads] 数据，以及所有性能和量度。 支持的API端点包括：

* [营销活动分析](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [广告组分析](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [广告分析](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

使用 [!DNL Pinterest Ads] 从中获取数据的源 [!DNL Pinterest] Experience Platform，您可以在其中执行数据分析。 回溯范围为90天，从摄取日期开始返回数据。 [!DNL Pinterest Ads] 使用持有者令牌作为身份验证机制与 [!DNL Pinterest] API。

## 先决条件 {#prerequisites}

创建的第一步 [!DNL Pinterest Ads] 源连接是为了确保您拥有Pinterest开发人员帐户。 如果您还没有这样的网站，请访问 [注册](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) 注册和创建帐户的页面。

### 设置 [!DNL Pinterest] 应用程序和生成访问令牌 {#create-app-and-generate-token}

>[!IMPORTANT]
>
>建议使用 [!DNL Pinterest] 用于生成访问令牌的API，因为在UI中生成访问令牌可提供有限的访问权限。 通过UI，您只能访问以下范围： `pins:read`， `boards:read` 和 `user_accounts:read`. 此限制不足以用于 [!DNL Pinterest] API。

要生成访问令牌，请阅读 [!DNL Pinterest] 指南 [设置您的应用程序](https://developers.pinterest.com/docs/getting-started/set-up-app/) 和 [使用OAuth 2.0进行身份验证](https://developers.pinterest.com/docs/getting-started/authentication/).

### 收集所需的凭据 {#gather-required-credentials}

为了连接 [!DNL Pinterest Ads] 到Platform时，必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| 访问令牌 | 此 [!DNL Pinterest Ads] 您的用户帐户的访问令牌。 令牌的用户帐户必须是指定的的所有者 [!DNL Pinterest Ad] 账户或拥有通过Business Access向他们授予的必要角色之一：管理员、分析师或营销活动经理。 有关访问令牌的更多信息，请参阅 [[!DNL Pinterest] 生成访问令牌指南](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| 广告帐户ID | 相关 [!DNL Pinterest Ads] 广告业务部门的帐户ID。 有关检索广告帐户ID的信息。 访问 [[!DNL Pinterest] 有关在广告管理器中查找ID的指南](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| 营销活动、广告组或广告ID | 此 `campaign`， `ad group`，或 `ad` 与您的广告帐户ID相对应的ID。 要获取所需的ID，请导航至 [!DNL Pinterest] 第页对象 **pinterest业务中心** > **广告帐户摘要** > **营销活动** / **广告组** / **广告** 并复制每个名称下方提到的所需ID。 |

>[!NOTE]
>
>此 [!DNL Pinterest] API提供各个API来检索与每个ID关联的数据。 因此，您只需为您感兴趣的ID类型传递相应的ID。

## 护栏 {#guardrails}

以下部分提供了有关的数据护栏的信息 [!DNL Pinterest].

### [!DNL Pinterest] 日期范围 {#pinterest-date-range}

此 [!DNL Pinterest] API同时支持 `start_date` 和 `end_date` 参数以检索给定日期范围内的分析数据。

* 此 `start_date` 距当前日期不能超过90天。
* 此 `end_date` 之后不能超过90天 `start_date`.

在计划数据流时，必须配置以下频率和间隔设置之一：

| 频度 | 间隔 |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

例如，如果摄取设置为在2023年3月15日，频度和间隔设置配置为 `Day=1` 或 `Hour=24`，然后 [!DNL Pinterest] API将仅检索最早于2022年12月15日的数据，因为计算向后追溯了90天。

### [!DNL Pinterest] 时间范围 {#pinterest-time-range}

此 [!DNL Pinterest] API支持各种不同的时间粒度，以便检索数据：

| 时间粒度 | 描述 |
| --- | --- |
| **总计** | 数据量度在指定的日期范围内汇总。 |
| **日** | 数据量度每天进行细分。 |
| **HOUR** | 数据量度按小时进行划分。 |
| **每周** | 数据量度每周进行细分。 |
| **每月** | 数据量度按月细分。 |

对于Platform，使用 [!DNL Pinterest Ads] 源在内部配置为 `Day`，这意味着每天都会聚合数据。 例如，使用 `impressions recorded` 作为量度，因为粒度配置为 `DAY`，您将获得 `xx` 展示次数 `day 1`， `yy` 展示次数 `day 2` 等等。

>[!IMPORTANT]
>
>pinterest在其API上设置了每天最多1000次API调用的速率限制，用于从广告、广告组或广告营销活动中读取信息。 有关适用于基础API调用的速率限制的信息，请参阅 [[!DNL Pinterest] 有关速率限制的文档](https://developers.pinterest.com/docs/reference/ratelimits/).

## 连接 [!DNL Pinterest Ads] 目标平台 {#connect-to-platform}

以下文档提供了有关如何连接的信息 [!DNL Pinterest Ads] 使用API或用户界面连接到Platform：

### 连接 [!DNL Pinterest Ads] 到使用API的平台 {#connect-to-platform-using-api}

* [使用流服务API创建Pinterest基本连接](../../tutorials/api/create/advertising/pinterest-ads.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为广告源创建数据流](../../tutorials/api/collect/advertising.md)

### 连接 [!DNL Pinterest Ads] 到Platform，使用UI {#connect-to-platform-using-ui}

* [在UI中创建Pinterest源连接](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [在UI中为广告源连接创建数据流](../../tutorials/ui/dataflow/advertising.md)
