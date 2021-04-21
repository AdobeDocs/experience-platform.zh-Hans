---
keywords: Experience Platform；主页；热门话题；查询服务；查询服务；位置；位置；与查询服务连接；
solution: Experience Platform
title: 将Postico连接到查询服务
topic-legacy: connect
description: 此文档包含用于安装Adobe Experience Platform 查询服务的备份客户端Postico的链接。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 将[!DNL Postico]连接到查询服务(Mac)

本文档介绍将[!DNL Postico]与Adobe Experience Platform [!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已具有访问[!DNL Postico]的权限，并熟悉如何导航其接口。 有关[!DNL Postico]的详细信息，请参阅[official [!DNL Postico] 文档](https://eggerapps.at/postico/docs)。
> 
> 此外，[!DNL Postico]仅&#x200B;**在macOS设备上可用。**

要将[!DNL Postico]连接到查询服务，请打开[!DNL Postico]并选择&#x200B;**[!DNL New Favorite]**。

![](../images/clients/postico/open-postico.png)

您现在可以输入值以与Adobe Experience Platform连接。

有关查找数据库名称、主机、端口和登录凭据的详细信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找凭据，请登录[!DNL Platform]，然后选择&#x200B;**[!UICONTROL Queries]**，然后选择&#x200B;**[!UICONTROL Credentials]**。

插入凭据后，选择&#x200B;**[!DNL Connect]**&#x200B;以与查询服务连接。

![](../images/clients/postico/authentication-details.png)

连接到平台后，您将能够看到之前与查询服务建立的所有关系的列表。

![](../images/clients/postico/show-queries.png)

## 创建SQL语句

要创建新的SQL查询，请选择并打开“SQL查询”。

![](../images/clients/postico/create-query.png)

此时会显示一个框，您可以在此键入要执行的查询。 完成后，选择&#x200B;**[!DNL Execute Statement]**&#x200B;以运行查询。

![](../images/clients/postico/run-statement.png)

将显示一个表，其中显示已完成查询运行的结果。

![](../images/clients/postico/query-results.png)

## 后续步骤

现在，您已连接[!DNL Query Service]，可以使用[!DNL Postico]编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询指南](../best-practices/writing-queries.md)。
