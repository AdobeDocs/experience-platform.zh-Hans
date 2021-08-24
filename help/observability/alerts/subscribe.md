---
keywords: Experience Platform；主页；热门主题；日期范围
title: 订阅Adobe I/O事件通知
description: 本文档提供了有关如何订阅Adobe Experience Platform服务的Adobe I/O事件通知的步骤。 还提供了有关可用事件类型的参考信息，以及指向进一步文档的链接，说明如何解释每个适用 [!DNL Platform] 服务的返回事件数据。
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# 订阅Adobe I/O事件通知

[!DNL Observability Insights] 允许您订阅有关Adobe Experience Platform活动的Adobe I/O事件通知。这些事件会发送到配置的WebHook，以便有效地自动监控活动。

本文档提供了有关如何订阅Adobe Experience Platform服务的Adobe I/O事件通知的步骤。 此外，还提供了有关可用事件类型的参考信息，以及指向有关如何解释每个适用[!DNL Platform]服务的返回事件数据的进一步文档的链接。

## 快速入门

本文档要求您对webhook以及如何将webhook从一个应用程序连接到另一个应用程序有一定的了解。 有关Webhook的简介，请参阅[[!DNL I/O Events] 文档](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md)。

## 创建网页挂钩

要接收[!DNL I/O Event]通知，您必须通过指定唯一的Webhook URL作为事件注册详细信息的一部分来注册Webhook。

您可以使用所选的客户端配置WebHook。 有关在本教程中使用的临时Webhook地址，请访问[Webhook.site](https://webhook.site/)并复制提供的唯一URL。

![](../images/notifications/webhook-url.png)

在初始验证过程中，[!DNL I/O Events]会在GET请求中向Webhook发送`challenge`查询参数。 必须配置Webhook以在响应有效负载中返回此参数的值。 如果您使用的是Webhook.site，请选择右上角的&#x200B;**[!DNL Edit]**，然后在&#x200B;**[!DNL Response body]**&#x200B;下输入`$request.query.challenge$`，然后选择&#x200B;**[!DNL Save]**。

![](../images/notifications/response-challenge.png)

## 在Adobe开发人员控制台中创建新项目

转到[Adobe开发人员控制台](https://www.adobe.com/go/devs_console_ui)并使用Adobe ID登录。 接下来，按照Adobe开发人员控制台文档中[创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)上教程中概述的步骤操作。

## 订阅事件

创建新项目后，导航到该项目的概述屏幕。 从此处，选择&#x200B;**[!UICONTROL Add event]**。

![](../images/notifications/add-event-button.png)

此时会显示一个对话框，用于向项目添加事件提供程序：

* 如果要订阅Experience Platform警报，请选择&#x200B;**[!UICONTROL Platform notifications]**
* 如果要订阅Adobe Experience Platform [!DNL Privacy Service]通知，请选择&#x200B;**[!UICONTROL Privacy Service事件]**

选择事件提供程序后，请选择&#x200B;**[!UICONTROL Next]**。

![](../images/notifications/event-provider.png)

下一个屏幕显示要订阅的事件类型列表。 选择要订阅的事件，然后选择&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
>如果不确定要订阅您正在使用的服务的事件，请查阅特定于服务的通知文档：
>
>* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

下一个屏幕会提示您创建JSON Web令牌(JWT)。 您可以选择自动生成密钥对，或上传您自己在终端中生成的公共密钥。

在本教程中，将遵循第一个选项。 选择&#x200B;**[!UICONTROL 生成键对]**&#x200B;的选项框，然后选择右下角的&#x200B;**[!UICONTROL 生成键对]**&#x200B;按钮。

![](../images/notifications/generate-keypair.png)

生成密钥对时，浏览器会自动下载该密钥对。 由于此文件不会保留在开发人员控制台中，因此您必须自行存储。

下一个屏幕允许您查看新生成的键对的详细信息。 选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![](../images/notifications/keypair-generated.png)

在下一个屏幕中，在[!UICONTROL 事件注册详细信息]部分中提供事件注册的名称和说明。 最佳做法是创建一个唯一且易于识别的名称，以帮助区分此事件注册与同一项目中的其他事件注册。

![](../images/notifications/registration-details.png)

在同一屏幕的[!UICONTROL 如何接收事件]部分下方，您可以选择配置如何接收事件。 **** Webhook允许您提供用于接收事件的自定义Webhook地址，而 **[!UICONTROL 运行]** 时操作则允许您使用Adobe I/O Runtime [执行此操作](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)。

在本教程中，选择&#x200B;**[!UICONTROL Webhook]**&#x200B;并提供您之前创建的Webhook的URL。 完成后，选择&#x200B;**[!UICONTROL 保存已配置的事件]**&#x200B;以完成事件注册。

![](../images/notifications/receive-events.png)

此时会显示新创建事件注册的详细信息页面，您可以在其中编辑其配置、查看接收的事件、执行调试跟踪和添加新事件提供程序。

![](../images/notifications/registration-complete.png)

## 后续步骤

在本教程之后，您已注册一个Webhook，用于接收[!DNL Experience Platform]和/或[!DNL Privacy Service]的[!DNL I/O Event]通知。 有关可用事件以及如何解释每个服务的通知负载的详细信息，请参阅以下文档：

* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] （源）通知](../../sources/notifications.md)

有关如何监视[!DNL Experience Platform]和[!DNL Privacy Service]上的活动的详细信息，请参阅[[!DNL Observability Insights] 概述](../home.md)。
