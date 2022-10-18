---
title: Zendesk事件转发扩展
description: 适用于Adobe Experience Platform的Zendesk事件转发扩展。
source-git-commit: ae585660bbf057f25e6f0dfc2520e6bb0af9d8d0
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 6%

---

# [!DNL Zendesk] 事件API扩展概述

[曾代克](https://www.zendesk.com) 是客户服务解决方案和销售工具。 森德克酒店 [事件转发](../../../ui/event-forwarding/overview.md) 扩展利用 [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) 将事件从Adobe Experience Platform边缘网络发送到Zendesk以进一步处理。 您可以使用扩展收集客户配置文件交互，以用于下游分析和操作。

本文档介绍如何在UI中安装和配置扩展。

## 先决条件

您必须拥有Zendesk帐户才能使用此扩展。 您可以在 [Zendesk网站](https://www.zendesk.com/register/).

您还必须收集Zendesk配置的以下详细信息：

| 键类型 | 描述 | 示例 |
| --- | --- | --- |
| Subdomain | 在注册过程中， **子域** 是特定于帐户创建的。 请参阅 [Zendesk文档](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) 以了解更多信息。 | `xxxxx.zendesk.com` (其中 `xxxxx` 是在帐户创建期间提供的值) |
| API令牌 | Zendesk使用不记名令牌作为验证机制与Zendesk API通信。 登录到Zendesk门户后，生成API令牌。 请参阅 [Zendesk文档](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) 以了解更多信息。 | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style=&quot;table-layout:auto&quot;}

最后，您必须为API令牌创建事件转发密钥。 将密钥类型设置为 **[!UICONTROL 令牌]**，并将值设置为从Zendesk配置收集的API令牌。 请参阅 [事件转发中的机密](../../../ui/event-forwarding/secrets.md) 有关配置密钥的更多详细信息。

## 安装扩展 {#install}

要在UI中安装Zendesk扩展，请导航至 **事件转发** ，然后选择要将扩展添加到的资产，或改为创建新资产。

选择或创建所需的资产后，导航到 **扩展** > **目录**. 搜索“[!DNL Zendesk]&quot;，然后选择 **[!DNL Install]** 在Zendesk扩展上。

![在UI中为正在选择的Zendesk扩展安装按钮](../../../images/extensions/zendesk/install.png)

## 配置扩展 {#configure}

>[!IMPORTANT]
>
>根据您的实施需求，您可能需要先创建架构、数据元素和数据集，然后再配置该扩展。 请在开始之前查看所有配置步骤，以确定您需要为用例设置哪些实体。

选择 **扩展** 中。 在 **已安装**，选择 **配置** 在Zendesk扩展上。

![为在UI中选择的Zendesk扩展配置按钮](../../../images/extensions/zendesk/configure.png)

在 **[!UICONTROL Zendesk域]**，输入Zendesk子域的值。 在 **[!UICONTROL Zendesk令牌]**，选择之前创建的包含API令牌的密钥。

![在UI中填写的配置选项](../../../images/extensions/zendesk/input.png)

## 配置事件转发规则

开始创建新的事件转发规则 [规则](../../../ui/managing-resources/rules.md) 并根据需要配置其条件。 为规则选择操作时，选择 [!UICONTROL Splunk] 扩展，然后选择 [!UICONTROL 创建事件] 操作类型。

![定义规则](../../../images/extensions/zendesk/rule.png)

在设置操作配置时，系统会提示您将数据元素分配给将发送到Zendesk的各种属性。

![定义操作配置](../../../images/extensions/zendesk/action-configurations.png)

这些数据元素应按照以下引用进行映射。

### `event` 键

`event` 是一个JSON对象，表示用户触发的事件。 请参阅 [事件剖析](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/) ，以了解 `event` 对象。

可以在 `event` 对象：在映射到数据元素时：

| `event` key | 类型 | 平台路径 | 描述 | 必需 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字符串 | `arc.event.xdm._extconndev.event_source` | 发送事件的应用程序。 | 是 | 请勿使用 `Zendesk` 作为值，因为它是Zendesk标准事件的受保护源名称。 尝试使用该插件将会导致错误。<br>值长度不得超过40个字符。 |
| `type` | 字符串 | `arc.event.xdm._extconndev.event_type` | 事件类型的名称。 您可以使用此字段表示给定源的不同事件类型。 例如，您可以为用户登录创建一组事件，为购物车创建另一组事件。 | 是 | 值长度不得超过40个字符。 |
| `description` | 字符串 | `arc.event.xdm._extconndev.description` | 事件的描述。 | 否 | (不适用) |
| `created_at` | 字符串 | `arc.event.xdm.timestamp` | 反映事件创建时间的ISO-8601时间戳。 | 否 | (不适用) |
| `properties` | 对象 | `arc.event.xdm._extconndev.EventProperties` | 包含事件详细信息的自定义JSON对象。 | 是 | (不适用) |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>请参阅 [[!DNL Zendesk Events API] 文档](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) 以了解有关事件属性的其他指导。

### `profile` 键

`profile` 是一个JSON对象，表示触发该事件的用户。 请参阅 [剖面图](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/) ，以了解 `profile` 对象。

可以在 `profile` 对象：在映射到数据元素时：

| `profile` key | 类型 | 平台路径 | 描述 | 必需 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字符串 | `arc.event.xdm._extconndev.profile_source` | 与用户档案关联的产品或服务，例如 `Support`, `CompanyName`或 `Chat`. | 是 | (不适用) |
| `type` | 字符串 | `arc.event.xdm._extconndev.profile_type` | 配置文件类型的名称。 您可以使用此字段为给定源创建不同类型的用户档案。 例如，您可以为客户创建一组公司用户档案，为员工创建另一组公司用户档案。 | 是 | 配置文件类型长度不得超过40个字符。 |
| `name` | 字符串 | `arc.event.xdm._extconndev.name` | 用户档案中的人员姓名 | 否 | (不适用) |
| `user_id` | 字符串 | `arc.event.xdm._extconndev.user_id` | Zendesk中人员的用户ID。 | 否 | (不适用) |
| `identifiers` | 数组 | `arc.event.xdm._extconndev.identifiers` | 包含至少一个标识符的数组。 每个标识符都包含类型和值。 | 是 | 请参阅 [Zendesk文档](https://developer.zendesk.com/api-reference/custom-data/profiles_api/profiles_api/#identifiers-array) ，以了解有关 `identifiers` 数组。 所有字段和值必须唯一。 |
| `attributes` | 对象 | `arc.event.xdm._extconndev.attrbutes` | 包含用户定义的人员属性的对象。 | 否 | 请参阅 [Zendesk文档](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/#attributes) 以了解有关配置文件属性的更多信息。 |

{style=&quot;table-layout:auto&quot;}

## 在Zendesk中验证数据 {#validate}

如果事件收集和Adobe Experience Platform集成成功，则Zendesk控制台中的事件应显示如下。 这表示集成成功。

用户档案:

![“Zendesk配置文件”页面](../../../images/extensions/zendesk/zendesk-profiles.png)

事件：

![“Zendesk事件”页](../../../images/extensions/zendesk/zendesk-events.png)

## 请求限制 {#limits}

根据帐户类型，Zendesk [!DNL Events API] 每分钟可以处理以下请求数：

| [!DNL Account Type] | 每分钟的请求数 |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style=&quot;table-layout:auto&quot;}

请参阅 [Zendesk文档](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) 以了解有关这些限制的更多信息。

## 错误和疑难解答 {#errors-and-troubleshooting}

使用或配置扩展时，Zendesk事件API可能会返回以下错误：

| 错误代码 | 描述 | 分辨率 | 示例 |
|---|---|---|---|
| 400 | **配置文件长度无效：** 当配置文件属性的长度包含的字符数超过40个时，会发生此错误。 | 将配置文件属性数据的长度限制为最多40个字符。 | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **未找到路由：** 提供无效域时，会发生此错误。 | 确认以下格式提供了有效域： `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **身份验证无效或缺失：** 访问令牌无效、缺失或过期时会出现此错误。 | 验证访问令牌是否有效且未过期。 | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **权限不足：** 如果未提供足够的访问资源的权限，则会出现此错误。 | 验证是否已提供所需的权限。 | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **请求过多：** 超出端点对象记录限制时会发生此错误。 | 请参阅上文中关于 [请求限制](#limits) 有关每个限制阈值的详细信息。 | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style=&quot;table-layout:auto&quot;}

## 后续步骤

本文档介绍了如何在UI中安装和配置Zendesk事件转发扩展。 有关在Zendesk中收集事件数据的更多信息，请参阅官方文档：

* [事件入门](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [Zendesk事件API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/)
* [关于事件API](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [事件剖析](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [Zendesk Profiles API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/#profile-object)
* [关于用户档案API](https://developer.zendesk.com/documentation/custom-data/profiles/about-the-profiles-api/)
* [剖面图](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/)
