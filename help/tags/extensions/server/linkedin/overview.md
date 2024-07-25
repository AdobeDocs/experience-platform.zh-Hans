---
title: Linkedin转化API事件转发扩展
description: 通过这个Adobe Experience Platform事件转发扩展，您可以衡量Linkedin营销活动的效果。
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# [!DNL LinkedIn] 转化 API 扩展

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api)是一种转化跟踪工具，用于在来自广告商服务器的营销数据与[!DNL LinkedIn]之间建立直接连接。 这使广告商能够评估其[!DNL LinkedIn]营销活动的有效性，而不管转化的位置如何，并利用此信息推动营销活动优化。 [!DNL LinkedIn Conversions API]扩展可通过更完整的归因、改进的数据可靠性和更好的优化交付，帮助增强性能并降低每次操作的成本。

## 先决条件 {#prerequisites}

您必须在您的[!DNL LinkedIn Campaign Manager]帐户中[创建转化规则](https://www.linkedin.com/help/lms/answer/a1657171)。 [!DNL Adobe]建议在对话规则名称的开头包含“CAPI”，以使其不同于您可能已配置的其他转化规则类型。

### 创建密钥和数据元素

创建新的[!DNL LinkedIn] [事件转发密码](../../../ui/event-forwarding/secrets.md)，并为它提供一个表示身份验证成员的唯一名称。 这将用于验证与您的帐户的连接，同时保持值的安全。

接下来，[使用[!UICONTROL Core]扩展和[!UICONTROL Secret]数据元素类型创建数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element)以引用您刚刚创建的`LinkedIn`密码。

## 安装和配置[!DNL LinkedIn]扩展 {#install}

若要安装该扩展，请[创建事件转发属性](../../../ui/event-forwarding/overview.md#properties)或选择要编辑的现有属性。

在左侧导航中选择&#x200B;**[!UICONTROL 扩展]**。 在&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL LinkedIn]**&#x200B;扩展，然后选择&#x200B;**[!UICONTROL 安装]**。

![扩展目录显示[!DNL LinkedIn]扩展卡突出显示安装。](../../../images/extensions/server/linkedin/install-extension.png)

在下一个屏幕上，在`Access Token`字段中输入您之前创建的数据元素密码。 数据元素密钥将包含您的[!DNL LinkedIn] OAuth 2令牌。 完成后选择&#x200B;**[!UICONTROL 保存]**。

![突出显示包含[!UICONTROL 访问令牌]字段和[!UICONTROL 保存]的[!DNL LinkedIn]扩展配置页面。](../../../images/extensions/server/linkedin/configure-extension.png)

## 创建[!DNL Send Conversion]规则 {#tracking-rule}

设置完所有数据元素后，即可开始创建事件转发规则，以确定将事件发送到[!DNL LinkedIn]的时间和方式。

在事件转发属性中创建新事件转发[规则](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL 操作]**&#x200B;下，添加新操作并将扩展设置为&#x200B;**[!UICONTROL LinkedIn]**。 接下来，为&#x200B;**[!UICONTROL 操作类型]**&#x200B;选择&#x200B;**[!UICONTROL 发送转换]**。

![事件转发属性规则视图，突出显示添加事件转发规则操作配置所需的字段。](../../../images/extensions/server/linkedin/linkedin-event-action.png)

选择后，会显示其他控件以进一步配置事件。 选择&#x200B;**[!UICONTROL 保留更改]**&#x200B;以保存规则。

**[!UICONTROL 用户数据]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 电子邮件] | 与转化事件关联的联系人的电子邮件地址。 除非提供的值已经是SHA256字符串，否则电子邮件值将由SHA256中的扩展代码编码。 |
| [!UICONTROL LinkedIn第一方广告跟踪UUID] | 这是第一方Cookie ID。 广告商需要启用来自[[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag)的增强型转化跟踪，以激活将点击ID参数`li_fat_id`附加到点击URL的第一方Cookie。 |
| [!UICONTROL 客户信息数据] | 此字段包含具有额外属性的JSON对象，这些属性将与消息一起发送。<br><br>在&#x200B;**[!UICONTROL 原始]**&#x200B;选项下，您可以将JSON对象直接粘贴到提供的文本字段中，也可以选择数据元素图标（![数据集图标](/help/images/icons/database.png)）以从现有数据元素列表中进行选择来表示数据。<br><br>您还可以使用&#x200B;**[!UICONTROL JSON键值对编辑器]**&#x200B;选项通过UI编辑器手动添加每个键值对。 每个值都可以用原始输入表示，也可以改为选择数据元素。 接受的键值为： `firstName`、`lastName`、`companyName`、`title`和`country`。 |

{style="table-layout:auto"}

![显示输入到字段中的示例数据的[!DNL User Data]部分。](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL 转化数据]**

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 转换] | 在[LinkedIn促销活动管理器](https://www.linkedin.com/help/lms/answer/a1657171)中创建的转化规则的ID。 选择转换规则以获取ID，然后从浏览器URL中复制ID（例如，`/campaignmanager/accounts/508111232/conversions/15588877`）作为`/conversions/<id>`。 |
| [!UICONTROL 转换时间] | 转化事件发生的每个时间戳（以毫秒为单位）。 <br><br>注意：如果您的源记录转换时间戳（以秒为单位），请在结尾插入000以将其转换为毫秒。 |
| [!UICONTROL 货币] | ISO格式的货币代码。 |
| [!UICONTROL 金额] | 以小数字符串表示的转换值（例如，“100.05”）。 |
| [!UICONTROL 事件ID] | 广告商为指示每个事件而生成的唯一ID。 这是可选字段，用于[重复数据删除](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02)。 |

{style="table-layout:auto"}

![显示字段中的示例数据的[!DNL Conversion Data]部分。](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL 配置覆盖]**

>注意
>
>[!UICONTROL 配置覆盖]字段允许用户在每个规则上设置不同的[!DNL LinkedIn]访问令牌，从而允许每个规则使用可能有权访问不同[!DNL LinkedIn]广告帐户的访问令牌。

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 访问令牌] | [!DNL LinkedIn]访问令牌。 |

![显示字段输入示例数据的[!DNL Configuration Overrides]部分。](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## 后续步骤

本指南介绍了如何使用[!DNL LinkedIn Conversions API]事件转发扩展将数据发送到[!DNL LinkedIn]。 有关[!DNL Adobe Experience Platform]中事件转发功能的详细信息，请阅读[事件转发概述](../../../ui/event-forwarding/overview.md)。

有关如何使用Debugger和Event Forwarding Monitoring工具调试Experience Platform的详细信息，请阅读[Adobe Experience Platform Debugger概述](../../../../debugger/home.md)和[监视事件转发中的活动](../../../ui/event-forwarding/monitoring.md)。
