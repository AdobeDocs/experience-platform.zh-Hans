---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；数据库可视化工具；数据库可视化工具；连接到查询服务；
solution: Experience Platform
title: 将DbVisualizer连接到查询服务
description: 本文档介绍了将DbVisualizer与Adobe Experience Platform查询服务连接的步骤。
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---

# 将[!DNL DbVisualizer]连接到[!DNL Query Service] {#connect-dbvisualizer}

本文档介绍了将[!DNL DbVisualizer]数据库工具连接到Adobe Experience Platform [!DNL Query Service]的步骤。

## 快速入门

本指南要求您已具有对[!DNL DbVisualizer]桌面应用程序的访问权限，并且熟悉如何导航其界面。 要下载[!DNL DbVisualizer]桌面应用或了解详细信息，请参阅[官方 [!DNL DbVisualizer] 文档](https://www.dbvis.com/download/)。

要获取将[!DNL  DbVisualizer]连接到Experience Platform所需的凭据，您必须有权访问Experience Platform UI中的查询工作区。 如果您当前无权访问查询工作区，请联系您的组织管理员。

## 创建数据库连接 {#connect-database}

在本地计算机上安装了桌面应用程序后，请按照官方的BDVisualizer说明[创建新的数据库连接](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection)。

从[!DNL Connections]列表中选择&#x200B;**[!DNL PostgreSQL]**&#x200B;后，将显示新[!DNL PostgreSQL]连接的[!DNL Object View]选项卡。

### 为您的连接设置驱动程序属性 {#properties}

从[!DNL PostgreSQL]对象视图选项卡中，选择&#x200B;**[!DNL Properties]**&#x200B;选项卡，然后从导航侧边栏中选择&#x200B;**[!DNL Driver Properties]**。 有关[驱动程序属性](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties)的详细信息，请参阅官方文档。

接下来，输入下表所述的驱动程序属性。

>[!IMPORTANT]
>
>要将DBVisualizer与Adobe Experience Platform连接，必须启用SSL。 请参阅[SSL模式文档](./ssl-modes.md)，了解对Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用`verify-full` SSL模式进行连接。

| 属性 | 描述 |
| ------ | ------ |
| `PGHOST` | [!DNL PostgreSQL]服务器的主机名。 此值是您的Experience Platform **[!UICONTROL 主机]凭据**。 |
| `ssl` | 定义SSL值`1`以允许使用SSL。 |
| `sslmode` | 这将控制SSL保护的级别。 将第三方客户端连接到Adobe Experience Platform时，建议您使用`require` SSL模式。 `require`模式确保所有通信都需要加密，并且网络被信任可以连接到正确的服务器。 不需要验证服务器SSL证书。 |
| `user` | 连接到数据库的用户名是您的组织ID。 它是一个以`@Adobe.Org`结尾的字母数字字符串。 此值是您的Experience Platform **[!UICONTROL 用户名]凭据**。 |

使用搜索栏查找每个属性，然后为参数值选择相应的单元格。 单元格将以蓝色突出显示。 在值字段中输入Experience Platform凭据，然后选择&#x200B;**[!DNL Apply]**&#x200B;以添加驱动程序属性。

>[!NOTE]
>
>要添加第二个`user`配置文件，请从参数列中选择`user`，然后选择蓝色+ （加号）图标为每个用户添加凭据。 选择&#x200B;**[!DNL Apply]**&#x200B;以添加驱动程序属性。

[!DNL Edited]列显示一个复选标记，表示参数值已更新。

### 输入查询服务凭据 {#query-service-credentials}

要查找将BBVisualizer与查询服务连接所需的凭据，请登录到Experience Platform UI，然后从左侧导航中选择&#x200B;**[!UICONTROL 查询]**，然后选择&#x200B;**[!UICONTROL 凭据]**。 有关查找&#x200B;**主机**、**端口**、**数据库**、**用户名**&#x200B;和&#x200B;**密码**&#x200B;凭据的详细信息，请阅读[凭据指南](../ui/credentials.md)。

![Experience Platform查询工作区的“凭据”页面中突出显示了凭据和即将过期的凭据。](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service]还提供未过期的凭据，以允许对第三方客户端进行一次性设置。 请参阅文档[有关如何生成和使用未过期的凭据](../ui/credentials.md#non-expiring-credentials)的完整说明。 如果您希望将BDVisualizer作为一次性设置进行连接，则必须完成此过程。 获得的`credential`和`technicalAccountId`值包含DBVisualizer `password`参数的值。

## 身份验证 {#authentication}

要在每次建立连接时都要求用户ID和基于密码的身份验证，请导航到[!DNL Properties]选项卡，然后从[!DNL PostgreSQL]下的导航侧边栏中选择&#x200B;**[!DNL Authentication]**。

在连接身份验证面板中，选中&#x200B;**[!DNL Require Userid]**&#x200B;和&#x200B;**[!DNL Require Password]**&#x200B;复选框，然后选择&#x200B;**[!DNL Apply]**。 有关[设置身份验证选项](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options)的详细信息，请参阅官方文档。

## 连接到Experience Platform

您可以使用过期或不过期的凭据建立连接。 要建立连接，请从[!DNL PostgreSQL]对象视图选项卡中选择&#x200B;**[!DNL Connection]**&#x200B;选项卡，然后为以下设置输入您的Experience Platform凭据。 官方DBVisualizer网站上提供了[设置手动连接](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually)的补充说明。

>[!NOTE]
>
>下表中的BDVisualizer所需的所有凭据对于过期凭据和不过期凭据都是相同的，除非在参数描述中有所说明。

| 连接参数 | 描述 |
|---|---|
| **[!UICONTROL 名称]** | 为您的连接创建名称。 建议您提供易于识别的名称以识别连接。 |
| **[!UICONTROL 数据库服务器]** | 这是您的Experience Platform **[!UICONTROL 主机]**&#x200B;凭据。 |
| **[!UICONTROL 数据库端口]** | [!DNL Query Service]的端口。 您必须使用端口&#x200B;**80**&#x200B;或&#x200B;**5432**&#x200B;来连接[!DNL Query Service]。 |
| **[!UICONTROL 数据库]** | 使用您的Experience Platform **[!UICONTROL 数据库]**&#x200B;凭据值： `prod:all`。 |
| **[!UICONTROL 数据库用户ID]** | 这是您的Experience Platform组织ID。 使用您的Experience Platform **[!UICONTROL 用户名]**&#x200B;凭据值。 ID将采用`ORG_ID@AdobeOrg`格式。 |
| **[!UICONTROL 数据库密码]** | 此字母数字字符串是您的Experience Platform **[!UICONTROL 密码]**&#x200B;凭据。 如果要使用未过期的凭据，此值是从JSON配置文件中下载的`technicalAccountID`和`credential`中的连接参数。 密码值采用以下形式： {technicalAccountId}：{credential}。 未过期凭据的配置JSON文件是在其初始化期间的一次性下载，Adobe不会保留其副本。 |

输入所有相关凭据后，选择&#x200B;**[!DNL Connect]**。

[!DNL Connect]对话框出现在会话的第一次。 输入用户ID和密码，然后选择&#x200B;**[!DNL Connect]**。 日志中将显示一条消息，确认连接成功。

## 后续步骤

现在您已将[!DNL DbVisualizer]与[!DNL Query Service]连接，可以使用[!DNL DbVisualizer]编写查询。 有关如何编写和运行查询的详细信息，请阅读有关查询执行](../best-practices/writing-queries.md)的[指南。
