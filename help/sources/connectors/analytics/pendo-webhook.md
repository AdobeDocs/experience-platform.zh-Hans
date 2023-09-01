---
title: Pendo源概述
description: 了解如何使用API或用户界面利用Webhook将Pendo连接到Adobe Experience Platform
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>此 [!DNL Pendo] 源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记源代码的更多信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、数据库和许多其他来源)中摄取数据。

Experience Platform支持从第三方Analytics应用程序中摄取数据。 对Analytics提供商的支持包括 [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) 是一个产品分析应用程序，旨在帮助软件公司开发能够引起客户共鸣的产品。 该应用程序允许软件制造商将其产品与范围广泛的工具结合使用，从而为用户带来更好的产品体验并为产品团队带来新的见解。

此 [!DNL Pendo] 源允许您从中摄取支持的webhook事件架构及其关联的事件数据 [!DNL Pendo.io] 使用 [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). 此 [!DNL Pendo] 源与 [!DNL Pendo] URL Webhook。

支持的Webhook包括：

* [指南](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) 显示
* [轮询](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) 显示/提交
* [网络推广者得分](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) 显示/提交

## 先决条件 {#prerequisites}

在创建之前 [!DNL Pendo] 源连接时，您必须首先确保具备以下条件：

A [!DNL Pendo] 帐户。 如果您还没有这样的人，请参阅 [[!DNL Pendo] 注册](https://app.pendo.io/register) 注册和创建帐户的页面。

### 设置 [!DNL Pendo] Webhook {#set-up-webhook}

成功创建数据流后，必须设置webhook以通知Platform [!DNL Pendo] 事件。 [!DNL Pendo] Webhook可以在某些事件发生时将实时通知推送给其他服务，并将此信息发送给您的 [!DNL Pendo] 源。 有关更多信息，请参阅上的教程 [获取您的流端点URL](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) 和 [设置 [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## 正在连接 [!DNL Pendo] 目标平台 {#connect-to-platform}

以下文档提供了有关如何创建 [!DNL Pendo] 要连接的流连接器 [!DNL Platform] 使用API或用户界面：

### 连接 [!DNL Pendo] 到使用API的平台 {#connect-to-platform-using-api}

* [创建源连接以引入 [!DNL Pendo] 使用API将数据发送到Platform。](../../tutorials/api/create/analytics/pendo-webhook.md)

### 连接 [!DNL Pendo] 到Platform，使用UI {#connect-to-platform-using-ui}

* [创建源连接以引入 [!DNL Pendo] 使用用户界面将数据发送到Platform](../../tutorials/ui/create/analytics/pendo-webhook.md)
