---
title: Pendo源概述
description: 了解如何使用API或用户界面通过Web挂接将Pendo连接到Adobe Experience Platform
badge: "Beta"
source-git-commit: 24691e3ded33c3af31fd0cee107f2f3ca898585f
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>的 [!DNL Pendo] 来源为测试版。 请阅读 [源概述](../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

Adobe Experience Platform允许从外部源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、数据库和许多其他源。

Experience Platform支持从第三方分析应用程序摄取数据。 对分析提供商的支持包括 [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) 是一个产品分析应用程序，旨在帮助软件公司开发能够与客户产生共鸣的产品。 该应用程序允许软件制造商将其产品嵌入各种工具，这些工具既可为用户带来更好的产品体验，也可为产品团队带来新的洞察。

的 [!DNL Pendo] 源允许您从中摄取受支持的webhook事件架构及其关联的事件数据 [!DNL Pendo.io] 使用 [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). 的 [!DNL Pendo] 源适用于 [!DNL Pendo] URL Webhooks。

支持的Web挂接包括：

* [指南](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) 显示
* [投票](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) 显示/提交
* [净启动子分数](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) 显示/提交

## 先决条件 {#prerequisites}

在创建 [!DNL Pendo] 源连接时，必须首先确保您具有以下内容：

A [!DNL Pendo] 帐户。 如果您还没有看到 [[!DNL Pendo] 注册](https://app.pendo.io/register) 页面以注册和创建帐户。

### 设置 [!DNL Pendo] 网钩 {#set-up-webhook}

成功创建数据流后，必须设置Web挂接以通知平台 [!DNL Pendo] 事件。 [!DNL Pendo] Webhooks可在发生某些事件时向其他服务推送实时通知，并将此信息发送给 [!DNL Pendo] 来源。 有关更多信息，请阅读 [获取流端点URL](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) 和 [设置 [!DNL Pendo] 网钩](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## 连接 [!DNL Pendo] 到平台 {#connect-to-platform}

以下文档提供了有关如何创建 [!DNL Pendo] 流连接器连接到 [!DNL Platform] 使用API或用户界面：

### 连接 [!DNL Pendo] 到使用API的平台 {#connect-to-platform-using-api}

* [创建源连接以引入 [!DNL Pendo] 使用API将数据发送到平台。](../../tutorials/api/create/analytics/pendo-webhook.md)

### 连接 [!DNL Pendo] 到使用UI的平台 {#connect-to-platform-using-ui}

* [创建源连接以引入 [!DNL Pendo] 使用用户界面将数据发送到平台](../../tutorials/ui/create/analytics/pendo-webhook.md)

