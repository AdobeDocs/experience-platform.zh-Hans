---
title: Salesforce Marketing Cloud (V2) Source概述
description: 了解如何使用API或用户界面将Salesforce Marketing Cloud (V2)连接到Adobe Experience Platform。
source-git-commit: 3c200ff1a29c3462a5d4fef554f6a410cfcbdde8
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud] (V2)源概述

>[!IMPORTANT]
>
>原始[[!DNL Salesforce Marketing Cloud] (V1)](salesforce-marketing-cloud.md)源自2026年1月起已被弃用。 此已弃用的源没有迁移可用，您必须使用新的[!DNL Salesforce Marketing Cloud] (V2)源重新实施数据。

Adobe [Real-Time CDP](../../../rtcdp/overview.md)与[!DNL Salesforce Marketing Cloud]之间的集成旨在利用数据扩展，因为它们提供了灵活性和控制力。 与标准系统表（数据视图和内置对象）不同，标准系统表仅限于预定义字段并主要服务于系统级跟踪，您可以使用数据扩展来定义自定义字段、组织各种业务特定的数据并定制数据结构以满足独特的要求。

由于这种级别的自定义和可伸缩性，Real-Time CDP与[!DNL Salesforce Marketing Cloud]之间的集成依赖于数据扩展而不是标准系统表。 此方法为管理数据提供了更灵活、可扩展和集成的基础，确保它符合您的业务目标

您可以使用[!DNL Salesforce Marketing Cloud]源将您的[!DNL Salesforce Marketing Cloud]帐户连接到Real-Time CDP和Adobe Experience Platform。 请阅读以下文档以了解如何入门。

## 用例示例 {#use-case-examples}

### 使用联系人数据个性化电子邮件营销活动

零售品牌想要根据客户的生命周期阶段（例如，新客户、回头客、忠诚客户）个性化电子邮件促销活动。 为此，他们创建一个Contact Data Extension来存储关键客户信息，包括姓名、电子邮件、生命周期阶段和购买行为。 然后，将这些数据摄取到Experience Platform中，以进行更深入的分段和定位。

通过将联系人数据扩展中的数据摄取到Experience Platform中，品牌可以根据客户的生命周期阶段和购买行为来细分客户。 例如，他们可以向新客户发送欢迎选件，向回头客提供忠诚度奖励，甚至可以通过有针对性的选件重新吸引不活跃客户。 此方法可确保个性化通信，并实现更相关、更有效的客户参与。

### 引入Campaign数据以进行个性化分段

营销团队想要根据客户与先前营销活动的参与度来定位客户，从而优化电子邮件营销活动。 为此，他们在[!DNL Salesforce Marketing Cloud]中创建了一个Campaign数据扩展来存储客户参与数据，如电子邮件打开次数、点击次数和营销活动响应。 然后，将这些数据摄取到Experience Platform中，进一步进行分段和个性化。

通过将此数据从Campaign数据扩展引入Experience Platform，营销团队可以根据过去的参与情况细分客户，例如那些点击了产品选件或积极响应的客户。 参与的客户会在未来的电子邮件中收到定向促销活动，而做出负面响应的客户可能会收到客户服务跟进通知。 与Experience Platform的这种集成可确保营销团队根据客户行为提供更加个性化和相关的内容。

### 根据活动数据定位客户

营销团队想要根据客户的活动（如网站访问、表单提交或与以前的电子邮件营销活动的交互）来定位客户。 要实现此目的，他们需创建活动数据扩展，以存储有关每个客户参与活动的信息。 然后，将这些数据摄取到Experience Platform中，以便进一步细分和个性化的营销活动定位。

通过将活动数据扩展中的数据摄取到Experience Platform中，营销团队可以根据客户的参与历史记录进行客户细分。 例如，如果客户最近访问过网站但未完成购买，则会向他们发送包含特殊优惠的提醒电子邮件。 同样，填写表单的客户可以接收个性化的跟进通信。 此方法可确保每位客户都能根据其最近的活动收到相关内容，从而提高参与度和转化率。

## 先决条件 {#prerequisites}

