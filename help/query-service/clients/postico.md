---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；postico;Postico；连接到查询服务；
solution: Experience Platform
title: 将Postico连接到查询服务
description: 本文档包含用于安装备份客户端Postico for Adobe Experience Platform查询服务的链接。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# 连接 [!DNL Postico] 到查询服务(Mac)

本文档介绍了连接的步骤 [!DNL Postico] 与Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已拥有 [!DNL Postico] 并熟悉如何导航其界面。 有关 [!DNL Postico] 可在 [官方 [!DNL Postico] 文档](https://eggerapps.at/postico/docs).
> 
> 此外， [!DNL Postico] is **仅** 可在macOS设备上获取。

连接 [!DNL Postico] 要查询服务，请打开 [!DNL Postico] 选择 **[!DNL New Favorite]**. 此时将显示连接设置对话框。 在此，您可以输入参数值以连接Adobe Experience Platform。 输入下面列出的连接设置。 有关如何 [使用Postico连接到PostgreSQL服务器](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) 官方的Postico网站也提供。

| 连接参数 | 描述 |
|---|---|
| **[!DNL Host]:** | PostgreSQL服务器的主机名。 |
| **[!DNL Port]:** | 的端口 [!DNL Query Service]. 必须使用端口 **80** 或 **5432** 连接 [!DNL Query Service]. |
| **[!DNL User]** | 为特定连接创建名称。 将字段留空，以使用您的Mac登录名。 |
| **[!DNL Password]** | 此字母数字字符串是您的Experience Platform **[!UICONTROL 密码]** 凭据。 如果要使用未过期的凭据，此值是 `technicalAccountID` 和 `credential` 在配置JSON文件中下载。 密码值采用以下形式：{technicalAccountId}:{credential}。 用于未过期凭据的配置JSON文件是在初始化期间一次性下载，Adobe不会保留的副本。 |
| **[!DNL Database]** | 使用Experience Platform **[!UICONTROL 数据库]** 凭据值： `prod:all`. |

有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md). 要查找您的凭据，请登录到 [!DNL Platform]，然后选择 **[!UICONTROL 查询]**，后跟 **[!UICONTROL 凭据]**.

插入凭据后，选择 **[!DNL Connect]** 与查询服务连接。

连接到Platform后，您将能够看到以前与查询服务建立的所有关系的列表。

## 创建SQL语句

要创建新SQL查询，请选择 **[!DNL SQL Query]** 来访问Advertising Cloud。 或者，使用键盘快捷键(⇧ ⌘ T)导航到查询视图，并输入要执行的查询。 完成后，选择 **[!DNL Execute Statement]** 以运行查询。 随即会出现一个表，其中包含已完成查询运行的结果。

有关 [使用查询视图](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## 后续步骤

现在你已经连接了 [!DNL Query Service]，您可以使用 [!DNL Postico] 来编写查询。 有关如何编写和运行查询的详细信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
