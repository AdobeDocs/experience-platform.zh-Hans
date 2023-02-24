---
title: 章节源概述
description: 了解如何使用API或用户界面通过Web挂接将Chatlio连接到Adobe Experience Platform
badge: "Beta"
source-git-commit: 2c13cb5a951a3144d0047b567194732acdc35dab
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>的 [!DNL Chatlio] 来源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

Experience Platform支持从流应用程序中摄取数据。 对流提供商的支持包括 [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) 是与 [!DNL Slack] 并且便于多个支持代理同时帮助单个网站访客。 [!DNL Chatlio] 使用 [!DNL Chatio Zapier App] 连接 [!DNL Chatlio] 拥有2000多种不同的应用程序和服务。

的 [!DNL Chatlio] 源允许您从中摄取受支持的webhook事件架构及其关联的事件数据 [!DNL Chatlio.com] 使用 [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

支持的Web挂接包括：

* 导出聊天记录
* 导出离线消息
* 新对话已开始
* 访客未及时获得答案
* 访客在聊天后留下反馈

## 先决条件 {#prerequisites}

在创建 [!DNL Chatlio] 源连接时，必须首先确保您具有以下内容：

* A [!DNL Chatlio] 帐户。 如果您还没有访问 [[!DNL Chatlio] 注册页面](https://chatlio.com/app/#/signup) 注册并创建帐户。
* 成功注册帐户后，请在 [[!DNL Chatlio] 设置文档](https://chatlio.com/docs/setup/) 完成帐户设置。

### 设置 [!DNL Chatlio] WebHook {#set-up-webhook}

成功创建数据流后，必须设置Web挂接以通知平台 [!DNL Chatlio] 事件。 当客户属性发生更改或用户打开您的消息时，Web挂接可立即通知您，并将此信息发送给您的 [!DNL Chatlio] 来源。

有关更多信息，请阅读 [获取流端点URL](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) 和 [设置 [!DNL Chatlio] 网钩](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## 连接 [!DNL Chatlio] 到平台 {#connect-to-platform}

以下文档提供了有关如何创建 [!DNL Chatlio] 流连接器连接到 [!DNL Platform] 使用API或用户界面：

### 连接 [!DNL Chatlio] 到使用API的平台 {#connect-to-platform-using-api}

* [创建源连接以引入 [!DNL Chatlio] 使用API将数据发送到平台。](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### 连接 [!DNL Chatlio] 到使用UI的平台 {#connect-to-platform-using-ui}

* [创建源连接以引入 [!DNL Chatlio] 使用用户界面将数据发送到平台](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)

