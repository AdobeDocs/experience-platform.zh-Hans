---
title: Mailchimp扩展概述
description: 使用事件转发来触发Mailchimp电子邮件。
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 5%

---

# Mailchimp事件转发扩展概述

>[!NOTE]
>  
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

邮差 [事件转发](../../../ui/event-forwarding/overview.md) 扩展将事件发送到Mailchimp营销API，这可以触发Mailchimp营销活动、历程或交易的电子邮件。

本文档介绍了如何使用Add Event操作设置扩展和配置规则。

## 先决条件

本文档假设您熟悉该扩展使用的相关Mailchimp产品。 有关更多信息，请参阅Mailchimp帮助文档 [营销活动](https://mailchimp.com/help/getting-started-with-campaigns/)， [历程](https://mailchimp.com/help/about-customer-journeys/)、和 [事务](https://mailchimp.com/help/transactional/).

使用此扩展需要Mailchimp帐户。 您可以注册帐户 [此处](https://login.mailchimp.com/signup/). 在Mailchimp帐户仪表板中，记下以下值以用于本指南：

- 您的Mailchimp域前缀
- 您的API密钥
- 受众ID
- 默认的“发件人”电子邮件地址

根据您的Mailchimp帐户计划，您对Mailchimp客户历程工具的访问权限可能会受到限制。

>[!TIP]
>  
>如果您使用Mailchimp自动化，如事务性电子邮件或客户历程，则步骤和屏幕可能稍有不同，此处列出。 但是，要使用此扩展，您仍然需要上述相同的信息。 请参阅 [Mailchimp帮助中心](https://mailchimp.com/help/) 以了解有关您的特定帐户和计划的每个值的详细信息。

### 域前缀

登录Mailchimp并登录仪表板视图后，浏览器的地址栏应显示URL，如 `https://us11.admin.mailchimp.com` 或只是 `us11.admin.mailchimp.com`. 在此示例中，前缀 `us11` 只是一个占位符，您的值将有所不同。 请用您的前缀记录您的URL，以供后续步骤使用。

### API密钥

要查找您帐户的API密钥，请在Mailchimp UI中选择您的配置文件图标，然后选择 **个人资料**. 您应会看到URL，如下所示 `https://us11.admin.mailchimp.com/account/profile/` 但使用 **您的** 前缀而不是 `us11`.

选择 **其他内容**，则 **API密钥**：

![附加菜单， API密钥链接](../../../images/extensions/server/mailchimp/menu-API-keys.png)

下 **您的API密钥**，您可以选择现有密钥，也可以选择 **创建密钥** 以创建一个新的存储库。 您可以创建一个新密钥，以专门用于此扩展。 复制API密钥并将其保存以供稍后步骤使用。 有关更多详细信息，请参阅Mailchimp文档，了解如何 [生成API密钥](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### 受众ID和发件人地址

选择 **Audience** 在左侧导航中，然后 **受众仪表板**. 接下来，选择要与此扩展一起使用的受众。 要了解更多信息，请参阅Mailchimp文档 [创建受众](https://mailchimp.com/help/create-audience/).

创建并选择受众后，选择 **管理受众** 下拉列表并选择 **设置**. 此屏幕显示受众的各种设置。

在“设置”屏幕底部，您应会看到 `Unique id for audience [audience name]` 位置 `[audience name]` 是实际受众的名称。 复制受众ID并将其保存以供稍后步骤使用。

选择 **受众名称和默认值** 并确认 **默认发件人电子邮件地址** 对于您的营销活动具有正确的值。 请注意，受众ID也会列在本页顶部，与您在上一步中向下复制的值相同。

## Mailchimp自动化

根据您的Mailchimp计划以及您使用事务性电子邮件、客户历程或其他Mailchimp自动化，您的特定旅程设置可能会有所不同。

>[!IMPORTANT]
>  
>您选择用于在Mailchimp中触发自动化或历程的事件名称与必须随此扩展发送的事件名称相同。 记下Mailchimp自动化中的事件名称，并将其保存以供稍后步骤使用。

## 安装和配置

此部分列出了安装和配置扩展的步骤。 要安全地保存Mailchimp API密钥，您必须使用事件转发 [密钥](../../../ui/event-forwarding/secrets.md).

### 创建密码和数据元素

在事件转发属性中， [创建 [!UICONTROL 令牌] 密码](../../../ui/event-forwarding/secrets.md#token) 已调用 `Mailchimp API Key`.

下一步， [创建数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 使用 [!UICONTROL 核心] 扩展和 [!UICONTROL 密码] 要引用 `Mailchimp API Key` 您刚刚创建的密码。 输入 `Mailchimp Token` 作为数据元素名称。

### 安装和配置 扩展

在同一事件转发属性中，选择 **[!UICONTROL 扩展]，** 则 **[!UICONTROL 目录]** 以显示可用于安装的扩展。 在此处，搜索Mailchimp扩展并选择 **[!UICONTROL 安装]**.

![安装Mailchimp扩展](../../../images/extensions/server/mailchimp/install.png)

出现配置屏幕。 下 **[!UICONTROL Mailchimp服务器前缀域名]**，输入您之前从Mailchimp帐户复制的域，包括唯一的域前缀。

>[!IMPORTANT]
>
>不包括 `http://` 或 `https://` 在此字段中。

![扩展配置](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

下 **[!UICONTROL Mailchimp令牌]**，选择数据元素图标，然后选择 `Mailchimp Token` 您之前创建的数据元素。 选择 **[!UICONTROL 保存]** 以保存更改。

扩展现在已安装并配置为可在资产中使用。

## 数据收集

在中使用此扩展时 [规则](../../../ui/managing-resources/rules.md)，则扩展会随每个事件发送到Mailchimp的多个数据值。 对于典型实施，您可以配置 [Adobe Experience Platform Web SDK扩展](../../client/web-sdk/overview.md) 以将该数据发送至 [!DNL Platform Edge Network] 以供扩展在event forwarding属性中使用。

此扩展所需的数据可以作为XDM数据或非XDM数据从Web SDK发送。 请参阅文档以了解有关 [发送XDM数据](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

例如，如果客户购买产品或注册了您网站上的事件，则您可以使用此扩展通过Mailchimp发送确认电子邮件。 将所需信息从Web SDK发送到Edge Network后，该扩展将通过Mailchimp触发电子邮件。

![添加事件操作配置](../../../images/extensions/server/mailchimp/action-configurations.png)

### 数据元素

上一部分中的屏幕截图显示了可随每个事件从该扩展发送到Mailchimp的数据。 在配置Web SDK以将此数据发送到Edge Network后，您可以在事件转发属性中创建数据元素，以便扩展可以访问这些值。

下表提供了每个可能值的更多详细信息。

| 名称 | 示例路径 | 类型 | 描述 | 必需 | 限制 |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> 或<br /> `arc.event.data._tenant.emailId` | 字符串 | 接收电子邮件的地址 | **是** | 必须存在于Mailchimp受众中 |
| `listId` | `arc.event.xdm._tenant.listId`<br /> 或<br /> `arc.event.data._tenant.listid` | 字符串 | 受众ID | **是** | 必须匹配现有的受众ID |
| `name` | `arc.event.xdm._tenant.name`<br /> 或<br /> `arc.event.data._tenant.name` | 字符串 | 事件名称 | **是** | 2-30个字符长 |
| `properties` | `arc.event.xdm._tenant.properties`<br /> 或<br /> `arc.event.data._tenant.properties` | 对象 | JSON格式的可选属性列表，其中包含有关事件的详细信息 | 否 |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> 或<br /> `arc.event.data._tenant.isSyncing` | 布尔 | 使用创建的事件 `is_syncing` 设置为 `true` **不会** 触发自动化 | 否 |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> 或 `arc.event.data._tenant.occuredAt` | 字符串 | 事件发生时间的ISO 8601时间戳 | 否 |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>此 **示例路径** 上述值仅为示例。 字段名称和 [路径](../../../ui/event-forwarding/overview.md#data-element-path) 在这些数据元素中引用的数据在您的资产中可能会有所不同，具体取决于您在上述步骤中命名和配置Web SDK的方式。

在事件转发属性中，您可以为上述每个字段创建一个数据元素。 创建后，您可以引用以下位置中的数据元素： [!UICONTROL 添加事件] 此扩展的操作中执行了此调用。

![添加事件操作配置](../../../images/extensions/server/mailchimp/action-configurations.png)

您现在可以使用此扩展和Add Event操作来触发受众的Mailchimp电子邮件。

## 数据验证

使用事件转发扩展时， [Adobe Experience Platform调试器](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 非常有用。 在日志部分的Edge日志下，您可以看到事件转发规则在触发请求后发出的请求。 以下屏幕截图显示了扩展对Mailchimp API发出的请求。

![Adobe Experience Platform调试器](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

在Mailchimp仪表板中，受众或受众成员的“活动信息源”视图上提供了该受众或受众成员的事件列表。 这应该与扩展发送的事件匹配，并显示发送的任何可选数据以及它们收到的电子邮件或营销活动。 请参阅 [Mailchimp自动化帮助指南](https://mailchimp.com/help/automation/) 了解更多详细信息。
