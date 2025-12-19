---
title: Nextdoor转换API扩展
description: 了解如何使用Nextdoor转化API扩展发送转化事件以跟踪广告营销活动的效果。
last-substantial-update: 2025-12-18T00:00:00Z
source-git-commit: 56c69696300dd9de8c0e98ecc71cafc7328f1620
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 8%

---


# [!DNL Nextdoor]转换API扩展 — 用户指南

## 概述

[!DNL Nextdoor]是社区社交网络服务，可将人们连接到其本地社区。 这是一个平台，邻居可以在这里交流、共享信息、了解当地活动和新闻的最新消息，并与所在地区的其他人一起买卖商品。

使用[[!DNL Nextdoor] 转换API扩展](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API)将转换事件直接发送到[!DNL Nextdoor's]转换API。 此扩展可通过发送服务器端转化数据，帮助您跟踪和衡量[!DNL Nextdoor]广告营销活动的效果。

本指南向您说明如何在事件转发[!DNL Nextdoor]规则[中安装、配置和使用](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules)转换API扩展。

## 先决条件 {#prerequisites}

您需要有效的[!DNL Nextdoor]广告管理器帐户才能使用此扩展。 如果您还没有帐户，请转到[[!DNL Nextdoor Ads] 注册页面](https://ads.nextdoor.com/v2/signup)进行注册并创建帐户。

### 收集所需的配置详细信息 {#configuration-details}

要将Experience Platform连接到[!DNL Nextdoor]，您需要以下信息：

| 凭据 | 描述 | 安全说明 |
| --- | --- | --- |
| 数据Source ID | [!DNL Nextdoor]中的唯一数据源标识符，可通过访问Assets > Pixels页并生成Nextdoor Pixel在[!DNL Nextdoor Ads Manager]帐户中找到。 | 可以在您的组织内安全共享此内容。 |
| 访问令牌 | 用于安全通信的API身份验证访问令牌。 您可以通过登录到[!DNL Nextdoor Ads Manager]帐户并访问API设置来生成此令牌。 | 确保此令牌的安全，因为它提供对您帐户的访问权限。 |

## 安装和配置[!DNL Nextdoor]扩展 {#install}

要安装扩展，请在左侧导航中选择&#x200B;**[!UICONTROL Extensions]**。 在&#x200B;**[!UICONTROL Catalog]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL Nextdoor Conversion API Extension]**，然后选择&#x200B;**[!UICONTROL Install]**。

![扩展目录显示[!DNL Nextdoor]扩展卡突出显示安装。](../../../images/extensions/server/nextdoor/install-extension.png)

在下一个屏幕上，输入从[!DNL Nextdoor Ads Manager]生成的配置值：

* **[!UICONTROL Data Source ID]**
* **[!UICONTROL Access Token]**

完成后，选择&#x200B;**[!UICONTROL Save]**。

![[!DNL Nextdoor]转换API扩展的[!DNL Nextdoor]配置屏幕。](../../../images/extensions/server/nextdoor/configure.png)

## 配置事件转发规则 {#config-rule}

设置所有数据元素后，即可创建事件转发规则，以确定将事件发送到[!DNL Nextdoor]的时间和方式。

在事件转发属性中创建新的[规则](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL Actions]**&#x200B;下，添加新操作并将扩展设置为&#x200B;**[!UICONTROL Nextdoor Conversion API Extension]**。 要将Edge Network事件发送到[!DNL Nextdoor]，请将&#x200B;**[!UICONTROL Action Type]**&#x200B;设置为&#x200B;**[!UICONTROL Report Web Conversions]**。

![为数据收集UI中的[!UICONTROL Report Web Conversions]规则选择的[!DNL Nextdoor]操作类型。](../../../images/extensions/server/nextdoor/select-action.png)

进行此选择后，将显示其他控件，允许您进一步配置事件，如下所述。 完成后，选择&#x200B;**[!UICONTROL Keep Changes]**&#x200B;以保存规则。

**主体参数**

以下核心参数定义您的转化事件：

| 参数 | 描述 | 数据类型 | 必需 | 选项/格式 | 示例 |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Event Name] | 指定要跟踪的转化事件的类型。 | 字符串（下拉列表） | 必需 | <ul><li>购买</li><li>潜在客户</li><li>注册</li><li>添加到购物车</li><li>启动签出</li><li>页面查看</li><li>搜索</li><li>查看内容</li><li>添加到愿望清单</li><li>订阅</li><li>自定义</li></li>转换1-10</li></ul> | `Purchase` |
| [!UICONTROL Event ID] | 用于防止报告重复事件的唯一标识符。 如果留空，将自动生成。 | 字符串 | 可选 | 唯一字符串标识符 | `order_12345` |
| [!UICONTROL Event Time (Unix Epoch)] | 发生转化事件的时间戳。 如果留空，则默认为当前时间。 | 整数 | 可选 | Unix时间戳（以秒为单位） | `1703980800` （2023年12月30日） |
| [!UICONTROL Action Source] | 发生转化的渠道或平台。 | 字符串（下拉列表） | 必需 | <ul><li>网站</li><li>电子邮件</li><li>应用程序</li><li>phone_call</li><li>聊天</li><li>physical_store</li><li>system_generate</li><li>其他</li></ul> | `website` |
| [!UICONTROL Data Source ID] | 覆盖特定事件的全局数据源ID。 如果留空，将从配置继承。 | 字符串 | 可选 | 字母数字字符串 | `12345` |
| [!UICONTROL Action Source URL] | 发生转换的特定URL。 | 字符串 | 可选 | 包含协议的完整URL | https://example.com/checkout/success |

**隐私和合规性参数**

请使用以下参数确保隐私合规性：

| 参数 | 描述 | 数据类型 | 必需 | 值/格式 | 示例 |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Restricted Data Usage] | 用于限制数据使用以实现隐私合规性的标记。 | 整数 | 可选 | <ul><li>0 =无限制</li><li>1 =限制</li></ul> | `0` |
| [!UICONTROL Restricted Data Usage (Country)] | 特定于国家/地区的数据处理限制。 | 整数 | 可选 | 1 =美国（可能支持其他代码） | `1` |
| [!UICONTROL Restricted Data Usage (State)] | 针对美国用户的特定州限制。 | 整数 | 可选 | 1000 = CA，1001 = CO等 | `1000` |
| [!UICONTROL Test Event] | 将事件标记为开发/调试测试。 | 字符串 | 可选 | 任何非空字符串 | `test` |

