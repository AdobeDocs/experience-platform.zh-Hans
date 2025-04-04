---
title: Mailchimp扩展概述
description: 使用事件转发来触发Mailchimp电子邮件。
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 5%

---

# Mailchimp事件转发扩展概述

>[!NOTE]
>  
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

Mailchimp [事件转发](../../../ui/event-forwarding/overview.md)扩展将事件发送到Mailchimp营销API，这可以触发Mailchimp营销活动、历程或交易的电子邮件。

本文档介绍如何使用Add Event操作设置扩展和配置规则。

## 先决条件

本文档假设您熟悉扩展使用的相关Mailchimp产品。 有关详细信息，请参阅[营销活动](https://mailchimp.com/help/getting-started-with-campaigns/)、[历程](https://mailchimp.com/help/about-customer-journeys/)和[交易](https://mailchimp.com/help/transactional/)的Mailchimp帮助文档。

使用此扩展需要Mailchimp帐户。 您可以在[此处](https://login.mailchimp.com/signup/)注册帐户。 在Mailchimp帐户仪表板中，请注意本指南中使用的以下值：

- 您的Mailchimp域前缀
- 您的API密钥
- 受众ID
- 默认的“发件人”电子邮件地址

根据您的Mailchimp客户计划，您对Mailchimp客户历程工具的访问权限可能会受到限制。

>[!TIP]
>  
>如果您使用Mailchimp自动化，如事务性电子邮件或客户历程，则步骤和屏幕可能稍有不同，此处列出。 但是，要使用此扩展，您仍需要上述相同的信息。 有关特定帐户和计划的每个值的详细信息，请参阅[Mailchimp帮助中心](https://mailchimp.com/help/)。

### 域前缀

登录到Mailchimp并登录仪表板视图后，浏览器的地址栏应显示`https://us11.admin.mailchimp.com`之类的URL或仅显示`us11.admin.mailchimp.com`。 在此示例中，前缀`us11`只是占位符，您的值将不同。 在后续步骤中使用前缀记录您的URL。

### API密钥

要查找您帐户的API密钥，请在Mailchimp UI中选择您的配置文件图标，然后选择&#x200B;**配置文件**。 您应该会看到类似`https://us11.admin.mailchimp.com/account/profile/`的URL，但带有&#x200B;**您的**&#x200B;前缀而不是`us11`。

选择&#x200B;**额外项**，然后选择&#x200B;**API密钥**：

![额外菜单，API密钥链接](../../../images/extensions/server/mailchimp/menu-API-keys.png)

在&#x200B;**您的API密钥**&#x200B;下，您可以选择现有密钥，也可以选择&#x200B;**创建密钥**&#x200B;以创建新密钥。 您可以创建一个新键以专门用于此扩展。 复制API密钥并将其保存以供稍后步骤使用。 有关更多详细信息，请参阅关于如何[生成API密钥](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key)的Mailchimp文档。

### 受众ID和发件人地址

在左侧导航中选择&#x200B;**受众**，然后选择&#x200B;**受众仪表板**。 接下来，选择要与此扩展一起使用的受众。 若要了解更多信息，请参阅[创建受众](https://mailchimp.com/help/create-audience/)上的Mailchimp文档。

创建并选择受众后，选择&#x200B;**管理受众**&#x200B;下拉菜单，然后选择&#x200B;**设置**。 此屏幕显示受众的各种设置。

在“设置”屏幕底部，您应该看到`Unique id for audience [audience name]`，其中`[audience name]`是实际受众的名称。 复制受众ID并将其保存以供稍后步骤使用。

选择&#x200B;**受众名称和默认值**，并确认&#x200B;**默认发件人电子邮件地址**&#x200B;具有正确的营销活动值。 请注意，此页面顶部还列出了受众ID，与您在上一步中向下复制的值相同。

## Mailchimp自动化

根据您的Mailchimp计划以及您使用事务性电子邮件、客户历程或其他Mailchimp自动化，您的特定旅程设置可能会有所不同。

>[!IMPORTANT]
>  
>您选择用于在Mailchimp中触发自动化或历程的事件名称与必须使用此扩展发送的事件名称相同。 记下Mailchimp自动化中的事件名称，并将其保存以供稍后步骤使用。

## 安装和配置

此部分列出了安装和配置扩展的步骤。 若要安全地保存Mailchimp API密钥，必须使用事件转发[密钥](../../../ui/event-forwarding/secrets.md)。

### 创建密码和数据元素

在事件转发属性中，[创建名为`Mailchimp API Key`的[!UICONTROL 令牌]密码](../../../ui/event-forwarding/secrets.md#token)。

接下来，[使用[!UICONTROL Core]扩展和[!UICONTROL Secret]数据元素类型创建数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element)以引用您刚刚创建的`Mailchimp API Key`密码。 输入`Mailchimp Token`作为数据元素名称。

### 安装和配置扩展

在同一事件转发属性中，选择&#x200B;**[!UICONTROL 扩展]、**&#x200B;和&#x200B;**[!UICONTROL 目录]**&#x200B;以显示可供安装的扩展。 从此处搜索Mailchimp扩展并选择&#x200B;**[!UICONTROL 安装]**。

![安装Mailchimp扩展](../../../images/extensions/server/mailchimp/install.png)

出现配置屏幕。 在&#x200B;**[!UICONTROL Mailchimp服务器前缀域名]**&#x200B;下，输入您之前从Mailchimp帐户复制的域，包括唯一的域前缀。

>[!IMPORTANT]
>
>请勿在此字段中包含`http://`或`https://`。

![扩展配置](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

在&#x200B;**[!UICONTROL Mailchimp令牌]**&#x200B;下，选择数据元素图标，然后选择您之前创建的`Mailchimp Token`数据元素。 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改。

扩展现在已安装并配置为可在资产中使用。

## 数据收集

在[规则](../../../ui/managing-resources/rules.md)中使用此扩展时，该扩展会通过每个事件向Mailchimp发送多个数据值。 对于典型实施，您可以将[Adobe Experience Platform Web SDK扩展](../../client/web-sdk/overview.md)配置为将该数据发送到[!DNL Experience Platform Edge Network]，以供扩展在事件转发属性中使用。

此扩展所需的数据可以作为XDM数据（使用[`xdm`](/help/web-sdk/commands/sendevent/xdm.md)对象）或非XDM数据（使用[`data`](/help/web-sdk/commands/sendevent/data.md)对象）从Web SDK发送。

例如，如果客户购买产品或注册了您网站上的事件，则您可以使用此扩展通过Mailchimp发送确认电子邮件。 将所需信息从Web SDK发送到Edge Network后，该扩展将通过Mailchimp触发电子邮件。

![添加事件操作配置](../../../images/extensions/server/mailchimp/action-configurations.png)

### 数据元素

上一部分中的屏幕截图显示了可随每个事件一起从此扩展发送到Mailchimp的数据。 在配置Web SDK以将此数据发送到Edge Network后，您可以在event forwarding属性中创建数据元素，以便扩展可以访问这些值。

下表提供了每个可能值的更多详细信息。

| 名称 | 示例路径 | 类型 | 描述 | 必需 | 限制 |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br />或<br /> `arc.event.data._tenant.emailId` | 字符串 | 接收电子邮件的地址 | **是** | 必须存在于Mailchimp受众中 |
| `listId` | `arc.event.xdm._tenant.listId`<br />或<br /> `arc.event.data._tenant.listid` | 字符串 | 受众 ID | **是** | 必须匹配现有的受众ID |
| `name` | `arc.event.xdm._tenant.name`<br />或<br /> `arc.event.data._tenant.name` | 字符串 | 事件名称 | **是** | 2-30个字符长 |
| `properties` | `arc.event.xdm._tenant.properties`<br />或<br /> `arc.event.data._tenant.properties` | 对象 | JSON格式的可选属性列表，其中包含有关事件的详细信息 | 否 |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br />或<br /> `arc.event.data._tenant.isSyncing` | 布尔 | 使用`is_syncing`设置为`true` **创建的事件将不会**&#x200B;触发自动处理 | 否 |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br />或`arc.event.data._tenant.occuredAt` | 字符串 | 事件发生时间的ISO 8601时间戳 | 否 |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>上述&#x200B;**示例路径**&#x200B;值仅为示例。 这些数据元素中引用的字段名称和[路径](../../../ui/event-forwarding/overview.md#data-element-path)在您的资产中可能不同，具体取决于您在上面步骤中命名和配置Web SDK的方式。

在事件转发属性中，您可以为上述每个字段创建一个数据元素。 创建后，您可以引用此扩展的[!UICONTROL 添加事件]操作中的数据元素。

![添加事件操作配置](../../../images/extensions/server/mailchimp/action-configurations.png)

您现在可以使用此扩展和Add Event操作来触发受众的Mailchimp电子邮件。

## 数据验证

使用事件转发扩展时，[Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)非常有用。 在日志部分的Edge日志下，您可以查看事件转发规则触发后发出的请求。 以下屏幕截图显示了扩展对Mailchimp API发出的请求。

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

在Mailchimp仪表板中，受众或受众成员的“活动信息源”视图上提供了该受众或受众成员的事件列表。 此操作应该匹配扩展发送的事件，并显示发送的任何可选数据以及它们收到的电子邮件或营销活动。 有关详细信息，请参阅[Mailchimp自动化帮助指南](https://mailchimp.com/help/automation/)。
