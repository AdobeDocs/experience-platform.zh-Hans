---
title: Zendesk事件转发扩展
description: 适用于Adobe Experience Platform的Zendesk事件转发扩展。
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 5%

---

# [!DNL Zendesk] Events API扩展概述

[Zendesk](https://www.zendesk.com) 是一个客户服务解决方案和销售工具。 Zendesk [事件转发](../../../ui/event-forwarding/overview.md) 扩展可利用 [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) 将事件从Adobe Experience Platform Edge Network发送到Zendesk以供进一步处理。 您可以使用该扩展收集客户配置文件交互，以用于下游分析和操作。

本文档介绍如何在UI中安装和配置扩展。

## 先决条件

您必须拥有Zendesk帐户才能使用此扩展。 您可以在以下网址注册Zendesk帐户： [Zendesk网站](https://www.zendesk.com/register/).

您还必须为Zendesk配置收集以下详细信息：

| 键类型 | 描述 | 示例 |
| --- | --- | --- |
| Subdomain | 在注册过程中， **子域** 创建时特定于帐户。 请参阅 [Zendesk文档](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) 了解更多信息。 | `xxxxx.zendesk.com` (其中 `xxxxx` 是在帐户创建期间提供的值) |
| api令牌 | Zendesk使用持有者令牌作为身份验证机制与Zendesk API通信。 登录到Zendesk门户后，生成API令牌。 请参阅 [Zendesk文档](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) 了解更多信息。 | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style="table-layout:auto"}

最后，必须为API令牌创建事件转发密码。 将密码类型设置为 **[!UICONTROL 令牌]**，并将值设置为您从Zendesk配置收集的API令牌。 请参阅以下文档： [事件转发中的密钥](../../../ui/event-forwarding/secrets.md) 有关配置密钥的更多详细信息。

## 安装扩展 {#install}

要在UI中安装Zendesk扩展，请导航到 **事件转发** ，然后选择要为其添加扩展的资产，或改为创建新资产。

选择或创建所需的属性后，导航到 **扩展** > **目录**. 搜索“”[!DNL Zendesk]&quot;，然后选择 **[!DNL Install]** 在Zendesk扩展上。

![在UI中选择的Zendesk扩展的“安装”按钮](../../../images/extensions/server/zendesk/install.png)

## 配置扩展 {#configure}

>[!IMPORTANT]
>
>根据您的实施需求，您可能需要在配置扩展之前创建架构、数据元素和数据集。 请在开始之前查看所有配置步骤，以确定需要为用例设置哪些实体。

选择 **扩展** 左侧导航栏中。 下 **已安装**，选择 **配置** 在Zendesk扩展中。

![用于在UI中选择的Zendesk扩展的“配置”按钮](../../../images/extensions/server/zendesk/configure.png)

下 **[!UICONTROL Zendesk域]**，输入您的Zendesk子域的值。 下 **[!UICONTROL Zendesk令牌]**，选择您之前创建的包含API令牌的密码。

![配置选项已在UI中填写](../../../images/extensions/server/zendesk/input.png)

## 配置事件转发规则

开始创建新的事件转发规则 [规则](../../../ui/managing-resources/rules.md) 并根据需要配置其条件。 为规则选择操作时，选择 [!UICONTROL Zendesk] 扩展，然后选择 [!UICONTROL 创建事件] 操作类型。

![定义规则](../../../images/extensions/server/zendesk/rule.png)

设置操作配置时，系统会提示您将数据元素分配给将发送到Zendesk的各种属性。

![定义操作配置](../../../images/extensions/server/zendesk/action-configurations.png)

这些数据元素应该映射，如下所述。

### `event` 键

`event` 是一个JSON对象，它表示用户触发的事件。 请参阅Zendesk文档 [事件的剖析](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/) 以获取有关所捕获属性的详细信息， `event` 对象。

以下键值可在中引用 `event` 数据元素时的对象：

| `event` key | 类型 | 平台路径 | 描述 | 必需 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字符串 | `arc.event.xdm._extconndev.event_source` | 发送事件的应用程序。 | 是 | 不使用 `Zendesk` 作为值，因为它是Zendesk标准事件的受保护源名称。 尝试使用它会导致错误。<br>值长度不得超过40个字符。 |
| `type` | 字符串 | `arc.event.xdm._extconndev.event_type` | 事件类型的名称。 您可以使用此字段表示给定源的不同类型的事件。 例如，您可以为用户登录创建一组事件，为购物车创建另一组事件。 | 是 | 值长度不得超过40个字符。 |
| `description` | 字符串 | `arc.event.xdm._extconndev.description` | 事件的描述。 | 否 | (不适用) |
| `created_at` | 字符串 | `arc.event.xdm.timestamp` | 反映事件创建时间的ISO-8601时间戳。 | 否 | (不适用) |
| `properties` | 对象 | `arc.event.xdm._extconndev.EventProperties` | 一个自定义JSON对象，其中包含有关事件的详细信息。 | 是 | (不适用) |

{style="table-layout:auto"}

>[!NOTE]
>
>请参阅 [[!DNL Zendesk Events API] 文档](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) 以获取有关事件属性的其他指南。

### `profile` 键

`profile` 是一个JSON对象，它表示触发事件的用户。 请参阅Zendesk文档 [轮廓剖析](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/) 以获取有关所捕获属性的详细信息， `profile` 对象。

以下键值可在中引用 `profile` 数据元素时的对象：

| `profile` key | 类型 | 平台路径 | 描述 | 必需 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字符串 | `arc.event.xdm._extconndev.profile_source` | 与配置文件关联的产品或服务，例如 `Support`， `CompanyName`，或 `Chat`. | 是 | (不适用) |
| `type` | 字符串 | `arc.event.xdm._extconndev.profile_type` | 配置文件类型的名称。 您可以使用此字段为给定源创建不同类型的配置文件。 例如，您可以为客户创建一组公司配置文件，为员工创建另一组公司配置文件。 | 是 | 配置文件类型长度不得超过40个字符。 |
| `name` | 字符串 | `arc.event.xdm._extconndev.name` | 个人资料中的人员姓名 | 否 | (不适用) |
| `user_id` | 字符串 | `arc.event.xdm._extconndev.user_id` | Zendesk中的人员的用户ID。 | 否 | (不适用) |
| `identifiers` | 数组 | `arc.event.xdm._extconndev.identifiers` | 至少包含一个标识符的数组。 每个标识符都由一个类型和值组成。 | 是 | 请参阅 [Zendesk文档](https://developer.zendesk.com/api-reference/custom-data/profiles_api/profiles_api/#identifiers-array) 欲知关于 `identifiers` 数组。 所有字段和值都必须是唯一的。 |
| `attributes` | 对象 | `arc.event.xdm._extconndev.attrbutes` | 包含有关人员的用户定义的属性的对象。 | 否 | 请参阅 [Zendesk文档](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/#attributes) 以了解有关配置文件属性的更多信息。 |

{style="table-layout:auto"}

## 验证Zendesk中的数据 {#validate}

如果事件收集和Adobe Experience Platform集成成功，则Zendesk控制台中的事件应如下所示。 这表示集成成功。

用户档案:

![Zendesk配置文件页面](../../../images/extensions/server/zendesk/zendesk-profiles.png)

事件：

![Zendesk事件页面](../../../images/extensions/server/zendesk/zendesk-events.png)

## 请求限制 {#limits}

根据帐户类型，Zendesk [!DNL Events API] 可以处理以下每分钟请求数：

| [!DNL Account Type] | 每分钟请求数 |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style="table-layout:auto"}

请参阅 [Zendesk文档](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) 以了解有关这些限制的详细信息。

## 错误和疑难解答 {#errors-and-troubleshooting}

使用或配置扩展时，Zendesk Events API可能会返回以下错误：

| 错误代码 | 描述 | 解决方法 | 示例 |
|---|---|---|---|
| 400 | **配置文件长度无效：** 当配置文件属性的长度包含超过40个字符时，会发生此错误。 | 将配置文件属性数据的长度限制为最多40个字符。 | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **未找到路由：** 当提供了无效的域时，会发生此错误。 | 验证是否以下列格式提供了有效的域： `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **身份验证无效或缺失：** 当访问令牌无效、缺失或过期时，会发生此错误。 | 验证访问令牌是否有效且未过期。 | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **权限不足：** 当未提供足够的权限来访问资源时，会发生此错误。 | 验证是否已提供所需的权限。 | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **请求过多：** 当超过终结点对象记录限制时，会发生此错误。 | 请参阅上文关于 [请求限制](#limits) 以了解有关每限制阈值的详细信息。 | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style="table-layout:auto"}

## 后续步骤

本文档介绍了如何在UI中安装和配置Zendesk事件转发扩展。 有关在Zendesk中收集事件数据的更多信息，请参阅官方文档：

* [事件快速入门](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [Zendesk Events API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/)
* [关于事件API](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [事件的剖析](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [Zendesk配置文件API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/#profile-object)
* [关于配置文件API](https://developer.zendesk.com/documentation/custom-data/profiles/about-the-profiles-api/)
* [轮廓剖析](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/)
