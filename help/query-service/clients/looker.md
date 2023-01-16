---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；登录者；登录者；连接到查询服务；
solution: Experience Platform
title: 将Looker连接到查询服务
description: 本文档将介绍如何将Looker与Adobe Experience Platform查询服务连接。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: b059a0191fbf2c3e5d2dfceb9802e2aaa429f7ed
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---

# 连接 [!DNL Looker] 查询服务

本文档介绍了连接的步骤 [!DNL Looker] 与Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已拥有 [!DNL Looker] 并熟悉如何导航其界面。 有关 [!DNL Looker] 可在 [官方 [!DNL Looker] 文档](https://docs.looker.com/).

## 创建新数据库连接 {#create-connection}

登录后 [!DNL Looker]，选择 **[!DNL Admin]**，后跟 **[!DNL Connections]**. 的 [!DNL Connections] 页面。 在 [!DNL Connections] 页面，选择 **[!DNL Add Connection]**.

从此处，输入下面列出的连接设置的详细信息。 有关 [创建新数据库连接的说明和可用属性的说明](https://cloud.google.com/looker/docs/connecting-to-your-db#creating_a_new_database_connection).

- **[!DNL Name]:** 连接的名称。
- **[!DNL Dialect]:** 用于SQL数据库的方言。 [!DNL Query Service] 使用 **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** 主机端点及其端口 [!DNL Query Service].
- **[!DNL Database]:** 将使用的数据库。
- **[!DNL Username and Password]:** 将使用的登录凭据。 用户名将以 `ORG_ID@AdobeOrg`.
- **SSL**:启用SSL以确保跨网络的安全连接。

要查找将Looker与查询服务连接所需的凭据，请登录到平台UI并选择 **[!UICONTROL 查询]** 从左侧导航，然后是 **[!UICONTROL 凭据]**. 有关查找 **主机**, **端口**, **数据库**, **用户名**&#x200B;和 **密码** 凭据，请阅读 [凭据指南](../ui/credentials.md).

![“Experience Platform查询”工作区的“凭据”页面中突出显示了“凭据”和“过期凭据”。](../images/clients/looker/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 此外，还提供了未过期的凭据，以便能够与第三方客户端进行一次性设置。 请参阅相关文档 [有关如何生成和使用未过期凭据的完整说明](../ui/credentials.md#non-expiring-credentials). 如果希望以一次性设置的方式连接Looker，则必须完成此过程。 的 `credential` 和 `technicalAccountId` 获取的值包括Looker的值 `password` 参数。

要了解Adobe Experience Platform中对第三方连接的SSL支持，请参阅 [[!DNL Query Service] SSL文档](./ssl-modes.md). 本文档提供了有关如何使用 `verify-full` SSL模式。

输入连接详细信息后，选择 **[!DNL Test These Settings]** 以确保凭据正常工作。 有关 [测试连接设置](https://cloud.google.com/looker/docs/connecting-to-your-db#testing_your_connection_settings) 在官方的Looker文档中提供。 成功连接后，屏幕上会显示一条消息，指示您可以连接。 连接成功后，选择 **[!DNL Add Connection]** 创建连接。

## 后续步骤

现在你已经连接了 [!DNL Query Service]，您可以使用 [!DNL Looker] 来编写查询。 有关如何编写和运行查询的详细信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
