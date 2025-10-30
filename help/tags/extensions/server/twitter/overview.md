---
keywords: 事件转发扩展；twitter；twitter事件转发扩展
title: Twitter事件转发扩展
description: 通过这个Adobe Experience Platform事件转发扩展，您可以将事件摄取到Twitter中，以满足您的业务要求。
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 2%

---

# [!DNL Twitter] 事件转发扩展

[[!DNL Twitter]](https://twitter.com/i/flow/login)是一种在线社交媒体和社交网络服务，用户在该服务上发布并与280个字符长的消息（称为推文）交互。 用户可以使用浏览器、移动前端软件或通过其[API](https://developer.twitter.com/en/docs/twitter-api)以编程方式与Twitter交互

[!DNL Twitter] Web Conversions API [事件转发](../../../ui/event-forwarding/overview.md)扩展允许您利用Adobe Experience Platform Edge Network中捕获的数据并将其发送给[!DNL Twitter]。 本文档介绍了扩展的使用案例、安装方法，以及如何将其功能集成到事件转发[规则](../../../ui/managing-resources/rules.md)中。

[!DNL Twitter]需要[OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a)才能使用[!DNL Twitter] [!DNL Web Conversions] API进行身份验证。

## 用例

如果要使用[!DNL Twitter]中Edge Network的数据来利用其客户分析和定位功能，应使用此扩展。

例如，以组织中的营销团队为例。 团队从其网站捕获用户交互事件数据，作为来自其网站的事件数据，并使用此事件转发扩展将其加载到[!DNL Twitter]中。

然后，营销和分析团队可以利用[!DNL Twitter's]功能执行其他分析并定位这些用户以进行有针对性的广告活动。

有关特定于[!DNL Twitter]的用例的更多信息，请参阅[[!DNL Twitter] 用例](https://developer.twitter.com/en/use-cases/build-for-businesses)文档。

## [!DNL Twitter]先决条件和护栏 {#prerequisites}

您必须拥有有效的[!DNL Twitter]帐户才能使用此扩展。 转到[[!DNL Twitter] 注册页面](https://help.twitter.com/en/using-twitter/create-twitter-account)进行注册并创建帐户（如果还没有帐户）。

您必须将帐户设置为[!DNL Twitter]开发人员帐户。 若要了解如何注册为开发人员，请参阅[[!DNL Twitter] 开发人员帐户](https://developer.twitter.com/en/support/twitter-api/developer-account1)。

### API护栏 {#guardrails}

[!DNL Twitter] Web转换API具有每15分钟间隔60,000个请求的速率限制，其中每个请求允许500个事件。

### 收集所需的配置详细信息 {#configuration-details}

要将Experience Platform连接到[!DNL Twitter]，需要以下输入：

| 键类型 | 描述 |
| --- | --- |
| 使用者密钥 | 用&#x200B;于访问[!DNL Twitter] API的应用程序API密钥。 有关指导，请参阅有关[!DNL Twitter]API密钥和密钥[的](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret)文档。 |
| 使用者密码 | API密钥允许您的应用程序访问[!DNL Twitter] API。 有关指导，请参阅有关[!DNL Twitter]API密钥和密钥[的](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret)文档。 |
| 令牌密码 | 您应用程序的不过期令牌密码，用于通过OAuth向[!DNL Twitter] API进行身份验证。 有关指导，请参阅有关[!DNL Twitter]获取使用访问令牌[的](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)文档。 |
| 访问令牌 | 您应用程序的不过期访问令牌，用于通过OAuth对[!DNL Twitter] API进行身份验证。 有关指导，请参阅有关[!DNL Twitter]获取使用访问令牌[的](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)文档。 |
| 像素ID | [!DNL Twitter]像素是在您的网站上实施的网站标记，用于跟踪网站操作或转化。 有关指导，请参阅有关[!DNL Twitter]网站[的转化跟踪的](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)文档。 |

## 安装和配置[!DNL Twitter]扩展 {#install}

若要安装该扩展，请[创建事件转发属性](../../../ui/event-forwarding/overview.md#properties)或选择现有属性进行编辑。

在左侧导航中选择&#x200B;**[!UICONTROL Extensions]**。 在&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL Install]**&#x200B;扩展卡片上的[!DNL Twitter]。

![目录显示[!DNL Twitter]扩展突出显示安装。](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>根据您的实施需求，您可能需要在配置扩展之前创建架构、数据元素和数据集。 请在开始之前查看所有配置步骤，以确定需要为用例设置哪些实体。

在下一个屏幕上，输入您之前从[收集的以下](#configuration-details)配置值[!DNL Twitter]：

* **[!UICONTROL Pixel Id]**
* **[!UICONTROL Consumer Key]**
* **[!UICONTROL Consumer Secret]**
* **[!UICONTROL Token]**
* **[!UICONTROL Token Secret]**

完成后，选择&#x200B;**[!UICONTROL Save]**。

![[!DNL Twitter]扩展的[!DNL Twitter]配置屏幕。](../../../images/extensions/server/twitter/configure.png)

## 配置事件转发规则 {#config-rule}

设置完所有数据元素后，即可开始创建事件转发规则，以确定将事件发送到[!DNL Twitter]的时间和方式。

在事件转发属性中创建新的[规则](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL Actions]**&#x200B;下，添加新操作并将扩展设置为&#x200B;**[!UICONTROL Twitter]**。 要将Edge Network事件发送到[!DNL Twitter]，请将&#x200B;**[!UICONTROL Action Type]**&#x200B;设置为&#x200B;**[!UICONTROL Send Web Conversion]。**

选择后，会显示其他控件以进一步配置事件。 您需要将[!DNL Twitter]事件属性映射到您之前创建的数据元素。 有关详细信息，请参阅[[!DNL Twitter] Web转换API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)。

![创建转化事件规则的[!DNL Twitter]。](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL User Identification]**

| 字段名称 | 描述 | 示例 | 必需 |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] Click ID] | [!DNL Twitter]点进URL中解析的点击ID。 | `26l6412g5p4iyj65a2oic2ayg2` | 如果未添加其他标识符，则此为必填字段。 |
| [!UICONTROL Email] | 使用SHA256进行哈希处理的电子邮件地址。 文本必须为小写，并且必须在进行哈希处理之前删除任何尾随或前导空格。 | `eventforwarding@example.com` | 如果未添加其他标识符，则此为必填字段。 |
| [!UICONTROL Phone] | 电话用作匹配转化事件的标识符。 在进行哈希处理之前，电话号码必须是E164格式`[+][country code][area code][local phone number]`。 | `+911234567875` | 如果未添加其他标识符，则此为必填字段。 |

**[!UICONTROL Conversion Data]**

| 字段名称 | 描述 | 示例 | 必需 |
| --- | --- | --- | --- |
| [!UICONTROL Conversion Time] | ISO 8601或`yyyy-MM-dd'T'HH:mm:ss:SSSZ`格式字符串形式的日期时间。 | 2022-02-18T01:14:00.603Z | 是 |
| [!UICONTROL Event Id] | 特定事件的以36为底的ID。 此ID应与您的[!DNL Twitter]广告帐户中包含的预配置事件匹配。 这称为事件管理器中相应事件的ID。 | o87ne或tw-o8z6j-o87ne (tw-pixel_id-event-id) | 是 |
| [!UICONTROL Number of Items] | 在事件中购买的项目数。 该值必须为大于0的正数。 | 4 | 否 |
| [!UICONTROL Currency] | 在事件中购买项目的货币。 这以ISO-4217表示，如果未提供，则默认为USD。 | 美元 | 否 |
| [!UICONTROL Value] | 在事件中购买项目的价格值。 | 100.00 | 否 |
| [!UICONTROL Conversion ID] | 转化事件的标识符，可用于同一事件标记中Web像素转化和转化API转化之间的重复数据删除。 | 23294827 | 否 |
| [!UICONTROL Description] | 包含有关转化的任何其他信息的描述。 | 测试转换 | 否 |

## 验证[!DNL Twitter]中的数据

创建并执行事件转发规则后，验证发送到[!DNL Twitter] API的事件是否在[!DNL Twitter] UI中按预期显示。

如果事件收集和[!DNL Experience Platform]集成成功，您将会在[!DNL Twitter] [!UICONTROL Events manager]中看到事件。

![&#x200B; [!DNL Twitter]事件管理器](../../../images/extensions/server/twitter/event-manager.png)

## 后续步骤

本指南介绍了如何使用事件转发将转化事件发送到[!DNL Twitter]。 有关这些底层技术的更多信息，请参阅官方文档：

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] Web转换API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] 用户访问令牌](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [像素ID和转化跟踪](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
