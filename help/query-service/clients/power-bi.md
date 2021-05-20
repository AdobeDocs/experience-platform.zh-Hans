---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Power BI;power bi；连接到查询服务；
solution: Experience Platform
title: 将Power BI连接到查询服务
topic-legacy: connect
description: 本文档将介绍如何将Power BI与Adobe Experience Platform查询服务连接。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 2109abd02b9c6c321c21a8fe3826509d22b1c2e2
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# 将[!DNL Power BI]连接到查询服务(PC)

本文档介绍了将Power BI与Adobe Experience Platform查询服务连接的步骤。

>[!NOTE]
>
> 本指南假定您已经拥有[!DNL Power BI]的访问权限，并熟悉如何导航其界面。 有关[!DNL Power BI]的更多信息，请参阅[official [!DNL Power BI] 文档](https://docs.microsoft.com/zh-cn/power-bi/)。
>
> 此外，Power BI在Windows设备上仅&#x200B;****&#x200B;可用。

安装Power BI后，您需要安装`Npgsql`（用于PostgreSQL的.NET驱动程序包）。 有关Npgsql的更多信息，请参阅[Npgsql文档](https://www.npgsql.org/doc/index.html)。

>[!IMPORTANT]
>
>您必须下载v4.0.10或更低版本，因为较新版本会导致错误。

在自定义设置屏幕上的“[!DNL Npgsql GAC Installation]”下，选择&#x200B;**[!DNL Will be installed on local hard drive]**。

要确保npgsql已正确安装，请先重新启动计算机，然后再继续执行后续步骤。

## 将[!DNL Power BI]连接到[!DNL Query Service]

要将[!DNL Power BI]连接到[!DNL Query Service]，请打开[!DNL Power BI]并在顶部菜单功能区中选择&#x200B;**[!DNL Get Data]**。

![](../images/clients/power-bi/open-power-bi.png)

选择&#x200B;**[!DNL PostgreSQL database]**，然后选择&#x200B;**[!DNL Connect]**。

![](../images/clients/power-bi/get-data.png)

您现在可以输入服务器和数据库的值。 有关查找数据库名称、主机、端口和登录凭据的更多信息，请访问Platform](https://platform.adobe.com/query/configuration)上的[凭据页。 要查找凭据，请登录到[!DNL Platform]，然后选择&#x200B;**[!UICONTROL 查询]**，接着选择&#x200B;**[!UICONTROL 凭据]**。

**[!DNL Server]** 是在连接详细信息下找到的主机。对于生产环境，请将端口`:80`添加到主机字符串的末尾。 **[!DNL Database]** 可以是“all”或数据集表名称。

此外，您还可以选择&#x200B;**[!DNL Data Connectivity mode]**。 选择&#x200B;**[!DNL Import]**&#x200B;以显示所有可用表的列表，或选择&#x200B;**[!DNL DirectQuery]**&#x200B;直接创建查询。

要了解有关&#x200B;**[!DNL Import]**&#x200B;模式的更多信息，请阅读[预览和导入表](#preview)中的部分。 要了解有关&#x200B;**[!DNL DirectQuery]**&#x200B;模式的更多信息，请阅读有关[创建SQL语句](#create)的章节。 确认数据库详细信息后，选择&#x200B;**[!DNL OK]**。

![](../images/clients/power-bi/connectivity-mode.png)

出现提示，要求输入您的用户名、密码和应用程序设置。 填写这些详细信息，然后选择&#x200B;**[!DNL Connect]**&#x200B;以继续下一步。

![](../images/clients/power-bi/import-mode.png)

## 预览和导入表 {#preview}

如果已选择&#x200B;**[!DNL Import]**&#x200B;模式，则会出现一个对话框，显示所有可用表的列表。 选择要预览的表，然后选择&#x200B;**[!DNL Load]**&#x200B;以将数据集导入[!DNL Power BI]。

![](../images/clients/power-bi/preview-table.png)

表格现已导入Power BI。

![](../images/clients/power-bi/import-table.png)

## 创建SQL语句 {#create}

如果已选择&#x200B;**[!DNL DirectQuery]**&#x200B;模式，则需要使用要创建的SQL查询填写“高级选项”部分。

在&#x200B;**[!DNL SQL statement]**&#x200B;下，插入要创建的SQL查询。 确保选中标记为&#x200B;**[!DNL Include relationship columns]**&#x200B;的复选框。 写入查询后，选择&#x200B;**[!DNL OK]**&#x200B;以继续。

![](../images/clients/power-bi/direct-query-mode.png)

此时将显示查询预览。 选择&#x200B;**[!DNL Load]**&#x200B;可查看查询结果。

![](../images/clients/power-bi/preview-direct-query.png)

## 后续步骤

现在，您已连接[!DNL Query Service]，接下来可以使用[!DNL Power BI]编写查询。 有关如何编写和运行查询的详细信息，请阅读[运行查询](../best-practices/writing-queries.md)的指南。
