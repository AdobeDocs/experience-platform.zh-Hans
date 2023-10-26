---
title: Linkedin转化API事件转发扩展
description: 通过这个Adobe Experience Platform事件转发扩展，您可以衡量Linkedin营销活动的效果。
last-substantial-update: 2023-10-25T00:00:00Z
source-git-commit: ca65f010cda5d37c40fd57075a26e365c76bdc0b
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 1%

---

# [!DNL LinkedIn] 转化 API 扩展

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) 是一个转化跟踪工具，用于在来自广告商服务器的营销数据与 [!DNL LinkedIn]. 这使广告商能够评估其有效性 [!DNL LinkedIn] 营销活动，无论转换的位置如何，都可利用此信息来推动活动优化。 此 [!DNL LinkedIn Conversions API] 扩展可通过更完整的归因、改进的数据可靠性和更好的优化交付，帮助增强性能并降低每次操作的成本。

## 先决条件 {#prerequisites}

您必须在 [!DNL LinkedIn] 营销活动广告帐户。 [!DNL Adobe] 建议在对话规则名称的开头包含“CAPI”，以将其与您可能已配置的其他转化规则类型区分开来。

### 创建密钥和数据元素

新建 `LinkedIn` [事件转发密码](../../../ui/event-forwarding/secrets.md) 并为它提供一个唯一的名称，以表示进行身份验证的成员。 这将用于验证与您的帐户的连接，同时保持值的安全。

下一步， [创建数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 使用 [!UICONTROL 核心] 扩展和 [!UICONTROL 密码] 要引用 `LinkedIn` 你刚刚创建的密码。

## 安装和配置 [!DNL LinkedIn] 扩展 {#install}

要安装扩展， [创建事件转发属性](../../../ui/event-forwarding/overview.md#properties) 或选择要编辑的现有属性。

选择 **[!UICONTROL 扩展]** 在左侧导航中。 在 **[!UICONTROL 目录]** 选项卡，选择 **[!UICONTROL linkedIn]** 扩展，然后选择 **[!UICONTROL 安装]**.

![扩展目录显示 [!DNL LinkedIn] 扩展卡突出显示安装。](../../../images/extensions/server/linkedin/install-extension.png)

在下一个屏幕中，将您之前创建的数据元素密码输入到 `Access Token` 字段。 数据元素密钥将包含 [!DNL LinkedIn] Oauth 2令牌。 选择 **[!UICONTROL 保存]** 完成后。

![此 [!DNL LinkedIn] 扩展配置页面，其中包含 [!UICONTROL 访问令牌] 字段和 [!UICONTROL 保存] 突出显示。](../../../images/extensions/server/linkedin/configure-extension.png)

## 创建 [!DNL Send Conversion] 规则 {#tracking-rule}

设置完所有数据元素后，您可以开始创建事件转发规则，以确定将事件发送到的时间和方式 [!DNL LinkedIn].

创建新的事件转发 [规则](../../../ui/managing-resources/rules.md) 在事件转发属性中。 下 **[!UICONTROL 操作]**，添加新操作并将扩展设置为 **[!UICONTROL linkedIn]**. 接下来，选择 **[!UICONTROL 发送Web转换]** 对于 **[!UICONTROL 操作类型]**.

![Event Forwarding Property Rules视图，突出显示添加事件转发规则操作配置所需的字段。](../../../images/extensions/server/linkedin/linkedin-event-action.png)

选择后，会显示其他控件以进一步配置事件。 选择 **[!UICONTROL 保留更改]** 以保存规则。

**[!UICONTROL 用户数据]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 电子邮件] | 与转化事件关联的联系人的电子邮件地址。 除非提供的值已经是SHA256字符串，否则电子邮件值将由SHA256中的扩展代码编码。 |
| [!UICONTROL linkedIn第一方广告跟踪UUID] | 这是第一方Cookie ID。 广告商需要启用增强的转化跟踪 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) 要激活附加了点击ID参数的第一方Cookie，请执行以下操作 `li_fat_id` 到单击URL。 |
| [!UICONTROL 客户信息数据] | 此字段包含具有额外属性的JSON对象，这些属性将与消息一起发送。<br><br>在 **[!UICONTROL 原始]** 选项，您可以将JSON对象直接粘贴到提供的文本字段中，或者选择数据元素图标(![数据集图标](../../../images/extensions/server/aws/data-element-icon.png))以从现有数据元素列表中进行选择以表示数据。<br><br>您也可以使用 **[!UICONTROL JSON键值对编辑器]** 选项，用于通过UI编辑器手动添加每个键值对。 每个值都可以用原始输入表示，也可以改为选择数据元素。 接受的键值为： `firstName`， `lastName`， `companyName`， `title` 和 `country`. |

{style="table-layout:auto"}

![此 [!DNL User Data] 部分显示了输入到字段中的示例数据。](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL 转化数据]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 转化] | 在中创建的转化规则的ID [linkedIn营销活动管理器](https://www.linkedin.com/help/lms/answer/a1657171) 或通过 [!DNL LinkedIn Campaign Manager]. |
| [!UICONTROL 转化时间] | 转化事件发生的每个时间戳（以毫秒为单位）。 <br><br> 注意：如果源以秒为单位记录转化时间戳，请在结尾插入000以将其转换为毫秒。 |
| [!UICONTROL 货币] | ISO格式的货币代码。 |
| [!UICONTROL 数量] | 以小数字符串表示的转换值（例如，“100.05”）。 |
| [!UICONTROL 事件ID] | 广告商为指示每个事件而生成的唯一ID。 这是一个可选字段，用于删除重复项。 |

{style="table-layout:auto"}

![此 [!DNL Conversion Data] 部分显示字段中的示例数据。](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL 配置覆盖]**

>注意
>
>此 [!UICONTROL 配置覆盖] 字段允许用户设置其他 [!DNL LinkedIn] 访问每个规则的令牌，从而允许每个规则使用可能有权访问不同 [!DNL LinkedIn] 广告帐户。

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 访问令牌] | 此 [!DNL LinkedIn] 访问令牌。 |

![此 [!DNL Configuration Overrides] 部分显示字段中的示例数据输入。](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## 后续步骤

本指南介绍了如何将数据发送到 [!DNL LinkedIn] 使用 [!DNL LinkedIn Conversions API] 事件转发扩展。 有关中的事件转发功能的详细信息 [!DNL Adobe Experience Platform]，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
