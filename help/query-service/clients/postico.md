---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；postico；Postico；连接到查询服务；
solution: Experience Platform
title: 将Postico连接到查询服务
description: 本文档包含安装Adobe Experience Platform查询服务的备份客户端Postico的链接。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Connect [!DNL Postico] 以查询服务(Mac)

本文档介绍了连接的步骤 [!DNL Postico] 使用Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假定您已经有权访问 [!DNL Postico] 并熟悉如何导航其界面。 有关以下内容的更多信息 [!DNL Postico] 可在以下位置找到： [正式 [!DNL Postico] 文档](https://eggerapps.at/postico/docs).
> 
> 此外， [!DNL Postico] 是 **仅限** 在macOS设备上可用。

连接 [!DNL Postico] 要查询服务，请打开 [!DNL Postico] 并选择 **[!DNL New Favorite]**. 出现连接设置对话框。 在此处，您可以输入参数值以与Adobe Experience Platform连接。 输入下面列出的连接设置。 操作说明 [使用Postico连接到PostgreSQL服务器](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) 也可从Postico官方网站获取。

| 连接参数 | 描述 |
|---|---|
| **[!DNL Host]:** | PostgreSQL服务器的主机名。 |
| **[!DNL Port]:** | 的端口 [!DNL Query Service]. 必须使用端口 **80** 或 **5432** 以连接 [!DNL Query Service]. |
| **[!DNL User]** | 为特定连接创建名称。 将该字段留空将使用您的Mac登录名。 |
| **[!DNL Password]** | 该字母数字字符串是您的Experience Platform **[!UICONTROL 密码]** 凭据。 如果您希望使用不会过期的凭据，则此值是来自 `technicalAccountID` 和 `credential` 下载。 密码值的格式为：{technicalAccountId}：{credential}。 未过期的凭据的配置JSON文件是在其初始化期间的一次性下载，该Adobe不会保留的副本。 |
| **[!DNL Database]** | 使用您的Experience Platform **[!UICONTROL 数据库]** 凭据值： `prod:all`. |

有关查找数据库名称、主机、端口和登录凭据的详细信息，请阅读 [凭据指南](../ui/credentials.md). 要查找您的凭据，请登录 [!DNL Platform]，然后选择 **[!UICONTROL 查询]**，后接 **[!UICONTROL 凭据]**.

插入凭据后，选择 **[!DNL Connect]** 以连接查询服务。

连接到Platform后，您将能够看到一个列表，其中包含之前与Query Service建立的所有关系。

## 创建SQL语句

要创建新的SQL查询，请选择 **[!DNL SQL Query]** 从侧边栏中。 或者，使用键盘快捷键(⇧⌘T)导航到查询视图，然后输入要执行的查询。 完成后，选择 **[!DNL Execute Statement]** 以运行查询。 此时将显示一个表，其中包含已完成的查询运行的结果。

有关以下内容的更多信息，请参阅Postico官方文档 [使用查询视图](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## 后续步骤

现在您已连接到 [!DNL Query Service]，您可以使用 [!DNL Postico] 以编写查询。 有关如何编写和运行查询的更多信息，请阅读 [运行查询指南](../best-practices/writing-queries.md).
