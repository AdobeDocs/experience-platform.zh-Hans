---
title: 聊天源概述
description: 了解如何使用API或用户界面利用Webhook将Chatlio连接到Adobe Experience Platform
badge: 测试版
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>此 [!DNL Chatlio] 源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从流应用程序中摄取数据。 对流媒体提供商的支持包括 [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) 是一个与完全集成的实时聊天应用程序 [!DNL Slack] 和便于多个支持代理同时帮助单个网站访客。 [!DNL Chatlio] 使用 [!DNL Chatio Zapier App] 以连接 [!DNL Chatlio] 拥有2000多种不同的应用程序和服务。

此 [!DNL Chatlio] 源允许您从中摄取支持的webhook事件架构及其关联的事件数据 [!DNL Chatlio.com] 使用 [[!DNL Chatlio] Webhook](https://chatlio.com/docs/webhooks/).

支持的Webhook包括：

* 导出聊天记录
* 导出脱机消息
* 新对话已开始
* 访客未及时获得答案
* 访客在聊天后留下反馈

## 先决条件 {#prerequisites}

在创建 [!DNL Chatlio] 源连接中，您必须首先确保具有以下内容：

* A [!DNL Chatlio] 帐户。 如果您还没有这样的客户，请访问 [[!DNL Chatlio] 注册页面](https://chatlio.com/app/#/signup) 注册并创建您的帐户。
* 成功注册帐户后，请按照 [[!DNL Chatlio] 设置文档](https://chatlio.com/docs/setup/) 以完成帐户设置。

### 设置 [!DNL Chatlio] webhook {#set-up-webhook}

成功创建数据流后，必须设置webhook以通知Platform [!DNL Chatlio] 事件。 Webhook可以在客户属性发生更改或有人打开您的消息并将此信息发送给您的时立即通知您 [!DNL Chatlio] 源。

有关更多信息，请阅读上的教程 [获取您的流端点URL](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) 和 [设置 [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connect [!DNL Chatlio] 目标平台 {#connect-to-platform}

以下文档提供了有关如何创建 [!DNL Chatlio] 要连接的流连接器 [!DNL Platform] 使用API或用户界面：

### Connect [!DNL Chatlio] 到使用API的平台 {#connect-to-platform-using-api}

* [创建源连接以引入 [!DNL Chatlio] 使用API将数据发送到Platform。](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connect [!DNL Chatlio] 使用UI到Platform {#connect-to-platform-using-ui}

* [创建源连接以引入 [!DNL Chatlio] 使用用户界面将数据发送到Platform](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
