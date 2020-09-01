---
keywords: Experience Platform;home;popular topics;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: 与PSQL连接
topic: connect
description: 'PSQL是在计算机上安装Postgres时附带的命令行界面。 您可以按照以下说明安装它。 '
translation-type: tm+mt
source-git-commit: d2f098cb9e4aaf5beaad02173a22a25a87a43756
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 1%

---


# 与PSQL连接

PSQL是在计算机上安装时附带的命 [!DNL Postgres] 令行界面。 您可以按照以下说明安装它。

## 在Mac上安装Postgres

打开终端窗口并发出以下三个命令：

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

发出这些命令后，您应当看到以下内容：

```shell
/usr/local/bin/psql
```

## 安装 [!DNL Postgres] 在PC上

从此位 [!DNL Postgres] 置下载和 [安装](https://www.postgresql.org/download/windows/)。

编辑路径变量：

![图像](../images/clients/psql/path.png)

添加显示的包含“”的两[!DNL Postgres]行。

保存更新，然后打开命令提示符并键入：

```shell
psql -V
```

您应该看到这样的内容：

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL和 [!DNL Query Service]

返回Connect [!DNL Platform] BI“工 **[!UICONTROL 具”页面上的]** UI。

单击 **[!UICONTROL “复制]****[!UICONTROL PSQL命令”]**。

![图像](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]
>
>如果您在电脑上，使用文本编辑器删除命令字符串中的换行符，然后复制该字符串。

将命令字符串粘贴到终端或命令窗口中，然后按Enter。

您应当看到这样的结果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果看不到至少版本10.5，则需要下载该版本或更高版本。