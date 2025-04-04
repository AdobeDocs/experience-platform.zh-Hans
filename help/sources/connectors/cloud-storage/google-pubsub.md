---
title: Google PubSub Source概述
description: 了解如何使用API或用户界面将Google PubSub连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# [!DNL Google PubSub]源

>[!IMPORTANT]
>
>[!DNL Google PubSub]源在源目录中可供已购买Real-Time CDP Ultimate的用户使用。

Adobe Experience Platform为云提供商（如[!DNL AWS]、[!DNL Google Cloud Platform]和[!DNL Azure]）提供本机连接，允许您将这些系统中的数据引入Experience Platform以用于下游服务和目标。

云存储源可以将您的数据导入Experience Platform，而无需下载、设置格式或上传。 引入的数据可以格式化为XDM JSON、XDM Parquet或分隔。 该过程的每个步骤都集成到源工作流中。 Experience Platform允许您从[!DNL Google PubSub]实时引入数据。

## 先决条件 {#prerequisites}

此部分概述在将[!DNL Google PubSub]帐户连接到Experience Platform之前必须完成的先决条件设置。

### 创建服务帐户 {#create-service-account}

**服务帐户**&#x200B;是应用程序或计算工作负载经常使用的帐户类型，而不是个人使用的帐户类型。 服务帐户由其电子邮件地址标识，该地址是该帐户独有的。

* 一方面，服务帐户是&#x200B;**主体** — 您可以授予服务帐户访问[!DNL Google Cloud]资源的权限。 例如，您可以在给定项目中向服务帐户授予计算管理员角色`(roles/compute.admin)`。 然后，该服务帐户将能够管理该特定项目中的计算引擎资源。
* 另一方面，服务帐户也是资源 — 您可以向其他承担者授予访问服务帐户的权限。 例如，您可以在服务帐户上授予用户服务帐户用户角色`(roles/iam.serviceAccountUser)`，以便用户将该服务帐户附加到资源。 或者，您可以授予用户服务帐户管理员角色`(roles/iam.serviceAccountAdmin)`，以允许用户完成查看、编辑、禁用和删除服务帐户等任务。

有关为您的用例确定正确的身份验证类型的更多信息，请阅读身份验证方法的[[!DNL Google] 指南](https://cloud.google.com/docs/authentication)。

按照下面列出的步骤创建服务帐户：

首先，导航到[!DNL Google Developer Console]的[!DNL IAM]页面，然后选择&#x200B;**[!DNL Create Service Account]**。

![Google Developer Console中的“创建服务帐户”窗口](../../images/tutorials/create/google-pubsub/create-service-account.png)

接下来，输入服务帐户的显示名称和ID，然后选择&#x200B;**[!DNL Create and Continue]**。

![Google Developer Console中的服务帐户详细信息](../../images/tutorials/create/google-pubsub/service-account-details.png)

### 生成服务帐户密钥 {#generate-service-account-keys}

要为服务帐户生成密钥，请在服务帐户页中选择密钥标头。 从该位置，选择&#x200B;**[!DNL Add key]**，然后从下拉菜单中选择&#x200B;**[!DNL Create new key]**。 您还可以使用此面板上传现有密钥。

![Google Developer Console中的add key窗口](../../images/tutorials/create/google-pubsub/add-key.png)

成功后，您将收到一条消息，指示私钥已保存到您的计算机，并将下载文件。 然后，在Experience Platform上创建[!DNL Google PubSub]帐户时，您可以将此文件的内容用作凭据。

### 在主题和订阅级别授予权限 {#grant-permissions}

要授予主题和订阅级别的权限，请导航到主题控制台页面，然后选择&#x200B;**[!DNL Show info panel]**。 接下来，在[!DNL Permissions]选项卡下，选择[!DNL Add Principal]，然后添加服务帐户主体以及权限。

![Google Developer Console中的弹出窗口，您可以在其中授予主题和订阅级别的权限](../../images/tutorials/create/google-pubsub/add-principal.png)

## 最佳[!DNL Google PubSub usage]的配置 {#optimal-configurations}

本节概述了建议在Experience Platform上优化使用[!DNL Google PubSub]源的配置。

### 订阅属性 {#subscription-properties}

使用[!DNL Google Developer Console]将&#x200B;**增加您的确认截止日期**。 这允许[!DNL Google Publisher]在再次发送消息之前根据您配置的时间等待。 这种延迟有助于在订阅者级别减少不必要的负载。

![Google Developer Console中的确认截止日期接口。](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

启用&#x200B;**[!DNL exactly one delivery]**。 此配置通知[!DNL Google Publisher]确保在确认截止日期到期之前，不会重新发送发送到订阅的邮件。 您可以使用此设置来确保确认消息不会被重新发送到订阅。

![Google Developer Console中只有一个投放配置页面。](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

您可以启用&#x200B;**[!DNL Retry after exponential backoff delay]**&#x200B;以降低进一步使服务器不堪重负的风险。 您可以在[!DNL Google Developer Console]中启用此配置，以便在尝试其他连接之前为系统提供更多恢复时间，从而更好地缓解暂时性故障（通常可自行解决的暂时性错误）。

![Google Developer Console中的“重试策略”窗口。](../../images/tutorials/create/google-pubsub/retry-policy.png)

您必须&#x200B;**将订阅消息保留持续时间设置为24小时或更长**，以确保未确认的数据不会在高峰加载期间丢失。 此外，**启用死信主题**&#x200B;以确保即使在极少数边缘情况下也不会发生数据丢失。

>[!IMPORTANT]
>
>每个[!DNL Google PubSub]订阅只能创建一个源数据流。 重用订阅（甚至跨沙盒）会导致数据丢失。

## 将[!DNL Google PubSub]连接到Experience Platform

以下文档提供了有关如何使用API或用户界面将[!DNL Google PubSub]连接到Experience Platform的信息：

### 使用API

* [使用流服务API创建Google PubSub源连接](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [使用流服务API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

* [在UI中创建Google PubSub源连接](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
