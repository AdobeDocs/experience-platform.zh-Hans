---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: 与Looker连接
topic: connect
description: 此文档将步骤连接到Looker和Adobe Experience Platform查询服务。
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 连接 [!DNL Looker]

要连接 [!DNL Looker] Adobe Experience Platform [!DNL Query Service] ，请按照以下步骤操作：

登录后， [!DNL Looker]单击“管 **[!UICONTROL 理]**”，然后 **[!UICONTROL 单击“连接]**”。

![](../images/clients/looker/click-admin-connections.png)

在此页上，单击“新建 **连接”**。

![](../images/clients/looker/click-new-connection.png)

从此处，您可以填写连接设置的详细信息。

![](../images/clients/looker/new-connection.png)

- **名称：** 连接的名称。
- **方言：** 用于SQL数据库的方言。 [!DNL Query Service] 使用 **[!DNL PostgreSQL]**。
- **主机和端口：** 主机端点及其端口 [!DNL Query Service]。
- **数据库：** 将使用的数据库。
- **用户名和密码：** 将使用的登录凭据。 用户名将采用以下形式 `ORG_ID@AdobeOrg`。

>[!NOTE]
>
>有关查找主机和端口、数据库名称和登录凭据的详细信息，请访 [问平台上的凭据页](https://platform.adobe.com/query/configuration)。 要查找凭据，请登录， [!DNL Platform]单击 **[!UICONTROL 查询]**，然后单 **[!UICONTROL 击凭据]**。

输入连接详细信息后，单击“ **[!UICONTROL 测试这些设置]** ”以确保凭据正常工作。 如果他们这样做，将在下面显示一条消息，告知您可以连接。 如果连接确实成功，请单击“添 **[!UICONTROL 加连接]** ”以创建连接。

![](../images/clients/looker/click-test-connection.png)

## 后续步骤

现在您已连接 [!DNL Query Service]，可以 [!DNL Looker] 编写查询。 有关如何编写和运行查询的更多信息，请阅读运 [行查询指南](../creating-queries/creating-queries.md)。