---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 与Looker连接
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 与Looker连接

要将Looker与Adobe Experience Platform上的Adobe查询服务连接，请按照以下步骤操作：

登录到Looker后，单击“管 **理员**”，然后单击“ **连接”**。

![](../images/clients/looker/click-admin-connections.png)

在此页上，单击“新 **建连接”**。

![](../images/clients/looker/click-new-connection.png)

在此处，您可以填写连接设置的详细信息。

![](../images/clients/looker/new-connection.png)

- **名称：** 连接的名称。
- **方言：** 用于SQL数据库的方言。 查询服务使 **用PostgreSQL**。
- **主机和端口：** 主机端点及其查询服务的端口。
- **数据库：** 将使用的数据库。
- **用户名和密码：** 将使用的登录凭据。 用户名将采用以下形式 `ORG_ID@AdobeOrg`。

>[!NOTE] 有关查找主机和端口、数据库名和登录凭据的详细信息，请访问平台 [上的凭据页](https://platform.adobe.com/query/configuration)。 要查找凭据，请登录到平台，单击 **查询**，然后单击 **凭据**。

输入连接详细信息后，单击“ **测试这些设置** ”以确保凭据正常工作。 如果他们这样做，将在下面显示一条消息，告知您可以连接。 如果连接确实成功，请单击“添 **加连接** ”以创建连接。

![](../images/clients/looker/click-test-connection.png)

## 后续步骤

现在您已连接查询服务，可以使用Looker编写查询。 有关如何编写和运行查询的详细信息，请阅读运行 [查询指南](../creating-queries/creating-queries.md)。