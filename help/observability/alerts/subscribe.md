---
keywords: Experience Platform；主页；热门主题；日期范围
title: 订阅Adobe I/O事件通知
description: 本文档提供了有关如何为Adobe Experience Platform服务订阅Adobe I/O事件通知的步骤。 还提供了有关可用事件类型的参考信息，以及指向有关如何解释每个适用的 [!DNL Experience Platform] 服务的返回事件数据的更多文档的链接。
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# 订阅Adobe I/O事件通知

[!DNL Observability Insights]允许您订阅有关Adobe Experience Platform活动的Adobe I/O事件通知。 这些事件被发送到配置的webhook以促进活动监控的高效自动化。

本文档提供了有关如何为Adobe Experience Platform服务订阅Adobe I/O事件通知的步骤。 还提供了有关可用事件类型的参考信息，以及指向有关如何解释每个适用的[!DNL Experience Platform]服务的返回事件数据的更多文档的链接。

## 快速入门

本文档要求您对Webhook以及如何将Webhook从一个应用程序连接到另一个应用程序有一定的了解。 有关Webhook的介绍，请参阅[[!DNL I/O Events] 文档](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md)。

## 创建webhook

为了接收[!DNL I/O Event]通知，您必须通过指定唯一的webhook URL作为事件注册详细信息的一部分来注册webhook。

您可以使用所选客户端配置webhook。 若要在本教程中使用临时webhook地址，请访问[Webhook.site](https://webhook.site/)，并复制提供的唯一URL。

![](../images/notifications/webhook-url.png)

在初始验证过程中，[!DNL I/O Events]在GET请求中向webhook发送`challenge`查询参数。 您必须配置webhook以在响应有效负载中返回此参数的值。 如果您使用的是Webhook.site，请选择右上角的&#x200B;**[!DNL Edit]**，然后在&#x200B;**[!DNL Response body]**&#x200B;下输入`$request.query.challenge$`再选择&#x200B;**[!DNL Save]**。

![](../images/notifications/response-challenge.png)

## 在Adobe Developer Console中创建新项目

转到[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)并使用您的Adobe ID登录。 接下来，按照Adobe Developer Console文档中有关[创建空项目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/)的教程中概述的步骤进行操作。

## 订阅事件

>[!NOTE]
>
>Adobe I/O中已弃用数据摄取通知事件。您应该改用&#x200B;**源流运行信息** I/O事件。

创建新项目后，导航到该项目的概述屏幕。 从此处选择&#x200B;**[!UICONTROL 添加事件]**。

![](../images/notifications/add-event-button.png)

此时将显示一个对话框，允许您向项目添加事件提供程序：

* 如果您正在订阅Experience Platform警报，请选择&#x200B;**[!UICONTROL 平台通知]**
* 如果您正在订阅Adobe Experience Platform [!DNL Privacy Service]通知，请选择&#x200B;**[!UICONTROL Privacy Service事件]**

选择事件提供程序后，选择&#x200B;**[!UICONTROL 下一步]**。

![](../images/notifications/event-provider.png)

下一个屏幕显示要订阅的事件类型列表。 选择要订阅的事件，然后选择&#x200B;**[!UICONTROL 下一步]**。

>[!NOTE]
>
>如果您不确定要订阅服务的事件，请查阅以下文档：
>
>* [平台通知](./rules.md)
>* [Privacy Service通知](../../privacy-service/privacy-events.md)

>[!IMPORTANT]
>
>Edge相关警报当前为测试版，仅向部分测试版客户提供。

![](../images/notifications/choose-event-subscriptions.png)

下一个屏幕提示您创建JSON Web令牌(JWT)。 您可以选择自动生成密钥对，或上传您在终端中生成的公共密钥。

在本教程中，我们将介绍第一个选项。 选中&#x200B;**[!UICONTROL 生成密钥对]**&#x200B;的选项框，然后选择右下角的&#x200B;**[!UICONTROL 生成密钥对]**&#x200B;按钮。

![](../images/notifications/generate-keypair.png)

当密钥对生成时，浏览器会自动下载密钥对。 您必须自行存储此文件，因为它未保留在Developer Console中。

下一个屏幕允许您查看新生成的密钥对的详细信息。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../images/notifications/keypair-generated.png)

在下一个屏幕中，在[!UICONTROL 事件注册详细信息]部分中提供事件注册的名称和描述。 最佳实践是创建唯一、易于识别的名称，以帮助将此事件注册与同一项目中的其他事件注册区分开来。

![](../images/notifications/registration-details.png)

在[!UICONTROL 如何接收事件]部分下的同一屏幕上，您可以选择配置如何接收事件。 **[!UICONTROL Webhook]**&#x200B;允许您提供自定义webhook地址来接收事件，而&#x200B;**[!UICONTROL 运行时操作]**&#x200B;允许您使用[Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)执行相同的操作。

在本教程中，选择&#x200B;**[!UICONTROL Webhook]**，并提供您之前创建的webhook的URL。 完成后，选择&#x200B;**[!UICONTROL 保存配置的事件]**&#x200B;以完成事件注册。

![](../images/notifications/receive-events.png)

此时将显示新创建的事件注册的详细信息页面，您可以在此页面编辑其配置、查看接收的事件、执行调试跟踪以及添加新的事件提供程序。

![](../images/notifications/registration-complete.png)

## 后续步骤

通过学习本教程，您已注册webhook以接收[!DNL Experience Platform]和/或[!DNL Privacy Service]的[!DNL I/O Event]通知。 有关可用事件以及如何解释每个服务的通知负载的详细信息，请参阅以下文档：

* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Flow Service] （源）通知](../../sources/notifications.md)

有关如何监视[!DNL Experience Platform]和[!DNL Privacy Service]上的活动的详细信息，请参阅[[!DNL Observability Insights] 概述](../home.md)。
