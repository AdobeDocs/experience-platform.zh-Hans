---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；postico;Postico；连接到查询服务；
solution: Experience Platform
title: 将Postico连接到查询服务
topic-legacy: connect
description: 本文档包含用于安装备份客户端Postico for Adobe Experience Platform查询服务的链接。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 将[!DNL Postico]连接到查询服务(Mac)

本文档介绍将[!DNL Postico]与Adobe Experience Platform [!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经拥有[!DNL Postico]的访问权限，并熟悉如何导航其界面。 有关[!DNL Postico]的更多信息，请参阅[official [!DNL Postico] 文档](https://eggerapps.at/postico/docs)。
> 
> 此外，[!DNL Postico]在macOS设备上仅&#x200B;****&#x200B;可用。

要将[!DNL Postico]连接到查询服务，请打开[!DNL Postico]并选择&#x200B;**[!DNL New Favorite]**。

![](../images/clients/postico/open-postico.png)

您现在可以输入值以连接Adobe Experience Platform。

有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读[凭据指南](../ui/credentials.md)。 要查找凭据，请登录到[!DNL Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，接着选择&#x200B;**[!UICONTROL 凭据]**。

插入凭据后，选择&#x200B;**[!DNL Connect]**&#x200B;以连接查询服务。

![](../images/clients/postico/authentication-details.png)

连接到Platform后，您将能够看到以前与查询服务建立的所有关系的列表。

![](../images/clients/postico/show-queries.png)

## 创建SQL语句

要创建新的SQL查询，请选择并打开“SQL查询”。

![](../images/clients/postico/create-query.png)

随即会出现一个框，您可以在此处键入要执行的查询。 完成后，选择&#x200B;**[!DNL Execute Statement]**&#x200B;以运行查询。

![](../images/clients/postico/run-statement.png)

将出现一个表格，其中显示了完成查询运行的结果。

![](../images/clients/postico/query-results.png)

## 后续步骤

现在，您已连接[!DNL Query Service]，接下来可以使用[!DNL Postico]编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询指南](../best-practices/writing-queries.md)。
