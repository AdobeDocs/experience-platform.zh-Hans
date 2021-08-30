---
keywords: Experience Platform；主页；热门主题；表格；表格；查询服务；查询服务；连接到查询服务；
solution: Experience Platform
title: 将 Tableau 连接到查询服务
topic-legacy: connect
description: 本文档将介绍如何将Tableau与Adobe Experience Platform查询服务连接。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 3%

---

# 将[!DNL Tableau]连接到查询服务

本文档介绍将Tableau与Adobe Experience Platform [!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经拥有[!DNL Tableau]的访问权限，并熟悉如何导航其界面。 有关[!DNL Tableau]的更多信息，请参阅[official [!DNL Tableau] 文档](https://help.tableau.com/current/pro/desktop/en-us/default.htm)。

要将[!DNL Tableau]连接到[!DNL Query Service]，请打开[!DNL Tableau]，然后在&#x200B;**[!DNL To a Server]**&#x200B;部分选择&#x200B;**[!DNL More]**，然后选择&#x200B;**[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

您现在可以输入值以连接Adobe Experience Platform。 有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读[凭据指南](../ui/credentials.md)。 要查找凭据，请登录到[!DNL Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，接着选择&#x200B;**[!UICONTROL 凭据]**。

在尝试连接之前，请确保已选中&#x200B;**[!UICONTROL SSL Required]**&#x200B;框。

填写所有凭据后，选择&#x200B;**[!DNL Sign In]**&#x200B;以继续。

![](../images/clients/tableau/sign-in.png)

您现在已连接到Adobe Experience Platform，并在侧面显示表的列表。

![](../images/clients/tableau/connected.png)

## 后续步骤

现在，您已连接[!DNL Query Service]，接下来可以使用[!DNL Tableau]编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询](../best-practices/writing-queries.md)的指南。
