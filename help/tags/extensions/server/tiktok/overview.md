---
title: AdobeTikTok web events API扩展集成
description: 通过这个Adobe Experience Platform Web事件API，您可以直接与TikTok共享网站交互。
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 3%

---

# [!DNL TikTok] Web事件API扩展概述

此 [!DNL TikTok] events API是安全的 [边缘网络服务器API](/help/server-api/overview.md) 界面，通过该界面可与用户共享信息 [!DNL TikTok] 直接了解用户在您网站上的操作。 您可以利用事件转发规则发送来自 [!DNL Adobe Experience Platform Edge Network] 到 [!DNL TikTok] 通过使用 [!DNL TikTok] Web事件API扩展。

## [!DNL TikTok] 先决条件 {#prerequisites}

配置 [!DNL TikTok] 用于的Web事件API [!DNL TikTok] events API，您需要生成 [!DNL TikTok] 像素代码和访问令牌。

您必须拥有有效的 [!DNL TikTok] 用于业务帐户，以创建 [!DNL TikTok] 像素。 转到 [[!DNL TikTok] 企业注册页面](https://www.tiktok.com/business/en-US/solutions/business-account) 以注册并创建帐户（如果尚未注册）。

您必须登录您的企业帐户才能进行设置 [!DNL TikTok] 使用合作伙伴设置的像素。 为此，请执行以下步骤：

1. 导航至 **[!UICONTROL 资产]** 选项卡并选择 **[!UICONTROL 事件]**.
2. 在Web事件下，选择 **[!UICONTROL 管理]**.
3. 选择 **[!UICONTROL 设置Web事件]**.
4. 选择 **[!UICONTROL 合作伙伴设置]** 作为连接方法。

请参阅 [像素入门](https://ads.tiktok.com/help/article/get-started-pixel) 指南，以了解有关如何设置 [!DNL TikTok] 像素。

成功创建像素后，即可生成访问令牌。 为此，请导航到像素，然后选择 **[!UICONTROL 设置]** 选项卡。 在Events API下，选择 **[!UICONTROL 生成访问令牌]**.

请参阅 [[!DNL TikTok] 快速入门指南](https://business-api.tiktok.com/portal/docs?id=1739584855420929) 有关如何设置像素代码和访问令牌的更多信息。

## 安装和配置 [!DNL TikTok] Web事件API扩展 {#install}

要安装扩展，请选择 **[!UICONTROL 扩展]** 在左侧导航中。 在 **[!UICONTROL 目录]** 选项卡，选择 **[!UICONTROL TikTok Web事件API扩展]** 然后选择 **[!UICONTROL 安装]**.

![扩展目录显示 [!DNL TikTok] 扩展卡突出显示安装。](../../../images/extensions/server/tiktok/install-extension.png)

在下一个屏幕上，输入您之前从中生成的以下配置值 [!DNL TikTok] 广告管理器：

* **[!UICONTROL 像素代码]**
* **[!UICONTROL 访问令牌]**

完成后，选择 **[!UICONTROL 保存]**.

![[!DNL TikTok] 的配置屏幕 [!DNL TikTok] Web事件API扩展。](../../../images/extensions/server/tiktok/configure.png)

## 配置事件转发规则 {#config-rule}

设置完所有数据元素后，您可以开始创建事件转发规则，以确定将事件发送到的时间和方式 [!DNL TikTok].

新建 [规则](../../../ui/managing-resources/rules.md) 在事件转发属性中。 下 **[!UICONTROL 操作]**，添加新操作并将扩展设置为 **[!UICONTROL TikTok Web事件API扩展]**. 要将Edge Network事件发送到 [!DNL TikTok]，设置 **[!UICONTROL 操作类型]** 到 **[!UICONTROL 发送TikTok Web事件API事件].**

![此 [!UICONTROL 发送TikTok Web事件API事件] 要为选择的操作类型 [!DNL TikTok] 数据收集UI中的规则。](../../../images/extensions/server/tiktok/select-action.png)

选择后，会显示用于进一步配置事件的其他控件，如下所述。 完成后，选择 **[!UICONTROL 保留更改]** 以保存规则。

**[!UICONTROL Web事件和参数]**

Web事件和参数包含有关事件的常规信息。 支持的标准事件包括 [!DNL TikTok] 集成工具和，可用于报表、优化转化和构建受众。

| 输入 | 描述 |
| --- | --- |
| 活动名称 | 事件的名称。 这些操作具有由创建的预定义名称 [!DNL TikTok] 和是必填字段。 请参阅 [[!DNL TikTok] 营销API](https://business-api.tiktok.com/portal/docs?id=1741601162187777) 文档，以了解有关受支持事件的更多信息。 |
| 事件时间 | ISO 8601或中的字符串形式的日期时间 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 格式。 这是必填字段。 |
| 事件ID | 广告商为指示每个事件而生成的唯一ID。 这是一个可选字段，用于删除重复项。 |

{style="table-layout:auto"}

![此 [!DNL Web Events and Parameters] 部分显示了输入到字段中的示例数据。](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL 用户上下文参数]**

用户上下文参数包含用于匹配Web访客事件的客户信息 [!DNL TikTok] 用户。 包括多种类型的匹配数据可以提高定位和优化模型的准确性。

| 输入 | 描述 |
| --- | --- |
| IP 地址 | 浏览器的非哈希公共IP地址。 支持IPv4和IPv6地址。 IPv6地址的完整和压缩形式均可识别。 |
| 用户代理 | 来自用户设备的非哈希用户代理。 |
| 电子邮件 | 与转化事件关联的联系人的电子邮件地址。 |
| 电话 | 电话号码必须为E164格式[+][国家/地区代码][区号][local phone number] 进行哈希处理之前。 |
| Cookie ID | 如果您使用的是Pixel SDK，将自动在 `_ttp` Cookie（如果已启用Cookie）。 此 `_ttp` 可以提取值并将其用于此字段。 |
| 外部ID | 任何唯一标识符，例如用户ID、外部Cookie ID等，都必须使用SHA256进行哈希处理。 |
| TikTok点击ID | 此 `ttclid` 每次选择广告时，都会将其添加到登陆页面的URL [!DNL TikTok]. |
| Page URL | 事件时的页面URL。 |
| 页面反向链接URL | 页面反向链接的URL。 |

{style="table-layout:auto"}

![此 [!DNL User Context Parameters] 部分显示了输入到字段中的示例数据。](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL 属性参数]**

使用属性参数配置其他支持的属性。

| 输入 | 描述 |
| --- | --- |
| 价格 | 单个项目的成本。 |
| 数量 | 在事件中购买的项目数。 该值必须为大于0的正数。 |
| 内容类型 | 值： `product` 或 `product_group` 必须分配给content_type对象属性，具体取决于您在设置产品目录时配置数据馈送的方式。 |
| 内容 ID | 产品项目的唯一标识符。 |
| 内容类别 | 页面/产品的类别。 |
| 内容名称 | 页面/产品的名称。 |
| 货币 | 在事件中购买项目的货币。 这以ISO-4217表示。 |
| 值 | 订单的总价。 此值将等于价格*数量。 |
| 描述 | 项目或页面的描述。 |
| 查询 | 用于查找产品的文本字符串。 |
| 状态 | 订单、项目或服务的状态。 例如，“submitted”。 |

{style="table-layout:auto"}

![此 [!DNL Properties Parameters] 部分显示了输入到字段中的示例数据。](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## 事件去重 {#deduplication}

[!DNL TikTok] 如果同时使用 [!DNL TikTok] 像素SDK和 [!DNL TikTok] 要将相同事件发送到的Web事件API扩展 [!DNL TikTok].

如果从客户端和服务器发送的不同事件类型没有任何重叠，则不需要重复数据删除。 要确保您的报表不会受到负面影响，您必须确保共享的任何单个事件 [!DNL TikTok] 像素SDK和 [!DNL TikTok] 为Web事件API扩展去重。

发送共享事件时，请确保每个事件都包含像素ID、事件ID和名称。 相互之间在5分钟内到达的重复事件将被合并。 如果第一个事件中数据字段不存在，则它将与后续事件组合。 将删除在48小时内收到的所有重复事件。

请参阅 [!DNL TikTok] 文档 [事件去重](https://ads.tiktok.com/help/article/event-deduplication) 以了解有关此过程的更多详细信息。

## 后续步骤

本指南介绍了如何将服务器端事件数据发送到 [!DNL TikTok] 使用 [!DNL TikTok] Web事件API扩展。 有关中的事件转发功能的详细信息 [!DNL Adobe Experience Platform]，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
