---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 与PSQL连接
topic: connect
translation-type: tm+mt
source-git-commit: 8310204071375a55329f661c9ac678f96979a594

---


# 与PSQL连接

PSQL是在计算机上安装Postgres时附带的命令行界面。 您可以按照以下说明安装它。

## 在Mac上安装Postgres

打开一个终端窗口并发出以下三个命令：

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

发出这些命令后，您应看到以下内容：

```shell
/usr/local/bin/psql
```

## 在PC上安装Postgres

从此位置下载并安装 [Postgres](https://www.postgresql.org/download/windows/)。

编辑路径变量：

![图像](../images/clients/psql/path.png)

添加显示的包含“Postgres”的两行。

保存更新，然后打开命令提示符并键入：

```shell
psql -V
```

您应当看到以下内容：

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL和查询服务

返回“Connect BI工具”页面上的平台UI。

单 **击** “PSQL命令”的复制。

![图像](../images/clients/psql/connect-bi.png)

> [!IMPORTANT]:如果您在PC上，使用文本编辑器删除命令字符串中的换行符，然后复制该字符串。

将命令字符串粘贴到终端或命令窗口中，然后按Enter。

您应当看到这样的结果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果看不到至少版本10.5，则需要下载该版本或更高版本。