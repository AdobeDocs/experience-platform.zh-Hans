---
keywords: Experience Platform；主页；热门主题；Tableau；Tableau；查询服务；查询服务；连接到查询服务；
solution: Experience Platform
title: 将Tableau连接到查询服务
description: 本文档介绍了将Tableau与Adobe Experience Platform查询服务连接的步骤。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 将[!DNL Tableau]连接到查询服务

本文档提供了有关将[!DNL Tableau]与Adobe Experience Platform [!DNL Query Service]连接的信息。

>[!NOTE]
>
> 本指南假定您已具有访问[!DNL Tableau]的权限并熟悉如何导航其界面。 有关[!DNL Tableau]的详细信息，请参阅[官方 [!DNL Tableau] 文档](https://help.tableau.com/current/pro/desktop/en-us/default.htm)。

有关如何[使用Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm)连接到PostgreSQL服务器的说明，请参阅官方的Tableau网站。 出现连接设置对话框后，在参数字段中输入Experience Platform凭据以与Adobe Experience Platform连接。 下面列出了所需的连接参数。

| 连接参数 | 描述 |
|---|---|
| **[!DNL Server]** | SFTP存储位置的地址。 使用Experience Platform **[!UICONTROL 主机]**&#x200B;凭据的值。 |
| **[!DNL Port]:** | [!DNL Query Service]的端口。 您必须使用端口&#x200B;**80**&#x200B;或&#x200B;**5432**&#x200B;来连接[!DNL Query Service]。 |
| **[!DNL Database]** | 要访问的数据库。 使用Experience Platform **[!UICONTROL 数据库]**&#x200B;凭据的值： `prod:all`。 |
| **[!DNL Authentication]:** | 您选择的证明用户身份的方法。 建议从下拉菜单的可用选项中选择[!DNL Username and Password]。 |
| **[!DNL Username]** | 这是您的Experience Platform组织ID。 使用Experience Platform **[!UICONTROL 用户名]**&#x200B;凭据的值。 ID将采用`ORG_ID@AdobeOrg`格式。 |
| **[!DNL Password]** | 此字母数字字符串是您的Experience Platform **[!UICONTROL 密码]**&#x200B;凭据。 如果要使用未过期的凭据，此值是从JSON配置文件中下载的`technicalAccountID`和`credential`中的连接参数。 密码值采用以下形式： {technicalAccountId}：{credential}。 未过期凭据的配置JSON文件是在其初始化期间的一次性下载，Adobe不会保留其副本。 |

有关查找用户名、密码和登录凭据的详细信息，请阅读[凭据指南](../ui/credentials.md)。 若要查找凭据，请登录到[!DNL Experience Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，然后选择&#x200B;**[!UICONTROL 凭据]**。

>[!IMPORTANT]
>
>作为Tableau或Power BI用户，您可以通过查询服务凭据选项卡将Customer Journey Analytics连接到您的BI工具。 有关如何[将您的BI工具](../ui/credentials.md#connect-to-customer-journey-analytics)连接到Customer Journey Analytics的说明，请参阅凭据文档。

在尝试连接之前，请确保已选中&#x200B;**[!UICONTROL 要求SSL]**&#x200B;框。 请参阅[SSL模式文档](./ssl-modes.md)，了解对Adobe Experience Platform查询服务的第三方连接的SSL支持。

>[!IMPORTANT]
>
>第三方BI工具中的嵌套数据结构可以扁平化，以提高其可用性并减少检索、分析、转换和报告数据所需的工作量。 有关在连接到数据库时如何激活此设置的说明，请参阅有关[`FLATTEN`功能](../key-concepts/flatten-nested-data.md)的文档。

填写完您的所有凭据后，确认您的设置以继续。 您现在已与Adobe Experience Platform建立了连接。

## 后续步骤

现在您已与[!DNL Query Service]连接，可以使用[!DNL Tableau]编写查询。 有关如何编写和运行查询的详细信息，请阅读有关[运行查询](../best-practices/writing-queries.md)的指南。
