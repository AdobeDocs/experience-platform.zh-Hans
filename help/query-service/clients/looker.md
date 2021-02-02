---
keywords: Experience Platform；主题；热门主题；查询服务；查询服务；登录者；登录者；连接到查询服务；
solution: Experience Platform
title: 与Looker连接
topic: connect
description: 此文档将步骤连接到Looker和Adobe Experience Platform查询服务。
translation-type: tm+mt
source-git-commit: bc1bbdddd75b11ac180b5e6faa391fd74e5f7e02
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---


# [!DNL Looker]

本文档介绍将[!DNL Looker]与Adobe Experience Platform[!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经具有访问[!DNL Looker]的权限，并且熟悉如何导航其接口。 有关[!DNL Looker]的详细信息，请参阅[offical [!DNL Looker] 文档](https://docs.looker.com/)。

## 连接[!DNL Looker]与平台

登录[!DNL Looker]后，选择&#x200B;**[!DNL Admin]**，后跟&#x200B;**[!DNL Connections]**。

![](../images/clients/looker/click-admin-connections.png)

在此页上，选择&#x200B;**[!DNL New Connection]**。

![](../images/clients/looker/click-new-connection.png)

从此处，您可以填写连接设置的详细信息。

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** 连接的名称。
- **[!DNL Dialect]:** 用于SQL数据库的方言。[!DNL Query Service] 使用 **[!DNL PostgreSQL]**。
- **[!DNL Host and Port]:** 主机端点及其端口 [!DNL Query Service]。
- **[!DNL Database]:** 将使用的数据库。
- **[!DNL Username and Password]:** 将使用的登录凭据。用户名将采用`ORG_ID@AdobeOrg`的形式。

>[!NOTE]
>
>有关查找主机和端口、数据库名称和登录凭据的详细信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找您的凭据，请登录[!DNL Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，后跟&#x200B;**[!UICONTROL 凭据]**。

输入连接详细信息后，选择&#x200B;**[!DNL Test These Settings]**&#x200B;以确保凭据正常工作。 如果他们这样做，将在下面显示一条消息，指示您可以进行连接。 如果连接确实成功，请选择&#x200B;**[!DNL Add Connection]**&#x200B;以创建连接。

![](../images/clients/looker/click-test-connection.png)

## 后续步骤

现在您已连接[!DNL Query Service]，可以使用[!DNL Looker]编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询指南](../best-practices/writing-queries.md)。