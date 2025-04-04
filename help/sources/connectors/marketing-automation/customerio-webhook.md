---
title: Customer.io Source概述
description: 了解如何使用API或用户界面利用Webhook将Customer.io连接到Adobe Experience Platform
badge: Beta 版
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>[!DNL Customer.io]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从流应用程序中摄取数据。 对流式提供程序的支持包括[!DNL Customer.io]。

[[!DNL Customer.io]](https://customer.io/)是一个自动消息传送平台，面向希望获得更多控制力和灵活性以制作和发送数据驱动电子邮件、推送通知、应用程序内消息和短信的营销人员。

[!DNL Customer.io]源允许您使用[[!DNL Customer.io] 报告Webhook](https://customer.io/docs/api/webhooks/)从[!DNL Customer.io]摄取支持的webhook事件架构及其关联的事件数据。

支持的webhook事件架构包括：

* 客户事件
* 电子邮件事件
* 短信事件
* 推送通知事件
* 应用程序内消息事件
* Slack事件
* Webhook活动

有关通过Webhook提供的事件列表，请参阅[[!DNL Customer.io] 报告Webhook事件](https://customer.io/docs/webhooks/#events)文档。

## 先决条件 {#prerequisites}

在创建[!DNL Customer.io]源连接之前，必须首先确保您具备以下条件：

* [!DNL Customer.io]帐户。 如果您没有帐户，请阅读[[!DNL Customer.io] 注册页面](https://fly.customer.io/signup)以注册和创建您的帐户。
* 创建帐户后，您还需要验证帐户。 按照[[!DNL Customer.io] 帐户验证](https://customer.io/docs/account-verification/)页面上记录的步骤完成此过程。

### 设置[!DNL Customer.io] Webhook {#set-up-webhook}

成功创建数据流后，必须设置报告Webhook以通知Experience Platform有关[!DNL Customer.io]事件的信息。 Webhook可以在客户属性更改或用户打开您的消息时立即通知您，并将此信息发送给您的[!DNL Customer.io]源。 有关详细信息，请阅读有关[获取您的流终结点URL](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint)和[设置 [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook)的教程。

## 正在将[!DNL Customer.io]连接到Experience Platform {#connect-to-platform}

以下文档提供了有关如何使用API或用户界面创建[!DNL Customer.io]流连接以与[!DNL Experience Platform]连接的信息：

### 使用API将[!DNL Customer.io]连接到Experience Platform {#connect-to-platform-using-api}

* [创建源连接和数据流以使用API将 [!DNL Customer.io] 数据引入Experience Platform。](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### 使用UI将[!DNL Customer.io]连接到Experience Platform {#connect-to-platform-using-ui}

* [使用用户界面创建源连接和数据流以将 [!DNL Customer.io] 数据引入Experience Platform](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
