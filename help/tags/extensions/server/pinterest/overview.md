---
keywords: 事件转发扩展；pinterest;pinterest事件转发扩展
title: Pinterest事件转发扩展
description: 此Adobe Experience Platform事件转发扩展允许您根据业务要求将事件摄取到Pinterest。
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 87c76ef4b95bc05a64d9d124d69c2a51b7b77c08
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 4%

---

# [!DNL Pinterest] 事件转发扩展

[!DNL Pinterest] 是一个可视发现引擎，用于查找各种创意，如菜谱、家居装饰、风格灵感等。 有几十亿个针 [!DNL Pinterest]，也可以在 [!DNL Pinterest]. 您可以整理用户交互事件并利用 [!DNL Pinterest Analytics] 以了解用户行为并运行定向广告。

的 [[!DNL Pinterest] 转化](https://developers.pinterest.com/docs/conversions/conversion-management/) API [事件转发](../../../ui/event-forwarding/overview.md) 扩展允许您利用在Adobe Experience Platform边缘网络中捕获的数据，并将其发送到 [!DNL Pinterest]. 本文档介绍扩展的用例、如何安装该扩展，以及如何将其功能集成到事件转发中 [规则](../../../ui/managing-resources/rules.md).

转化访问令牌是使用的身份验证方法 [!DNL Pinterest] 与交互时 [!DNL Pinterest] API。

## 用例

如果要在 [!DNL Pinterest] 以利用其客户分析功能。

例如，以组织中的营销团队为例。 团队从其网站中捕获用户交互事件数据并将其加载到 [!DNL Pinterest] 使用此事件转发扩展。

然后，营销和分析团队可以利用 [!DNL Pinterest] Analytics功能可了解关键用户交互和行为，从而让您更好地了解用户并将他们定位到目标广告营销活动。

有关特定用例的更多信息 [!DNL Pinterest]，请参阅 [[!DNL Pinterest] 用例](https://business.pinterest.com/en/success-stories) 文档。

## [!DNL Pinterest] 先决条件 {#prerequisites}

您必须拥有 [!DNL Pinterest] [业务帐户](https://help.pinterest.com/en/business/article/get-a-business-account) 以使用此扩展。 转到 [[!DNL Pinterest] 注册页面](https://www.pinterest.com/business/create/) 注册并创建帐户（如果尚未注册）。

您还需要 [!DNL Pinterest] 开发人员帐户，该帐户需要与您的 [!DNL Pinterest] 商业帐户。 要将您的开发人员帐户与您的业务帐户关联，请参阅 [[!DNL Pinterest ] 开发人员帐户](https://developers.pinterest.com/account-setup/).

### 收集所需的配置详细信息 {#configuration-details}

要将Experience Platform连接到 [!DNL Pinterest]，则需要输入以下数据：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| 广告帐户Id | 您的 [!DNL Pinterest] 广告帐户Id。 请参阅 [[!DNL Pinterest] 文档](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) 以获取指导。 | 123456789012 |
| 转化访问令牌 | 您的 [!DNL Pinterest] 转化访问令牌。 请参阅 [[!DNL Pinterest] 转化API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) 文档以供指导。 <br> **由于此令牌未过期，因此只需执行一次此操作。** | {YOUR_PINTEREST_BEARER_TOKEN} |

## 安装和配置 [!DNL Pinterest] 扩展 {#install}

要安装扩展，请 [创建事件转发属性](../../../ui/event-forwarding/overview.md#properties) 或选择要编辑的现有属性。

在左侧导航中，选择 **[!UICONTROL 扩展]**. 选择 **[!UICONTROL 安装]** 在 [!DNL Pinterest] 扩展 **[!UICONTROL 目录]** 选项卡。

![显示 [!DNL Pinterest] 扩展 [!UICONTROL 安装] 突出显示。](../../../images/extensions/server/pinterest/install.png)

### 配置 [!DNL Pinterest] 扩展

>[!IMPORTANT]
>
>根据您的实施需求，您可能需要先创建架构、数据元素和数据集，然后再配置该扩展。 请在开始之前查看所有配置步骤，以确定您需要为用例设置哪些实体。

在左侧导航中，选择 **[!UICONTROL 扩展]**. 选择 **[!UICONTROL 配置]** 在 [!DNL Pinterest] 扩展 [!UICONTROL 已安装]**选项卡。

![[!DNL Pinterest] 扩展，如 [!UICONTROL 安装] 选项卡 [!UICONTROL 配置] 突出显示。](../../../images/extensions/server/pinterest/configure.png)

在下一个屏幕中，输入 [!UICONTROL 广告帐户Id] 和 [!UICONTROL 转化访问令牌] 之前在 [配置详细信息](#configuration-details) 中。 完成后，选择 **[!UICONTROL 保存]**.

![的 [!DNL Pinterest] [!UICONTROL 配置] 屏幕高亮显示 [!UICONTROL 广告帐户Id] 和 [!UICONTROL 转化访问令牌] 输入字段。](../../../images/extensions/server/pinterest/input.png)

## 配置事件转发规则 {#config-rule}

设置所有数据元素后，您可以开始创建事件转发规则，以确定事件何时以及如何发送到 [!DNL Pinterest].

新建 [规则](../../../ui/managing-resources/rules.md) 在事件转发属性中。 在 **[!UICONTROL 操作]**，添加新操作并将扩展设置为 **[!UICONTROL Pinterest]**. 要将Adobe Experience Edge Network事件发送到 [!DNL Pinterest]，请设置 **[!UICONTROL 操作类型]** to **[!UICONTROL 发送事件].**

![的 [!DNL Pinterest] [!UICONTROL 发送事件] 规则创建。](../../../images/extensions/server/pinterest/rule.png)

选择后，将显示其他控件以进一步配置事件。 您需要映射 [!DNL Pinterest] 事件属性添加到您之前创建的数据元素。

### [!UICONTROL 事件数据]

创建新规则时需要以下事件数据：

| 字段名称 | 描述 | 示例 |
| --- | --- | --- | 
| [!UICONTROL 活动名称] | 用户事件的类型。 但是，这可以是任何事件类型，用于利用 [!DNL Pinterest Analytics] 建议使用 [[!DNL Pinterest] 事件代码](https://help.pinterest.com/en/business/article/add-event-codes) | *结帐 <br> * add_to_cart <br> * page_visit <br> *注册 <br> * [用户定义的事件] |
| [!UICONTROL 操作源] | 表示发生转化事件的位置的源。 | * app_android <br> * app_ios <br> * web <br> *脱机 |
| [!UICONTROL 事件时间] | 这是指事件时间。 使用的默认时间格式为UNIX，格式为 `<seconds>.<miliseconds>` 取决于您的本地时区。 有关更多信息，请参阅 [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500表示在纪元后1433188255秒和500毫秒，或2015年6月1日星期一7时:50:55 PM GMT。 |
| [!UICONTROL 事件ID] | 一个唯一的ID字符串，用于标识此事件，并可用于在通过转化API和Pinterest跟踪摄取的事件之间进行重复数据删除。 如果没有此选项，事件的数据可能会被重复计数，并且会报告量度虚增。 | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL 事件属性] | 包含事件自定义属性的JSON对象。 从提供原始JSON或使用一组简化的键值输入中进行选择。 | { &quot;event_source_url&quot;:&quot;http://site.com&quot; } |

![的 [!DNL Pinterest] [!UICONTROL 事件数据] 在规则操作中突出显示。](../../../images/extensions/server/pinterest/event-data.png)

可以配置以下事件属性：

| 字段名称 | 描述 |
| --- | --- |
| 事件源URL | Web转化事件的URL。 |
| 应用程序存储ID | 应用商店应用程序ID。 |
| 应用程序名称 | 应用程序的名称。 |
| Application Version | 应用程序的版本。 |
| 设备品牌 | 用户使用的设备的品牌。 |
| 设备载体 | 用户设备的移动运营商。 |
| 设备型号 | 用户设备的型号。 |
| Device Type | 用户使用的设备类型。 |
| 操作系统版本 | 设备操作系统的版本。 |
| 用户语言 | 表示用户语言的双字符ISO-639-1语言代码。 |

### [!UICONTROL 用户数据]

以下用户数据可由非必填字段输入：

| 字段名称 | 描述 | 示例 |
| --- | --- | --- | 
| [!UICONTROL 电子邮件] | 用户电子邮件地址或用户地址电子邮件的SHA256哈希。 | ebd543592...f2b7e1 |
| [!UICONTROL 移动广告ID] | 用户的“Google广告ID”(GAID)或“Apple的广告商标识符”(IDFA)的Sha256哈希 | ebd543592...f2b7e1 |
| [!UICONTROL 客户端IP地址] | 用户的IP地址，可以采用IPv4或IPv6格式。 用于匹配。 | 192.168.0.1 |
| [!UICONTROL 客户端用户代理] | 用户Web浏览器的用户代理字符串。 | Mozilla/5.0(平台；rv:geckoversion)Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL 客户信息数据] | 包含其他客户信息的JSON对象。 从提供原始JSON或使用一组简化的键值输入中进行选择。 | { &quot;ph&quot;:&quot;122333445&quot; } |

![的 [!DNL Pinterest] [!UICONTROL 用户数据] 在规则操作中突出显示。](../../../images/extensions/server/pinterest/user-data.png)

可配置的客户信息属性包括：

| 字段名称 | 描述 |
| --- | --- |
| Phone | 用户联系电话。 只接受数字，并且应使用国家/地区代码、地区代码和数字输入。 |
| 性别 | 性别可以输入为“f”（女性）、“m”（男性）或“n”（非二进制）。 |
| 出生日期 | 出生日期，按年、月和日输入。 |
| 姓氏 | 用户的姓氏。 |
| 名字 | 用户的名字。 |
| 城市 | 用户的居住城市。 此功能主要用于计费目的。 |
| State | 用户的状态，以小写形式提供为双字母代码。 |
| 邮政编码 | 用户的zipcode，主要用于计费目的。 |
| 国家/地区 | 双字符ISO-3166国家/地区代码，用于指示用户的国家/地区。 |
| 外部ID | 广告商中用于标识其空间中用户的唯一ID。 例如，用户ID、忠诚度ID等。 |
| 点击ID | 域的_epik Cookie中存储的唯一标识符或URL的&amp;epik=查询参数中存储的唯一标识符。 |

>[!IMPORTANT]
>
>在将数据发送到 [!DNL Pinterest] API端点，扩展将对以下字段的值进行哈希和标准化：电子邮件、电话号码、名字、姓氏、性别、出生日期、城市、州、邮政编码、国家/地区和外部ID。 如果SHA256字符串已存在，则扩展将不会对这些字段的值进行哈希处理。

### [!UICONTROL 自定义数据]

可以为规则输入以下自定义数据：

| 字段名称 | 描述 |
| --- | --- |
| 货币 | ISO-4217货币代码。 如果未提供， [!DNL Pinterest] 将默认使用在帐户创建期间设置的广告商货币。 |
| 值 | 事件的总值。 在请求中接受为字符串。 这将被解析为一个双位数。 |
| 搜索字符串 | 与用户转化事件相关的搜索字符串。 |
| 订单ID | 订单ID。 发送 `order_id` 将提供帮助 [!DNL Pinterest] 必要时删除重复事件。 |
| 产品数量 | 事件的产品总数。 例如，结帐事件中购买的项目总数。 |
| 内容ID | 产品ID的列表（数组）。 |
| 内容 | 包含产品信息（如价格和数量）的对象列表（数组）。 |

![的 [!DNL Pinterest] [!UICONTROL 自定义数据] 在规则操作中突出显示。](../../../images/extensions/server/pinterest/custom-data.png)

## 在中验证数据 [!DNL Pinterest]

创建并执行事件转发规则后，验证是否将事件发送到 [!DNL Pinterest] API会按预期显示在 [!DNL Pinterest] UI。

如果事件集合和 [!DNL Experience Platform] 集成成功后，您将在 [!DNL Pinterest] UI。

![的 [!DNL Pinterest] 事件管理器](../../../images/extensions/server/pinterest/event-history.png)

您可以进一步深入查看 [!DNL Pinterest] 事件数据分发。

![的 [!DNL Pinterest] 数据分布](../../../images/extensions/server/pinterest/event-history-distribution.png)

## 后续步骤

本指南介绍了如何安装和配置 [!DNL Pinterest] 事件转发UI中的扩展。 有关更多信息，请参阅官方文档：

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] 转化API概述](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
