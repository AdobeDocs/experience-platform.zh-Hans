---
keywords: 事件转发扩展；mixpanel;mixpanel事件转发扩展
title: Mixpanel跟踪事件API事件转发扩展
description: 此Adobe Experience Platform事件转发扩展会将Adobe Experience Edge Network事件发送到Mixpanel。
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API事件转发扩展

[[!DNL Mixpanel]](https://www.mixpanel.com) 是一款产品分析工具，可用于捕获有关用户与数字产品交互情况的数据。 您可以使用简单的交互式报表分析产品数据，通过该报表，只需单击几下即可查询和可视化数据。 [!DNL Mixpanel] 旨在通过允许每个人实时分析用户数据来识别趋势、了解用户行为并对产品做出决策，从而提高团队的效率。

[!DNL Mixpanel] 采用基于事件、以用户为中心的模型，将每次交互连接到单个用户。 的 [!DNL Mixpanel] 数据模型基于用户、事件和属性的概念构建。

>[!NOTE]
>
>请参阅 [!DNL Mixpanel] 文档 [身份管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) 了解如何 [!DNL Mixpanel] 合并事件以创建身份聚类。 还建议您在 [非重复ID](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) 以了解如何在事件数据中使用这些用户来标识用户。

## 用例

如果要在 [!DNL Mixpanel] 以利用其产品分析功能。

例如，假定零售组织拥有多渠道业务（网站和移动设备）。 该组织从其平台中捕获作为事件数据的事务性或对话式输入并将其加载到 [!DNL Mixpanel] 使用事件转发扩展。

然后，分析团队可以利用 [!DNL Mixpanel's] 用于处理数据集和获取业务分析的功能，可用于生成图形、功能板或其他可视化图表，以告知业务利益相关方。

有关特定用例的更多信息 [!DNL Mixpanel]，请参阅以下文档：

* [新 [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [什么是 [!DNL Mixpanel]？](https://developer.mixpanel.com/docs)
* [12次必试 [!DNL Mixpanel] 功能](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] 先决条件 {#prerequisites-mixpanel}

您必须拥有 [!DNL Mixpanel] 帐户来使用此扩展。 转到 [[!DNL Mixpanel] 注册页面](https://mixpanel.com/register/) 注册并创建帐户（如果尚未注册）。

确保 [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) 已为您的项目启用设置。 导航到 **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** 和切换设置。

### 了解中的身份聚类 [!DNL Mixpanel]

在 [!DNL Mixpanel]，标识群集包含 `distinct_id` 连接到单个用户的值。 [!DNL Mixpanel] 处理每个用户的标识群集，解析单个规范 `distinct_id` 从每个群集中报告。 您还可以包含自己的标识符（称为本地标识符） `distinct_id`)，用于用户标识事件之前发生的匿名事件。

[!DNL Mixpanel] 通过两种方法解析身份聚类：

* **识别** : [!DNL Mixpanel] 将您选择的标识符与匿名标识符关联 `distinct_id`. 如果您的网站具有 [!DNL Mixpanel] 启用了SDK，平台将使用 `distinct_id` 分配给当前已登录的用户。
* **别名**: [!DNL Mixpanel] 合并了两个非匿名 `distinct id`如果满足其他合并条件，则一起使用。

>[!NOTE]
>
>请参阅 [!DNL Mixpanel] 文档 [身份管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) 以了解有关这些方法的更多详细信息。
>
>确认您已启用 [[!DNL Mixpanel] 身份合并功能](#prerequisites-mixpanel) 以确保正确解析身份群集。

### 收集所需的配置详细信息 {#configuration-details}

将Experience Platform连接到 [!DNL Mixpanel] 您必须输入以下内容：

| 键类型 | 描述 | 示例 |
| --- | --- | --- |
| 项目令牌 | 与 [!DNL Mixpanel] 帐户。 请参阅 [!DNL Mixpanel] 文档 [查找项目令牌](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) 以获取指导。 | `25470xxxxxxxxxxxxxxxxxxx1289` |

## 安装和配置 [!DNL Mixpanel] 扩展 {#install}

要安装扩展，请 [创建事件转发属性](../../../ui/event-forwarding/overview.md#properties) 或选择要编辑的现有属性。

选择 **[!UICONTROL 扩展]** 中。 在 **[!UICONTROL 目录]** 选项卡，选择 **[!UICONTROL 安装]** 在 [!DNL Mixpanel] 扩展。

![安装 [!DNL Mixpanel] 扩展。](../../../images/extensions/server/mixpanel/install-extension.png)

## 创建 [!DNL Send Event] 规则

开始在事件转发属性中创建新规则。 在 **[!UICONTROL 操作]**，添加新操作并将扩展设置为 **[!UICONTROL Mixpanel]**. 接下来，将操作类型设置为 **[!UICONTROL 跟踪事件]** 将Adobe Experience Edge Network事件发送到 [!DNL Mixpanel].

| 输入 | 描述 | 必需 |
| --- | --- | --- |
| [!UICONTROL 项目令牌] | 此字段应映射到与 [!DNL Mixpanel] 帐户。 | 是 |
| [!UICONTROL 事件类型] | 事件名称。 | 是 |
| [!UICONTROL 事件时间] | 事件时间。 |  |
| [!UICONTROL Mixpanel Distinct ID] | 执行事件的用户的唯一标识符。 |  |
| [!UICONTROL 插入ID] | 事件的唯一标识符，用于重复数据删除。 |  |
| [!UICONTROL 事件属性] | 包含事件自定义属性的JSON对象。 从提供原始JSON或使用一组简化的键值输入中进行选择。 |  |

>[!NOTE]
>
>有关 [!DNL Mixpanel] 事件，请参阅 [官方文档](https://developer.mixpanel.com/reference/import-events#event).

![添加事件转发规则操作配置。](../../../images/extensions/server/mixpanel/track-event-action.png)

一旦 [!UICONTROL 跟踪事件] 操作会添加到规则中，您可以配置规则的条件，以便该规则仅针对某些事件触发，或者将条件部分留空，以使规则针对所有事件触发。

>[!IMPORTANT]
>
>如果您的网站使用 [!DNL Mixpanel] SDK中，您可以继续执行 [验证数据 [!DNL Mixpanel]](#validate). 如果您没有使用 [!DNL Mixpanel] SDK，您必须 [创建单独的身份跟踪规则](#create-an-identity-tracking-rule) 确保适当的事件和 `distinct_id` 值会发送到 [!DNL Mixpanel] 用户标识事件发生时。

## 在中验证数据 [!DNL Mixpanel] {#validate}

如果您的实施成功且收集了事件，您将在 [[!DNL Mixpanel] 控制台](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

检查 [!DNL Mixpanel] 已合并使用电子邮件值填充的登录后事件以及使用 **[!UICONTROL 发送事件]**. 如果实施正确， [!DNL Mixpanel] 将他们与 [用户配置文件](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## 后续步骤

本指南介绍了如何将转化事件发送到 [!DNL Mixpanel] 使用事件转发。 此事件转发扩展可利用 [!DNL Mixpanel] SDK和JavaScript API。 有关这些基础技术的更多信息，请参阅官方文档：

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

有关Experience Platform中事件转发功能的更多信息，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
