---
keywords: 事件转发扩展；pinterest；pinterest事件转发扩展
title: Pinterest事件转发扩展
description: 通过这个Adobe Experience Platform事件转发扩展，您可以将事件摄取到Pinterest中，以满足您的业务需求。
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 3%

---

# [!DNL Pinterest] 事件转发扩展

[!DNL Pinterest]是一个可视化发现引擎，用于查找配方、家庭装饰、风格灵感等创意。 [!DNL Pinterest]上有数十亿个pin，也可以与[!DNL Pinterest]上的其他人共享。 您可以整理用户交互事件并利用[!DNL Pinterest Analytics]了解用户行为并运行目标播发。

[[!DNL Pinterest] 转化](https://developers.pinterest.com/docs/conversions/conversion-management/) API [事件转发](../../../ui/event-forwarding/overview.md)扩展允许您利用Adobe Experience Platform Edge Network中捕获的数据并将其发送给[!DNL Pinterest]。 本文档介绍了扩展的使用案例、安装方法，以及如何将其功能集成到事件转发[规则](../../../ui/managing-resources/rules.md)中。

转化访问令牌是[!DNL Pinterest]与[!DNL Pinterest] API交互时使用的身份验证方法。

## 用例

如果要在[!DNL Pinterest]中使用Edge Network中的数据以利用其客户分析功能，则应该使用此扩展。

例如，以组织中的营销团队为例。 团队从其网站捕获用户交互事件数据，并使用此事件转发扩展将其加载到[!DNL Pinterest]中。

然后，营销和分析团队可以利用[!DNL Pinterest] Analytics功能来了解关键用户交互和行为，从而让您更好地了解用户并将他们定位到有针对性的广告促销活动中。

有关特定于[!DNL Pinterest]的用例的更多信息，请参阅[[!DNL Pinterest] 用例](https://business.pinterest.com/en/success-stories)文档。

## [!DNL Pinterest]先决条件 {#prerequisites}

您必须拥有有效的[!DNL Pinterest] [商业帐户](https://help.pinterest.com/en/business/article/get-a-business-account)才能使用此扩展。 转到[[!DNL Pinterest] 注册页面](https://www.pinterest.com/business/create/)进行注册并创建帐户（如果还没有帐户）。

您还需要一个[!DNL Pinterest]开发人员帐户，该帐户需要与您的[!DNL Pinterest]业务帐户关联。 若要将开发人员帐户与业务帐户关联，请参阅[[!DNL Pinterest &#x200B;] 开发人员帐户](https://developers.pinterest.com/account-setup/)。

### 收集所需的配置详细信息 {#configuration-details}

要将Experience Platform连接到[!DNL Pinterest]，需要以下输入：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 广告帐户ID | 您的[!DNL Pinterest]广告帐户Id。 有关指导，请参阅[[!DNL Pinterest] 文档](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager)。 | 123456789012 |
| 转化访问令牌 | 您的[!DNL Pinterest]转化访问令牌。 请参阅[[!DNL Pinterest] 转化API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token)文档以获取指导。<br> **您只需执行此操作一次，因为此令牌不会过期。** | {YOUR_PINTEREST_BEARER_TOKEN} |

## 安装和配置[!DNL Pinterest]扩展 {#install}

若要安装该扩展，请[创建事件转发属性](../../../ui/event-forwarding/overview.md#properties)或选择现有属性进行编辑。

在左侧导航中，选择&#x200B;**[!UICONTROL Extensions]**。 在&#x200B;**[!UICONTROL Install]**&#x200B;选项卡的[!DNL Pinterest]扩展的卡片中选择&#x200B;**[!UICONTROL Catalog]**。

![目录显示[!DNL Pinterest]扩展，其中突出显示[!UICONTROL Install]。](../../../images/extensions/server/pinterest/install.png)

### 配置 [!DNL Pinterest] 扩展

>[!IMPORTANT]
>
>根据您的实施需求，您可能需要在配置扩展之前创建架构、数据元素和数据集。 请在开始之前查看所有配置步骤，以确定需要为用例设置哪些实体。

在左侧导航中，选择&#x200B;**[!UICONTROL Extensions]**。 在&#x200B;**[!UICONTROL Configure]**&#x200B;选项卡的[!DNL Pinterest]扩展的卡片中选择&lbrace;0**。[!UICONTROL Installed]

在![[!DNL Pinterest]选项卡中显示的[!UICONTROL Install]扩展突出显示[!UICONTROL Configure]。](../../../images/extensions/server/pinterest/configure.png)

在下一个屏幕上，输入您之前在[!UICONTROL Ads Account Id]配置详细信息[!UICONTROL Conversion Access Token]部分中收集的[和](#configuration-details)。 完成后，选择&#x200B;**[!UICONTROL Save]**。

![&#x200B; [!DNL Pinterest] [!UICONTROL Configure]屏幕突出显示[!UICONTROL Ads Account Id]和[!UICONTROL Conversion Access Token]输入字段。](../../../images/extensions/server/pinterest/input.png)

## 配置事件转发规则 {#config-rule}

设置完所有数据元素后，即可开始创建事件转发规则，以确定将事件发送到[!DNL Pinterest]的时间和方式。

在事件转发属性中创建新的[规则](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL Actions]**&#x200B;下，添加新操作并将扩展设置为&#x200B;**[!UICONTROL Pinterest]**。 要将Edge Network事件发送到[!DNL Pinterest]，请将&#x200B;**[!UICONTROL Action Type]**&#x200B;设置为&#x200B;**[!UICONTROL Send Event]。**

![创建[!DNL Pinterest] [!UICONTROL Send Event]规则。](../../../images/extensions/server/pinterest/rule.png)

选择后，会显示其他控件以进一步配置事件。 您需要将[!DNL Pinterest]事件属性映射到您之前创建的数据元素。

### [!UICONTROL Event Data]

创建新规则需要以下事件数据：

| 字段名称 | 描述 | 示例 |
| --- | --- | --- | 
| [!UICONTROL Event Name] | 用户事件的类型。 这可以是任何事件类型，但若要利用[!DNL Pinterest Analytics]，建议使用[[!DNL Pinterest] 事件代码](https://help.pinterest.com/en/business/article/add-event-codes) | &amp;amp；ast；签出<br> &amp;amp；ast； add_to_cart <br> &amp;amp；ast； page_visit <br> &amp;amp；ast；注册<br> &amp;amp；ast； [用户定义的事件] |
| [!UICONTROL Action Source] | 指示转化事件发生的位置的源。 | &amp;amp；ast； app_android <br> &amp;amp；ast； app_ios <br> &amp;amp；ast； Web <br> &amp;amp；ast；脱机 |
| [!UICONTROL Event Time] | 这是指事件时间。 使用的默认时间格式为UNIX，格式为`<seconds>.<miliseconds>`，具体取决于您的本地时区。 有关详细信息，请参阅[[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create)。 | 1433188255.500表示新纪元后的1433188255秒和500毫秒，或2015年6月1日星期一晚上7:50:55 GMT。 |
| [!UICONTROL Event ID] | 一个唯一的ID字符串，可标识此事件，并可用于在通过转化API和Pinterest跟踪摄取的事件之间删除重复项。 否则，事件的数据可能会被重复计数，并将报告量度虚增。 | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Event Properties] | 包含事件的自定义属性的JSON对象。 从提供原始JSON或使用一组简化的键值输入中进行选择。 | { &quot;event_source_url&quot;： &quot;http://site.com&quot; } |

![在规则操作中突出显示[!DNL Pinterest] [!UICONTROL Event Data]。](../../../images/extensions/server/pinterest/event-data.png)

可以配置以下事件属性：

| 字段名称 | 描述 |
| --- | --- |
| 事件Source URL | Web转换事件的URL。 |
| 应用程序商店ID | 应用商店应用程序ID。 |
| 应用程序名称 | 应用程序的名称。 |
| Application Version | 应用程序的版本。 |
| 设备品牌 | 用户正在使用的设备的品牌。 |
| 设备托架 | 用户的设备的移动设备运营商。 |
| 设备型号 | 用户设备的型号。 |
| Device Type | 用户正在使用的设备类型。 |
| 操作系统版本 | 设备的操作系统版本。 |
| 用户语言 | 用于指示用户语言的双字符ISO-639-1语言代码。 |

### [!UICONTROL User Data]

可以输入的以下用户数据不是必填字段：

| 字段名称 | 描述 | 示例 |
| --- | --- | --- | 
| [!UICONTROL Email] | 用户电子邮件地址或用户地址电子邮件的SHA256哈希。 | ebd543592...f2b7e1 |
| [!UICONTROL Mobile Adverstising IDs] | 用户的“Google Advertising ID”(GAID)或“Apple的广告商标识符”(IDFA)的Sha256哈希 | ebd543592...f2b7e1 |
| [!UICONTROL Client IP Address] | 用户的IP地址，可以是IPv4或IPv6格式。 用于匹配。 | 192.168.0.1 |
| [!UICONTROL Client User Agent] | 用户Web浏览器的用户代理字符串。 | Mozilla/5.0 （平台；rv:geckoversion） Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Customer information data] | 包含其他客户信息的JSON对象。 从提供原始JSON或使用一组简化的键值输入中进行选择。 | { &quot;ph&quot;： &quot;122333445&quot; } |

![在规则操作中突出显示[!DNL Pinterest] [!UICONTROL User Data]。](../../../images/extensions/server/pinterest/user-data.png)

可以配置的客户信息属性包括：

| 字段名称 | 描述 |
| --- | --- |
| 电话 | 用户联系电话。 仅接受数字，并且应输入国家/地区代码、区号和号码。 |
| 性别 | 性别可以输入为“f”（女性）、“m”（男性）或“n”（非二进制）。 |
| 出生日期 | 出生日期，按年、月、日输入。 |
| 姓氏 | 用户的姓氏。 |
| 名字 | 用户的名字。 |
| 城市 | 用户的居住城市。 这主要用于计费目的。 |
| State | 用户的状态，以小写形式提供为两个字母的代码。 |
| 邮政编码 | 用户的邮政编码，主要用于计费目的。 |
| 国家/地区 | 双字符ISO-3166国家/地区代码，指示用户的国家/地区。 |
| 外部 ID | 广告商的唯一ID，用于标识其空间中的用户。 例如，用户ID、忠诚度ID等。 |
| 点击ID | 域上存储在_epik Cookie中的唯一标识符或URL中的&amp;epik=查询参数。 |

>[!IMPORTANT]
>
>将数据发送到[!DNL Pinterest] API端点之前，扩展将散列并标准化以下字段的值：电子邮件、电话号码、名字、姓氏、性别、出生日期、城市、州、邮政编码、国家/地区和外部ID。 如果已经存在SHA256字符串，扩展将不会对这些字段的值进行哈希处理。

### [!UICONTROL Custom Data]

可以为规则输入以下自定义数据：

| 字段名称 | 描述 |
| --- | --- |
| 货币 | ISO-4217货币代码。 如果未提供，则[!DNL Pinterest]将默认使用在创建帐户期间设置的广告商货币。 |
| 值 | 事件的总值。 被接受为请求中的字符串。 这将被解析为两位数。 |
| 搜索字符串 | 与用户转化事件相关的搜索字符串。 |
| 订单ID | 订单ID。 发送`order_id`将帮助[!DNL Pinterest]在必要时删除重复事件。 |
| 产品数量 | 事件的产品总数。 例如，在结账事件中购买的项目总数。 |
| 内容Id | 产品ID列表（数组）。 |
| 目录 | 包含产品信息（如价格和数量）的对象列表（数组）。 |

![在规则操作中突出显示[!DNL Pinterest] [!UICONTROL Custom Data]。](../../../images/extensions/server/pinterest/custom-data.png)

## 验证[!DNL Pinterest]中的数据

创建并执行事件转发规则后，验证发送到[!DNL Pinterest] API的事件是否在[!DNL Pinterest] UI中按预期显示。

如果事件收集和[!DNL Experience Platform]集成成功，您将在[!DNL Pinterest] UI中看到事件。

![&#x200B; [!DNL Pinterest]事件管理器](../../../images/extensions/server/pinterest/event-history.png)

您可以进一步穿透钻取并查看[!DNL Pinterest]事件数据分发。

![数据分发[!DNL Pinterest]](../../../images/extensions/server/pinterest/event-history-distribution.png)

## 后续步骤

本指南介绍了如何在UI中安装和配置[!DNL Pinterest]事件转发扩展。 有关更多信息，请参阅官方文档：

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] 转化API概述](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
