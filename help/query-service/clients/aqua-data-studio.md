---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Aqua Data Studio；Aqua Data Studio；连接到查询服务；
solution: Experience Platform
title: 将Aqua Data Studio连接到查询服务
description: 本文档介绍了将Aqua Data Studio与Adobe Experience Platform Query Service连接的步骤。
exl-id: 4770e221-48a7-45d8-80a4-60b5cbc0ec33
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Connect [!DNL Aqua Data Studio] 查询服务

本文档介绍了连接的步骤 [!DNL Aqua Data Studio] 使用Adobe Experience Platform [!DNL Query Service].

## 快速入门

本指南要求您已有权访问 [!DNL Aqua Data Studio] 并熟悉如何导航其界面。 有关以下内容的更多信息 [!DNL Aqua Data Studio] 可在以下位置找到： [正式 [!DNL Aqua Data Studio] 文档](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1).

>[!NOTE]
>
>有 [!DNL Windows] 和 [!DNL macOS] 版本 [!DNL Aqua Data Studio]. 本指南中的屏幕截图是使用 [!DNL macOS] 桌面应用程序。 不同版本之间的UI中可能存在细微差异。

获取进行连接所需的凭据 [!DNL Aqua Data Studio] 要Experience Platform，您必须有权访问 [!UICONTROL 查询] Platform UI中的工作区。 如果您当前无权访问 [!UICONTROL 查询] 工作区。

## 注册服务器 {#register-server}

安装后 [!DNL Aqua Data Studio]，您必须先注册服务器。 有关如何执行操作的说明，请参阅Aqua Data Studio官方文档 [启动 [!DNL Register Server] 对话框](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#launching_the_register_server_dialog) 和 [注册服务器](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation18/page/81/Registering-a-Database-Server#steps_to_register_a_server_in_aqua_data_studio).

一旦 **[!DNL Register Server]** 将出现一个PostgresSQL服务器对话框，为服务器设置提供以下详细信息。

- **[!DNL Name]**：连接的名称。 建议您提供一个易记名称来识别连接。
- **[!DNL Login Name]**：登录名是您的Platform组织ID。 它采取以下形式 `ORG_ID@AdobeOrg`.
- **[!DNL Password]**：这是一个字母数字字符串，可在 [!DNL Query Service] 凭据仪表板。
- **[!DNL Host and Port]**：的主机端点及其端口 [!DNL Query Service]. 必须使用端口80连接 [!DNL Query Service].
- **[!DNL Database]：** 将使用的数据库。 使用Platform UI凭据的值 `dbname`： `prod:all`.

### [!DNL Query Service] 凭据

要查找您的凭据，请登录 [!DNL Platform] UI并选择 **[!UICONTROL 查询]** 从左侧导航中，后面是 **[!UICONTROL 凭据]**. 有关查找登录凭据、主机、端口和数据库名称的完整说明，请阅读 [凭据指南](../ui/credentials.md).

[!DNL Query Service] 还提供了不会过期的凭据，以允许对第三方客户端进行一次性设置。 请参阅相关文档 [有关如何生成和使用不会到期的凭据的完整说明](../ui/credentials.md#non-expiring-credentials).

### 设置SSL模式

接下来，必须将SSL模式值设置为 `?sslmode=require`. 这是从以下位置完成的 [!DNL Driver] 的选项卡 [!DNL Edit Server Properties] 对话框。 有关如何执行操作的说明，请参阅Aqua Data Studio官方文档 [编辑驱动程序属性](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation13/page/116/PostgreSQL#drivers) 和 [为配置SSL [!DNL PostgreSQL]](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation20/page/SSL-Configuration/SSL-Configuration). 使用搜索栏查找 `sslmode` 属性。

>[!IMPORTANT]
>
>请参阅 [[!DNL Query Service] SSL文档](./ssl-modes.md) 了解到Adobe Experience Platform查询服务的第三方连接的SSL支持，以及如何使用进行连接 `verify-full` SSL模式。

输入连接详细信息后，从同一选项卡中选择 **[!DNL Test Connection]** 以确保您的凭据正常工作。 如果连接测试成功，请选择 **[!DNL Save]** 注册服务器。 将出现确认对话框，确认连接，并且连接图标显示在仪表板上。 您现在可以连接到服务器并查看其方案对象。

## 后续步骤

现在您已连接到 [!DNL Query Service]，您可以使用 **[!DNL Query Analyzer]** 范围 [!DNL Aqua Data Studio] 执行和编辑SQL语句。 有关如何编写和运行查询的更多信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
