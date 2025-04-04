---
keywords: Experience Platform；主页；热门主题；Pinterest Ads；
title: Pinterest Ads Source概述
description: 了解如何使用API或用户界面将Pinterest Ads连接到Adobe Experience Platform。
badge: Beta 版
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 1%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>[!DNL Pinterest Ads]源为测试版。 有关使用带有Beta标记的连接器的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方广告系统中提取数据。 对广告提供商的支持包括[!DNL Pinterest Ads]。

[[!DNL Pinterest]](https://www.pinterest.com)是一个可视化发现引擎，用于在Web上查找食谱、家庭装饰、风格灵感和其他创意。 这些图像以插接板格式通过图像、动画GIF和视频进行小范围呈现。 [[!DNL Pinterest Ads]](https://ads.pinterest.com/)允许您使用[!DNL Pinterest]扩展业务并吸引4亿用户。

通过[!DNL Pinterest Ads]，您可以通过定向广告联系用户以发现和购买您的产品。 来自[!DNL Pinterest Ads]的pin已获得赞助，以便在相关搜索结果中获得额外的曝光。 订阅了[!DNL Pinterest Business]的用户可以选择提升现有性能最佳的pin，创建新图像或视频，甚至提升已从网站固定的图像。 [!DNL Pinterest Ads]提供了多种广告格式，以帮助您实现特定的营销活动目标。

## [!DNL Pinterest] API {#pinterest-apis}

[!DNL Pinterest Ads]源利用[!DNL Pinterest] API检索您的[!DNL Pinterest Ads]数据以及所有性能和量度。 支持的API端点包括：

* [促销活动分析](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [广告组分析](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [广告分析](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

使用[!DNL Pinterest Ads]源将数据从[!DNL Pinterest]带到Experience Platform，您可以在其中执行数据分析。 回溯范围为90天，从摄取日期开始返回数据。 [!DNL Pinterest Ads]使用持有者令牌作为与[!DNL Pinterest] API通信的身份验证机制。

## 先决条件 {#prerequisites}

创建[!DNL Pinterest Ads]源连接的第一步是确保您拥有Pinterest开发人员帐户。 如果您还没有帐户，请访问[注册](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/)页面以注册并创建帐户。

### 设置[!DNL Pinterest]应用并生成访问令牌 {#create-app-and-generate-token}

>[!IMPORTANT]
>
>建议使用[!DNL Pinterest] API生成您的访问令牌，因为在UI中生成访问令牌可提供有限的访问权限。 通过UI，您只能访问以下范围： `pins:read`、`boards:read`和`user_accounts:read`。 此限制不足以用于[!DNL Pinterest] API的分析端点。

要生成访问令牌，请阅读[设置应用程序](https://developers.pinterest.com/docs/getting-started/set-up-app/)和[使用OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/)进行身份验证上的[!DNL Pinterest]指南。

### 收集所需的凭据 {#gather-required-credentials}

为了将[!DNL Pinterest Ads]连接到Experience Platform，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| 访问令牌 | 您的用户帐户的[!DNL Pinterest Ads]访问令牌。 令牌的用户帐户必须是指定[!DNL Pinterest Ad]帐户的所有者或者拥有通过“业务访问”向他们授予的必要角色之一：管理员、分析人员或营销活动管理员。 有关访问令牌的更多信息，请参阅有关生成访问令牌的[[!DNL Pinterest] 指南](https://developers.pinterest.com/docs/getting-started/set-up-app/)。 |
| 广告帐户ID | 业务部门的相关[!DNL Pinterest Ads]广告帐户ID。 有关检索广告帐户ID的信息。 访问有关在广告管理器](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager)中查找ID的[[!DNL Pinterest] 指南。 |
| 营销活动、广告组或广告ID | 与您的广告帐户ID对应的`campaign`、`ad group`或`ad` ID。 要获取所需的ID，请导航到&#x200B;**Pinterest Business Hub** > **广告帐户摘要** > **促销活动** / **广告组** / **广告**&#x200B;的[!DNL Pinterest]页面，并复制每个名称下方提及的所需ID。 |

>[!NOTE]
>
>[!DNL Pinterest] API提供各个API以检索与每个ID关联的数据。 因此，您只需为您感兴趣的ID类型传递相应的ID。

## 护栏 {#guardrails}

以下部分提供了有关[!DNL Pinterest]的数据护栏的信息。

### [!DNL Pinterest]日期范围 {#pinterest-date-range}

[!DNL Pinterest] API支持`start_date`和`end_date`参数以检索给定日期范围内的分析数据。

* `start_date`不能早于当前日期90天。
* `end_date`在`start_date`之后不能超过90天。

在计划数据流时，必须配置以下频率和间隔设置之一：

| 频度 | 间隔 |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

例如，如果摄取在2023年3月15日设置，频度和间隔设置配置为`Day=1`或`Hour=24`，则[!DNL Pinterest] API将仅从2022年12月15日之前检索数据，因为计算回溯了90天。

### [!DNL Pinterest]时间范围 {#pinterest-time-range}

[!DNL Pinterest] API支持各种时间粒度，以便检索数据：

| 时间粒度 | 描述 |
| --- | --- |
| **总计** | 数据量度在指定的日期范围内汇总。 |
| **天** | 数据量度每天进行细分。 |
| **小时** | 数据量度按小时进行划分。 |
| **每周** | 数据量度每周进行细分。 |
| **每月** | 数据量度按月细分。 |

对于Experience Platform，[!DNL Pinterest Ads]源在内部配置为`Day`，这意味着数据将每天聚合。 例如，使用`impressions recorded`作为度量，由于粒度配置为`DAY`，因此您将在`day 1`上获得`xx`次展示，在`day 2`上获得`yy`次展示，依此类推。

>[!IMPORTANT]
>
>Pinterest在其API上设置了每天最多1000次API调用的速率限制，用于从广告、广告组或广告营销活动中读取信息。 有关适用于基础API调用的速率限制的信息，请参阅[[!DNL Pinterest] 有关速率限制](https://developers.pinterest.com/docs/reference/ratelimits/)的文档。

## 将[!DNL Pinterest Ads]连接到Experience Platform {#connect-to-platform}

以下文档提供了有关如何使用API或用户界面将[!DNL Pinterest Ads]连接到Experience Platform的信息：

### 使用API将[!DNL Pinterest Ads]连接到Experience Platform {#connect-to-platform-using-api}

* [使用流服务API创建Pinterest基本连接](../../tutorials/api/create/advertising/pinterest-ads.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为广告源创建数据流](../../tutorials/api/collect/advertising.md)

### 使用UI将[!DNL Pinterest Ads]连接到Experience Platform {#connect-to-platform-using-ui}

* [在UI中创建Pinterest源连接](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [在UI中为广告源连接创建数据流](../../tutorials/ui/dataflow/advertising.md)
