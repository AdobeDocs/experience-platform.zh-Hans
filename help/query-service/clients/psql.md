---
keywords: Experience Platform；主页；热门主题；PSQL；psqlconnect到查询服务；查询服务；查询服务；
solution: Experience Platform
title: 将PSQL连接到查询服务
description: PSQL是在计算机上安装PostgreSQL时提供的命令行接口。 您可以按照以下说明安装它。
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 将PSQL连接到查询服务

PSQL是安装时安装的命令行接口 [!DNL PostgreSQL] 在你的电脑上。 本文档介绍了将PSQL与Adobe Experience Platform连接的步骤 [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已经有权访问 [!DNL PSQL] 并熟悉如何使用它。 有关以下内容的更多信息 [!DNL PSQL] 可在以下位置找到： [正式 [!DNL PSQL] 文档](https://www.postgresql.org/docs/current/app-psql.html).

在计算机上安装PSQL后，即可将PSQL与查询服务连接。 返回到 [!DNL Platform] UI，然后选择 **[!UICONTROL 查询]**，后接 **[!UICONTROL 凭据]**.

在 **[!UICONTROL PSQL命令]** 部分，选择 **[!UICONTROL 复制到剪贴板]** 图标(![复制图标](../images/clients/psql/copy-icon.png))以复制命令字符串。

![高亮显示复制图标的查询功能板凭据选项卡。](../images/clients/psql/connect-bi.png)

将命令字符串粘贴到终端或命令行窗口中，然后按 **输入** 在键盘上。

>[!IMPORTANT]
>
>如果您在PC上，请使用文本编辑器删除命令字符串中的换行符，然后复制该字符串。 如果您使用的是版本12.0或更高版本，则需要添加 `PGGSSENCMODE=disable` 到连接字符串中。 此外，如果您使用的是不会过期的凭据，请确保将密码字段替换为不会过期的凭据密码。 要了解有关不会过期的凭据的更多信息，请阅读 [凭据指南](../ui/credentials.md).

您应会看到如下结果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果您没有看到最低版本10.5，则需要下载该版本或更高版本。

## 后续步骤

现在您已连接到 [!DNL Query Service]，您可以使用PSQL编写查询。 有关如何编写和运行查询的更多信息，请阅读以下指南： [正在运行查询](../best-practices/writing-queries.md).
