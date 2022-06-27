---
title: Mailchimp扩展概述
description: 使用事件转发触发Mailchimp电子邮件。
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
source-git-commit: b445e25ebda39e1604b926dc40d8ed52ad2e9b54
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 5%

---

# Mailchimp事件转发扩展概述

>[!NOTE]
>  
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

《邮箱》 [事件转发](../../../ui/event-forwarding/overview.md) 扩展会向Mailchimp营销API发送事件，以触发Mailchimp营销活动、历程或交易的电子邮件。

本文档介绍如何使用Add Event操作设置扩展和配置规则。

## 先决条件

本文档假定您熟悉扩展利用的相关Mailchimp产品。 有关详细信息，请参阅 [营销活动](https://mailchimp.com/help/getting-started-with-campaigns/), [历程](https://mailchimp.com/help/about-customer-journeys/)和 [交易](https://mailchimp.com/help/transactional/).

使用此扩展需要Mailchimp帐户。 您可以注册帐户 [此处](https://login.mailchimp.com/signup/). 在Mailchimp帐户仪表板中，记下以下值以供在本指南中使用：

- 您的Mailchimp域前缀
- 您的API密钥
- 受众ID
- 默认的“发件人”电子邮件地址

根据您的Mailchimp帐户计划，您可能对Mailchimp客户历程工具的访问有限。

>[!TIP]
>  
>如果您使用Mailchimp自动化(如事务性电子邮件或客户历程)，则步骤和屏幕可能会与此处列出的步骤和屏幕略有不同。 但是，要使用此扩展，您仍需要相同的信息，如上所述。 请参阅 [Mailchimp帮助中心](https://mailchimp.com/help/) 以了解您特定帐户和计划中每个值的详细信息。

### 域前缀

登录到Mailchimp并登录到功能板视图后，浏览器的地址栏应显示如下URL `https://us11.admin.mailchimp.com` 或 `us11.admin.mailchimp.com`. 在本例中，前缀为 `us11` 只是占位符，且值将不同。 在URL中记录前缀，以备稍后执行步骤。

### API密钥

要查找您帐户的API密钥，请在Mailchimp UI中选择您的配置文件图标，然后选择 **用户档案**. 您应会看到类似 `https://us11.admin.mailchimp.com/account/profile/` 但 **您的** 前缀，而不是 `us11`.

选择 **额外信息**，则 **API密钥**:

![“额外”菜单、API密钥链接](../../../images/extensions/mailchimp/menu-API-keys.png)

在 **您的API密钥**，则可以选择现有键或选择 **创建键** 来创建新受众。 您可以创建一个新键，以专门与此扩展一起使用。 复制API密钥并保存该密钥，以供稍后步骤使用。 有关更多详细信息，请参阅Mailchimp文档，其中介绍了如何 [生成API密钥](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### 受众ID和发件人地址

选择 **受众** ，然后 **受众仪表板**. 接下来，选择要与此扩展一起使用的受众。 要了解更多信息，请参阅Mailchimp文档 [创建受众](https://mailchimp.com/help/create-audience/).

创建并选择受众后，选择 **管理受众** 下拉列表和选择 **设置**. 此屏幕显示受众的各种设置。

在“设置”屏幕的底部，您应会看到 `Unique id for audience [audience name]` where `[audience name]` 是实际受众的名称。 复制受众ID并保存该ID，以供稍后步骤使用。

选择 **受众名称和默认值** 并确认 **默认发件人电子邮件地址** 的值正确。 请注意，受众ID也会列在此页面顶部，它与您在上一步中向下复制的值相同。

## Mailchimp自动化

根据您的Mailchimp计划以及您是使用事务型电子邮件、客户历程还是其他Mailchimp自动化，您的特定历程设置可能会有所不同。

>[!IMPORTANT]
>  
>您选择在Mailchimp中触发自动化或历程的事件名称，与必须随此扩展一起发送的事件名称相同。 记下Mailchimp自动化中的事件名称，并保存该名称以供稍后步骤使用。

## 安装和配置

此部分列出了安装和配置扩展的步骤。 要安全地保存Mailchimp API密钥，您必须使用事件转发 [秘密](../../../ui/event-forwarding/secrets.md).

### 创建密钥和数据元素

在事件转发属性中， [创建 [!UICONTROL 令牌] 秘密](../../../ui/event-forwarding/secrets.md#token) 调用 `Mailchimp API Key`.

下一个， [创建数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 使用 [!UICONTROL 核心] 扩展和 [!UICONTROL 密码] 要引用的数据元素类型 `Mailchimp API Key` 你刚刚创造的秘密。 输入 `Mailchimp Token` 作为数据元素名称。

### 安装和配置 扩展

在同一事件转发属性中，选择 **[!UICONTROL 扩展],** then **[!UICONTROL 目录]** 以显示可用于安装的扩展。 从此处，搜索Mailchimp扩展并选择 **[!UICONTROL 安装]**.

![安装Mailchimp扩展](../../../images/extensions/mailchimp/install.png)

出现配置屏幕。 在 **[!UICONTROL Mailchimp服务器前缀域名]**，输入您之前从Mailchimp帐户复制的域，包括您的唯一域前缀。

>[!IMPORTANT]
>
>不包括 `http://` 或 `https://` 中。

![扩展配置](../../../images/extensions/mailchimp/mailchimp-domain.png)

在 **[!UICONTROL 邮件令牌]**，选择数据元素图标，然后选择 `Mailchimp Token` 您之前创建的数据元素。 选择 **[!UICONTROL 保存]** 以保存更改。

现在，已安装并配置该扩展以在您的资产中使用。

## 数据收集

在 [规则](../../../ui/managing-resources/rules.md)，扩展会随每个事件向Mailchimp发送多个数据值。 对于典型的实施，您可以配置 [Adobe Experience Platform Web SDK扩展](../sdk/overview.md) 将数据发送到 [!DNL Platform Edge Network] ，以供扩展在事件转发属性中使用。

此扩展所需的数据可以从Web SDK以XDM数据或非XDM数据的形式发送。 请参阅相关文档，了解有关 [发送XDM数据](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

例如，如果客户购买了商品或在您的网站上注册了事件，则可以通过使用此扩展的Mailchimp发送确认电子邮件。 将所需信息从Web SDK发送到边缘网络后，该扩展会使用Mailchimp触发电子邮件。

![添加事件操作配置](../../../images/extensions/mailchimp/action-configurations.png)

### 数据元素

上一部分的屏幕截图显示了您可以随每个事件一起从此扩展发送到Mailchimp的数据。 配置Web SDK以将此数据发送到边缘网络后，您可以在事件转发属性中创建数据元素，以便扩展可以访问这些值。

下表提供了每个可能值的更多详细信息。

| 名称 | 示例路径 | 类型 | 描述 | 必需 | 限制 |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> 或<br /> `arc.event.data._tenant.emailId` | 字符串 | 接收电子邮件的地址 | **是** | 必须存在于Mailchimp受众中 |
| `listId` | `arc.event.xdm._tenant.listId`<br /> 或<br /> `arc.event.data._tenant.listid` | 字符串 | 受众ID | **是** | 必须匹配现有受众ID |
| `name` | `arc.event.xdm._tenant.name`<br /> 或<br /> `arc.event.data._tenant.name` | 字符串 | 事件名称 | **是** | 长度为2-30个字符 |
| `properties` | `arc.event.xdm._tenant.properties`<br /> 或<br /> `arc.event.data._tenant.properties` | 对象 | JSON格式的可选属性列表，其中包含事件的详细信息 | 否 |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> 或<br /> `arc.event.data._tenant.isSyncing` | 布尔 | 通过创建的事件 `is_syncing` 设置为 `true` **将不会** 触发自动化 | 否 |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> 或 `arc.event.data._tenant.occuredAt` | 字符串 | 事件发生时的ISO 8601时间戳 | 否 |  |

{style=&quot;table-layout:auto&quot;}

>[!IMPORTANT]
>  
>的 **示例路径** 以上值仅为示例。 字段名称和 [路径](../../../ui/event-forwarding/overview.md#data-element-path) 在这些数据元素中引用的内容在您的资产中可能会有所不同，具体取决于您在上述步骤中命名和配置Web SDK的方式。

在事件转发属性中，您可以为上述每个字段创建一个数据元素。 创建后，即可在 [!UICONTROL 添加事件] 此扩展的操作。

![添加事件操作配置](../../../images/extensions/mailchimp/action-configurations.png)

您现在可以使用此扩展和“添加事件”操作来触发受众的邮件点击电子邮件。

## 数据验证

使用事件转发扩展时， [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 非常有用。 在日志部分的边缘日志下，您可以看到触发事件转发规则后发出的请求。 以下屏幕截图显示了扩展向Mailchimp API发出的请求。

![Adobe Experience Platform Debugger](../../../images/extensions/mailchimp/debugger-edge-logs.png)

在Mailchimp功能板的受众或受众成员的活动馈送视图中，提供了该受众或受众成员的事件列表。 这应该与扩展发送的事件匹配，并显示已发送的任何可选数据以及收到的电子邮件或营销活动。 请参阅 [Mailchimp自动化帮助指南](https://mailchimp.com/help/automation/) 以了解更多详细信息。