请阅读以下各节，了解在将源连接到Experience Platform之前必须完成的先决条件设置。

### 设置应用程序以进行身份验证 {#set-up-application-for-authentication}

在构建与[!DNL Salesforce Marketing Cloud]的集成时，第一步是在&#x200B;**中创建**&#x200B;已安装的包[!DNL Salesforce Marketing Cloud]。 已安装的包会生成验证API调用所需的客户端凭据，定义集成类型和关联的权限范围。 此外，安装的包为您的租户提供正确的API端点。 它还用作托管的容器，用于管理、监控和撤销访问，确保所有集成都是安全、可审核的，并与Salesforce推荐的身份验证模型保持一致。

要创建已安装的包，请使用[!DNL Salesforce Marketing Cloud]用户界面并导航到&#x200B;**[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]**，然后选择&#x200B;**[!DNL New]**。 使用[!DNL New Package Details]界面为您的包提供名称和信息。 完成后，选择&#x200B;**[!DNL Save]**。

![Salesforce Marketing Cloud UI的新包界面。](../../images/tutorials/create/sfmc/new-package.png)

创建新包后，选择&#x200B;**[!DNL Add Component]**。

![Salesforce Marketing Cloud UI的添加组件界面。](../../images/tutorials/create/sfmc/add-component.png)

选择&#x200B;**[!DNL API Integration]**&#x200B;作为组件类型。

![已选择“API集成”的组件选择窗口。](../../images/tutorials/create/sfmc/api-integration.png)

选择&#x200B;**[!DNL Server-to-Server]**&#x200B;作为您的集成类型。

![集成类型选择窗口](../../images/tutorials/create/sfmc/server-to-server.png)

最后，导航到&#x200B;**[!DNL Scope]** > **[!DNL Data]**。 在&#x200B;**[!DNL Data Extensions]**&#x200B;下，选择&#x200B;**[!DNL Read]**。

![Salesforce营销中范围的数据扩展部分](../../images/tutorials/create/sfmc/data-extensions.png)

选择&#x200B;**[!DNL Save]**，然后复制并保存您的&#x200B;**客户端密钥**。 完成后，选择&#x200B;**[!DNL Finish]**。

![用于生成客户端密钥的Salesforce Marketing Cloud窗口。](../../images/tutorials/create/sfmc/generate-secret.png)

在退出[!DNL Salesforce Marketing Cloud] UI之前，复制&#x200B;**客户端ID**&#x200B;和&#x200B;**唯一的基本URI前缀**，因为您将同时使用这两个值来创建与Experience Platform的连接。 对于身份验证基础URI，请确保在`.auth.marketingcloudapis.com/`之后删除所有内容

![可检索客户端ID和唯一基本URI的Salesforce Marketing Cloud组件接口。](../../images/tutorials/create/sfmc/client-id-and-uri.png)

有关创建已安装软件包的详细步骤，请阅读[[!DNL Salesforce] 文档](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment)。

### 收集所需的凭据 {#gather-required-credentials}

必须提供以下凭据的值才能将[!DNL Salesforce Marketing Cloud]连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| 客户端 ID | 授权Experience Platform时，[!DNL Salesforce Marketing Cloud]用于识别您的帐户的公开标识符。 可从[!DNL Salesforce Marketing Cloud] UI的组件面板中检索客户端ID。 |
| 客户端密码 | 只有客户端应用程序和授权服务器才知道的机密密钥。 您可以按照上述[应用程序设置步骤](#set-up-application-for-authentication)生成客户端密钥。 |
| 基本端点 | [!DNL Salesforce Marketing Cloud]的身份验证基本URI的前缀。 |

{style="table-layout:auto"}

## 将[!DNL Salesforce Marketing Cloud]连接到Experience Platform

继续在Experience Platform中配置[!DNL Salesforce Marketing Cloud]源连接。 有关通过UI设置连接的分步指南，请参阅此处的[教程](../../tutorials/ui/create/marketing-automation/sfmc.md)。 阅读本教程以了解如何连接[!DNL Salesforce Marketing Cloud]帐户、选择数据、映射字段、计划摄取和监视数据流。
