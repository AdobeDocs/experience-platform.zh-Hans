---
title: Zendesk事件转发扩展
description: 适用于Adobe Experience Platform的Zendesk事件转发扩展。
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 4%

---

# [!DNL Zendesk]事件API扩展概述

[Zendesk](https://www.zendesk.com)是客户服务解决方案和销售工具。 Zendesk [事件转发](../../../ui/event-forwarding/overview.md)扩展利用[[!DNL Zendesk Events API]](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/)将事件从Adobe Experience PlatformEdge Network发送到Zendesk以进行进一步处理。 您可以使用该扩展收集客户配置文件交互，以用于下游分析和操作。

本文档介绍如何在UI中安装和配置扩展。

## 先决条件

您必须拥有Zendesk帐户才能使用此扩展。 您可以在[Zendesk网站](https://www.zendesk.com/register/)上注册Zendesk帐户。

您还必须为Zendesk配置收集以下详细信息：

| 密钥类型 | 描述 | 示例 |
| --- | --- | --- |
| Subdomain | 在注册过程中，将创建特定于帐户的唯一&#x200B;**子域**。 有关详细信息，请参阅[Zendesk文档](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/)。 | `xxxxx.zendesk.com` （其中`xxxxx`是在创建帐户期间提供的值） |
| api令牌 | Zendesk使用持有者令牌作为身份验证机制与Zendesk API通信。 登录到Zendesk门户后，生成API令牌。 有关详细信息，请参阅[Zendesk文档](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token)。 | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style="table-layout:auto"}

最后，必须为API令牌创建事件转发密码。 将密钥类型设置为&#x200B;**[!UICONTROL Token]**，并将值设置为您从Zendesk配置中收集的API令牌。 有关配置密码的更多详细信息，请参阅有关事件转发中的[密码](../../../ui/event-forwarding/secrets.md)的文档。

## 安装扩展 {#install}

要在UI中安装Zendesk扩展，请导航到&#x200B;**事件转发**，然后选择要将扩展添加到的属性，或改为创建新属性。

选择或创建所需的属性后，导航到&#x200B;**扩展** > **目录**。 搜索“[!DNL Zendesk]”，然后在Zendesk扩展中选择&#x200B;**[!DNL Install]**。

在UI中选择的Zendesk扩展的![安装按钮](../../../images/extensions/server/zendesk/install.png)

## 配置扩展 {#configure}

>[!IMPORTANT]
>
>根据您的实施需求，您可能需要在配置扩展之前创建架构、数据元素和数据集。 请在开始之前查看所有配置步骤，以确定需要为用例设置哪些实体。

在左侧导航中选择&#x200B;**扩展**。 在&#x200B;**Installed**&#x200B;下，选择Zendesk扩展上的&#x200B;**Configure**。

在UI中选择的Zendesk扩展的![配置按钮](../../../images/extensions/server/zendesk/configure.png)

在&#x200B;**[!UICONTROL Zendesk域]**&#x200B;下，输入您的Zendesk子域值。 在&#x200B;**[!UICONTROL Zendesk令牌]**&#x200B;下，选择您之前创建的包含API令牌的密码。

在UI中填写了![配置选项](../../../images/extensions/server/zendesk/input.png)

## 配置事件转发规则

开始创建新的事件转发规则[规则](../../../ui/managing-resources/rules.md)，并根据需要配置其条件。 为规则选择操作时，请选择[!UICONTROL Zendesk]扩展，然后选择[!UICONTROL 创建事件]操作类型。

![定义规则](../../../images/extensions/server/zendesk/rule.png)

设置操作配置时，系统会提示您将数据元素分配给将发送到Zendesk的各种属性。

![定义操作配置](../../../images/extensions/server/zendesk/action-configurations.png)

这些数据元素应该按照以下方式映射。

### `event`键

`event`是一个JSON对象，它表示用户触发的事件。 有关`event`对象捕获的属性的详细信息，请参阅事件[&#128279;](https://developer.zendesk.com/documentation/ticketing/events/anatomy-of-an-event/)的剖析Zendesk文档。

映射到数据元素时，可以在`event`对象中引用以下键：

| `event`键 | 类型 | 平台路径 | 描述 | 必需 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字符串 | `arc.event.xdm._extconndev.event_source` | 发送事件的应用程序。 | 是 | 请勿使用`Zendesk`作为值，因为它是Zendesk标准事件的受保护源名称。 尝试使用它会导致错误。<br>值长度不能超过40个字符。 |
| `type` | 字符串 | `arc.event.xdm._extconndev.event_type` | 事件类型的名称。 您可以使用此字段表示给定源的不同类型的事件。 例如，您可以为用户登录创建一组事件，为购物车创建另一组事件。 | 是 | 值长度不得超过40个字符。 |
| `description` | 字符串 | `arc.event.xdm._extconndev.description` | 事件的描述。 | 否 | （不适用） |
| `created_at` | 字符串 | `arc.event.xdm.timestamp` | 反映事件创建时间的ISO-8601时间戳。 | 否 | （不适用） |
| `properties` | 对象 | `arc.event.xdm._extconndev.EventProperties` | 包含有关事件的详细信息的自定义JSON对象。 | 是 | （不适用） |

{style="table-layout:auto"}

>[!NOTE]
>
>有关事件属性的其他指导，请参阅[[!DNL Zendesk Events API] 文档](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/)。

### `profile`键

`profile`是一个JSON对象，它表示触发事件的用户。 有关`profile`对象捕获的属性的详细信息，请参阅配置文件[&#128279;](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/)的剖析Zendesk文档。

映射到数据元素时，可以在`profile`对象中引用以下键：

| `profile`键 | 类型 | 平台路径 | 描述 | 必需 | 限制 |
| --- | --- | --- | --- | --- | --- |
| `source` | 字符串 | `arc.event.xdm._extconndev.profile_source` | 与配置文件关联的产品或服务，如`Support`、`CompanyName`或`Chat`。 | 是 | （不适用） |
| `type` | 字符串 | `arc.event.xdm._extconndev.profile_type` | 配置文件类型的名称。 您可以使用此字段为给定源创建不同类型的配置文件。 例如，您可以为客户创建一组公司配置文件，为员工创建另一组公司配置文件。 | 是 | 配置文件类型长度不得超过40个字符。 |
| `name` | 字符串 | `arc.event.xdm._extconndev.name` | 个人资料中的人员姓名 | 否 | （不适用） |
| `user_id` | 字符串 | `arc.event.xdm._extconndev.user_id` | Zendesk中的人员的用户ID。 | 否 | （不适用） |
| `identifiers` | 数组 | `arc.event.xdm._extconndev.identifiers` | 至少包含一个标识符的数组。 每个标识符都由类型和值组成。 | 是 | 有关`identifiers`数组的详细信息，请参阅[Zendesk文档](https://developer.zendesk.com/api-reference/ticketing/users/profiles_api/profiles_api/#identifiers-array)。 所有字段和值都必须是唯一的。 |
| `attributes` | 对象 | `arc.event.xdm._extconndev.attrbutes` | 包含有关人员的用户定义的属性的对象。 | 否 | 有关配置文件属性的更多信息，请参阅[Zendesk文档](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/#attributes)。 |

{style="table-layout:auto"}

## 验证Zendesk中的数据 {#validate}

如果事件收集和Adobe Experience Platform集成成功，则Zendesk控制台中的事件应如下所示。 这表示集成成功。

配置文件：

![Zendesk配置文件页面](../../../images/extensions/server/zendesk/zendesk-profiles.png)

事件：

![Zendesk活动页面](../../../images/extensions/server/zendesk/zendesk-events.png)

## 请求限制 {#limits}

根据帐户类型，Zendesk [!DNL Events API]可以处理以下每分钟请求数：

| [!DNL Account Type] | 每分钟请求数 |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style="table-layout:auto"}

有关这些限制的详细信息，请参阅[Zendesk文档](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.)。

## 错误和故障排除 {#errors-and-troubleshooting}

使用或配置扩展时，Zendesk Events API可能会返回以下错误：

| 错误代码 | 描述 | 解决方法 | 示例 |
|---|---|---|---|
| 400 | **配置文件长度无效：**&#x200B;当配置文件属性的长度超过40个字符时，会发生此错误。 | 将配置文件属性数据的长度限制为最多40个字符。 | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **未找到路由：**&#x200B;当提供的域无效时，会发生此错误。 | 验证是否按以下格式提供了有效的域： `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **无效或缺少身份验证：**&#x200B;当访问令牌无效、缺失或过期时，会发生此错误。 | 验证访问令牌是否有效且未过期。 | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **权限不足：**&#x200B;当没有提供足够的权限来访问资源时，会发生此错误。 | 验证是否已提供所需的权限。 | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **请求太多：**&#x200B;当超过终结点对象记录限制时，会发生此错误。 | 有关每限制阈值的详细信息，请参阅上文关于[请求限制](#limits)的部分。 | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style="table-layout:auto"}

## 后续步骤

本文档介绍了如何在UI中安装和配置Zendesk事件转发扩展。 有关在Zendesk中收集事件数据的更多信息，请参阅官方文档：

* [事件入门](https://developer.zendesk.com/documentation/ticketing/events/getting-started-with-events/)
* [Zendesk事件API](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/)
* [关于事件API](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/)
* [事件的剖析](https://developer.zendesk.com/documentation/ticketing/events/anatomy-of-an-event/)
* [Zendesk配置文件API](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/#profile-object)
* [关于配置文件API](https://developer.zendesk.com/documentation/ticketing/profiles/about-the-profiles-api/)
* [个人资料剖析](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/)
