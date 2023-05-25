---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；数据库可视化工具；数据库可视化工具；连接到查询服务；
solution: Experience Platform
title: 将DbVisualizer连接到查询服务
description: 本文档介绍了将DbVisualizer与Adobe Experience Platform查询服务连接的步骤。
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# Connect [!DNL DbVisualizer] 到 [!DNL Query Service] {#connect-dbvisualizer}

本文档介绍了连接 [!DNL DbVisualizer] 使用Adobe Experience Platform的数据库工具 [!DNL Query Service].

## 快速入门

本指南要求您已有权访问 [!DNL DbVisualizer] 并熟悉如何导航其界面。 要下载 [!DNL DbVisualizer] 桌面应用程序或者有关更多信息，请参阅 [正式 [!DNL DbVisualizer] 文档](https://www.dbvis.com/download/).

获取进行连接所需的凭据 [!DNL  DbVisualizer] 要Experience Platform，您必须有权访问Platform UI中的查询工作区。 如果您当前无权访问查询工作区，请联系您的组织管理员。

## 创建数据库连接 {#connect-database}

在本地计算机上安装桌面应用程序后，按照官方的BDVisualizer说明进行操作，以便 [创建新数据库连接](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

选择后 **[!DNL PostgreSQL]** 从 [!DNL Connections] 列表，一个 [!DNL Object View] 选项卡中的新 [!DNL PostgreSQL] 出现“connection（连接）”。

### 为连接设置驱动程序属性 {#properties}

从 [!DNL PostgreSQL] 对象视图选项卡，选择 **[!DNL Properties]** 选项卡，然后 **[!DNL Driver Properties]** 导航侧边栏中的。 有关的更多信息 [驱动程序属性](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) 可在官方文件中找到。

接下来，输入下表中描述的驱动程序属性。

>[!IMPORTANT]
>
>要将DBVisualizer与Adobe Experience Platform连接，必须启用SSL。 请参阅 [SSL模式文档](./ssl-modes.md) 了解到Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用进行连接 `verify-full` SSL模式。

| 属性 | 描述 |
| ------ | ------ |
| `PGHOST` | 的主机名 [!DNL PostgreSQL] 服务器。 此值是您的Experience Platform **[!UICONTROL 主机] 凭据**. |
| `ssl` | 定义SSL值 `1` 以启用使用SSL。 |
| `sslmode` | 这将控制SSL保护的级别。 建议您使用 `require` 将第三方客户端连接到Adobe Experience Platform时的SSL模式。 此 `require` 模式可确保所有通信都需要加密，并且网络被信任可以连接到正确的服务器。 不需要服务器SSL证书验证。 |
| `user` | 连接到数据库的用户名是您的组织ID。 它是一个以结尾的字母数字字符串 `@Adobe.Org`. 此值是您的Experience Platform **[!UICONTROL 用户名] 凭据**. |

使用搜索栏查找每个属性，然后为参数值选择相应的单元格。 单元格将以蓝色突出显示。 在值字段中输入您的Platform凭据，然后选择 **[!DNL Apply]** 以添加驱动程序属性。

>[!NOTE]
>
>添加第二个 `user` 配置文件，选择 `user` 从参数列中，选择蓝色+ （加号）图标以添加每个用户的凭据。 选择 **[!DNL Apply]** 以添加驱动程序属性。

此 [!DNL Edited] 列会显示一个复选标记，表示参数值已更新。

### 输入查询服务凭据 {#query-service-credentials}

要查找连接BBVisualizer与查询服务所需的凭据，请登录Platform UI并选择 **[!UICONTROL 查询]** 从左侧导航中，后面是 **[!UICONTROL 凭据]**. 有关查找的详细信息 **主机**， **端口**， **数据库**， **用户名**、和 **密码** 凭据，请阅读 [凭据指南](../ui/credentials.md).

![“Experience Platform查询”工作区的“凭据”页面中突出显示了凭据和即将过期的凭据。](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] 还提供了不会过期的凭据，以允许对第三方客户端进行一次性设置。 请参阅相关文档 [有关如何生成和使用不会到期的凭据的完整说明](../ui/credentials.md#non-expiring-credentials). 如果要将BDVisualizer作为一次性设置连接，则必须完成此过程。 此 `credential` 和 `technicalAccountId` 获得的值包括DBVisualizer的值 `password` 参数。

## 身份验证 {#authentication}

要在每次建立连接时都要求用户ID和基于密码的身份验证，请导航到 [!DNL Properties] 选项卡并选择 **[!DNL Authentication]** 导航侧边栏中的 [!DNL PostgreSQL].

在“连接身份验证”面板中，选中 **[!DNL Require Userid]** 和 **[!DNL Require Password]** 复选框，然后选择 **[!DNL Apply]**. 有关的更多信息 [设置身份验证选项](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) 可以在官方文件中找到。

## 连接到平台

您可以使用过期或非过期凭据建立连接。 要建立连接，请选择 **[!DNL Connection]** 选项卡 [!DNL PostgreSQL] “对象视图”选项卡，并为以下设置输入您的Experience Platform凭据。 补充说明 [设置手动连接](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) 可从官方的DBVisualizer网站获取。

>[!NOTE]
>
>除非在参数描述中有所说明，否则下表中BDVisualizer要求的所有凭据对于过期凭据和非过期凭据都是相同的。

| 连接参数 | 描述 |
|---|---|
| **[!UICONTROL 名称]** | 为您的连接创建名称。 建议您提供易于识别的名称，以识别连接。 |
| **[!UICONTROL 数据库服务器]** | 这是您的Experience Platform **[!UICONTROL 主机]** 凭据。 |
| **[!UICONTROL 数据库端口]** | 的端口 [!DNL Query Service]. 必须使用端口 **80** 或 **5432** 以连接 [!DNL Query Service]. |
| **[!UICONTROL 数据库]** | 使用您的Experience Platform **[!UICONTROL 数据库]** 凭据值： `prod:all`. |
| **[!UICONTROL 数据库用户ID]** | 这是您的平台组织ID。 使用您的Experience Platform **[!UICONTROL 用户名]** 凭据值。 ID的格式为 `ORG_ID@AdobeOrg`. |
| **[!UICONTROL 数据库密码]** | 该字母数字字符串是您的Experience Platform **[!UICONTROL 密码]** 凭据。 如果您希望使用不会过期的凭据，则此值是来自 `technicalAccountID` 和 `credential` 下载。 密码值的格式为：{technicalAccountId}：{credential}。 未过期的凭据的配置JSON文件是在其初始化期间的一次性下载，该Adobe不会保留的副本。 |

输入所有相关凭据后，选择 **[!DNL Connect]**.

此 [!DNL Connect] 对话在第一次会议时出现。 输入用户ID和密码，然后选择 **[!DNL Connect]**. 日志中会显示一条确认连接成功的消息。

## 后续步骤

现在您已连接 [!DNL DbVisualizer] 替换为 [!DNL Query Service]，您可以使用 [!DNL DbVisualizer] 以编写查询。 有关如何编写和运行查询的更多信息，请阅读 [查询执行指南](../best-practices/writing-queries.md).
