---
keywords: Experience Platform；主页；热门主题；PSQL;psqlconnect到查询服务；查询服务；查询服务；
solution: Experience Platform
title: 将PSQL连接到查询服务
topic-legacy: connect
description: PSQL是在计算机上安装PostgreSQL时提供的命令行接口。 您可以按照以下说明进行安装。
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 1%

---

# 将PSQL连接到查询服务

PSQL是在计算机上安装[!DNL PostgreSQL]时安装的命令行界面。 本文档介绍了将PSQL与Adobe Experience Platform [!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经拥有[!DNL PSQL]的访问权限，并熟悉其使用方式。 有关[!DNL PSQL]的更多信息，请参阅[官方[!DNL PSQL]文档](https://www.postgresql.org/docs/current/app-psql.html)。

在计算机上安装PSQL后，即可将PSQL与查询服务连接。 返回到[!DNL Platform] UI，然后选择&#x200B;**[!UICONTROL 查询]**，接着选择&#x200B;**[!UICONTROL 凭据]**。

![图像](../images/clients/psql/connect-bi.png)

选择图标以复制标有&#x200B;**[!UICONTROL PSQL命令]**&#x200B;的部分，然后在按Enter键之前将命令字符串粘贴到终端或命令行窗口中。

>[!IMPORTANT]
>
>如果您在PC上，请使用文本编辑器删除命令字符串中的换行符，然后复制该字符串。 如果您使用的是12.0或更高版本，则需要将`PGGSSENCMODE=disable`添加到连接字符串。 此外，如果您使用的是未过期的凭据，请确保将密码字段替换为未过期的凭据密码。 要了解有关未过期凭据的更多信息，请阅读[凭据指南](../ui/credentials.md)。

您应会看到如下结果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果您至少看不到版本10.5，则需要下载该版本或更高版本。

## 后续步骤

现在，您已连接[!DNL Query Service]，可以使用PSQL来编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询](../best-practices/writing-queries.md)的指南。
