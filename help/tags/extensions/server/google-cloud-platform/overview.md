---
title: Google Cloud Platform事件转发扩展
description: 此Adobe Experience Platform事件转发扩展可将Edge Network事件发送到Google Cloud Platform。
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---

# [!DNL Google Cloud Platform] 事件转发扩展

[[!DNL Google Cloud Platform]](https://cloud.google.com/)是一个云计算平台，它提供了多种服务，如分布式计算、数据库存储、内容交付，以及用于客户关系管理(CRM)和企业资源规划(ERP)的软件即服务(SaaS)集成服务。

[!DNL Google Cloud Platform] [事件转发](../../../ui/event-forwarding/overview.md)扩展利用[[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub)将事件从Adobe Experience PlatformEdge Network发送到[!DNL Google Cloud Platform]以供进一步处理。 本指南介绍如何安装扩展并在事件转发规则中部署其功能。

## 先决条件

若要使用此扩展，您必须具有包含现有[!DNL Cloud Pub/Sub]主题的[!DNL Google Cloud Platform]帐户。 如果您没有预先存在的主题，请参阅有关创建和管理主题的[[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic)文档。

### 创建密钥和数据元素

首先，创建一个新的`Google OAuth 2` [事件转发密码](../../../ui/event-forwarding/secrets.md)，该密码将用于验证与您的帐户的连接，同时保证值安全。

接下来，[使用&#x200B;**[!UICONTROL Core]**&#x200B;扩展和&#x200B;**[!UICONTROL Secret]**&#x200B;数据元素类型创建数据元素](../../../ui/managing-resources/data-elements.md#create-a-data-element)以引用您刚刚创建的`Google OAuth 2`密码。

## 安装和配置[!DNL Google Cloud Platform]扩展 {#install}

若要安装该扩展，请[创建事件转发属性](../../../ui/event-forwarding/overview.md#properties)或选择现有属性进行编辑。

在左侧导航中选择&#x200B;**[!UICONTROL 扩展]**。 在&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中，在[!DNL Google Cloud Platform]扩展的卡片中选择&#x200B;**[!UICONTROL 安装]**。

![目录[!DNL Google Cloud Platform]扩展突出显示安装。](../../../images/extensions/server/google-cloud-platform/install-extension.png)

在配置屏幕上，在&#x200B;**[!UICONTROL 访问令牌]**&#x200B;字段中输入您之前创建的数据元素密码。 数据元素密钥将包含您的[!DNL Google Cloud Platform] OAuth 2令牌。 完成后选择&#x200B;**[!UICONTROL 保存]**。

![扩展配置页面[!DNL Google Cloud Platform]。](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## 创建[!DNL Send Data to Cloud Pub/Sub]规则 {#tracking-rule}

安装扩展后，创建新的事件转发[规则](../../../ui/managing-resources/rules.md)并根据需要配置其条件。 配置规则的操作时，请选择&#x200B;**[!UICONTROL Google Cloud Platform]**&#x200B;扩展，然后选择操作类型的&#x200B;**[!UICONTROL 将数据发送到Cloud Pub/Sub]**。

![[!UICONTROL Google Cloud Platform]的操作配置视图（该操作已突出显示）和[!UICONTROL 将数据发送到Cloud Pub/Sub]。](../../../images/extensions/server/google-cloud-platform/event-action.png)

| 输入 | 描述 |
| --- | --- |
| [!UICONTROL 主题] | 将从事件转发接收事件的主题。 值的格式必须为`projects/{projectName}/topics/{topicName}`。 |
| [!UICONTROL 数据] | 此字段包含要以JSON格式转发到[!DNL Cloud Pub/Sub]主题的数据。<br><br>在&#x200B;**[!UICONTROL 原始]**&#x200B;选项下，您可以将JSON对象直接粘贴到提供的文本字段中，也可以选择数据元素图标（![数据集图标](../../../images/extensions/server/aws/data-element-icon.png)）以从现有数据元素列表中进行选择来表示数据。<br><br>您还可以使用&#x200B;**[!UICONTROL JSON键值对编辑器]**&#x200B;选项通过UI编辑器手动添加每个键值对。 每个值都可以用原始输入表示，也可以改为选择数据元素。 |
| [!UICONTROL 属性] | 此字段包含具有额外属性的JSON对象，将与消息一起发送。<br><br>在&#x200B;**[!UICONTROL 原始]**&#x200B;选项下，您可以将JSON对象直接粘贴到提供的文本字段中，也可以选择数据元素图标（![数据集图标](../../../images/extensions/server/aws/data-element-icon.png)）以从现有数据元素列表中进行选择来表示数据。<br><br>您还可以使用&#x200B;**[!UICONTROL JSON键值对编辑器]**&#x200B;选项通过UI编辑器手动添加每个键值对。 每个值都可以用原始输入表示，也可以改为选择数据元素。 |

{style="table-layout:auto"}

## 后续步骤

本指南介绍如何使用[!DNL Google Cloud Platform]事件转发扩展将数据发送到[!DNL Cloud Pub/Sub]。 有关Experience Platform中事件转发功能的详细信息，请参阅[事件转发概述](../../../ui/event-forwarding/overview.md)。
