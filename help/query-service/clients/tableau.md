---
keywords: Experience Platform；主页；热门主题；表；表；查询服务；查询服务；连接到查询服务；
solution: Experience Platform
title: 将Tableau连接到查询服务
topic-legacy: connect
description: 此文档将逐步介绍将Tableau与Adobe Experience Platform 查询服务相连的步骤。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 将[!DNL Tableau]连接到查询服务

本文档介绍了将Tableau与Adobe Experience Platform [!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已具有访问[!DNL Tableau]的权限，并熟悉如何导航其接口。 有关[!DNL Tableau]的详细信息，请参阅[official [!DNL Tableau] 文档](https://help.tableau.com/current/pro/desktop/en-us/default.htm)。

要将[!DNL Tableau]连接到[!DNL Query Service]，请打开[!DNL Tableau]，并在&#x200B;**[!DNL To a Server]**&#x200B;部分选择&#x200B;**[!DNL More]**，然后选择&#x200B;**[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

您现在可以输入值以与Adobe Experience Platform连接。 有关查找数据库名称、主机、端口和登录凭据的详细信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找凭据，请登录[!DNL Platform]，然后选择&#x200B;**[!UICONTROL Queries]**，然后选择&#x200B;**[!UICONTROL Credentials]**。

请确保在尝试连接之前已选中&#x200B;**[!UICONTROL SSL Required]**&#x200B;框。

填写完所有凭据后，选择&#x200B;**[!DNL Sign In]**&#x200B;继续。

![](../images/clients/tableau/sign-in.png)

您现在已连接到Adobe Experience Platform，侧面显示表的列表。

![](../images/clients/tableau/connected.png)

## 后续步骤

现在，您已连接[!DNL Query Service]，可以使用[!DNL Tableau]编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询](../best-practices/writing-queries.md)的指南。
