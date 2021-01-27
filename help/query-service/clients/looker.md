---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: 与Looker连接
topic: connect
description: 此文档将步骤连接到Looker和Adobe Experience Platform查询服务。
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 连接[!DNL Looker]

要在Adobe Experience Platform将[!DNL Looker]与[!DNL Query Service]连接，请执行以下步骤：

登录[!DNL Looker]后，单击&#x200B;**[!UICONTROL Admin]**，然后单击&#x200B;**[!UICONTROL Connections]**。

![](../images/clients/looker/click-admin-connections.png)

在此页上，单击&#x200B;**新建连接**。

![](../images/clients/looker/click-new-connection.png)

从此处，您可以填写连接设置的详细信息。

![](../images/clients/looker/new-connection.png)

- **名称：** 连接的名称。
- **方言：** 用于SQL数据库的方言。[!DNL Query Service] 使用 **[!DNL PostgreSQL]**。
- **主机和端口：** 主机端点及其端口 [!DNL Query Service]。
- **数据** 库：将使用的数据库。
- **用户名和密码：** 将使用的登录凭据。用户名将采用`ORG_ID@AdobeOrg`的形式。

>[!NOTE]
>
>有关查找主机和端口、数据库名称和登录凭据的详细信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找您的凭据，请登录[!DNL Platform]，单击&#x200B;**[!UICONTROL 查询]**，然后单击&#x200B;**[!UICONTROL 凭据]**。

输入连接详细信息后，单击&#x200B;**[!UICONTROL “测试这些设置”]**&#x200B;以确保凭据正常工作。 如果他们这样做，将在下面显示一条消息，告知您可以连接。 如果连接确实成功，请单击&#x200B;**[!UICONTROL 添加连接]**&#x200B;以创建连接。

![](../images/clients/looker/click-test-connection.png)

## 后续步骤

现在您已连接[!DNL Query Service]，可以使用[!DNL Looker]编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询指南](../best-practices/writing-queries.md)。