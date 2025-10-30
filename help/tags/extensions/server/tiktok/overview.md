---
title: Adobe TikTok web events API扩展集成
description: 通过这个Adobe Experience Platform Web事件API，您可以直接与TikTok共享网站交互。
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 2%

---

# [!DNL TikTok] Web事件API扩展概述

[!DNL TikTok]事件API是一个安全的[Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)接口，允许您直接与[!DNL TikTok]共享有关您网站上的用户操作的信息。 您可以使用[!DNL Adobe Experience Platform Edge Network] Web事件API扩展利用事件转发规则将数据从[!DNL TikTok]发送到[!DNL TikTok]。

## [!DNL TikTok]先决条件 {#prerequisites}

要将[!DNL TikTok] Web事件API配置为使用[!DNL TikTok]事件API，您需要生成[!DNL TikTok]像素代码并访问令牌。

您必须拥有有效的[!DNL TikTok]商业帐户，才能使用合作伙伴设置创建[!DNL TikTok]像素。 转到[[!DNL TikTok] 商业注册页面](https://www.tiktok.com/business/en-US/solutions/business-account)进行注册并创建帐户（如果尚未注册）。

您必须登录您的企业帐户才能使用合作伙伴设置设置[!DNL TikTok] Pixel。 为此，请执行以下步骤：

1. 导航到&#x200B;**[!UICONTROL Assets]**&#x200B;选项卡并选择&#x200B;**[!UICONTROL Event]**。
2. 在Web事件下，选择&#x200B;**[!UICONTROL Manage]**。
3. 选择 **[!UICONTROL Set Up Web Events]**。
4. 选择&#x200B;**[!UICONTROL Partner Setup]**&#x200B;作为您的连接方法。

有关如何设置[像素的更多信息，请参阅](https://ads.tiktok.com/help/article/get-started-pixel)像素入门[!DNL TikTok]指南。

成功创建像素后，即可生成访问令牌。 为此，请导航到“像素”并选择&#x200B;**[!UICONTROL Settings]**&#x200B;选项卡。 在“事件API”下，选择&#x200B;**[!UICONTROL Generate Access Token]**。

有关如何设置像素代码和访问令牌的更多信息，请参阅[[!DNL TikTok] 快速入门指南](https://business-api.tiktok.com/portal/docs?id=1739584855420929)。

## 安装和配置[!DNL TikTok] Web事件API扩展 {#install}

要安装扩展，请在左侧导航中选择&#x200B;**[!UICONTROL Extensions]**。 在&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL TikTok Web Events API Extension]**，然后选择&#x200B;**[!UICONTROL Install]**。

![扩展目录显示[!DNL TikTok]扩展卡突出显示安装。](../../../images/extensions/server/tiktok/install-extension.png)

在下一个屏幕上，输入您之前从[!DNL TikTok]广告管理器生成的以下配置值：

* **[!UICONTROL Pixel Code]**
* **[!UICONTROL Access Token]**

完成后，选择&#x200B;**[!UICONTROL Save]**。

![[!DNL TikTok] Web事件API扩展的[!DNL TikTok]配置屏幕。](../../../images/extensions/server/tiktok/configure.png)

## 配置事件转发规则 {#config-rule}

设置完所有数据元素后，即可开始创建事件转发规则，以确定将事件发送到[!DNL TikTok]的时间和方式。

在事件转发属性中创建新的[规则](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL Actions]**&#x200B;下，添加新操作并将扩展设置为&#x200B;**[!UICONTROL TikTok Web Events API Extension]**。 要将Edge Network事件发送到[!DNL TikTok]，请将&#x200B;**[!UICONTROL Action Type]**&#x200B;设置为&#x200B;**[!UICONTROL Send TikTok Web Events API Event]。**

![为数据收集UI中的[!UICONTROL Send TikTok Web Events API Event]规则选择的[!DNL TikTok]操作类型。](../../../images/extensions/server/tiktok/select-action.png)

选择后，会显示用于进一步配置事件的其他控件，如下所述。 完成后，选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以保存规则。

**[!UICONTROL Web Events and Parameters]**

Web事件和参数包含有关事件的常规信息。 标准事件在[!DNL TikTok]集成工具中受支持，可用于报告、优化转化和构建受众。

| 输入 | 描述 |
| --- | --- |
| 活动名称 | 事件的名称。 这些操作具有由[!DNL TikTok]创建的预定义名称，是必填字段。 有关受支持事件的更多信息，请参阅[[!DNL TikTok] 营销API](https://business-api.tiktok.com/portal/docs?id=1741601162187777)文档。 |
| 事件时间 | ISO 8601或`yyyy-MM-dd'T'HH:mm:ss:SSSZ`格式字符串形式的日期时间。 这是必填字段。 |
| 事件 ID | 广告商为指示每个事件而生成的唯一ID。 这是一个可选字段，用于删除重复项。 |

{style="table-layout:auto"}

![显示输入到字段中的示例数据的[!DNL Web Events and Parameters]部分。](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL User Context Parameters]**

用户上下文参数包含用于将Web访客事件与[!DNL TikTok]用户匹配的客户信息。 包括多种类型的匹配数据可以提高定位和优化模型的准确性。

| 输入 | 描述 |
| --- | --- |
| IP地址 | 浏览器的非哈希公共IP地址。 支持IPv4和IPv6地址。 IPv6地址的完整和压缩形式均可识别。 |
| 用户代理 | 来自用户设备的非哈希用户代理。 |
| 电子邮件 | 与转化事件关联的联系人的电子邮件地址。 |
| 电话 | 在进行哈希处理之前，电话号码必须是E164格式`[+][country code][area code][local phone number]`。 |
| Cookie ID | 如果您使用的是Pixel SDK，则在启用Cookie的情况下，它将自动在`_ttp` Cookie中保存唯一标识符。 `_ttp`值可提取并用于此字段。 |
| 外部 ID | 任何唯一标识符，例如用户ID、外部Cookie ID等，都必须使用SHA256进行哈希处理。 |
| TikTok点击ID | 每次在`ttclid`上选择广告时都添加到登陆页面URL的[!DNL TikTok]。 |
| Page URL | 事件时的页面URL。 |
| 页面反向链接URL | 页面反向链接的URL。 |

{style="table-layout:auto"}

![显示输入到字段中的示例数据的[!DNL User Context Parameters]部分。](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Properties Parameters]**

使用属性参数配置其他支持的属性。

| 输入 | 描述 |
| --- | --- |
| 价格 | 单个项目的成本。 |
| 数量 | 在事件中购买的项目数。 该值必须为大于0的正数。 |
| 内容类型 | 必须将`product`或`product_group`的值分配给content_type对象属性，具体取决于您在设置产品目录时配置数据馈送的方式。 |
| 内容Id | 产品项目的唯一标识符。 |
| 内容类别 | 页面/产品的类别。 |
| 内容名称 | 页面/产品的名称。 |
| 货币 | 在事件中购买项目的货币。 这以ISO-4217表示。 |
| 值 | 订单的总价。 此值将等于价格*数量。 |
| 描述 | 项目或页面的描述。 |
| 查询 | 用于查找产品的文本字符串。 |
| 状态 | 订单、项目或服务的状态。 例如，“submitted”。 |

{style="table-layout:auto"}

![显示输入到字段中的示例数据的[!DNL Properties Parameters]部分。](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## 事件去重 {#deduplication}

如果您同时使用[!DNL TikTok] pixel SDK和[!DNL TikTok] Web事件API扩展将相同的事件发送到[!DNL TikTok]，则需要设置[!DNL TikTok]像素以进行重复数据删除。

如果从客户端和服务器发送的不同事件类型没有任何重叠，则不需要重复数据删除。 要确保您的报表不会受到负面影响，您必须确保为[!DNL TikTok]像素SDK和[!DNL TikTok] Web事件API扩展共享的任何单个事件删除重复项。

发送共享事件时，请确保每个事件都包含像素ID、事件ID和名称。 相互之间在5分钟内到达的重复事件将被合并。 如果第一个事件中数据字段不存在，则它将与后续事件组合。 将删除在48小时内收到的所有重复事件。

有关此过程的更多详细信息，请参阅有关[!DNL TikTok]事件重复数据删除[的](https://ads.tiktok.com/help/article/event-deduplication)文档。

## 后续步骤

本指南介绍了如何使用[!DNL TikTok] Web事件API扩展将服务器端事件数据发送到[!DNL TikTok]。 有关[!DNL Adobe Experience Platform]中事件转发功能的详细信息，请参阅[事件转发概述](../../../ui/event-forwarding/overview.md)。
