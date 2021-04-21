---
keywords: Experience Platform；主页；热门主题；日期范围
solution: Experience Platform
title: 订阅Adobe I/O事件通知
topic-legacy: developer guide
description: 本文档提供了如何订阅Adobe Experience Platform服务的Adobe I/O事件通知的步骤。 还提供了有关可用事件类型的参考信息，以及指向关于如何解释每个适用 [!DNL Platform] 服务的返回事件数据的进一步文档的链接。
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# 订阅Adobe I/O事件通知

[!DNL Observability Insights] 允许您订阅有关Adobe Experience Platform活动的Adobe I/O事件通知。这些事件被发送到已配置的webhook，以促进活动监控的高效自动化。

本文档提供了如何订阅Adobe Experience Platform服务的Adobe I/O事件通知的步骤。 还提供了有关可用事件类型的参考信息，以及指向关于如何解释每个适用[!DNL Platform]服务返回的事件数据的进一步文档的链接。

## 入门指南

此文档需要了解webhook以及如何将webhook从一个应用程序连接到另一个应用程序。 有关webhook的简介，请参阅[[!DNL I/O Events] 文档](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md)。

## 创建Webhook

要接收[!DNL I/O Event]通知，您必须通过指定唯一的webhook URL作为事件注册详细信息的一部分来注册webhook。

您可以使用您选择的客户端配置网络挂接。 要获得用作本教程一部分的临时Webhook地址，请访问[Webhook.site](https://webhook.site/)并复制提供的唯一URL。

![](../images/notifications/webhook-url.png)

在初始验证过程中，[!DNL I/O Events]向webhook发送GET请求中的`challenge`查询参数。 必须配置webhook以在响应有效负荷中返回此参数的值。 如果您使用的是Webhook.site，请选择右上角的&#x200B;**[!DNL Edit]**，然后在&#x200B;**[!DNL Response body]**&#x200B;下输入`$request.query.challenge$`，然后选择&#x200B;**[!DNL Save]**。

![](../images/notifications/response-challenge.png)

## 在Adobe开发人员控制台中创建新项目

转到[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)并使用您的Adobe ID登录。 接下来，按照教程中概述的步骤操作，该教程位于“Adobe开发人员控制台”文档中的[创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)。

## 订阅事件

创建新项目后，导航到该项目的概述屏幕。 从此处选择&#x200B;**[!UICONTROL Add event]**。

![](../images/notifications/add-event-button.png)

此时会显示一个对话框，允许您向项目添加事件提供程序：

* 如果订阅[!DNL Experience Platform]通知，请选择&#x200B;**[!UICONTROL Platform notifications]**
* 如果您订阅Adobe Experience Platform [!DNL Privacy Service]通知，请选择&#x200B;**[!UICONTROL Privacy Service Events]**

选择事件提供程序后，请选择&#x200B;**[!UICONTROL Next]**。

![](../images/notifications/event-provider.png)

下一个屏幕显示要订阅的列表事件类型。 选择要订阅的事件，然后选择&#x200B;**[!UICONTROL Next]**。

>[!NOTE]
>
>如果您不确定要订阅您所使用服务的事件，请查阅特定于服务的通知文档：
>
>* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

下一个屏幕会提示您创建JSON Web令牌(JWT)。 您可以选择自动生成密钥对，或上传您自己在终端中生成的公钥。

就本教程而言，将遵循第一个选项。 选择&#x200B;**[!UICONTROL Generate a key pair]**&#x200B;的选项框，然后选择右下角的&#x200B;**[!UICONTROL Generate keypair]**&#x200B;按钮。

![](../images/notifications/generate-keypair.png)

键对生成时，浏览器会自动下载它。 您必须自己存储此文件，因为它不会保留在开发人员控制台中。

下一个屏幕允许您查看新生成的键对的详细信息。 选择&#x200B;**[!UICONTROL Next]**&#x200B;继续。

![](../images/notifications/keypair-generated.png)

在下一个屏幕中，在[!UICONTROL Event registration details]部分中提供事件注册的名称和说明。 最佳实践是创建一个唯一、易于识别的名称，以帮助区分此事件注册与同一项目中的其他客户。

![](../images/notifications/registration-details.png)

在位于[!UICONTROL How to receive events]部分下的同一屏幕上，您可以选择配置如何接收事件。 **[!UICONTROL Webhook]** 允许您提供自定义webhook地址以接收事件，而 **[!UICONTROL Runtime action]** 允许您使用Adobe I/O Runtime进行 [相同](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)。

对于本教程，请选择&#x200B;**[!UICONTROL Webhook]**&#x200B;并提供您之前创建的Webhook的URL。 完成后，选择&#x200B;**[!UICONTROL Save configured events]**&#x200B;以完成事件注册。

![](../images/notifications/receive-events.png)

随后将显示新创建的事件注册的详细信息页，您可以在该页中编辑其配置、查看接收的事件、执行调试跟踪和添加新的事件提供程序。

![](../images/notifications/registration-complete.png)

## 后续步骤

通过本教程，您注册了一个webhook以接收[!DNL Experience Platform]和/或[!DNL Privacy Service]的[!DNL I/O Event]通知。 有关可用事件以及如何解释每个服务的通知负载的详细信息，请参阅以下文档：

* [[!DNL Privacy Service] 通知](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] 通知](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] 通知](../../sources/notifications.md)

有关如何在[!DNL Experience Platform]和[!DNL Privacy Service]上监控活动的详细信息，请参阅[[!DNL Observability Insights] 概述](../home.md)。
