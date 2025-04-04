---
title: Pendo Source概述
description: 了解如何使用API或用户界面利用Webhook将Pendo连接到Adobe Experience Platform
badge: Beta 版
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>[!DNL Pendo]源为测试版。 有关使用测试版标记源的更多信息，请阅读[源概述](../../home.md#terms-and-conditions)。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。 您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方Analytics应用程序中摄取数据。 对Analytics提供商的支持包括[!DNL Pendo]。

[[!DNL Pendo]](https://pendo.io/)是一个产品分析应用程序，旨在帮助软件公司开发可与客户引起共鸣的产品。 该应用程序允许软件制造商将其产品与范围广泛的工具结合使用，从而为用户带来更好的产品体验并为产品团队带来新的见解。

[!DNL Pendo]源允许您使用[[!DNL Pendo] Webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks)从[!DNL Pendo.io]摄取支持的webhook事件架构及其关联的事件数据。 [!DNL Pendo]源与[!DNL Pendo] URL Webhook配合使用。

支持的Webhook包括：

* 已显示[指南](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide)
* 已显示/提交[轮询](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-)
* 已显示/已提交[网络推广人得分](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey)

## 先决条件 {#prerequisites}

在创建[!DNL Pendo]源连接之前，必须首先确保您具备以下条件：

[!DNL Pendo]帐户。 如果您还没有帐户，请查看[[!DNL Pendo] 注册](https://app.pendo.io/register)页面以注册和创建您的帐户。

### 设置[!DNL Pendo] Webhook {#set-up-webhook}

成功创建数据流后，必须设置webhook以通知Experience Platform有关[!DNL Pendo]事件的信息。 发生某些事件时，[!DNL Pendo] Webhook可以将实时通知推送到其他服务，并将此信息发送到您的[!DNL Pendo]源。 有关详细信息，请阅读有关[获取您的流终结点URL](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint)和[设置 [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook)的教程。

## 正在将[!DNL Pendo]连接到Experience Platform {#connect-to-platform}

以下文档提供了有关如何使用API或用户界面创建[!DNL Pendo]流连接器以与[!DNL Experience Platform]连接的信息：

### 使用API将[!DNL Pendo]连接到Experience Platform {#connect-to-platform-using-api}

* [使用API创建源连接以将 [!DNL Pendo] 数据引入Experience Platform。](../../tutorials/api/create/analytics/pendo-webhook.md)

### 使用UI将[!DNL Pendo]连接到Experience Platform {#connect-to-platform-using-ui}

* [使用用户界面创建源连接以将 [!DNL Pendo] 数据引入Experience Platform](../../tutorials/ui/create/analytics/pendo-webhook.md)
