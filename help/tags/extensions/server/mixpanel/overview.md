---
keywords: 事件转发扩展；mixpanel；mixpanel事件转发扩展
title: Mixpanel跟踪事件API事件转发扩展
description: 此Adobe Experience Platform事件转发扩展可将Adobe Experience Edge Network事件发送到Mixpanel。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API事件转发扩展

[[!DNL Mixpanel]](https://www.mixpanel.com) 是一款产品分析工具，用于捕获有关用户如何与数字产品交互的数据。 您可以使用简单的交互式报表分析产品数据，只需单击几下即可查询和可视化数据。 [!DNL Mixpanel] 旨在通过允许所有人实时分析用户数据以确定趋势、了解用户行为并做出产品决策来提高团队效率。

[!DNL Mixpanel] 采用基于事件、以用户为中心的模型，将每个交互连接到单个用户。 此 [!DNL Mixpanel] 数据模型基于用户、事件和属性的概念构建。

>[!NOTE]
>
>请参阅 [!DNL Mixpanel] 相关文档 [身份管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) 了解如何 [!DNL Mixpanel] 合并事件以创建身份群集。 还建议您在以下位置查看文档： [不同ID](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) 以了解如何使用事件数据识别用户。

## 用例

如果要使用来自Edge Network的数据，应使用此扩展 [!DNL Mixpanel] 以利用其产品分析功能。

例如，假定零售组织具有多渠道存在（网站和移动设备）。 组织从其平台捕获事务性或对话性输入作为事件数据，并将其加载到 [!DNL Mixpanel] 使用事件转发扩展。

然后，分析团队可以利用 [!DNL Mixpanel's] 处理数据集和获取业务洞察的功能，可用于生成图形、仪表板或其他可视化图表以告知业务利益相关者。

有关特定用例的更多信息 [!DNL Mixpanel]，请参阅以下文档：

* [新到 [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [什么是 [!DNL Mixpanel]？](https://developer.mixpanel.com/docs)
* [12次必试 [!DNL Mixpanel] 功能](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] 先决条件 {#prerequisites-mixpanel}

您必须拥有有效的 [!DNL Mixpanel] 帐户，以便使用此扩展。 转到 [[!DNL Mixpanel] 注册页面](https://mixpanel.com/register/) 以注册并创建帐户（如果尚未注册）。

确保 [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) 已为您的项目启用设置。 导航到 **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** 并切换设置。

### 了解中的标识集群 [!DNL Mixpanel]

In [!DNL Mixpanel]，标识集群包含 `distinct_id` 连接到单个用户的值。 [!DNL Mixpanel] 处理每个用户的身份聚类，解析单个canonical `distinct_id` 报表中使用的每个群集。 您还可以包含自己的标识符(称为 `distinct_id`)对于发生于用户标识事件之前的匿名事件。

[!DNL Mixpanel] 通过两种方法解析标识群集：

* **识别** ： [!DNL Mixpanel] 将所选标识符连接到匿名标识符 `distinct_id`. 如果您的网站具有 [!DNL Mixpanel] SDK已启用，平台将使用 `distinct_id` 分配给当前登录的用户。
* **别名**： [!DNL Mixpanel] 合并两个非匿名 `distinct id`如果满足其他合并条件，则将其合并。

>[!NOTE]
>
>请参阅 [!DNL Mixpanel] 文档 [身份管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) 以了解有关这些方法的更多详细信息。
>
>确认您已启用 [[!DNL Mixpanel] 身份合并功能](#prerequisites-mixpanel) 以确保正确解析身份群集。

### 收集所需的配置详细信息 {#configuration-details}

为了将Experience Platform连接到 [!DNL Mixpanel] 必须输入以下内容：

| 键类型 | 描述 | 示例 |
| --- | --- | --- |
| 项目令牌 | 与您的关联的项目令牌 [!DNL Mixpanel] 帐户。 请参阅 [!DNL Mixpanel] 相关文档 [查找项目令牌](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) 以获取指导。 | `25470xxxxxxxxxxxxxxxxxxx1289` |

## 安装和配置 [!DNL Mixpanel] 扩展 {#install}

要安装扩展， [创建事件转发属性](../../../ui/event-forwarding/overview.md#properties) 或者选择现有的属性进行编辑。

选择 **[!UICONTROL 扩展]** 左侧导航栏中。 在 **[!UICONTROL 目录]** 选项卡，选择 **[!UICONTROL 安装]** 在的卡片上 [!DNL Mixpanel] 扩展。

![安装 [!DNL Mixpanel] 扩展。](../../../images/extensions/server/mixpanel/install-extension.png)

## 创建 [!DNL Send Event] 规则

开始在事件转发属性中创建新规则。 下 **[!UICONTROL 操作]**，添加新操作并将扩展设置为 **[!UICONTROL Mixpanel]**. 接下来，将操作类型设置为 **[!UICONTROL 跟踪事件]** 要将Adobe Experience Edge Network事件发送到 [!DNL Mixpanel].

| 输入 | 描述 | 必需 |
| --- | --- | --- |
| [!UICONTROL 项目令牌] | 此字段应当映射到与您的关联的项目令牌 [!DNL Mixpanel] 帐户。 | 是 |
| [!UICONTROL 事件类型] | 事件名称。 | 是 |
| [!UICONTROL 事件时间] | 事件时间。 | |
| [!UICONTROL Mixpanel非重复ID] | 执行事件的用户的唯一标识符。 | |
| [!UICONTROL 插入Id] | 事件的唯一标识符，用于重复数据删除。 | |
| [!UICONTROL 事件属性] | 包含事件的自定义属性的JSON对象。 从提供原始JSON或使用一组简化的键值输入中进行选择。 | |

>[!NOTE]
>
>有关a标准字段的更多信息 [!DNL Mixpanel] 事件，请参阅 [官方文档](https://developer.mixpanel.com/reference/import-events#event).

![添加事件转发规则操作配置。](../../../images/extensions/server/mixpanel/track-event-action.png)

一旦 [!UICONTROL 跟踪事件] 操作已添加到规则中，您可以配置规则的条件，使其仅对某些事件触发，也可以将条件部分留空以使规则对所有事件触发。

>[!IMPORTANT]
>
>如果您的网站使用 [!DNL Mixpanel] 在SDK中，您可以继续的下一步 [在中验证数据 [!DNL Mixpanel]](#validate). 如果您没有使用 [!DNL Mixpanel] SDK，您必须 [创建单独的身份跟踪规则](#create-an-identity-tracking-rule) 确保适当的事件及 `distinct_id` 值将发送到 [!DNL Mixpanel] 发生用户标识事件时。

## 验证数据 [!DNL Mixpanel] {#validate}

如果成功实施并收集了事件，您将会在 [[!DNL Mixpanel] 控制台](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

检查 [!DNL Mixpanel] 合并了填入了电子邮件值的发布登录事件和使用时创建的事件 **[!UICONTROL 发送事件]**. 如果实施正确， [!DNL Mixpanel] 会将它们与单个 [用户配置文件](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## 后续步骤

本指南介绍了如何将转化事件发送到 [!DNL Mixpanel] 使用事件转发。 此事件转发扩展可利用 [!DNL Mixpanel] SDK和JavaScript API。 有关这些底层技术的更多信息，请参阅官方文档：

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

有关Experience Platform中事件转发功能的详细信息，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