**客户信息参数**

>[!IMPORTANT]
>
>您必须至少提供一个客户信息参数，才能进行正确的事件归因和匹配。

| 参数 | 描述 | 数据类型 | 必需 | 格式 | 示例 |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL Email] | 用于身份匹配的客户电子邮件地址。 | 字符串 | 至少需要一个客户字段 | 纯文本或SHA-256哈希 | `user@example.com` |
| [!UICONTROL Phone Number] | 用于身份匹配的客户的电话号码。 | 字符串 | 至少需要一个客户字段 | E.164格式（使用SHA-256进行哈希处理） | `+15551234567` |
| [!UICONTROL First Name] | 用于增强匹配的客户的名字。 | 字符串 | 至少需要一个客户字段 | 纯文本或SHA-256哈希 | `John` |
| [!UICONTROL Last Name] | 用于增强匹配的客户的姓氏。 | 字符串 | 至少需要一个客户字段 | 纯文本或SHA-256哈希 | `Smith` |
| [!UICONTROL Date of Birth] | 用于人口统计匹配的客户的出生日期。 | 字符串 | 可选 | YYYYMMDD (SHA-256 hashed) | `19900115` |
| [!UICONTROL Gender] | 用于人口统计定位的客户性别。 | 字符串 | 可选 | M/F/O(SHA-256 hashed) | `M` |
| [!UICONTROL External ID] | 您的内部客户标识符。 | 字符串 | 可选 | 任何唯一字符串 | `customer_12345` |
| [!UICONTROL Street Address] | 客户的街道地址。 | 字符串 | 可选 | SHA-256哈希 | `123 Main Street` （散列） |
| [!UICONTROL City] | 客户的城市。 | 字符串 | 可选 | SHA-256哈希 | `San Francisco` （散列） |
| [!UICONTROL State] | 客户的省/市/自治区。 | 字符串 | 可选 | 双字母代码（SHA-256散列） | `CA` （散列） |
| [!UICONTROL Zip Code] | 客户的邮政编码。 | 字符串 | 可选 | 美国的前5位（SHA-256散列） | `94102` （散列） |
| [!UICONTROL Country] | 客户所在的国家/地区。 | 字符串 | 可选 | ISO-3166-1 alpha-2 （SHA-256哈希处理） | `US` （散列） |
| [!UICONTROL Click ID] | 归因的Nextdoor点击标识符。 | 字符串 | 可选 | 从`ndclid` URL参数捕获 | `nd_click_12345abcdef` |
| [!UICONTROL Client IP Address] | 用户设备的IP地址。 | 字符串 | 可选 | IPv4或IPv6地址 | `192.168.1.1` |
| [!UICONTROL Client User Agent] | 浏览器用户代理字符串。 | 字符串 | 可选 | 原始浏览器用户代理字符串 | `Mozilla/5.0 (Windows...)` |

