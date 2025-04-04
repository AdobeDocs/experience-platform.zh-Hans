---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；postico；postico；连接到查询服务；
solution: Experience Platform
title: 将Postico连接到查询服务
description: 本文档包含用于安装Adobe Experience Platform查询服务的备份客户端Postico的链接。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# 将[!DNL Postico]连接到查询服务(Mac)

本文档介绍了将[!DNL Postico]与Adobe Experience Platform [!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已具有访问[!DNL Postico]的权限并熟悉如何导航其界面。 有关[!DNL Postico]的详细信息，请参阅[官方 [!DNL Postico] 文档](https://eggerapps.at/postico/docs)。
> 
> 此外，[!DNL Postico]仅&#x200B;**在macOS设备上可用**。

要将[!DNL Postico]连接到查询服务，请打开[!DNL Postico]并选择&#x200B;**[!DNL New Favorite]**。 出现连接设置对话框。 在此处，您可以输入参数值以与Adobe Experience Platform连接。 输入下面列出的连接设置。 有关如何[使用Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html)连接到PostgreSQL服务器的说明，也可以从官方的Postico网站获得。

| 连接参数 | 描述 |
|---|---|
| **[!DNL Host]:** | PostgreSQL服务器的主机名。 |
| **[!DNL Port]:** | [!DNL Query Service]的端口。 您必须使用端口&#x200B;**80**&#x200B;或&#x200B;**5432**&#x200B;来连接[!DNL Query Service]。 |
| **[!DNL User]** | 为特定连接创建名称。 将该字段留空将使用您的Mac登录名。 |
| **[!DNL Password]** | 此字母数字字符串是您的Experience Platform **[!UICONTROL 密码]**&#x200B;凭据。 如果要使用未过期的凭据，此值是从JSON配置文件中下载的`technicalAccountID`和`credential`中的连接参数。 密码值采用以下形式： {technicalAccountId}：{credential}。 未过期凭据的配置JSON文件是在其初始化期间的一次性下载，Adobe不会保留其副本。 |
| **[!DNL Database]** | 使用您的Experience Platform **[!UICONTROL 数据库]**&#x200B;凭据值： `prod:all`。 |

有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读[凭据指南](../ui/credentials.md)。 若要查找凭据，请登录到[!DNL Experience Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，然后选择&#x200B;**[!UICONTROL 凭据]**。

插入凭据后，选择&#x200B;**[!DNL Connect]**&#x200B;以与查询服务连接。

连接到Experience Platform后，您将能够查看之前与查询服务建立的所有关系的列表。

## 创建SQL语句

要创建新的SQL查询，请从侧栏中选择&#x200B;**[!DNL SQL Query]**。 或者，使用键盘快捷键(⇧⌘T)导航到查询视图，然后输入要执行的查询。 完成后，选择&#x200B;**[!DNL Execute Statement]**&#x200B;以运行查询。 此时将显示一个表，其中包含已完成的查询运行的结果。

有关[使用查询视图](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html)的详细信息，请参阅正式Postico文档。

## 后续步骤

现在您已与[!DNL Query Service]连接，可以使用[!DNL Postico]编写查询。 有关如何编写和运行查询的详细信息，请参阅[运行查询指南](../best-practices/writing-queries.md)。
