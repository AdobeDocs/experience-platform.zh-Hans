---
keywords: 事件转发扩展；mixpanel；mixpanel事件转发扩展
title: Mixpanel跟踪事件API事件转发扩展
description: 此Adobe Experience Platform事件转发扩展将Edge Network事件发送到Mixpanel。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API事件转发扩展

[[!DNL Mixpanel]](https://www.mixpanel.com)是一种产品分析工具，允许您捕获有关用户如何与数字产品交互的数据。 您可以使用简单的交互式报表分析产品数据，这些报表只需点击几下即可查询和可视化数据。 [!DNL Mixpanel]旨在通过允许所有人实时分析用户数据以确定趋势、了解用户行为并做出产品决策来提高团队效率。

[!DNL Mixpanel]采用基于事件的以用户为中心的模型，将每个交互连接到单个用户。 [!DNL Mixpanel]数据模型基于用户、事件和属性的概念构建。

>[!NOTE]
>
>请参阅有关[身份管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management)的[!DNL Mixpanel]文档，了解[!DNL Mixpanel]如何合并事件以创建身份群集。 还建议您查看有关[不同ID](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-)的文档，以了解如何在事件数据中使用它们来标识用户。

## 用例

如果要在[!DNL Mixpanel]中使用Edge Network中的数据以利用其产品分析功能，则应该使用此扩展。

例如，以具有多渠道存在（网站和移动设备）的零售组织为例。 组织从其平台捕获事务性或对话性输入作为事件数据，并使用事件转发扩展将其加载到[!DNL Mixpanel]中。

然后，分析团队可以利用[!DNL Mixpanel's]功能处理数据集并获取业务见解，该功能可用于生成图形、功能板或其他可视化以告知业务利益相关者。

有关特定于[!DNL Mixpanel]的使用案例的详细信息，请参阅以下文档：

* [新用户 [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [什么是 [!DNL Mixpanel]？](https://developer.mixpanel.com/docs)
* [12必须尝试 [!DNL Mixpanel] 功能](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel]先决条件 {#prerequisites-mixpanel}

您必须拥有有效的[!DNL Mixpanel]帐户才能使用此扩展。 转到[[!DNL Mixpanel] 注册页面](https://mixpanel.com/register/)进行注册并创建帐户（如果还没有帐户）。

请确保已为您的项目启用[[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices)设置。 导航到&#x200B;**[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]**&#x200B;并切换设置。

### 了解[!DNL Mixpanel]中的标识群集

在[!DNL Mixpanel]中，标识群集包含连接到单个用户的`distinct_id`值的集合。 [!DNL Mixpanel]处理每个用户的标识群集，从每个群集中解析一个要用于报告的规范`distinct_id`。 您还可以包含您自己的标识符（称为本地`distinct_id`），用于用户标识事件之前发生的匿名事件。

[!DNL Mixpanel]通过两种方法解析标识群集：

* **标识** ： [!DNL Mixpanel]将您选择的标识连接到匿名`distinct_id`。 如果您的网站启用了[!DNL Mixpanel] SDK，Experience Platform将使用分配给当前登录用户的`distinct_id`。
* **别名**： [!DNL Mixpanel]在满足其他合并条件时将两个非匿名`distinct id`合并在一起。

>[!NOTE]
>
>有关这些方法的更多详细信息，请参阅[身份管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification)上的[!DNL Mixpanel]文档。
>
>确认您已启用[[!DNL Mixpanel] 身份合并功能](#prerequisites-mixpanel)，以确保正确解析身份群集。

### 收集所需的配置详细信息 {#configuration-details}

要将Experience Platform连接到[!DNL Mixpanel]，您必须输入以下内容：

| 键类型 | 描述 | 示例 |
| --- | --- | --- |
| 项目令牌 | 与您的[!DNL Mixpanel]帐户关联的项目令牌。 有关指导，请参阅有关[查找项目令牌](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-)的[!DNL Mixpanel]文档。 | `25470xxxxxxxxxxxxxxxxxxx1289` |

## 安装和配置[!DNL Mixpanel]扩展 {#install}

若要安装该扩展，请[创建事件转发属性](../../../ui/event-forwarding/overview.md#properties)或选择现有属性进行编辑。

在左侧导航中选择&#x200B;**[!UICONTROL 扩展]**。 在&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中，在[!DNL Mixpanel]扩展的卡片中选择&#x200B;**[!UICONTROL 安装]**。

![正在安装[!DNL Mixpanel]扩展。](../../../images/extensions/server/mixpanel/install-extension.png)

## 创建[!DNL Send Event]规则

开始在事件转发属性中创建新规则。 在&#x200B;**[!UICONTROL 操作]**&#x200B;下，添加新操作并将扩展设置为&#x200B;**[!UICONTROL Mixpanel]**。 接下来，将操作类型设置为&#x200B;**[!UICONTROL 跟踪事件]**&#x200B;以将Edge Network事件发送到[!DNL Mixpanel]。

| 输入 | 描述 | 必需 |
| --- | --- | --- |
| [!UICONTROL 项目令牌] | 此字段应当映射到与您的[!DNL Mixpanel]帐户关联的项目令牌。 | 是 |
| [!UICONTROL 事件类型] | 事件名称。 | 是 |
| [!UICONTROL 事件时间] | 事件时间。 | |
| [!UICONTROL Mixpanel非重复ID] | 执行事件的用户的唯一标识符。 | |
| [!UICONTROL 插入ID] | 事件的唯一标识符，用于重复数据删除。 | |
| [!UICONTROL 事件属性] | 包含事件的自定义属性的JSON对象。 从提供原始JSON或使用一组简化的键值输入中进行选择。 | |

>[!NOTE]
>
>有关[!DNL Mixpanel]事件的标准字段的更多信息，请参阅[官方文档](https://developer.mixpanel.com/reference/import-events#event)。

![添加事件转发规则操作配置。](../../../images/extensions/server/mixpanel/track-event-action.png)

将[!UICONTROL Track Event]操作添加到规则后，您可以配置规则的条件，使其仅对特定事件触发，或者将条件部分留空以使规则对所有事件触发。

>[!IMPORTANT]
>
>如果您的网站使用的是[!DNL Mixpanel] SDK，则可以继续下一步操作： [在 [!DNL Mixpanel]](#validate)内验证您的数据。 如果您未使用[!DNL Mixpanel] SDK，则必须[创建单独的身份跟踪规则](#create-an-identity-tracking-rule)，以确保在发生用户识别事件时，将适当的事件和`distinct_id`值发送到[!DNL Mixpanel]。

## 验证[!DNL Mixpanel]中的数据 {#validate}

如果实施成功且已收集事件，您将会在[[!DNL Mixpanel] 控制台](https://help.mixpanel.com/hc/en-us/articles/4402837164948)中看到事件。

检查[!DNL Mixpanel]是否已合并使用电子邮件值填充的帖子登录事件和使用&#x200B;**[!UICONTROL 发送事件]**&#x200B;时创建的事件。 如果实施正确，[!DNL Mixpanel]会将它们与单个[用户配置文件](https://help.mixpanel.com/hc/en-us/articles/115004501966)相关联。

## 后续步骤

本指南介绍了如何使用事件转发将转化事件发送到[!DNL Mixpanel]。 此事件转发扩展利用[!DNL Mixpanel] SDK和JavaScript API。 有关这些底层技术的更多信息，请参阅官方文档：

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

有关Experience Platform中事件转发功能的更多信息，请参阅[事件转发概述](../../../ui/event-forwarding/overview.md)。
