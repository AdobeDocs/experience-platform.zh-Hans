---
keywords: Experience Platform；主页；热门主题；PSQL;psqlconnect到查询服务；查询服务；查询服务；
solution: Experience Platform
title: 与PSQL连接
topic: connect
description: 'PSQL是在计算机上安装PostgreSQL时附带的命令行界面。 您可以按照以下说明安装它。 '
translation-type: tm+mt
source-git-commit: bc1bbdddd75b11ac180b5e6faa391fd74e5f7e02
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---


# PSQL

PSQL是在计算机上安装[!DNL PostgreSQL]时安装的命令行接口。 本文档介绍将PSQL与Adobe Experience Platform[!DNL Query Service]连接的步骤。

>[!NOTE]
>
> 本指南假定您已经具有访问[!DNL PSQL]的权限，并且熟悉如何使用它。 有关[!DNL PSQL]的详细信息，请参阅[official [!DNL PSQL] documentation](https://www.postgresql.org/docs/current/app-psql.html)。

## Connect PSQL和[!DNL Query Service]

在计算机上安装PSQL后，即可将PSQL与查询服务连接。 返回[!DNL Platform] UI，然后选择&#x200B;**[!UICONTROL 查询]**，后跟&#x200B;**[!UICONTROL 凭据]**。

![图像](../images/clients/psql/connect-bi.png)

选择该图标以复制标记为&#x200B;**[!UICONTROL PSQL命令]**&#x200B;的部分，然后在按Enter之前将命令字符串粘贴到终端或命令行窗口中。

>[!IMPORTANT]
>
>如果您在电脑上，使用文本编辑器删除命令字符串中的换行符，然后复制该字符串。 此外，如果您使用的是版本12.0或更高版本，则需要将`PGGSSENCMODE=disable`添加到连接字符串中。

您应当看到这样的结果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果看不到至少版本10.5，则需要下载该版本或更高版本。

## 后续步骤

现在您已连接[!DNL Query Service]，可以使用PSQL编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询](../best-practices/writing-queries.md)的指南。