**自定义参数**

以下参数提供有关转化事件的其他上下文：

| 参数 | 描述 | 数据类型 | 必需 | 格式 | 示例 |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Order Value] | 采购交易记录的总值。 | 字符串 | 购买事件需要&#x200B;**&#x200B;** | ISO 4217货币+金额（无空格） | `USD123.45` |
| [!UICONTROL Order ID] | 唯一交易或订单标识符。 | 字符串 | 可选 | 任何唯一字符串 | `order_12345` |
| [!UICONTROL Delivery Category] | 产品/服务交付方法。 | 字符串 | 可选 | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | 有关已购买产品的详细信息。 | 字符串（JSON数组） | 可选 | 产品对象的JSON数组 | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**移动应用参数**

`Action Source = 'APP'`时必须包含这些参数：

| 参数 | 描述 | 数据类型 | 必需 | 格式 | 示例 |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL App ID*] | 移动应用程序标识符。 | 字符串 | 应用程序事件需要&#x200B;**&#x200B;** | <ul><li>捆绑包ID (iOS)</li><li>包名称(Android)</li></ul> | `com.company.app` |
| [!UICONTROL App Tracking Enabled] | iOS应用程序跟踪透明度同意状态。 | 字符串 | 应用程序事件需要&#x200B;**&#x200B;** | 布尔字符串 | `true` |
| [!UICONTROL Platform] | 移动操作系统。 | 字符串 | 应用程序事件需要&#x200B;**&#x200B;** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL App Version] | 移动应用程序的版本。 | 字符串 | 应用程序事件需要&#x200B;**&#x200B;** | 应用程序定义的版本字符串 | `2.0.0-beta` |

## 事件类型 {#event-types}

不同的转化方案支持以下事件类型：

| 活动名称 | 事件类型 | 描述 | 用例 | 必填字段 | 注释 |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Purchase] | 标准 | 已完成采购交易记录。 | 电子商务转化 | <ul><li>活动名称</li><li>订单价值</li><li>客户信息</li></ul> | 对于ROAS优化最为重要 |
| [!UICONTROL Lead] | 标准 | 商机开发或查询。 | 表单提交、联系请求 | <ul><li>活动名称</li><li>客户信息</li></ul> | B2B的高值转换 |
| [!UICONTROL Sign Up] | 标准 | 用户注册或帐户创建。 | 新闻稿注册、帐户注册 | <ul><li>活动名称</li><li>客户信息</li></ul> | 顶级funnel转化跟踪 |
| [!UICONTROL Add to Cart] | 标准 | 产品已添加到购物车。 | 电子商务funnel跟踪 | <ul><li>活动名称</li><li>客户信息</li></ul> | Mid-funnel参与信号 |
| [!UICONTROL Initiate Checkout] | 标准 | 签出过程已开始。 | 购买意向跟踪 | <ul><li>活动名称</li><li>客户信息</li></ul> | 强购买意向指示器 |
| [!UICONTROL Page View] | 标准 | 访问的重要页面。 | 内容参与，登陆页面 | <ul><li>活动名称</li><li>客户信息</li></ul> | 仅用于高价值页面 |
| [!UICONTROL Search] | 标准 | 在站点上执行的搜索。 | 产品/内容发现 | <ul><li>活动名称</li><li>客户信息</li></ul> | 指示活动用户参与 |
| [!UICONTROL View Content] | 标准 | 已查看的内容或产品。 | 产品页面查看次数、内容参与度 | <ul><li>活动名称</li><li>客户信息</li></ul> | 对再营销受众非常有用 |
| [!UICONTROL Add to Wishlist] | 标准 | 产品已添加到愿望清单。 | 未来购买意图 | <ul><li>活动名称</li><li>客户信息</li></ul> | 表示强烈的产品兴趣 |
| [!UICONTROL Subscribe] | 标准 | 订阅服务/新闻稿。 | 经常性收入、参与度 | <ul><li>活动名称</li><li>客户信息</li></ul> | 高生命周期值指示器 |
| [!UICONTROL Custom Conversion 1 - 10] | 自定义 | 特定于业务的转化事件。 | 定义您自己的转化类型 | <ul><li>活动名称</li><li>客户信息</li></ul> | 针对独特的业务操作进行自定义 |

## 数据元素集成 {#data-element}

