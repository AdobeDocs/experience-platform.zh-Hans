---
keywords: Experience Platform；主页；热门主题；日期范围
solution: Experience Platform
title: 订阅Adobe I/O事件通知
topic: developer guide
description: 本文档提供如何订阅Adobe I/O事件通知的Adobe Experience Platform服务步骤。 还提供了有关可用事件类型的参考信息，以及指向进一步文档的链接，说明如何解释每个适用 [!DNL Platform] 服务的返回事件数据。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---


# 订阅Adobe I/O事件通知

[!DNL Observability Insights] 允许您订阅Adobe I/O事件有关Adobe Experience Platform活动的通知。这些事件被发送到配置的网络挂接，以促进活动监控的高效自动化。

本文档提供如何订阅Adobe I/O事件通知的Adobe Experience Platform服务步骤。 还提供了有关可用事件类型的参考信息，以及指向进一步文档的链接，说明如何解释每个适用[!DNL Platform]服务返回的事件数据。

## 入门指南

此文档需要了解webhook以及如何将webhook从一个应用程序连接到另一个应用程序。 有关Webhooks的简介，请参阅[[!DNL I/O Events] 文档](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md)。

## 创建网络挂接

要接收[!DNL I/O Event]通知，您必须通过指定唯一的webhook URL作为事件注册详细信息的一部分来注册webhook。

您可以使用您选择的客户端配置网络挂接。 要获得用作本教程一部分的临时Webhook地址，请访问[Webhook.site](https://webhook.site/)并复制提供的唯一URL。

![](../images/notifications/webhook-url.png)

在初始验证过程中，[!DNL I/O Events]向webhook发送GET请求中的`challenge`查询参数。 必须配置Webhook以在响应有效负荷中返回此参数的值。 如果您使用的是Webhook.site，请选择右上角的&#x200B;**[!DNL Edit]**，然后在&#x200B;**[!DNL Response body]**&#x200B;下输入`$request.query.challenge$`，然后选择&#x200B;**[!DNL Save]**。

![](../images/notifications/response-challenge.png)

## 在Adobe开发人员控制台中创建新项目

转至[Adobe开发人员控制台](https://www.adobe.com/go/devs_console_ui)并使用您的Adobe ID登录。 接下来，按照Adobe开发者控制台文档中[创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)教程中概述的步骤操作。

## 订阅事件

创建新项目后，导航到该项目的概述屏幕。 从此处，选择&#x200B;**[!UICONTROL 添加事件]**。

![](../images/notifications/add-event-button.png)

此时会显示一个对话框，允许您向项目添加事件提供程序：

* 如果您订阅[!DNL Experience Platform]通知，请选择&#x200B;**[!UICONTROL 平台通知]**
* 如果您订阅的是Adobe Experience Platform[!DNL Privacy Service]通知，请选择&#x200B;**[!UICONTROL Privacy Service事件]**

选择事件提供程序后，选择&#x200B;**[!UICONTROL 下一步]**。

![](../images/notifications/event-provider.png)

下一个屏幕显示一列表事件类型进行订阅。 选择要订阅的事件，然后选择&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
>如果您不确定要订阅您所使用服务的事件，请查阅特定于服务的通知文档：
>
>* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

下一个屏幕会提示您创建JSON Web令牌(JWT)。 您可以选择自动生成密钥对，或上传您自己在终端中生成的公钥。

就本教程而言，将遵循第一个选项。 选中&#x200B;**[!UICONTROL 生成键对]**&#x200B;的选项框，然后选择右下角的&#x200B;**[!UICONTROL 生成键对]**&#x200B;按钮。

![](../images/notifications/generate-keypair.png)

当密钥对生成时，浏览器会自动下载该密钥对。 您必须自己存储此文件，因为它不会保留在开发人员控制台中。

下一个屏幕允许您查看新生成的密钥对的详细信息。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续。

![](../images/notifications/keypair-generated.png)

在下一个屏幕中，在[!UICONTROL 事件注册详细信息]部分提供事件注册的名称和说明。 最佳实践是创建一个唯一、易于识别的名称，以帮助区分此事件注册与同一项目中的其他客户。

![](../images/notifications/registration-details.png)

在[!UICONTROL 如何接收事件]部分下的同一屏幕中，您可以选择配置如何接收事件。 **[!UICONTROL Web]** Hook允许您提供自定义WebHook地址来接收事件，而 **[!UICONTROL Runtime]** action则允许您使用 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)。

对于本教程，选择&#x200B;**[!UICONTROL Webhook]**&#x200B;并提供您之前创建的Webhook的URL。 完成后，选择&#x200B;**[!UICONTROL 保存已配置的事件]**&#x200B;以完成事件注册。

![](../images/notifications/receive-events.png)

随后将显示新创建的事件注册的详细信息页面，您可以在该页面中编辑其配置、查看接收的事件、执行调试跟踪并添加新的事件提供程序。

![](../images/notifications/registration-complete.png)

## 后续步骤

通过本教程，您注册了一个webhook以接收[!DNL Experience Platform]和／或[!DNL Privacy Service]的[!DNL I/O Event]通知。 有关可用事件以及如何解释每个服务的通知有效负载的详细信息，请参阅以下文档：

* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)

有关如何在[!DNL Experience Platform]和[!DNL Privacy Service]上监视活动的详细信息，请参阅[[!DNL Observability Insights] 概述](../home.md)。