---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；登录者；登录者；连接到查询服务；
solution: Experience Platform
title: 将Looker连接到查询服务
topic-legacy: connect
description: 本文档将介绍如何将Looker与Adobe Experience Platform查询服务连接。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: ad3e1b0de6dd3b82cc82f0dc3d0f36b12cd3899e
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# 连接 [!DNL Looker] 查询服务

本文档介绍了连接的步骤 [!DNL Looker] 与Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已拥有 [!DNL Looker] 并熟悉如何导航其界面。 有关 [!DNL Looker] 可在 [官方 [!DNL Looker] 文档](https://docs.looker.com/).

登录后 [!DNL Looker]，选择 **[!DNL Admin]**，后跟 **[!DNL Connections]**.

![](../images/clients/looker/click-admin-connections.png)

在此页面上，选择 **[!DNL New Connection]**.

![](../images/clients/looker/click-new-connection.png)

从此处，您可以填写连接设置的详细信息。

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** 连接的名称。
- **[!DNL Dialect]:** 用于SQL数据库的方言。 [!DNL Query Service] 使用 **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** 主机端点及其端口 [!DNL Query Service].
- **[!DNL Database]:** 将使用的数据库。
- **[!DNL Username and Password]:** 将使用的登录凭据。 用户名将以 `ORG_ID@AdobeOrg`.
- **SSL**:启用SSL以确保跨网络的安全连接。

>[!IMPORTANT]
>
>请参阅 [[!DNL Query Service] SSL文档](./ssl-modes.md) 了解对与Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用 `verify-full` SSL模式。

有关查找主机和端口、数据库名称和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md). 要查找您的凭据，请登录到 [!DNL Platform]，然后选择 **[!UICONTROL 查询]**，后跟 **[!UICONTROL 凭据]**.

输入连接详细信息后，选择 **[!DNL Test These Settings]** 以确保凭据正常工作。 如果有，则下方将显示一条消息，指示您可以连接。 如果您的连接确实成功，请选择 **[!DNL Add Connection]** 创建连接。

![](../images/clients/looker/click-test-connection.png)

## 后续步骤

现在你已经连接了 [!DNL Query Service]，您可以使用 [!DNL Looker] 来编写查询。 有关如何编写和运行查询的详细信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
