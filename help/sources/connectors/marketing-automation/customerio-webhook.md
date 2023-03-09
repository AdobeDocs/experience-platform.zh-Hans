---
title: Customer.io源概述
description: 了解如何使用API或用户界面利用Webhook将Customer.io连接到Adobe Experience Platform
hide: true
hidefromtoc: true
badge: "Beta"
source-git-commit: f92a42a5d53121cc3338432a3cd975f0aa29b9a8
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>此 [!DNL Customer.io] 源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从流应用程序中摄取数据。 对流媒体提供商的支持包括 [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) 是一个自动化消息传送平台，面向希望获得更多控制和灵活度以制作和发送数据驱动电子邮件、推送通知、应用程序内消息和短信的营销人员。

此 [!DNL Customer.io] 源允许您从中摄取支持的webhook事件架构及其关联的事件数据 [!DNL Customer.io] 使用 [[!DNL Customer.io] 报告Webhook](https://customer.io/docs/api/webhooks/).

支持的webhook事件架构包括：

* 客户事件
* 电子邮件事件
* 短信事件
* 推送通知事件
* 应用程序内消息事件
* Slack事件
* Webhook活动

有关通过Webhook可用的事件列表，请参阅 [[!DNL Customer.io] 报告Webhook事件](https://customer.io/docs/webhooks/#events) 文档。

## 先决条件 {#prerequisites}

在创建 [!DNL Customer.io] 源连接中，您必须首先确保具有以下内容：

* A [!DNL Customer.io] 帐户。 如果您没有这样的人，请阅读 [[!DNL Customer.io] 注册页面](https://fly.customer.io/signup) 注册并创建您的帐户。
* 创建帐户后，您还需要验证帐户。 请按照 [[!DNL Customer.io] 帐户验证](https://customer.io/docs/account-verification/) 页面以完成该过程。

### 设置 [!DNL Customer.io] Webhook {#set-up-webhook}

成功创建数据流后，必须设置报告Webhook以通知Platform [!DNL Customer.io] 事件。 Webhook可以在客户属性发生更改或用户打开您的消息时立即通知您，并将此信息发送至 [!DNL Customer.io] 源。 有关更多信息，请阅读上的教程 [获取您的流端点URL](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) 和 [设置 [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## 正在连接 [!DNL Customer.io] 目标平台 {#connect-to-platform}

以下文档提供了有关如何创建 [!DNL Customer.io] 要连接的流连接 [!DNL Platform] 使用API或用户界面：

### Connect [!DNL Customer.io] 到使用API的平台 {#connect-to-platform-using-api}

* [创建源连接和数据流以引入 [!DNL Customer.io] 使用API将数据发送到Platform。](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connect [!DNL Customer.io] 使用UI到Platform {#connect-to-platform-using-ui}

* [创建源连接和数据流以引入 [!DNL Customer.io] 使用用户界面将数据发送到Platform](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)

