---
title: Customer.io源概述
description: 了解如何使用API或用户界面通过Web挂接将Customer.io连接到Adobe Experience Platform
badge: "Beta"
source-git-commit: 9d6a4b5f60f7895e2c1833493926db147064f3f1
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>的 [!DNL Customer.io] 来源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

Experience Platform支持从流应用程序中摄取数据。 对流提供商的支持包括 [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) 是一个自动消息平台，面向希望拥有更多控制和灵活性以制作和发送数据驱动的电子邮件、推送通知、应用程序内消息和短信的营销人员。

的 [!DNL Customer.io] 源允许您从中摄取受支持的webhook事件架构及其关联的事件数据 [!DNL Customer.io] 使用 [[!DNL Customer.io] 报表Webhook](https://customer.io/docs/api/webhooks/).

支持的Webhook事件架构包括：

* 客户事件
* 电子邮件事件
* 短信事件
* 推送通知事件
* 应用程序内消息事件
* Slack事件
* Webhook事件

有关可通过Web挂接获取的事件列表，请参阅 [[!DNL Customer.io] 报告Webhook事件](https://customer.io/docs/webhooks/#events) 文档。

## 先决条件 {#prerequisites}

在创建 [!DNL Customer.io] 源连接时，必须首先确保您具有以下内容：

* A [!DNL Customer.io] 帐户。 如果您没有阅读 [[!DNL Customer.io] 注册页面](https://fly.customer.io/signup) 注册并创建帐户。
* 创建帐户后，您还需要验证您的帐户。 按照 [[!DNL Customer.io] 帐户验证](https://customer.io/docs/account-verification/) 页面以完成该过程。

### 设置 [!DNL Customer.io] 网钩 {#set-up-webhook}

成功创建数据流后，必须设置一个Reporting Webhook以通知Platform [!DNL Customer.io] 事件。 Web挂接可以在客户属性发生更改或用户打开您的消息时立即通知您，并将此信息发送给您的 [!DNL Customer.io] 来源。 有关更多信息，请阅读 [获取流端点URL](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) 和 [设置 [!DNL Customer.io] 网钩](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## 连接 [!DNL Customer.io] 到平台 {#connect-to-platform}

以下文档提供了有关如何创建 [!DNL Customer.io] 流连接与 [!DNL Platform] 使用API或用户界面：

### 连接 [!DNL Customer.io] 到使用API的平台 {#connect-to-platform-using-api}

* [创建源连接和数据流以引入 [!DNL Customer.io] 使用API将数据发送到平台。](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### 连接 [!DNL Customer.io] 到使用UI的平台 {#connect-to-platform-using-ui}

* [创建源连接和数据流以引入 [!DNL Customer.io] 使用用户界面将数据发送到平台](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)

