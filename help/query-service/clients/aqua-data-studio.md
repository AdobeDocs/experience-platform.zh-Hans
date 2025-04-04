---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Aqua Data Studio；Aqua Data Studio；连接到查询服务；
solution: Experience Platform
title: 将Aqua Data Studio连接到查询服务
description: 本文档介绍了将Aqua Data Studio与Adobe Experience Platform查询服务连接的步骤。
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# 将[!DNL Aqua Data Studio]连接到查询服务

本文档介绍了将[!DNL Aqua Data Studio]与Adobe Experience Platform [!DNL Query Service]连接的步骤。

## 快速入门

本指南要求您已拥有[!DNL Aqua Data Studio]的访问权限并熟悉如何导航其界面。 有关[!DNL Aqua Data Studio]的详细信息，请参阅[官方 [!DNL Aqua Data Studio] 文档](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1)。

>[!NOTE]
>
>[!DNL Aqua Data Studio]有[!DNL Windows]和[!DNL macOS]版本。 本指南中的屏幕截图是使用[!DNL macOS]桌面应用程序拍摄的。 不同版本之间的UI可能存在细微差异。

要获取将[!DNL Aqua Data Studio]连接到Experience Platform所需的凭据，您必须有权访问Experience Platform UI中的[!UICONTROL 查询]工作区。 如果您当前无权访问[!UICONTROL 查询]工作区，请联系您的组织管理员。

## 注册服务器 {#register-server}

安装[!DNL Aqua Data Studio]后，必须首先注册服务器。 有关如何[启动 [!DNL Register Server] 对话框](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog)和[注册服务器](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio)的说明，请参阅正式的Aqua Data Studio文档。

在PostgresSQL服务器的&#x200B;**[!DNL Register Server]**&#x200B;对话框显示后，请为服务器设置提供以下详细信息。

- **[!DNL Name]**：连接的名称。 建议您提供一个易记名称来识别连接。
- **[!DNL Login Name]**：登录名是您的Experience Platform组织ID。 它采用`ORG_ID@AdobeOrg`的形式。
- **[!DNL Password]**：这是在[!DNL Query Service]凭据仪表板中找到的字母数字字符串。
- **[!DNL Host and Port]**： [!DNL Query Service]的主机终结点及其端口。 必须使用端口80连接[!DNL Query Service]。
- **[!DNL Database]：**&#x200B;将使用的数据库。 使用Experience Platform UI凭据`dbname`的值： `prod:all`。

### [!DNL Query Service]凭据

若要查找凭据，请登录到[!DNL Experience Platform] UI，然后从左侧导航中选择&#x200B;**[!UICONTROL 查询]**，然后选择&#x200B;**[!UICONTROL 凭据]**。 有关查找登录凭据、主机、端口和数据库名称的完整说明，请阅读[凭据指南](../ui/credentials.md)。

[!DNL Query Service]还提供未过期的凭据，以允许对第三方客户端进行一次性设置。 请参阅文档[有关如何生成和使用未过期的凭据](../ui/credentials.md#non-expiring-credentials)的完整说明。

### 设置SSL模式

接下来，必须将SSL模式值设置为`?sslmode=require`。 此操作从[!DNL Edit Server Properties]对话框的[!DNL Driver]选项卡完成。 有关如何[编辑驱动程序属性](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers)和[为 [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration)配置SSL的说明，请参阅Aqua Data Studio官方文档。 使用搜索栏查找`sslmode`属性。

>[!IMPORTANT]
>
>请参阅[[!DNL Query Service] SSL文档](./ssl-modes.md)，了解对Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用`verify-full` SSL模式连接。

输入连接详细信息后，在同一选项卡中选择&#x200B;**[!DNL Test Connection]**&#x200B;以确保凭据正常工作。 如果连接测试成功，请选择&#x200B;**[!DNL Save]**&#x200B;以注册服务器。 将出现确认对话框，确认连接，并且仪表板上将显示连接图标。 您现在可以连接到服务器并查看其方案对象。

## 后续步骤

现在您已连接到[!DNL Query Service]，可以使用[!DNL Aqua Data Studio]中的&#x200B;**[!DNL Query Analyzer]**&#x200B;执行和编辑SQL语句。 有关如何编写和运行查询的详细信息，请参阅[运行查询指南](../best-practices/writing-queries.md)。
