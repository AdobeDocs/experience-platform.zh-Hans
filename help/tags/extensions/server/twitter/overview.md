---
keywords: 事件转发扩展；twitter；twitter事件转发扩展
title: twitter事件转发扩展
description: 此Adobe Experience Platform事件转发扩展允许您根据业务需求将事件摄取到Twitter中。
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 3%

---

# [!DNL Twitter] 事件转发扩展

[[!DNL Twitter]](https://twitter.com/i/flow/login) 是一种在线社交媒体和社交网络服务，用户在该服务上发布和互动280个字符长的消息，称为推文。 用户可以使用浏览器、移动前端软件以编程方式与Twitter交互，也可以通过浏览器以编程方式与其交互。 [API](https://developer.twitter.com/en/docs/twitter-api)

此 [!DNL Twitter] Web转换API [事件转发](../../../ui/event-forwarding/overview.md) 通过扩展，您可以利用在Adobe Experience Platform Edge Network中捕获的数据并将其发送至 [!DNL Twitter]. 本文档介绍了扩展的用例，如何安装扩展，以及如何将其功能集成到事件转发中 [规则](../../../ui/managing-resources/rules.md).

[!DNL Twitter] 需要 [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) 进行身份验证 [!DNL Twitter] [!DNL Web Conversions] API。

## 用例

如果您要在以下位置使用来自Edge Network的数据，则应该使用此扩展： [!DNL Twitter] 以利用其客户分析和定位功能。

例如，以组织中的营销团队为例。 团队从其网站中捕获用户交互事件数据，作为来自其网站的事件数据并将其加载到 [!DNL Twitter] 使用此事件转发扩展。

然后，营销和分析团队可以利用 [!DNL Twitter's] 能够执行其他分析并定位这些用户以进行有针对性的广告活动。

有关特定用例的更多信息 [!DNL Twitter]，请参阅 [[!DNL Twitter] 用例](https://developer.twitter.com/en/use-cases/build-for-businesses) 文档。

## [!DNL Twitter] 先决条件和护栏 {#prerequisites}

您必须拥有有效的 [!DNL Twitter] 帐户，以便使用此扩展。 转到 [[!DNL Twitter] 注册页面](https://help.twitter.com/en/using-twitter/create-twitter-account) 以注册并创建帐户（如果尚未注册）。

您必须将帐户设置为 [!DNL Twitter] 开发人员帐户。 要了解如何注册为开发人员，请参阅 [[!DNL Twitter] 开发人员帐户](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### API护栏 {#guardrails}

此 [!DNL Twitter] Web转换API的速率限制为每15分钟间隔60,000个请求，其中每个请求允许500个事件。

### 收集所需的配置详细信息 {#configuration-details}

为了将Experience Platform连接到 [!DNL Twitter]时，需要以下输入值：

| 键类型 | 描述 |
| --- | --- |
| 使用者密钥 | 应用程序&#x200B;的API密钥，用于访问 [!DNL Twitter] API。 请参阅 [!DNL Twitter] 文档 [api密钥和密钥](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) 作为指导。 | |
| 使用者密码 | API密钥允许您的应用程序访问 [!DNL Twitter] API。 请参阅 [!DNL Twitter] 文档 [api密钥和密钥](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) 作为指导。 |
| 令牌密码 | 应用程序的不会过期的令牌密码，用于对进行身份验证 [!DNL Twitter] 通过OAuth的API。 请参阅 [!DNL Twitter] 文档 [获取使用访问令牌](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) 作为指导。 |
| 访问令牌 | 应用程序的不会过期的访问令牌，用于对进行身份验证 [!DNL Twitter] 通过OAuth的API。 请参阅 [!DNL Twitter] 文档 [获取使用访问令牌](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) 作为指导。 |
| 像素ID | 此 [!DNL Twitter] 像素是在您的网站上实施的网站标记，用于跟踪网站操作或转化。 请参阅 [!DNL Twitter] 文档 [网站的转化跟踪](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) 作为指导。 |

## 安装和配置 [!DNL Twitter] 扩展 {#install}

要安装扩展， [创建事件转发属性](../../../ui/event-forwarding/overview.md#properties) 或者选择现有的属性进行编辑。

选择 **[!UICONTROL 扩展]** 在左侧导航中。 在 **[!UICONTROL 目录]** 选项卡，选择 **[!UICONTROL 安装]** 在的卡片上 [!DNL Twitter] 扩展。

![目录显示 [!DNL Twitter] 扩展突出显示安装。](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>根据您的实施需求，您可能需要在配置扩展之前创建架构、数据元素和数据集。 请在开始之前查看所有配置步骤，以确定需要为用例设置哪些实体。

在下一个屏幕上，输入以下内容 [配置值](#configuration-details) 您之前收集到的 [!DNL Twitter]：

* **[!UICONTROL 像素ID]**
* **[!UICONTROL 使用者密钥]**
* **[!UICONTROL 使用者密码]**
* **[!UICONTROL 令牌]**
* **[!UICONTROL 令牌密码]**

完成后，选择 **[!UICONTROL 保存]**.

![[!DNL Twitter] 的配置屏幕 [!DNL Twitter] 扩展。](../../../images/extensions/server/twitter/configure.png)

## 配置事件转发规则 {#config-rule}

设置完所有数据元素后，您可以开始创建事件转发规则，以确定将事件发送到的时间和方式 [!DNL Twitter].

新建 [规则](../../../ui/managing-resources/rules.md) 在事件转发属性中。 下 **[!UICONTROL 操作]**，添加新操作并将扩展设置为 **[!UICONTROL twitter]**. 要将Edge Network事件发送到 [!DNL Twitter]，设置 **[!UICONTROL 操作类型]** 到 **[!UICONTROL 发送Web转换].**

选择后，会显示其他控件以进一步配置事件。 您需要映射 [!DNL Twitter] 事件属性到您之前创建的数据元素。 欲了解更多信息，请参见 [[!DNL Twitter] Web转换API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![此 [!DNL Twitter] 创建转化事件规则。](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL 用户标识]**

| 字段名称 | 描述 | 示例 | 必需 |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] 点击ID] | [!DNL Twitter] 点进URL中解析的点击ID。 | 26l6412g5p4iyj65a2oic2ayg2 | 如果未添加其他标识符，则此为必填字段。 |
| [!UICONTROL 电子邮件] | 使用SHA256进行哈希处理的电子邮件地址。 文本必须为小写，并且必须在进行哈希处理之前删除任何尾随或前导空格。 | eventforwarding@example.com | 如果未添加其他标识符，则此为必填字段。 |
| [!UICONTROL 电话] | 电话用作匹配转化事件的标识符。 电话号码必须为E164格式[+][国家/地区代码][区号][local phone number] 进行哈希处理之前。 | +911234567875 | 如果未添加其他标识符，则此为必填字段。 |

**[!UICONTROL 转化数据]**

| 字段名称 | 描述 | 示例 | 必需 |
| --- | --- | --- | --- |
| [!UICONTROL 转化时间] | ISO 8601或中的字符串形式的日期时间 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 格式。 | 2022-02-18T01:14:00.603赫 | 是 |
| [!UICONTROL 事件ID] | 特定事件的以36为底的ID。 此ID应该与ID中包含的预配置事件匹配。 [!DNL Twitter] 广告帐户。 这称为事件管理器中相应事件的ID。 | o87ne或tw-o8z6j-o87ne (tw-pixel_id-event-id) | 是 |
| [!UICONTROL 项目数] | 在事件中购买的项目数。 该值必须为大于0的正数。 | 4 | 否 |
| [!UICONTROL 货币] | 在事件中购买项目的货币。 这以ISO-4217表示，如果未提供，则默认为USD。 | 美元 | 否 |
| [!UICONTROL 值] | 在事件中购买项目的价格值。 | 100.00 | 否 |
| [!UICONTROL 转换ID] | 转化事件的标识符，可用于同一事件标记中Web像素转化和转化API转化之间的重复数据删除。 | 23294827 | 否 |
| [!UICONTROL 描述] | 包含有关转化的任何其他信息的描述。 | 测试转换 | 否 |

## 验证中的数据 [!DNL Twitter]

创建并执行事件转发规则后，验证是否已将事件发送到 [!DNL Twitter] API按预期显示在中 [!DNL Twitter] UI。

如果事件集合和 [!DNL Experience Platform] 集成成功，您将会在 [!DNL Twitter] [!UICONTROL 事件管理器].

![此 [!DNL Twitter] 事件管理器](../../../images/extensions/server/twitter/event-manager.png)

## 后续步骤

本指南介绍了如何将转化事件发送到 [!DNL Twitter] 使用事件转发。 有关这些底层技术的更多信息，请参阅官方文档：

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] Web转换API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] 用户访问令牌](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [像素ID和转化跟踪](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
