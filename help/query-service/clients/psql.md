---
keywords: Experience Platform；主页；热门主题；PSQL；psqlconnect到查询服务；查询服务；查询服务；
solution: Experience Platform
title: 将PSQL连接到查询服务
description: 了解如何将PSQL客户端连接到Adobe Experience Platform查询服务，包括支持的PostgreSQL版本和设置说明。
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 74f4ac5a3ca4c06e81111ef453ae0effd21b3f16
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# 将PSQL连接到查询服务

PSQL是与PostgreSQL一起安装在计算机上的命令行接口。 本文档介绍将PSQL与Adobe Experience Platform查询服务连接的步骤。

>[!IMPORTANT]
>
>查询服务仅支持与PSQL版本14.x连接。 14.x之前的版本（例如10.x到13.x）及更高版本（15.x及更高版本）不受正式支持。 确保安装了兼容的客户端版本。 有关参考，请参阅[PostgreSQL生命周期结束日期](https://endoflife.date/postgresql)。

在开始之前，请确保您有权访问PSQL并且熟悉使用客户端的基本知识。 有关PSQL的详细信息，请参阅[官方PSQL文档](https://www.postgresql.org/docs/current/app-psql.html)。

>[!IMPORTANT]
>
>下载PostgreSQL时，请确保选择版本14.x。默认情况下，PostgreSQL网站提供最新版本，该版本可能与查询服务不兼容。

安装PSQL后，可以将其连接到查询服务。 返回到Experience Platform UI，然后选择&#x200B;**[!UICONTROL 查询]**，最后选择&#x200B;**[!UICONTROL 凭据]**。

在&#x200B;**[!UICONTROL PSQL命令]**&#x200B;部分下，选择&#x200B;**[!UICONTROL 复制到剪贴板]**&#x200B;图标（![复制图标](/help/images/icons/copy.png)）以复制命令字符串。

![突出显示复制图标的查询仪表板凭据选项卡。](../images/clients/psql/connect-bi.png)

将命令字符串粘贴到终端中，然后按键盘上的&#x200B;**Enter**。

>[!IMPORTANT]
>
>如果您在PC上，请使用文本编辑器删除命令字符串中的换行符，然后复制该字符串。 如果您使用的是版本12.0或更高版本，则需要将`PGGSSENCMODE=disable`添加到连接字符串。 此设置禁用GSSAPI加密，这对于连接到Query Service是不必要的，并且可能会导致连接错误。<br>此外，如果您使用的是不会过期的凭据，请确保将密码字段替换为不会过期的凭据密码。 若要了解有关未过期的凭据的更多信息，请阅读[凭据指南](../ui/credentials.md)。

您应会看到如下结果：

```shell
psql (14.4, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果没有看到版本14.x，请从[官方的PostgreSQL下载页面](https://www.postgresql.org/download/)下载并安装支持的14.x版本的PSQL。

>[!NOTE]
>
>按照操作系统的安装说明操作，然后在终端中运行`psql --version`以验证已安装的PSQL版本。

## 后续步骤

现在，您已连接到查询服务，可以使用PSQL编写查询。 有关详细信息，请参阅[运行查询](../best-practices/writing-queries.md)指南。