所有字段都支持Adobe事件转发数据元素。 选择任意字段旁边的数据元素图标![数据元素](../../../images/extensions/server/nextdoor/data-element-icon.png)以：

* **选择现有数据元素**：从已创建的数据元素中进行选择。
* **添加新数据元素**：根据需要创建和定义新数据元素。
* **应用动态值**：使用源自您网站的动态内容填充字段。

## 最佳做法 {#best-practices}

遵循这些最佳实践可确保准确的转化跟踪、提高数据质量并遵守隐私法规。 这些建议将帮助您最大限度地提高[!DNL Nextdoor]转化API集成的效率并优化广告性能。

### 数据质量和隐私合规性

正确的数据处理对于最大限度地提高转化归因准确性同时维护用户隐私和合规性至关重要。 这些实践有助于确保您的客户数据格式正确、处理安全并符合隐私法规。

* **使用一致的数据格式**：一致地格式化电子邮件、电话号码和其他数据：

   * **电子邮件标准化**：将电子邮件转换为小写，修剪空白，并从[!DNL Gmail]地址中删除圆点。
   * **电话号码标准化**：使用E.164格式(+1234567890)以获得国际兼容性。
   * **地址标准化**：标准化街道缩写(St.， Ave.， Rd.)，并删除任何额外的空格。
   * **名称格式**：将名称转换为小写，删除额外的空格，并一致处理特殊字符。

* **哈希敏感数据**：请考虑在发送敏感客户数据之前对其进行哈希处理。 在进行哈希处理之前，请始终标准化您的数据，以确保哈希值保持一致：

   * 对电话号码、地址和其他PII使用SHA-256哈希处理。
   * 扩展会自动对纯文本电子邮件进行哈希处理，您可以发送任一格式。
   * 在所有跟踪实施中始终使用哈希数据。
      * **示例**：在哈希处理之前将“John@Example.COM”→“john@example.com”标准化。

* **提供完整的信息**：尽可能多地包含客户信息以便更好地匹配：

   * 可用时包含多个标识符（电子邮件+电话，或电子邮件+姓名+地址）。
   * 使用外部客户ID将转化事件链接到您的CRM数据。
   * 提供人口统计数据（年龄、性别）（可用时）并遵守隐私法。

* **同意管理**：确保您对数据收集有适当的同意：

   * 在收集客户数据之前实施适当的同意机制。
   * 遵循用户选择退出偏好设置和数据删除请求。
   * 对已选择退出的用户使用“受限数据使用情况”参数。
   * **资源**：
      * [GDPR合规性指南](https://gdpr.eu/compliance/)
      * [CCPA隐私要求](https://oag.ca.gov/privacy/ccpa)

* **数据最小化**：仅发送转化跟踪所需的数据：

   * 仅收集和发送对归因和优化至关重要的数据。
   * 定期审查和审核您发送的数据字段。
   * 删除不必要的客户信息以降低隐私风险。

* **使用准确的时间戳**：确保事件时间戳准确无误，以便进行正确归因。
   * 使用发生转换的实际时间，而不是处理数据时的实际时间。
   * 确保时间戳采用Unix纪元格式（自1970年1月1日以来的秒数）。
   * 考虑时间戳计算中的时区差异。

### 事件去重

防止发生重复的转化事件，以确保准确衡量促销活动并避免夸大性能指标。 实施适当的重复数据删除，以便每次转化都只计数一次，从而为优化决策提供可靠的数据。

* **提供唯一事件ID**：始终使用唯一事件ID以防止重复转化。
* **使用一致的命名**：在您的实施中应用一致的事件命名。

### 速率限制

[!DNL Nextdoor]转换API受速率限制的约束。 当前速率限制为每个广告商&#x200B;**100个请求/分钟**。 如果超过速率限制，则API将返回`HTTP 429 Too Many Requests`错误代码。

## 结论 {#conclusion}

[!DNL Nextdoor]转化API扩展提供了一种强大的方法来跟踪转化并衡量[!DNL Nextdoor]广告营销活动的有效性。 通过遵循本指南并实施最佳实践，您可以确保准确的转化跟踪并优化广告效果。

有关最新信息和其他资源，请访问[[!DNL Nextdoor Ads Manager]](https://ads.nextdoor.com)。

## 后续步骤 {#next-steps}

本指南向您展示了如何使用[!DNL Nextdoor]转换API扩展将服务器端事件数据发送到[!DNL Nextdoor]。 若要详细了解[!DNL Adobe Experience Platform]中的事件转发功能，请参阅[事件转发概述](../../../ui/event-forwarding/overview.md)。
