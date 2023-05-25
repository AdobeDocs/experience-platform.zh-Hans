---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；查找器；查找器；连接到查询服务；
solution: Experience Platform
title: 将查找器连接到查询服务
description: 本文档介绍了将Looker与Adobe Experience Platform查询服务连接的步骤。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# Connect [!DNL Looker] 查询服务

本文档介绍了连接的步骤 [!DNL Looker] 使用Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已经有权访问 [!DNL Looker] 并熟悉如何导航其界面。 有关以下内容的更多信息 [!DNL Looker] 可在以下位置找到： [正式 [!DNL Looker] 文档](https://docs.looker.com/).

## 创建新数据库连接 {#create-connection}

登录后 [!DNL Looker]，选择 **[!DNL Admin]**，后接 **[!DNL Connections]**. 此 [!DNL Connections] 页面打开。 在 [!DNL Connections] 页面，选择 **[!DNL Add Connection]**.

在此处，输入下面列出的连接设置的详细信息。 请参阅官方的Looker文档，了解 [有关创建新数据库连接的说明以及可用属性的说明](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]：** 连接的名称。
- **[!DNL Dialect]：** 用于SQL数据库的方言。 [!DNL Query Service] 用途 **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]：** 的主机端点及其端口 [!DNL Query Service].
- **[!DNL Database]：** 将使用的数据库。
- **[!DNL Username and Password]：** 将使用的登录凭据。 用户名将采用以下形式 `ORG_ID@AdobeOrg`.
- **SSL**：启用SSL以确保网络间的安全连接。

要查找将Looker与查询服务连接所需的凭据，请登录Platform UI并选择 **[!UICONTROL 查询]** 从左侧导航中，后面是 **[!UICONTROL 凭据]**. 有关查找的详细信息 **主机**， **端口**， **数据库**， **用户名**、和 **密码** 凭据，请阅读 [凭据指南](../ui/credentials.md).

![“Experience Platform查询”工作区的“凭据”页面中突出显示了凭据和即将过期的凭据。](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 还提供了不会过期的凭据，以允许对第三方客户端进行一次性设置。 请参阅相关文档 [有关如何生成和使用不会到期的凭据的完整说明](../ui/credentials.md#non-expiring-credentials). 如果您希望一次性连接Looker，则必须完成此过程。 此 `credential` 和 `technicalAccountId` 所获取的值包括“查看者”的值 `password` 参数。

要了解Adobe Experience Platform对第三方连接的SSL支持，请参阅 [[!DNL Query Service] SSL文档](./ssl-modes.md). 本文档提供了有关如何使用进行连接的说明 `verify-full` SSL模式。

输入连接详细信息后，选择 **[!DNL Test These Settings]** 以确保您的凭据正常工作。 有关的更多信息 [测试连接设置](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) 在官方的Looker文档中提供。 成功连接后，屏幕上会显示一条消息，指示您可以连接。 连接成功后，选择 **[!DNL Add Connection]** 以创建连接。

## 后续步骤

现在您已连接到 [!DNL Query Service]，您可以使用 [!DNL Looker] 以编写查询。 有关如何编写和运行查询的更多信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
