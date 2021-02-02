---
keywords: Experience Platform；主页；热门主题；表；表；查询服务；查询服务；连接到查询服务；
solution: Experience Platform
title: 与Tableau连接
topic: connect
description: 此文档步行前往连接Tableau和Adobe Experience Platform查询服务的步骤。
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# [!DNL Tableau]

本文档介绍将Tableau与Adobe Experience Platform[!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经具有访问[!DNL Tableau]的权限，并且熟悉如何导航其接口。 有关[!DNL Tableau]的详细信息，请参阅[offical [!DNL Tableau] 文档](https://help.tableau.com/current/pro/desktop/en-us/default.htm)。

## 连接[!DNL Tableau]与平台

要将[!DNL Tableau]连接到[!DNL Query Service]，请打开[!DNL Tableau]，在&#x200B;**[!DNL To a Server]**&#x200B;部分选择&#x200B;**[!DNL More]**，后跟&#x200B;**[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

您现在可以输入值以连接Adobe Experience Platform。 有关查找数据库名称、主机、端口和登录凭据的详细信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找您的凭据，请登录[!DNL Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，后跟&#x200B;**[!UICONTROL 凭据]**。

在尝试连接之前，请确保已选中&#x200B;**[!UICONTROL SSL Required]**&#x200B;框。

填写所有凭据后，选择&#x200B;**[!DNL Sign In]**&#x200B;继续。

![](../images/clients/tableau/sign-in.png)

您现在已连接到Adobe Experience Platform，侧面显示您的表格的列表。

![](../images/clients/tableau/connected.png)

## 后续步骤

现在您已连接[!DNL Query Service]，可以使用[!DNL Tableau]编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询](../best-practices/writing-queries.md)的指南。