---
title: Google Cloud Platform事件转发扩展
description: 此Adobe Experience Platform事件转发扩展将边缘网络事件发送到Google Cloud Platform。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# [!DNL Google Cloud Platform] 事件转发扩展

[[!DNL Google Cloud Platform]](https://cloud.google.com/) 是一个云计算平台，提供多种服务，如分布式计算、数据库存储、内容交付，以及用于客户关系管理(CRM)和企业资源规划(ERP)的软件即服务(SaaS)集成服务。

此 [!DNL Google Cloud Platform] [事件转发](../../../ui/event-forwarding/overview.md) 扩展利用 [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) 将事件从Adobe Experience Platform Edge Network发送到 [!DNL Google Cloud Platform] 以进行进一步处理。 本指南介绍如何安装扩展并在事件转发规则中部署其功能。

## 先决条件

要使用此扩展，您必须拥有 [!DNL Google Cloud Platform] 具有现有帐户的帐户 [!DNL Cloud Pub/Sub] 主题。 如果您没有预先存在的主题，请参阅 [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) 有关创建和管理主题的文档。

### 创建密钥和数据元素

首先，创建一个新的 `Google OAuth 2` [事件转发密码](../../../ui/event-forwarding/secrets.md)，用于验证与您的帐户的连接，同时保持值的安全。

下一步， [创建数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 使用 **[!UICONTROL 核心]** 扩展和 **[!UICONTROL 密码]** 要引用 `Google OAuth 2` 你刚刚创建的密码。

## 安装和配置 [!DNL Google Cloud Platform] 扩展 {#install}

要安装扩展， [创建事件转发属性](../../../ui/event-forwarding/overview.md#properties) 或者选择现有的属性进行编辑。

选择 **[!UICONTROL 扩展]** 在左侧导航中。 在 **[!UICONTROL 目录]** 选项卡，选择 **[!UICONTROL 安装]** 在的卡片上 [!DNL Google Cloud Platform] 扩展。

![目录 [!DNL Google Cloud Platform] 扩展突出显示安装。](../../../images/extensions/server/google-cloud-platform/install-extension.png)

在配置屏幕上，将您之前创建的数据元素密码输入到 **[!UICONTROL 访问令牌]** 字段。 数据元素密钥将包含 [!DNL Google Cloud Platform] Oauth 2令牌。 选择 **[!UICONTROL 保存]** 完成后。

![此 [!DNL Google Cloud Platform] 扩展配置页面。](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## 创建 [!DNL Send Data to Cloud Pub/Sub] 规则 {#tracking-rule}

安装扩展后，请创建新的事件转发 [规则](../../../ui/managing-resources/rules.md) 并根据需要配置其条件。 配置规则的操作时，选择 **[!UICONTROL Google Cloud平台]** 扩展，然后选择 **[!UICONTROL 将数据发送到Cloud Pub/Sub]** 操作类型的。

![操作配置视图 [!UICONTROL Google Cloud平台]，并突出显示操作 [!UICONTROL 将数据发送到Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 主题] | 将从事件转发接收事件的主题。 值必须具有格式 `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL 数据] | 此字段包含要转发到的数据 [!DNL Cloud Pub/Sub] JSON格式的主题。<br><br>在 **[!UICONTROL 原始]** 选项，您可以将JSON对象直接粘贴到提供的文本字段中，或者选择数据元素图标(![数据集图标](../../../images/extensions/server/aws/data-element-icon.png))以从现有数据元素列表中进行选择以表示数据。<br><br>您也可以使用 **[!UICONTROL JSON键值对编辑器]** 选项，用于通过UI编辑器手动添加每个键值对。 每个值都可以用原始输入表示，也可以改为选择数据元素。 |
| [!UICONTROL 属性] | 此字段包含具有额外属性的JSON对象，将与消息一起发送。<br><br>在 **[!UICONTROL 原始]** 选项，您可以将JSON对象直接粘贴到提供的文本字段中，或者选择数据元素图标(![数据集图标](../../../images/extensions/server/aws/data-element-icon.png))以从现有数据元素列表中进行选择以表示数据。<br><br>您也可以使用 **[!UICONTROL JSON键值对编辑器]** 选项，用于通过UI编辑器手动添加每个键值对。 每个值都可以用原始输入表示，也可以改为选择数据元素。 |

{style="table-layout:auto"}

## 后续步骤

本指南介绍如何将数据发送到 [!DNL Cloud Pub/Sub] 使用 [!DNL Google Cloud Platform] 事件转发扩展。 有关Experience Platform中事件转发功能的详细信息，请参阅 [事件转发概述](../../../ui/event-forwarding/overview.md).
