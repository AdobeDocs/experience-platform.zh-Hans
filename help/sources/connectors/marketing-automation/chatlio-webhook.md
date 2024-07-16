---
title: Chatlio Source概述
description: 了解如何使用API或用户界面利用Webhook将Chatlio连接到Adobe Experience Platform
badge: Beta 版
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>[!DNL Chatlio]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从流式应用程序引入数据。 对流式提供程序的支持包括[!DNL Chatlio]。

[[!DNL Chatlio]](https://chatlio.com/)是一个与[!DNL Slack]完全集成的实时聊天应用，它方便了多个支持代理同时帮助单个网站访客。 [!DNL Chatlio]使用[!DNL Chatio Zapier App]将[!DNL Chatlio]与2000多个不同的应用和服务连接。

[!DNL Chatlio]源允许您使用[[!DNL Chatlio] Webhook](https://chatlio.com/docs/webhooks/)从[!DNL Chatlio.com]摄取支持的webhook事件架构及其关联的事件数据。

支持的Webhook包括：

* 导出聊天记录
* 导出脱机消息
* 新对话已开始
* 访客未及时获得答案
* 访客在聊天后留下反馈

## 先决条件 {#prerequisites}

在创建[!DNL Chatlio]源连接之前，必须首先确保您具备以下条件：

* [!DNL Chatlio]帐户。 如果您还没有用户访问[[!DNL Chatlio] 注册页面](https://chatlio.com/app/#/signup)来注册和创建您的帐户。
* 成功注册帐户后，请按照[[!DNL Chatlio] 设置文档](https://chatlio.com/docs/setup/)完成帐户设置。

### 设置[!DNL Chatlio] webhook {#set-up-webhook}

成功创建数据流后，必须设置webhook以通知Platform有关[!DNL Chatlio]事件的信息。 Webhook可以在客户属性发生更改或用户打开您的邮件并将此信息发送到您的[!DNL Chatlio]源时立即通知您。

有关详细信息，请阅读有关[获取您的流终结点URL](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint)和[设置 [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook)的教程。

## 将[!DNL Chatlio]连接到平台 {#connect-to-platform}

以下文档提供了有关如何使用API或用户界面创建[!DNL Chatlio]流连接器以与[!DNL Platform]连接的信息：

### 使用API将[!DNL Chatlio]连接到平台 {#connect-to-platform-using-api}

* [使用API创建源连接以将 [!DNL Chatlio] 数据引入Platform。](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### 使用UI将[!DNL Chatlio]连接到平台 {#connect-to-platform-using-ui}

* [使用用户界面创建源连接以将 [!DNL Chatlio] 数据引入Platform](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
